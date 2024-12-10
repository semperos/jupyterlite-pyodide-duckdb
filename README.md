# Jupyterlite with Pyodide, DuckDB, and more

This repository provides a build configuration of Jupyterlite suitable for sensitive environments, where all components should be downloaded at build time and notebooks should not be able to pull down packages from the Internet.

## Building

```shell
uv run jupyter lite build
```

Once complete, copy `_output` somewhere your web server expects and open `lab/index.html` to get started.

Quick local webserver if needed for testing:

```shell
python3 -m http.server 9876
```

## Configuration

JupyterLite has two separate configuration planes:

* Build time in `jupyter_lite_config.json`
* Run time in `jupyter-lite.json`

In particular, the configuration in this repository pulls down Pyodide at build time and ensures the use of that bundled Pyodide installation at run time. In addition, the `comm` package is pulled down at build time to prevent needing to fetch it on the client.

The option to forbid falling back to PyPI is set to `true` in `jupyter-lite.json`. If you want to allow `%pip install` cells in your notebooks for packages not already included in this build, you can change this to `false`.
