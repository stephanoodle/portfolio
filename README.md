# Portfolio

Stephanie Coulter's portfolio: a landing page and case studies, published with GitHub Pages at https://stephanoodle.github.io/portfolio/.

| File | What it is |
|---|---|
| `index.html` | The landing page: intro, then one card per case study |
| `_data/writing.yml` | Writing samples, grouped by kind of article |
| `_data/kind_words.yml` | Recommendation excerpts |
| `_data/experience.yml` | The experience timeline |
| `case-studies/*.md` | The case studies. The `title`, `description`, and `tags` at the top feed the cards |
| `_layouts/default.html` | The page wrapper: header, navigation, footer, and the search and social tags (canonical link, `og:` tags for LinkedIn, structured data). No Twitter tags |
| `_layouts/case-study.html` | The case study page: topics, text, and a closing prompt |
| `services.md` | Services and prices, at `/services/`. Linked from the sidebar and the landing page. Prices match the services sheet and support sheet in the Professional Development repo |
| `guides/*.md` | Guides written for the people the work helps, not for hiring managers. Not linked from the landing page |
| `_layouts/guide.html` | The guide page: like a case study, but links back home |
| `assets/style.css` | Styles, with dark mode |
| `_config.yml` | Site settings, including `jekyll-sitemap`, and the author and LinkedIn link the search and social tags in `default.html` use. If the site moves to its own domain, `url` becomes that domain and `baseurl` becomes `""` |

## Adding a case study

1. Add a `.md` file to `case-studies/`, starting with the same `layout`, `title`, `description`, and `tags` block as the others
2. Add its file name to the `order` list in `index.html`
