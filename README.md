# Requirements Template

This is the template for requirements published by Netwerk Digitaal Erfgoed.

Requirements are written in Markdown and transformed to HTML using the
[Bikeshed preprocessor](https://tabatkins.github.io/bikeshed/).

## Generate HTML

To view HTML output locally (using a [Docker container](https://github.com/netwerk-digitaal-erfgoed/bikeshed-docker)),
run:

```bash
make spec
```

and open the `index.html` file:

```bash
open index.html
```

Alternatively, to update the HTML every time you make changes to [the source document](index.bs):

```bash
make watch
```
