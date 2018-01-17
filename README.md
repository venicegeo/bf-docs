![Beachfront](docs/userguide/images/logo_inverted.png)

# bf-docs

This repository contains the markdown source for Beachfront documentation.

## Table of Contents

* [Building HTML Documentation](#building-html-documentation)
* [Documentation Authors](#documentation-authors)

## Building HTML Documentation

The delivery method for this documentation is a static HTML site.  We use
[MkDocs](http://www.mkdocs.org/) to generate the static files from the markdown
documents contained in this repo.

MkDocs is a generator that uses source documents in markdown (using a [Python
implementation of Markdown](https://pypi.python.org/pypi/Markdown/)) to
generate a static HTML site.

As a developer, you don't _need_ to generate these static files yourself unless
you would like to preview your work.  If you do decide to do that, here's how:

### Install MkDocs

#### Install with a Package Manager

##### Linux

There may be a package available for your flavor of Linux.  For example, with Ubuntu:

```
[~/workspace/bf-docs]$ sudo apt-get install mkdocs
```

_Other packages are available to install additional themes and documentation._

##### OSX

MkDocs is available as a [Homebrew](https://brew.sh/) package:

```
[~/workspace/bf-docs]$ sudo brew install mkdocs
```

#### Manual Installation

If you can't or don't want to install MkDocs with your platform's package
manager, then you can do it manually.  You'll need Python >= 2.7.2 and the
Python package manager, pip:

```
[~/workspace/bf-docs]$ python --version
Python 2.7.2
[~/workspace/bf-docs]$ pip --version
pip 1.5.2
```

Then install with:

```
$ pip install mkdocs
```

_If you are installing on Windows, then see the instructions on
[www.mkdocs.org](http://www.mkdocs.org/#installation)._

### Build the Documentation

You can build the documentation static site with the command:

```
[~/workspace/bf-docs]$ mkdocs build
```

This will generate the static files in the project's `site/` directory.  But
you won't normally have a need to do this.  Typically you would run the `mkdocs
serve` command to run a local server on port 8000 to review the HTML documents:

```
[~/workspace/bf-docs]$ mkdocs serve
```

Then just use a browser to access http://localhost:8000/ to see the results.
This site will automatically reload when you make changes to the files.

> The behavior of `mkdocs` is controlled by the `mkdocs.yml` file in this
> repo's root directory.  See [MkDocs
> Configuration](http://www.mkdocs.org/user-guide/configuration/) for details.

## Documentation Authors

All documentation that is intended to be distributed as part of the static
Beachfront documentation site must be somewhere in the `docs/` directory and
should have the `.md` extension.

The documentation must be written in markdown for the [Python implementation of
Markdown](https://pypi.python.org/pypi/Markdown/) with the extensions:

* [SmartyPants](https://python-markdown.github.io/extensions/smarty/)
* [Sane Lists](https://python-markdown.github.io/extensions/sane_lists/)
* [Table of Contents](https://python-markdown.github.io/extensions/toc/)
