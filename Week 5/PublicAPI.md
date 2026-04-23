# Public API Documentation

## What I Did

For this task I wanted to create public facing documentation for my asset scanner tool from week 2. I decided to use Sphinx (Sphinx — Sphinx documentation, s.d.) to build the docs and GitHub Pages (GitHub Pages documentation, s.d.) to host them online.

## What Sphinx Is

Sphinx is a tool that takes text files you write and turns them into a proper looking website. The files you write are in a format called reStructuredText, which is a bit like Markdown but with more options for things like tables and parameter lists. Once you run Sphinx it generates all the HTML, CSS, and JavaScript for you so you dont have to write any of that yourself. (Sphinx — Sphinx documentation, s.d.)

## Setting It Up

I installed Sphinx and a theme called Read the Docs (A “How to” Guide for Sphinx + ReadTheDocs — Sphinx-RTD-Tutorial documentation, s.d.), which makes the site look professional.

```
py -m pip install sphinx sphinx-rtd-theme
```

Then I created a docs folder inside my Week 5 folder. Inside that I made a source folder which is where all the files I write go, and a build folder which is where Sphinx puts the generated website. The build folder never gets pushed to GitHub because it gets generated automatically. (Deploying Sphinx on Read the Docs, s.d.)

The main files I created were.

- conf.py, which tells Sphinx the project name and which theme to use.
- index.rst, which is the home page of the docs site.
- usage.rst, which explains how to run the scanner and the report generator
- api.rst, which is the full API reference for every function in both scripts.

## Writing the Docs

The api.rst file was the main piece of work. For each function I wrote what it does, what parameters it takes, what it returns, and what errors it can produce. I did this for all the functions in scan_assets.py and generate_report.py. Using Sphinx tables made this look a lot cleaner than just writing it in plain Markdown.

## Deploying to GitHub Pages

I created a GitHub Actions workflow file at .github/workflows/docs.yml. (Writing workflows, s.d.) This means every time I push to the main branch, GitHub automatically runs Sphinx and publishes the output to GitHub Pages. (GitHub Actions, 2026) I do not have to manually build or upload anything, it all happens on its own. (Workflows, s.d.)


## What the End Result Is

- https://bradleycurtisdev.github.io/ToolsAndProduction/

The docs are hosted as a public website that anyone can visit. It has a sidebar with navigation, a search bar, and all the API reference tables formatted properly. The source files stay in the repository and the built website is handled entirely by GitHub.

## Bibliography

A “How to” Guide for Sphinx + ReadTheDocs — Sphinx-RTD-Tutorial documentation (s.d.) At: https://sphinx-rtd-tutorial.readthedocs.io/en/latest/ (Accessed  11/03/2026).

Deploying Sphinx on Read the Docs (s.d.) At: https://docs.readthedocs.com/platform/stable/intro/sphinx.html (Accessed  12/03/2026).

GitHub Actions (2026) At: https://github.com/features/actions (Accessed  10/03/2026).

GitHub Pages documentation (s.d.) At: https://docs-internal.github.com/en/pages (Accessed  09/03/2026).

Sphinx — Sphinx documentation (s.d.) At: https://www.sphinx-doc.org/en/master/ (Accessed  09/03/2026).

Workflows (s.d.) At: https://docs-internal.github.com/en/actions/concepts/workflows-and-actions/workflows (Accessed  13/03/2026).

Writing workflows (s.d.) At: https://docs-internal.github.com/en/actions/how-tos/write-workflows (Accessed  13/03/2026).


## Declared Assets

This document was modified and formatted with the use of:

- Claude Sonnet 4.6 (Claude, s.d.)

Claude (s.d.) At: https://claude.ai/login?from=logout (Accessed  14/03/2026).


- Google Gemini 3.1 Pro (Google Gemini, s.d.)

At: https://gemini.google.com (Accessed  14/03/2026).
