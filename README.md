# CodeSee documentation

This is the [documentation website](https://docs.codesee.io/en/latest/) repo for [CodeSee](https://www.codesee.io/), a tool to help you visually understand your codebase.

## Documentation quickstart

This section shows you how to build the docs locally. This allows you to preview them while editing.

You need Python 3 installed on your machine (these instructions were tested with 3.9)

1. Clone the repo:
```
git clone https://github.com/Codesee-io/docs.git codesee-docs
```
2. Navigate into `codesee-doc`, and create a [virtual environment](https://docs.python.org/3/library/venv.html):
```
python -m venv venv
```
If you name your virtual environment something other than `venv` or `env`, add it to the `.gitignore`.
3. Activate your virtual environment: run the appropriate script for your system from `/venv/Scripts/`.
4. Install requirements:
```
pip install -r requirements.txt
```
5. You can now preview the docs locally with `mkdocs serve`, or build them with `mkdocs build`.