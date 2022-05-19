---
title: reStructuredtext basics
date: 2022-05-19 19:48:14
categories:
- linux related
tags: reStructuredtext
---

Describes basics of reStructuredtext

<!-- more -->


# reStructuredtext



Covering most common stuff

[Sphinx documentation contents — Sphinx documentation (sphinx-doc.org)](https://www.sphinx-doc.org/en/master/contents.html)



To introduce different sections in the left navigation bar of the `index.html`, change the **toctree** in `index.rst` as below. Here we have 2 different folders `Options` and `Guidelines`.

```rst
.. pyradnotes documentation master file, created by
   sphinx-quickstart on Wed May 18 14:53:47 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to pyradnotes's documentation!
======================================

A Tour of Life (This is a short description)

Pyrad

.. toctree::
   :maxdepth: 1
   :caption: Options:

   Options/justlogic
   Options/justcode
   Options/justhardware
   Options/hardwareandcode

.. toctree::
   :maxdepth: 1
   :caption: Guidelines:

   Guidelines/content
   Guidelines/workflow
```





### Syntax

Here is a reference cheat sheet https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst

#### Text formatting

```rst
.. emphasis, and include multiple words
*emphasis*

.. strong emphasis, and include multiple words
**strong emphasis**

.. Note that you can't place 3 aterisks to get the effect of Italic + bold

.. inline literal (code)
``inline literal``

.. The rendering and meaning of interpreted text is domain- or application-dependent.
`interpreted text`

.. 

```



#### Lists Bulleted, Numbered, and Multi-level

```rst
.. list without numbers
* ListItem 1
* ListItem 2
* ListItem 3

.. list which have emphasis, Italic, ...
* **ListItem** 1
* *ListItem* 2
* ``ListItem`` 3

.. Numbered list
#. ListItem 1
#. ListItem 2
#. ListItem 3

.. Levels
* ListItem 1
	* indented item
* ListItem 2
	* indented item
* ListItem 3
	* indented item

```



#### Admonitions (警告)

4 callouts: **Green**, **blue**, **yellow** and **red**

```rst
.. caution callout (yellow). Note you have to indent each line in this callout
.. caution:: 
    This is a caution paragraph,
    and you should notice this.
    * caution item 0
    * caution item 1

.. danger callout (red)
.. danger:: 
    This is a danger paragraph,
    and you should do something for this.
    * TODO item 0
    * TODO item 1

.. tip callout (green)
.. tip:: 
    This is a tip paragraph,
    and you could refer to this.
    * TIp item 0
    * Tip item 1

.. note caution (blue)
.. note:: 
    This is a note paragraph,
    something to keep in mind.
    * note item 0
    * note item 1



```



#### Images

```rst
.. Insert a picture from a folder 
   starting from the root of this project
.. image:: /Images/airplane.png


.. Insert a picture from current folder
.. image:: google.png
```



#### Code blocks

If the code in your file are all belong to a same programming language, you could set this in `conf.py` to indicate this as below.

```python
# in conf.py
highlight_language = 'tcl'
```

2 ways to specify code blocks

```rst
.. Insert a code block, note that all
   lines should be indented, and the
   code block should start from the 2nd
   line, and leave the 1st line empty
Here is a python function code sampe::

    def ByteToMega(v):
	    m = v / 1024 / 1024
	    print("%.3f GB" % m)


.. To indicate a specific language syntax
   highlighting. Still, pay attention to 
   the blank lines, and each line of the
   code block should be indented
Here is a tcl function code sample

.. code:: tcl

    proc isDesiredContext { m } {
        set res 0
        if { $m eq "Red-black tree" } {
            set res 1
        }
        return $res
    }

```



#### Tables

4 ways to render

- equal signs, single space to separate different columns

```reStructuredText
================ =============== ===== ===========
Platform         Self-Contained? Cost  Flexibility
================ =============== ===== ===========
Raspberry        No              $30   Limitless
Lego Mindstorms  Yes             $350  Medium
================ =============== ===== ===========
```

- Use table block, you can specify a table name. Note that a new empty line is needed before starting the table

```rst
.. table:: MyOptions

    ================ =============== ===== ===========
    Platform         Self-Contained? Cost  Flexibility
    ================ =============== ===== ===========
    Raspberry        No              $30   Limitless
    Lego Mindstorms  Yes             $350  Medium
    ================ =============== ===== ===========
```

- Draw all table cells... (en.. interesting... while I'd prefer not to do so)

```rst
+----------------+---------------+-----+-----------+
|Platform        |Self-          |     |           |
|                |Contained?     |Cost |Flexibility|
+================+===============+=====+===========+
|Raspberry       |No             |$30  |Limitless  |
+----------------+---------------+-----+-----------+
|Lego Mindstorms |Yes            |$350 |Medium     |
+----------------+---------------+-----+-----------+
```

- Use `list-table` block

  ```rst
  .. list-table:: Comparison
      :widths: 20 10 10 15
      :header-rows: 1
  
      * - Platform
        - Self-Contained?
        - Cost
        - Flexibility
      * - Raspberry Pi
        - No
        - $30
        - Limitless
      * - Lego Mindstorms
        - Yes
        - $350
        - Medium
  ```

- Use `csv-table` block

  ```rst
  .. csv-table:: Comparison
      :header: Platform, Self-Contained?, Cost, Flexibility
      :widths: 15 10 30 30
  
      Raspberry, No, $30, Limitless
      Lego Mindstorms, Yes, $350, Medium
  ```

  

#### Links

- External links

  - Directly add to the file

    ```rst
    https://pyrad.github.io/
    ```

  - Use bracket with underscore

    ```rst
    .. Syntax is ` LinkName <linkAddress>`_
    `Pyrad note <https://pyrad.github.io/>`_



- Internal Links to files

  - Link to a file, this syntax will show the name of the file

    ```rst
    .. Use syntax :doc:`/abs/path/to/file`
       and this shows the name of file
       Note that backtick should follow :doc:
       immediately
    :doc:`/Options/justlogic`
    ```

  - Link to a file by showing some different text

    ```rst
    .. Use syntax :doc:`ShowText </abs/path/to/file>`
       and this shows specified text
       Note that backtick should follow :doc:
       immediately
    :doc:`best starting point </Options/justlogic>`
    ```

- Internal Links to paragraphs

  - Set up an anchor for the paragraph to link to, then use same in other place

    ```rst
    .. Setup an anchor somewhere in a paragraph in a file
    .. _myRefAnchor:
    
    .. Set a link in other places to link to it
    :ref:`SomeTextToShow <myRefAnchor>`
    ```

    





