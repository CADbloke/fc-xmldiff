# Fuego Core XML Diff and Patch Tool #

The Fuego Core XML Diff and Patch tool is a fast and memory-efficient general-purpose tool for diffing and patching XML files. The underlying algorithms have been described in _T. Lindholm, J. Kangasharju, and S. Tarkoma: Fast and Simple XML Tree Differencing by Sequence Alignment, Proceedings of ACM DocEng 2006_. [acm.org](http://doi.acm.org/10.1145/1166160.1166183) [hiit.fi](http://www.hiit.fi/files/fi/fc/papers/doceng06-pc.pdf).

The source code for the tool is released under the permissive MIT license
News

  * June 26, 2009: Project reincarnated at code.google.com after hoslab.cs.helsinki.fi was shut down

  * March 25, 2009: Improved output of namespace prefixes by moving them to the root node. Also, the XAS parser now supports setting the text buffer size with the org.kxml2.io.textbuffer property. Try this if you are getting parse errors on documents with large attributes. Note: you'll need to build the fc-xas project and replace trunk/java/xmldiff/contrib/fc-xas-0.1.0.jar with the generated fc-xas.jar in order to pick up the text buffer size.

## Installation from Source ##

At this point, we only provide source-based installation from the Subversion repository. Sorry. We're looking into providing more straightforward methods, such as a downloadable binary. Please request an alternate method if you find that you'll need one.

To install the tool using the subversion repository, proceed as follows.

  1. Make sure you have Subversion, a Java Development Kit (>=version 1.6), and  Apache Ant (>=1.7, older ones may work) installed. In Debian based-distributions,  make sure the package ant-optional is installed.
  1. Check out the sources using Subversion:
```
      svn checkout http://fc-xmldiff.googlecode.com/svn/trunk/ fc-xmldiff-read-only
```
  1. Then in the checked out director (`fc-xmldiff-read-only` with the command above),
```
      cd java/xmldiff
```
  1. Run ant to get instructions on how to proceed project setup. The project setup should download all dependencies automatically.
```
      ant
```
  1. After project setup is completed, invoke (again)
```
      ant
```
> to compile the sources.

## Diffing XML ##
The easiest way to get the diff between the files `old.xml` and `new.xml` into `diff.xml` is to invoke the diff Ant task:

```
ant -Dbase=old.xml -Dnew=new.xml -Ddiff=diff.xml diff
```

Naturally, you may invoke the tool using java directly with the appropriate classpath. For instance,

```
java -Djava.ext.dirs=../contrib/jar:contrib -cp =build/lib/xmldiff.jar fc.xml.diff.Diff old.xml new.xml diff.xml
```

## Patching XML ##

As for diffing, their is an Ant target for patching. To patch `old.xml` with `diff.xml` to get `new.xml`, you run

```
ant -Dbase=old.xml -Ddiff=diff.xml -Dnew=new.xml patch
```

As in the previous case, direct invocation can also be used. In this case the main class is `fc.xml.diff.Patch`