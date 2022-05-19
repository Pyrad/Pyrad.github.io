---
title: Sphinx Install Basics
date: 2022-05-19 19:34:26
categories:
- linux related
tags: sphinx
---

Here are some basic steps to install sphinx and setups for it in Visual Studio Code

<!-- more -->

# Sphinx

## Sphinx Installation

### Install `sphinx` with `pip`

```sh
pip install sphinx
```

logs,

```bash
Collecting sphinx
  Downloading Sphinx-4.5.0-py3-none-any.whl (3.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.1/3.1 MB 1.2 MB/s eta 0:00:00
Collecting alabaster<0.8,>=0.7
  Downloading alabaster-0.7.12-py2.py3-none-any.whl (14 kB)
Collecting requests>=2.5.0
  Downloading requests-2.27.1-py2.py3-none-any.whl (63 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.1/63.1 kB 485.3 kB/s eta 0:00:00
Collecting sphinxcontrib-applehelp
  Downloading sphinxcontrib_applehelp-1.0.2-py2.py3-none-any.whl (121 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.2/121.2 kB 543.8 kB/s eta 0:00:00

... ...

Collecting certifi>=2017.4.17
  Downloading certifi-2021.10.8-py2.py3-none-any.whl (149 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 149.2/149.2 kB 306.7 kB/s eta 0:00:00
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in c:\synopsys_longc\python39\lib\site-packages (from packaging->sphinx) (2.4.7)
Installing collected packages: snowballstemmer, certifi, alabaster, zipp, urllib3, sphinxcontrib-serializinghtml, sphinxcontrib-qthelp, sphinxcontrib-jsmath, sphinxcontrib-htmlhelp, sphinxcontrib-devhelp, sphinxcontrib-applehelp, Pygments, packaging, MarkupSafe, imagesize, idna, docutils, charset-normalizer, babel, requests, Jinja2, importlib-metadata, sphinx
Successfully installed Jinja2-3.1.2 MarkupSafe-2.1.1 Pygments-2.12.0 alabaster-0.7.12 babel-2.10.1 certifi-2021.10.8 charset-normalizer-2.0.12 docutils-0.17.1 idna-3.3 imagesize-1.3.0 importlib-metadata-4.11.3 packaging-21.3 requests-2.27.1 snowballstemmer-2.2.0 sphinx-4.5.0 sphinxcontrib-applehelp-1.0.2 sphinxcontrib-devhelp-1.0.2 sphinxcontrib-htmlhelp-2.0.0 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.3 sphinxcontrib-serializinghtml-1.1.5 urllib3-1.26.9 zipp-3.8.0

```

After that some packages are installed

```sh
Jinja2-3.1.2		MarkupSafe-2.1.1		Pygments-2.12.0
alabaster-0.7.12	babel-2.10.1			certifi-2021.10.8 
charset-normalizer-2.0.12	docutils-0.17.1	idna-3.3 
imagesize-1.3.0		importlib-metadata-4.11.3	packaging-21.3 
requests-2.27.1		snowballstemmer-2.2.0		sphinx-4.5.0 
sphinxcontrib-applehelp-1.0.2	sphinxcontrib-devhelp-1.0.2
sphinxcontrib-htmlhelp-2.0.0	sphinxcontrib-jsmath-1.0.1
sphinxcontrib-qthelp-1.0.3		sphinxcontrib-serializinghtml-1.1.5 
urllib3-1.26.9 zipp-3.8.0
```



### Install `sphinx_rtd_theme` with `pip`

```sh
pip install sphinx_rtd_theme
```

logs,

```bash
Collecting sphinx_rtd_theme
  Downloading sphinx_rtd_theme-1.0.0-py2.py3-none-any.whl (2.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.8/2.8 MB 3.9 MB/s eta 0:00:00
Requirement already satisfied: docutils<0.18 in c:\synopsys_longc\python39\lib\site-packages (from sphinx_rtd_theme) (0.17.1)
Requirement already satisfied: sphinx>=1.6 in c:\synopsys_longc\python39\lib\site-packages (from sphinx_rtd_theme) (4.5.0)

... ...

Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in c:\synopsys_longc\python39\lib\site-packages (from packaging->sphinx>=1.6->sphinx_rtd_theme) (2.4.7)
Installing collected packages: sphinx_rtd_theme
Successfully installed sphinx_rtd_theme-1.0.0
```

 this time only one package is installed

```bash
sphinx_rtd_theme-1.0.0
```



## Create Sphinx Project

### Using `sphinx-quickstart`

Create a folder where you want to put your project into, and start with `sphinx-quickstart` in command prompt, and the following the instructions step by step,

- Where you want to put your project (root folder)
- Whether or not to separate `build` folder from `source` folder
  - for this one I answer `y` instead of the default value
- Fill Project name, author name and project release
- Project language

After questions above, all done.

Here is the log,

```bash
C:\Pyrad\SphinxReStructuredText\sphinxproject>sphinx-quickstart
Welcome to the Sphinx 4.5.0 quickstart utility.

Please enter values for the following settings (just press Enter to
accept a default value, if one is given in brackets).

Selected root path: .

You have two options for placing the build directory for Sphinx output.
Either, you use a directory "_build" within the root path, or you separate
"source" and "build" directories within the root path.
> Separate source and build directories (y/n) [n]: y

The project name will occur in several places in the built documentation.
> Project name: pyradnotes
> Author name(s): Pyrad
> Project release []:

If the documents are to be written in a language other than English,
you can select a language here by its language code. Sphinx will then
translate text that it generates into that language.

For a list of supported codes, see
https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
> Project language [en]:

Creating file C:\Pyrad\SphinxReStructuredText\sphinxproject\source\conf.py.
Creating file C:\Pyrad\SphinxReStructuredText\sphinxproject\source\index.rst.
Creating file C:\Pyrad\SphinxReStructuredText\sphinxproject\Makefile.
Creating file C:\Pyrad\SphinxReStructuredText\sphinxproject\make.bat.

Finished: An initial directory structure has been created.

You should now populate your master file C:\Pyrad\SphinxReStructuredText\sphinxproject\source\index.rst and create other documentation
source files. Use the Makefile to build the docs, like so:
   make builder
where "builder" is one of the supported builders, e.g. html, latex or linkcheck.
```

### Build html files

Now you can run `make <builder>` to **build docs**  by leveraging a **Makefile** which was generated just now.

Here `<builder>` could be **html, latex or linkcheck**.

For example, if I want to build html style webpage, I run, `make html`, and an `index.html` will be created in `.\build\html\index.html`, open this file to preview.

Here is the log,

```bash
C:\Pyrad\SphinxReStructuredText\sphinxproject>make html
Running Sphinx v4.5.0
making output directory... done
building [mo]: targets for 0 po files that are out of date
building [html]: targets for 1 source files that are out of date
updating environment: [new config] 1 added, 0 changed, 0 removed
reading sources... [100%] index
looking for now-outdated files... none found
pickling environment... done
checking consistency... done
preparing documents... done
writing output... [100%] index
generating indices... genindex done
writing additional pages... search done
copying static files... done
copying extra files... done
dumping search index in English (code: en)... done
dumping object inventory... done
build succeeded.

The HTML pages are in build\html.
```



Here now this project folder we have the following directories and files

```bash
C:\Pyrad\SphinxReStructuredText\sphinxproject>tree /f
Folder PATH listing for volume Windows
Volume serial number is 2E24-EB6F
C:.
│  make.bat
│  Makefile
│
├─build    ---> I skip this folder as all files in it are generated by Makefile each time
│
└─source
    │  conf.py
    │  index.rst
    │
    ├─_static
    └─_templates
```



### Change them to `sphinx_rtd_theme`

Open `source/conf.py`, and replace the theme

```bash
# html_theme = 'alabaster'
html_theme = 'sphinx_rtd_theme'
```



### Use VS Code

Instead of using windows command prompt, you could open the project folder in ***Visual Studio Code***, and run `make html` in built-in terminal (PowerShell), and open `.\build\html\index.html` directly.

```powershell
PS C:\Pyrad\SphinxReStructuredText\sphinxproject> make html
PS C:\Pyrad\SphinxReStructuredText\sphinxproject> .\build\html\index.html
PS C:\Pyrad\SphinxReStructuredText\sphinxproject> 
```

Also you can install extension `reStructedText` in ***Visual Studio Code***, which can help you with syntax highlighting when editing `.rst` files, also it can preview `.rst` files.

 Here is the article ([Configuration — restructuredtext 1.0 documentation](https://docs.restructuredtext.net/articles/configuration.html)) on how to set configurations in ***Visual Studio Code*** for reStructuredtext.

Please note that in order to use **preview** functionality of `reStructuredtext` extension , you should install esbonio too, which is a python package.

```powershell
pip install esbonio 
```

Just in case, check the file `.vscode\settings.json` , and set the variables correctly based on local project paths, still referring to [Configuration — restructuredtext 1.0 documentation](https://docs.restructuredtext.net/articles/configuration.html)

```json
{
    // "esbonio.sphinx.confDir": ""
    "esbonio.sphinx.buildDir": "${workspaceFolder}/build/html",
    "esbonio.sphinx.confDir"  : "${workspaceFolder}\\source",
    "esbonio.sphinx.srcDir"   : "${workspaceFolder}/source"
}
```

Besides, you can also install linter packages from python, see here for more details [Live Preview — restructuredtext 1.0 documentation](https://docs.restructuredtext.net/articles/preview.html).

```powershell
pip install doc8
pip install rstcheck
```

**After** all done, restart ***Visual Studio Code***, otherwise the **preview** may not work properly.


