---
layout: post
title: Jekyll and Windows
---

#How to Jekyll on Windows
A lot of people, including myself and this site, use Jekyll to create cool markdown-based blogs. A smaller subsection of those people use Windows - namely because developing on Windows is an absolute pain. But if you're reading this you're definitely one of the few!

##Short Answer:
You can't.

##Long Answer:
It is technically possible - there are a lot of guides on how to get Jekyll started on Windows - most revolve around using [Cygwin](https://www.cygwin.com/). Here are some links to get you started:

###Links
* [Jekyll homepage](http://jekyllrb.com/docs/windows/)
* [Julian Thilo's Comprehensive Ruby on Windows guide](http://jekyll-windows.juthilo.com/)
* [RVM on Windows script](http://blog.developwithpassion.com/2012/03/30/installing-rvm-with-cygwin-on-windows/)

There are a multitude of issues for the guide, which as of Dec 2014, ranging from Ruby having [outdated SSL certificates](http://railsapps.github.io/openssl-certificate-verify-failed.html)(and the only fix, RVM, is not really Windows compatible), to compile errors (spoiler: you'll download every Visual Studio version, ever).

##Solution
The easiest workaround I found was installing [CentOS 7](http://www.centos.org/download/) onto a VM. It's a lot to download for a blog setup, but I use that VM frequently for a stable dev environment. If you wanted a throwaway distro, you could try [Puppy Linux 5.6](http://distro.ibiblio.org/puppylinux/puppy-5.6/), the variations of which can be around a couple hundred MB. Installing Ruby and Jekyll took minimal googling on Linux, and after I setup the blog file structure, I could use my standard Sublime 3 text editor to create new posts, without having to go back into Linux.

##Its Still Not Over - Sometimes My Blogs Dont Render Properly 
You thought it was that easy? Nope.
Jekyll blogs require [http://jekyllrb.com/docs/frontmatter/](YAML Front Matter), a sort of header that classifies each file. The problem is that sometimes Windows will encode a [BOM character](http://en.wikipedia.org/wiki/Byte_order_mark) into the start of your UTF-8 file. Normal text editors will not render them, so you can't see them. **A BOM before your YAML header will stop Jekyll from rendering the pages properly - they'll look like you typed it all in plaintext in a HTML file.** 

If youre using Sublime, you can use [Package Control](https://sublime.wbond.net/installation) to install [HexViewer](https://sublime.wbond.net/packages/HexViewer) which will allow you to view and edit the hex. A BOM will show `EF BB BF` as the first bytes of your file. Typically you want `2D 2D 2D`, which is the 3 hyphens for the start of the YAML header. Change it accordingly, and save using `File > Save with Encoding > UTF-8` (don't save it as `UTF-8 with BOM`! This is exactly what you are trying to avoid!).

I hope this post helped someone troubleshoot their setup!
