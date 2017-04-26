Read the Docs YAML Config
=========================

Read the Docs now has support for configuring builds with a YAML file.
The file, `readthedocs.yml` (or `.readthedocs.yml`), must be in the root
directory of your project.

> **warning**
>
> This feature is in a beta state.
> :   Please file an
>     [issue](https://github.com/rtfd/readthedocs.org/issues) if you
>     find anything wrong.
>
Supported Settings
------------------

### formats

-   Default: `htmlzip`, `pdf`, `epub`
-   Options: `htmlzip`, `pdf`, `epub`, `none`

The formats of your documentation you want to be built. Choose `none` to
build none of the formats.

> **note**
>
> We will always build an HTML & JSON version of your documentation.
> :   These are used for web serving & search indexing, respectively.
>
~~~~ {.sourceCode .yaml}
# Don't build any extra formats
formats:
    - none
~~~~

~~~~ {.sourceCode .yaml}
# Build PDF & ePub
formats:
    - epub
    - pdf
~~~~

### requirements\_file

-   Default: None
-   Type: Path (specified from the root of the project)

The path to your Pip requirements file.

~~~~ {.sourceCode .yaml}
requirements_file: requirements/docs.txt
~~~~

### conda

The `conda` block allows for configuring our support for Conda.

#### conda.file

-   Default: None
-   Type: Path (specified from the root of the project)

The file option specified the Conda [environment
file](http://conda.pydata.org/docs/using/envs.html#share-an-environment)
to use.

~~~~ {.sourceCode .yaml}
conda:
    file: environment.yml
~~~~

> **note**
>
> Conda is only supported via the YAML file.

### python

The `python` block allows you to configure aspects of the Python
executable used for building documentation.

#### python.version

-   Default: `2.7`
-   Options: `2.7`, `2`, `3.5`, `3`

This is the version of Python to use when building your documentation.
If you specify only the major version of Python, the highest supported
minor version will be selected.

The supported Python versions depends on the version of the build image
your project is using. The default build image that is used to build
documentation contains support for Python `2.7` and `3.5`.

There is also an image in testing that supports Python versions `2.7`,
`3.3`, `3.4`, `3.5`, and `3.6`. If you would like access to this build
image, you can sign up for beta access here:

<https://goo.gl/forms/AKEoeWHixlzVfqKT2>

~~~~ {.sourceCode .yaml}
python:
   version: 3.5
~~~~

#### python.setup\_py\_install

-   Default: False
-   Type: Boolean

When true, install your project into the Virtualenv with
`python setup.py install` when building documentation.

~~~~ {.sourceCode .yaml}
python:
   setup_py_install: true
~~~~

#### python.pip\_install

-   Default: False
-   Type: Boolean

When true, install your project into the Virtualenv with pip when
building documentation.

~~~~ {.sourceCode .yaml}
python:
   pip_install: true
~~~~

#### python.extra\_requirements

-   Default: `[]`
-   Type: List

List of [extra
requirements](http://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-extras-optional-features-with-their-own-dependencies)
sections to install, additionally to the [package default
dependencies](http://setuptools.readthedocs.io/en/latest/setuptools.html#declaring-dependencies).
Only works if `python.pip_install` option above is set to `True`.

Let's say your Python package has a `setup.py` which looks like this:

~~~~ {.sourceCode .python}
from setuptools import setup

setup(
    name="my_package",
    # (...)
    install_requires=[
        'requests',
        'simplejson'],
    extras_require={
        'tests': [
            'nose',
            'pycodestyle >= 2.1.0'],
        'docs': [
            'sphinx >= 1.4',
            'sphinx_rtd_theme']}
)
~~~~

Then to have all dependencies from the `tests` and `docs` sections
installed in addition to the default `requests` and `simplejson`, use
the `extra_requirements` as such:

~~~~ {.sourceCode .yaml}
python:
    extra_requirements:
        - tests
        - docs
~~~~

Behind the scene the following Pip command will be run:

~~~~ {.sourceCode .shell}
$ pip install -e .[tests,docs]
~~~~
