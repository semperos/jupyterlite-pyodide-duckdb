# Jupyterlite with Pyodide, DuckDB, and more

Jupyter provides a notebook interface for running code and rendering Markdown.

Pyodide provides a WebAssembly (WASM) execution environment for Python code.

This repo uses [uv](https://docs.astral.sh/uv/) to manage Python dependencies; includes Pyodide at build time; and pulls in DuckDB, pandas, matplotlib, and several other libraries for data analysis workloads.

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
