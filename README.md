# Mozilla HTTP Observatory

The Mozilla HTTP Observatory is a set of tools to analyze your website and inform you if you are utilizing the many available methods to secure it.

It is split into three projects:

* [http-observatory](https://github.com/mozilla/http-observatory) - scanner/grader
* [observatory-cli](https://github.com/mozilla/observatory-cli) - command line interface
* [http-observatory-website](https://github.com/mozilla/http-observatory-website) - web interface

## Scanning sites with the HTTP Observatory

Sites can be scanned using:

* [observatory.mozilla.org](https://observatory.mozilla.org/) - the online interface
* [observatory-cli](https://github.com/mozilla/observatory-cli) - the official node.js command line interface
* [java-http-observatory-api](https://github.com/stoennies/java-http-observatory-api) - a third party java library and command line interface

## Contributing

### Prerequisites
* Python 3.11
* Git
* pip

#### Notes

These instructions assume that you have a working Python3.11 development environment with `pip` installed and capable of building requirements, which may require installing an additional python OS package (`-dev`, `-devel`).

```bash
# Clone the code
$ git clone https://github.com/mozilla/http-observatory.git
$ cd http-observatory
# Install poetry
$ pip install poetry
# Install the project dependencies and scripts
$ poetry install
# Activate the virtual environment
$ poetry shell
# Install the pre-commit hooks
$ pre-commit install
```

## Running a scan from the local codebase, without DB, for continuous integration
```bash
# Install the HTTP Observatory
$ git clone https://github.com/mozilla/http-observatory.git
$ cd http-observatory
$ pip install poetry
$ poetry install
```

### Using the scanner function calls
```python
>>> from httpobs.scanner import scan
>>> scan('observatory.mozilla.org')  # a scan with default options
>>> scan('observatory.mozilla.org',  # all the custom options
         http_port=8080,             # http server runs on port 8080
         https_port=8443,            # https server runs on port 8443
         path='/foo/bar',            # don't scan /, instead scan /foo/bar
         cookies={'foo': 'bar'},     # set the "foo" cookie to "bar"
         headers={'X-Foo': 'bar'},   # send an X-Foo: bar HTTP header
         verify=False)               # treat self-signed certs as valid for tests like HSTS/HPKP
```

### The same, but with the local CLI
```bash
$ poetry shell
$ httpobs-local-scan --http-port 8080 --https-port 8443 --path '/foo/bar' \
    --cookies '{"foo": "bar"}' --headers '{"X-Foo": "bar"}' --no-verify mozilla.org
```

## Authors

* April King

## License

* Mozilla Public License Version 2.0
