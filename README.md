# fk-html

HTML for fckt, built as code runs and written out with everything that needs escaping escaped.

```kotlin
import uk.m4xy.html.Htmls.*
import uk.m4xy.html.Tags.*

page {
  html {
    head { title { text("Links") } }
    body {
      h1 { text("Links") }
      ul([classes(["plain"])]) {
        links.forEach { link -> li { a(link.url) { text(link.name) } } }
      }
    }
  }
}
```

`page` gives the document as text, starting with its doctype. Each element of `Tags` takes its
attributes, then a block, and what the block adds goes inside it, so a loop or a `when` builds
HTML as it builds anything else. `text` adds text, escaped where it's written; `raw` adds HTML
that's trusted, as another library wrote it, as it is. `attribute("href", "/")` makes an attribute,
`flag("disabled")` one without a value, and `classes` and `id` the usual ones. `a` takes where it
links to first, and `img` its source and what it shows, in words. `main` is `mainElement`, as
`main` is a program's.

The builder is the `Markup` effect: each element handles it for its block, collecting what's added
as its children. `markup { ... }` gives what a block adds as an `Html`, a value: an `Element`, with
its attributes and children, `Text`, `Raw` or a `Fragment` of pieces, which can be made directly
too, and `render` writes one as text. An element that can't have children, as `br` or `img`, has no
end tag.

## Building

```sh
kiln build          # compiles and tests it
kiln publishLocal   # for other projects: library("uk.m4xy:fk-html:0.1.0")
```
