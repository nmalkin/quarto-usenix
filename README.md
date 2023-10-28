# Quarto Usenix (Journal) Style

This is a [journal format](https://quarto.org/docs/journals/) for [Quarto](https://quarto.org) that aims to match the [USENIX template](https://www.usenix.org/conferences/author-resources/paper-templates) for conferences such as USENIX Security, NSDI, OSDI, SOUPS, and [others](https://www.usenix.org/conferences).

## WARNING: read before you use this template

Please be aware that, if you compare the output of this template with the [USENIX sample PDF file](https://www.usenix.org/sites/default/files/usenix-2020-09.pdf), you'll find that there are subtle differences, such as link colors, spacing around environments, URL fonts, etc.
(Pull requests with fixes are welcome!)

Additionally:

### Tables are a Problem

Under the hood, Quarto uses [pandoc](https://pandoc.org/) for all document conversions, and pandoc generates tables using [longtable](https://www.ctan.org/pkg/longtable), which doesn't work in two-column layouts.
This is a [known and long-standing issue for pandoc](https://github.com/jgm/pandoc/issues/1023)
and [Quarto itself](https://github.com/quarto-dev/quarto-cli/discussions/2786#discussioncomment-3853259).
(Other templates [also face this problem](https://github.com/dfolio/quarto-ieee#unsuported-feature-and-limitations).)

I've [implemented the most commonly recommended workaround](_extensions/usenix/two_column_table.tex), which is what the official Quarto templates also use.
(See that file for more documentation and context.)
However:

- This only works for regular tables (`\begin{table}`).
  **Full-width tables (`\begin{table*}`) are still broken.**
  (As documented in the [file](_extensions/usenix/two_column_table.tex), you can switch between the two types, but having both is difficult.)

- I also encountered an odd **bug with longtable where entire pages would be omitted from the PDF**.
  I really suspect this is a problem with longtable (not this template, the workaround, Quarto, or pandoc), but I didn't track it down or confirm it with others.
  However, my only solution was to update the LaTeX that was output by Quarto, replacing longtables with regular tables.

Therefore, **if you plan to have tables in your paper, think twice before using this template** (or any Pandoc-based workflow, assuming you're dealing with two-column articles.)


## Creating a new article

To create a new article using this format:

```bash
quarto use template nmalkin/quarto-usenix
```

This will create a new directory with an example document that uses this format.

## Using with an existing document

To add this format to an existing document:

```bash
quarto add nmalkin/quarto-usenix
```

Then, add the format to your document options:

```yaml
format:
  usenix-pdf: default
```    

## Example

Here is the source code for a minimal sample document: [template.qmd](template.qmd).
It is meant to generate output that matches that of the [USENIX LaTeX template](https://www.usenix.org/sites/default/files/usenix2019_v3.1.tex).
