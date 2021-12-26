# DFD Hugo Link Handling

Hugo module with partials and shortcodes for improved link handling, including GitHub compatibility

## Status

TBD

## GitHub Repository

<https://github.com/danielfdickinson/link-handling-mod-hugo-dfd>

## Features

TBD

## Basic Usage

### Importing the Module

1. The first step to making use of this module is to add it to your site or theme.  In your configuration file:

   ``config.toml``
   ```toml
   [module]
     [[module.imports]]
       path = "github.com/danielfdickinson/link-handling-mod-hugo-dfd"
   ```
   OR
   ``config.yaml``
   ```yaml
   module:
     imports:
       - path: github.com/danielfdickinson/link-handling-mod-hugo-dfd
   ```
2. Execute
   ```bash
   hugo mod get github.com/danielfdickinson/link-handling-mod-hugo-dfd
   hugo mod tidy
   ```
