# Geonetwork Manual and Help

Documentation for GeoNetwork opensource is available via https://geonetwork-opensource.org.

This documentation is written under the creative commons license [Attribution-ShareAlike 3.0 Unported (CC BY-SA 3.0)](LICENSE.md).

Reference:

* [Documentation Writing Guide](docs/devel/docs/docs.md)

## Communication

The [project issue tracker](https://github.com/geonetwork/core-geonetwork/issues) is used for communication, with ongoing topics tagged [documentation](https://github.com/geonetwork/core-geonetwork/issues?q=is%3Aissue+label%3Adocumenation).

## Material for MkDocs

Documentation is [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) which is a Markdown documentation framework written on top of [MkDocs](https://www.mkdocs.org/).

If you are using python3:

1. Install using ``pip3`` and build:

   ```bash
   pip3 install -r requirements.txt
   ```

2. Use ***mkdocs** to preview locally:

   ```bash
   mkdocs serve
   ```
      
3. Preview: http://localhost:8000

   Preview uses a single version, so expect some warnings from version chooser:
   ```
   "GET /versions.json HTTP/1.1" code 404
   ```

4. Optional: Preview online help:
   
   ```bash
   mkdocs serve --config-file help.yml  
   ```

### VirtualEnv

If you use a python virtual environment:

1. Activate virtual environment:

   ```bash
   virtualenv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```
   
2. Use ***mkdocs*** to preview from virtual environment:

   ```bash
   mkdocs serve
   ```

3. Preview: http://localhost:8000

### Docker

If you are not familiar with python the mkdocs-material website has instructions for docker:

1. Run mkdocs in Docker environment:

   ```
   docker pull squidfunk/mkdocs-material
   docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
   ```
   
2. Preview: http://localhost:8000

## Maven Integration

1. Build documentation with ``compile`` phase:
   ```
   mvn compile
   ```

2. Assemble ``zip`` with ``package`` phase:
   ```bash
   mvn package
   ```

3. Both ``install`` and ``deploy`` are skipped (so ``mvn clean install`` is fine).

4. Use default profile to only build the default english docs:

   ```
   mvn install -Pdefault
   ```
   
## Deploy

We use ``mike`` for publishing to https://geonetwork.github.io using `<major>.<minor>` version:

1. Define the remote `website`:
   
   ```bash
   git remote add website https://github.com/geonetwork/geonetwork.github.io
   git fetch website
   git checkout -b gh-pages website/gh-pages
   git branch --set-upstream-to=websigte/gh-pages
   ```
   
   The file ``mkdocs.yml`` setting for ``remote_name`` is set to ``website``.
   To test with your own for, use ``--remote origion`` in the examples below.
   
2. To deploy SNAPSHOT development docs from the `main` branch to website `gh-pages` branch:

   ```bash
   mike deploy --push --update-aliases 4.4 devel
   ```
    
3. To deploy documentation for a new release:
   
   ```bash
   mike deploy --push --update-aliases 4.2 stable
   ```
   
   When starting a new branch you can make it the default:
   
   ```bash
   mike set-default --push 4.2
   ```

4. To publish documentation for a maintenance release:

   ```bash
   mike deploy --push --update-aliases 3.12 maintenance
   ```

5. To show published versions:

   ```bash
   
   mike list
   ```

4. To preview things locally (uses your local ``gh-pages`` branch):
   
   ```bash
   mike serve
   ```

Reference:

* https://squidfunk.github.io/mkdocs-material/setup/setting-up-versioning/
* https://github.com/squidfunk/mkdocs-material-example-versioning
* https://github.com/jimporter/mike