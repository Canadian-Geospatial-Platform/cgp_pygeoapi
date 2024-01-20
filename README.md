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
  - Comment out the extensions line and save the file. These extensions are now depretiated:
  ```
  [python: **.py]
  [jinja2: **/templates/**.html]
  # extensions=jinja2.ext.i18n,jinja2.ext.autoescape,jinja2.ext.with_
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
