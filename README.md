# Portfolio

Stephanie Coulter's portfolio: a landing page and case studies, published with GitHub Pages at https://stephanoodle.github.io/portfolio/.

| File | What it is |
|---|---|
| `index.html` | The landing page: intro, then one card per case study |
| `case-studies/*.md` | The case studies. The `title` and `description` at the top feed the cards |
| `_layouts/default.html` | The page wrapper: header, footer, contact links |
| `assets/style.css` | Styles, with dark mode |
| `_config.yml` | Site settings. `baseurl` becomes `""` if the site moves to its own domain |

## Adding a case study

1. Add a `.md` file to `case-studies/`, starting with the same `layout`, `title`, and `description` block as the others
2. Add its file name to the `order` list in `index.html`
