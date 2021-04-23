# spherex-tex

**SPHEREx TeX document resources and Docker environment.**

## Docker

To compile a document using the Docker image and the default SPHEREx Makefiles:

```sh
docker run -v `pwd`:/workspace -w /workspace ghcr.io/spherex/spherex-tex:latest sh -c 'make'
```

## spherex class reference

`spherex-tex` provides a custom class, named `spherex`, for formatting TeX documents. This section describes the commands and options that are provided by the `spherex` class.

### spherex documentclass and options

Use the `spherex` class through the `\documentclass` command:

```tex
\documentclass[MS]{spherex}
```

In this example, the `MS` option shows that the document is a _module specification_ (see below).

#### Document category options

Each SPHEREx document category has a corresponding option:

| Option | Document category     | Example                       |
| ------ | --------------------- | ----------------------------- |
| RQ     | Requirements          | `\documentclass[RQ]{spherex}` |
| PM     | Project Management    | `\documentclass[PM]{spherex}` |
| MS     | Module Specification  | `\documentclass[MS]{spherex}` |
| DP     | Data Products         | `\documentclass[DP]{spherex}` |
| TN     | Technical Note        | `\documentclass[TN]{spherex}` |
| IF     | Interface             | `\documentclass[IF]{spherex}` |
| TR     | Test/Technical Report | `\documentclass[TR]{spherex}` |
| RV     | Review Materials      | `\documentclass[RV]{spherex}` |
| OP     | Operations Procedures | `\documentclass[OP]{spherex}` |

### Preamble commands

`spherex` provides several commands that you can use in the preamble (before `\begin{document}`) to set metadata that appears in the document's title and header/footer.

#### \ssdcHandle

The document's handle. For example:

```tex
\ssdcHandle{SSDC-MS-000}
```

#### \version

This command specifies the document's version:

```tex
\version{1.0}
```

#### \docDate

This command specifies the publication date in `YYYY-MM-DD` format:

```tex
\docDate{2021-01-01}
```

In the SPHEREx document templates, the `\docDate` is automatically set from Git metadata. However, you can override that date by setting the date with this command _after_ the `\input{meta}` line in the preamble.

#### \title and \shortTitle

For most document categories, use the `\title` command to set the documents title. You can optionally also set an abbreviated title with the `\shortTitle` command that is used in page headers:

```tex
\title{Technical note title}
\shortTitle{Short Title}
```

#### \spherexlead

This command specifies the document's SPHEREx lead author:

```tex
\spherexlead[email=galileo@example.com]{Galileo Galilei}
```

#### \ipaclead

This command specifies the document's IPAC lead author:

```tex
\ipaclead[email=galileo@example.com]{Galileo Galilei}
```

#### \author and \person

Aside from the lead authors (`\ipaclead` and `\spherexlead`), authors are specified with the `\author` command. Each author is on a separate line (using `\\`) and marked-up with a `\person` command:

```tex
\author{
  \person[email=galileo@example.com]{Galileo~Galilei} \\
  \person{Isaac~Newton}
}
```

You can optionally set an author's email address with the `email` keyword option.

#### \approved

This command provides metadata about the document's approval:

```tex
\approved{2021-01-01}{Edwin Hubble}
```

The first argument is the date of approval (`YYYY-MM-DD` format).

The second argument is the approver's name.

#### \modulename

For module specification (`MS`) documents, this command sets the name of the module:

```tex
\modulename{Example Module}
```

**This command replaces the standard `\title` command for setting the document's title in MS documents.**

#### \pipelevel

For module specification (`MS`) documents, this command sets the pipeline level:

```tex
\pipelevel{L2}
```

#### \diagramindex

For module specification (`MS`) documents, this command sets the diagram index:

```tex
\diagramindex{13}
```

### Title page

The title page is generated by the `\maketitle` command, which you should include right after the `\begin{document}` command. The `spherex` class customizes the appearance of the title page based on the document category and the available metadata.

### Macros

The `spherex` class provides common macros. See the bottom of the [spherex.cls](./texmf/tex/latex/spherex/spherex.cls) source for a listing.

## Bibliography

spherex-tex includes a centrally maintained BibTeX file for the SPHEREx project: [texmf/bibtex/bib/spherex.bib](./texmf/bibtex/bib/spherex.bib). To use this bibliography from documents, include:

```tex
\bibliography{spherex}
```
