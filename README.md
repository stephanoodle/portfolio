# Portfolio

Stephanie Coulter's portfolio: a landing page and case studies, published with GitHub Pages at https://stephanoodle.github.io/portfolio/.

| File | What it is |
|---|---|
| `index.html` | The landing page: intro, then one card per case study |
| `_data/writing.yml` | Writing samples, grouped by kind of article |
| `_data/kind_words.yml` | Recommendation excerpts |
| `_data/experience.yml` | The experience timeline |
| `case-studies/*.md` | The case studies. The `title`, `description`, and `tags` at the top feed the cards. An optional `image` sets the link-preview picture |
| `_layouts/default.html` | The page wrapper: header, navigation, footer, and the search and social tags (canonical link, `og:` tags for LinkedIn, structured data). `og:image` only on pages with an `image`, sized for 1600 × 1200. No Twitter tags |
| `_layouts/case-study.html` | The case study page: topics, text, and a closing prompt |
| `services.md` | Services and prices, at `/services/`. Linked from the sidebar and the landing page. Prices match the services sheet and support sheet in the Professional Development repo |
| `guides/*.md` | Guides written for the people the work helps. The domain guide isn't linked from the landing page; the Open Library API guide is, under Writing samples, API documentation (Nov 20, 2026) |
| `_layouts/guide.html` | The guide page: like a case study, but links back home |
| `assets/style.css` | Styles, with dark mode |
| `assets/favicon-32.png`, `assets/apple-touch-icon.png` | The favicon: an SC monogram in yellow on purple, 32px for tabs and 180px for phone home screens (Nov 23, 2026). Source is `job-search/avatar/monogram.svg` in the Professional Development repo |
| `assets/og/*.png` | Link-preview pictures, one per case study, 1600 × 1200. Five are the Contra project cards, copied from `job-search/contra-media/` in the Professional Development repo. Four (controlled vocabulary, AI search visibility, ticket queue, registrar compliance) were made Nov 20, 2026 to match, from each case study's `title` and `description` |
| `_config.yml` | Site settings, including `jekyll-sitemap`, and the author and LinkedIn link the search and social tags in `default.html` use. If the site moves to its own domain, `url` becomes that domain and `baseurl` becomes `""` |

## Adding a case study

1. Add a `.md` file to `case-studies/`, starting with the same `layout`, `title`, `description`, and `tags` block as the others
2. Add its file name to the `order` list in `index.html`
3. For a link-preview picture, add a 1600 × 1200 PNG to `assets/og/` and an `image:` line pointing to it
