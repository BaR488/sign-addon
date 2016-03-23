# Sign Add-on

Sign a Firefox add-on with Mozilla's
[web service](http://addons-server.readthedocs.org/en/latest/topics/api/signing.html).

[![Build Status](https://travis-ci.org/mozilla/sign-addon.svg?branch=master)](https://travis-ci.org/mozilla/sign-addon)

## Installation

    npm install sign-addon

## Getting started

To sign add-ons, you first need to generate API credentials, a JWT issuer and
secret, from the
[AMO Developer Hub](https://addons.mozilla.org/en-US/developers/addon/api/key/).

Currently, this is intended for use in [NodeJS](https://nodejs.org/) only
and should work in 0.12 or higher.

## Command line use

TODO: add a command line script
([issue #9](https://github.com/mozilla/sign-addon/issues/9)).

## Programmatic use

Here is how to retrieve a signed version of an
[XPI file](https://developer.mozilla.org/en-US/docs/Mozilla/XPI):

````javascript
import signAddon from 'sign-addon';

signAddon(
  {
    xpiPath: '/path/to/your/addon.xpi',
    id: 'your-addon-id@somewhere',
    version: '0.0.1',
    apiKey: 'Your JWT issuer',
    apiSecret: 'Your JWT secret',
  })
  .then((result) => {
    if (result.success) {
      console.log("The following signed files were downloaded:");
      console.log(result.downloadedFiles);
    } else {
      console.error("Your add-on could not be signed!");
      console.error("Check the console for details.");
    }
    console.log(result.success ? "SUCCESS" : "FAIL");
  })
  .catch((error) => {
    console.error("Signing error:", error);
  });
````

## Development

Here's how to set up a development environment for the `sign-addon` package.
Install all requirements and run tests from the source:

    npm install
    npm start
