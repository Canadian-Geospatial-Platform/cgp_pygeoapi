# cgp_pygeoapi

## Templates and static files

The template files included in this repository are based on Environment and Climate Change Canada's implementation of [pygeoapi](https://pygeoapi.io/): [msc-pygeoapi](https://github.com/ECCC-MSC/msc-pygeoapi).
These templates are compatible with the GoC Web Experience Toolkit (WET) themes.

## Installation

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
