# cgp_pygeoapi

## About

The files included in this repository are based on Environment and Climate Change Canada's implementation of [pygeoapi](https://pygeoapi.io/): [msc-pygeoapi](https://github.com/ECCC-MSC/msc-pygeoapi).
These templates are compatible with the [GoC Web Experience Toolkit (WET)](https://wet-boew.github.io/GCWeb/index-en.html) themes.

A set of french translation files are included in the `locale` folder. These files were created using [Babel](https://babel.pocoo.org/en/latest/index.html) using translations from [msc-pygeoapi](https://github.com/ECCC-MSC/msc-pygeoapi) and the [Canada.ca theme](https://wet-boew.github.io/GCWeb/index-en.html).

## Installation

### Basic installation

The following steps are recommended for development only. For alternative installation options, see the docs for [pygeoapi](https://docs.pygeoapi.io/en/latest/installation.html).

From a terminal, enter the following commands:
- python3 -m venv cgp_pygeoapi
- cd cgp_pygeoapi
- . bin/activate
- git clone https://github.com/Canadian-Geospatial-Platform/cgp_pygeoapi.git
- cd cgp_pygeoapi
- pip3 install --upgrade pip
- pip3 install -r requirements.txt

To use an alternate base template, edit the pygeoapi-config.yml file. See the section 'Using an alternate base template' below for details.

To run the app, enter the following commands:
- python3 setup.py install
- export PYGEOAPI_CONFIG=pygeoapi-config.yml
- export PYGEOAPI_OPENAPI=pygeoapi-openapi.yml
- pygeoapi openapi generate $PYGEOAPI_CONFIG > $PYGEOAPI_OPENAPI
- pygeoapi serve

### Using an alternate base template

- Open the pygeoapi config file.
- Under 'server' and 'templates', add a new key, `base`. The value will be the relative path to the file, referenced from its location in the templates folder. For example, to use the `_base_geoca.html` base template, add the following:
```
templates:
        path: /path/to/templates
        static: /path/to/static/files
        base: _base_geoca.html
```
- From a terminal, enter the following command: python3 setup.py install
- Reset your server

### Translations

- Open the pygeoapi config file. By default this will be pygeoapi-config.yml.
- Under 'server', add the key 'locale_dir' and set the value to the location of the locale folder:
```
server:
    locale_dir: /path/to/locale
```
NOTE: Use the ***Absolute*** path for this directory.
- If your version of babel is 3.0 or higher:
  - Open the default mapping file `babel-mapping.ini`
  - Comment out or remove the `jinja2.ext.autoescape` and `jinja2.ext.with_` extensions. These extensions are now depretiated.
  - Keep the `jinja2.ext.i18n` extension only and save the file:
  ```
  [python: **.py]
  [jinja2: **/templates/**.html]
  # extensions=jinja2.ext.i18n,jinja2.ext.autoescape,jinja2.ext.with_
  extensions=jinja2.ext.i18n
  ```
- Compile the .po files by running the following.:
```
# English
pybabel compile -d <path/to/locale> -l en
# French
pybabel compile -d <path/to/locale> -l fr
```
- From a terminal, enter the following command: python3 setup.py install
- Restart your server

## Updating Translations

### Adding Translations

- When new translations are added, the messages.pot file needs to be rebuilt. To do this, run the following:
`pybabel extract -F babel-mapping.ini -o <path/to/locale>/messages.pot <input/directory/to/translate>`
- Rebuild the .po files for each language:
```
# English
pybabel update -d <path/to/locale> -l en -i <path/to/locale>/messages.pot
# French
pybabel update -d <path/to/locale> -l fr -i <path/to/locale>/messages.pot
```
- Compile the .po files by running the following.:
```
# English
pybabel compile -d <path/to/locale> -l en
# French
pybabel compile -d <path/to/locale> -l fr
```
- From a terminal, enter the following command: python3 setup.py install
- Restart your server
