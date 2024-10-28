# theta-client community documentation site

## setup for contribution to docs

On WSL on Windows 11

Virtual environment

```text
python -m venv venv
source venv/bin/activate
```

```text
pip install mkdocs-material
pip install pillow cairosvg
pip install mkdocs-glightbox
```

## references

* [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

## troubleshooting

pip not found

```
which pip
/home/craig/.local/bin/pip
```

set PATH or run `python -m pip`