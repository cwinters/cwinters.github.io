---
title: A little about embedded structs in Go
layout: post
tags: programming learning golang
---

Go doesn't have inheritance in the traditional sense, forcing you to rely on
composition. ["That's so Go"](http://en.wikipedia.org/wiki/That's_So_Raven)
should be a phrase, and this is a great example of one. Go seems like it was
created to avoid entirely many bad practices we've developed over the years,
and brittle inheritance hierarchies is certainly one of them.

One benefit of inheritance is that you don't have to repeat yourself, and
Go enables this as well with embedded structs. They have some warts, but
I was pleasantly surprised with the behavior when an embedded struct had the
same field as its container.

I'll show a short example here. First the structs:

{% highlight go linenos %}
type ProductFields struct {
	ID           uint   `json:"id"`
	Name         string `json:"name"`
	CurrentPrice string `json:"current_price"`
	IsOnSale     bool   `json:"is_on_sale"`
}

type Product struct {
	ID uint `json:"id"`
	ProductFields
}

type Variant struct {
	ID                 uint   `json:"id"`
	VariantDescription string `json:"variant"`
	ProductFields
}
{% endhighlight %}

As [I've learned](http://www.modcloth.com/), a Variant is an instance
of a Product with unique characteristics: size, color, materials, 
whatever. I think a Variant typically maps to a 
[SKU](http://en.wikipedia.org/wiki/Stock_keeping_unit).

Variants within a Product often share the same price, among other information,
so we have a set of fields that we want to display on both a `Product` and
`Variant` -- this is the `ProductFields` struct.

Note that it has an `ID` property that gets parsed/serialized to the JSON `id`
property, and the two container structs (`Product` and `Variant`) do as well.
How does Go resolve the conflict?

I think of it as "container wins" -- a field defined in a container
will override one from its embedded child. So when we serialize a `Product` to
JSON we'll see its ID, not the one from `ProductFields`. Here's 
an example use -- [full file here](https://gist.github.com/cwinters/b5fa13ba07b51e0e83c8):

{% highlight go %}
func main() {
	fields := ProductFields{
		ID:           9876,
		Name:         "Grabthar's Hammer",
		CurrentPrice: "59.99",
		IsOnSale:     false,
	}
	jsonDump("Product fields", fields)

	p := Product{
		ID:            123,
		ProductFields: fields,
	}
	jsonDump("Product", p)
{% endhighlight %}

Which will display like this -- note the ID displayed in the second JSON blob:
it belongs to the `Product` container: 

    Product fields as JSON:
      {"id":9876,"name":"Grabthar's Hammer","current_price":"59.99","is_on_sale":false}
    Product as JSON:
      {"id":123,"name":"Grabthar's Hammer","current_price":"59.99","is_on_sale":false}

The reverse works as well -- an `ID` in JSON that gets assigned to 
a struct of type `Variant` goes to the right place:

{% highlight go %}
	v := Variant{
		ID:                 8181,
		VariantDescription: "Size: Large / Color: Mauve",
		ProductFields:      fields,
	}
	variantJson := jsonDump("Variant", v)

	newVariant := Variant{}
	json.Unmarshal(variantJson, &newVariant)
	fmt.Printf("Variant serialized from JSON\n  [ID: %d] [Name: %s] [Price: %s] [On sale? %t] [Variant: %s]\n",
		newVariant.ID, newVariant.Name, newVariant.CurrentPrice, newVariant.IsOnSale, newVariant.VariantDescription)
{% endhighlight %}

which displays the following, putting the ID from the JSON where we expect:

    Variant as JSON:
      {"id":8181,"variant":"Size: Large / Color: Mauve","name":"Grabthar's Hammer","current_price":"59.99","is_on_sale":false}
    Variant serialized from JSON
      [ID: 8181] [Name: Grabthar's Hammer] [Price: 59.99] [On sale? false] [Variant: Size: Large / Color: Mauve]

The only thing that's kind of awkward is creating the structs with literals.
You can't just flatten out all the fields into a single definition, you need
to group the fields per struct so Go knows where to put everything. Annoying, 
but certainly workable, and "That's so Go" to not hide these sorts of details
about structs.
