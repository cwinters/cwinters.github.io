---
tags: java
layout: post
title: "Creating gzipped archives from Java"
---



Using the <a href="http://www.trustice.com/java/tar/">Javatar</a> library and the standard GZIP output stream you can create gzipped tarballs pretty easily. Since the Javatar library doesn't include any examples of creating an archive and you can spend a while spinning your wheels about how to most easily do this, here you go:
<pre class="sourceCode">
File destArchive = new File( "somefile.tar.gz" );
TarArchive archive = new TarArchive(
    new GZIPOutputStream( new FileOutputStream( destArchive ) )
);
// assume we've got a collection of 'someFiles' from somewhere
for ( Iterator it = someFiles.iterator(); it.hasNext(); )
{
    File recordFile = (File)it.next();
    TarEntry entry = new TarEntry( recordFile );
    entry.setName( recordFile.getName() );     // no leading dir info
    archive.writeEntry( entry, false );
}
archive.closeArchive();
</pre>



