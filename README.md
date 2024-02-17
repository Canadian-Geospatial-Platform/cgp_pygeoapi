# cgp_pygeoapi

## About

The files included in this repository are based on Environment and Climate Change Canada's implementation of [pygeoapi](https://pygeoapi.io/): [msc-pygeoapi](https://github.com/ECCC-MSC/msc-pygeoapi).
These templates are compatible with the [GoC Web Experience Toolkit (WET)](https://wet-boew.github.io/GCWeb/index-en.html) themes.

A set of french translation files are included in the `locale` folder. These files were created using [Babel](https://babel.pocoo.org/en/latest/index.html) using translations from [msc-pygeoapi](https://github.com/ECCC-MSC/msc-pygeoapi) and the [Canada.ca theme](https://wet-boew.github.io/GCWeb/index-en.html).

## Installation

### Templates and static files

- Clone this repository to any folder within your pygeoapi project.
- Open the pygeoapi config file. By default this will be pygeoapi-config.yml.
- Under 'server', uncomment the 'templates' section and edit the 'path' and 'static' values to point to the new folders:
```
templates:
        path: /path/to/templates
        static: /path/to/static/files
```
NOTE: The paths in your config file must be ***Absolute*** paths only. Resources referenced using relative paths won't load properly and throw a 404 error.
- save your changes and restart your server

### Using an alternate base template

- Open the pygeoapi config file.
- Under 'server' and 'templates', add a new key, `base`. The value will be the relative path to the file, referenced from its location in the templates folder. For example, to use the `_base_geoca.html` base template, add the following:
```
templates:
        path: /path/to/templates
        static: /path/to/static/files
        base: _base_geoca.html
```
- Reset your server

### Geocore Provider

- copy the `cgp.py` file to the following directory:
```
pygeoapi/lib/python3.10/site-packages/pygeoapi-0.16.dev0-py3.10.egg/pygeoapi/provider/
```
- open `plugin.py`. It can be found in the following directory:
```
/pygeoapi/lib/python3.10/site-packages/pygeoapi-0.16.dev0-py3.10.egg/pygeoapi/
```
- add the following provider to the PLUGINS.provider object:
```
'GeoCore': 'pygeoapi.provider.cgp.GeoCoreProvider'
```
- In your `pygeoapi-config.yml` file copy the contents of the `geocore_config.txt` file into the resources object.
- Restart your server to apply the changes.

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
- Restart your server
