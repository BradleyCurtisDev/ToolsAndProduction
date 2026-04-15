# Public API Documentation

## What I Did

For this task I had to write public facing documentation for my asset scanner tool from week 2. I decided to use Sphinx to build the docs and GitHub Pages to host them online, because my lecturer mentioned both of those as good options and they are used a lot in real projects.

## What Sphinx Is

Sphinx is a tool that takes text files you write and turns them into a proper looking website. The files you write are in a format called reStructuredText, which is a bit like Markdown but with more options for things like tables and parameter lists. Once you run Sphinx it generates all the HTML, CSS, and JavaScript for you so you dont have to write any of that yourself.

## Setting It Up

First I installed Sphinx and a theme called Read the Docs, which makes the site look professional.

```
py -m pip install sphinx sphinx-rtd-theme
```

Then I created a docs folder inside my Week 5 folder. Inside that I made a source folder which is where all the files I write go, and a build folder which is where Sphinx puts the generated website. The build folder never gets pushed to GitHub because it gets generated automatically.

The main files I created were.

- conf.py, which tells Sphinx the project name and which theme to use.
- index.rst, which is the home page of the docs site.
- usage.rst, which explains how to run the scanner and the report generator.
- api.rst, which is the full API reference for every function in both scripts.

## Writing the Docs

The api.rst file was the main piece of work. For each function I wrote what it does, what parameters it takes, what it returns, and what errors it can produce. I did this for all the functions in scan_assets.py and generate_report.py. Using Sphinx tables made this look a lot cleaner than just writing it in plain Markdown.

## Building It Locally

To build the site and preview it before pushing to GitHub I ran this command.

```
py -m sphinx "Week 5/docs/source" "Week 5/docs/build/html"
```

Then I opened the index.html file in my browser to check it looked right.

## Deploying to GitHub Pages

I created a GitHub Actions workflow file at .github/workflows/docs.yml. This means every time I push to the main branch, GitHub automatically runs Sphinx and publishes the output to GitHub Pages. I do not have to manually build or upload anything, it all happens on its own.

To turn GitHub Pages on I went to the repository settings, found the Pages section, and set the source to the gh-pages branch that Actions publishes to.

## What the End Result Is

The docs are hosted as a public website that anyone can visit. It has a sidebar with navigation, a search bar, and all the API reference tables formatted properly. The source files stay in the repository and the built website is handled entirely by GitHub.
