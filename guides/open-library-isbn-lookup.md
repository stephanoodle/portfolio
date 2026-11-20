---
layout: guide
title: "Looking Up a Book by ISBN with the Open Library API"
description: "Get a book's title, author, and cover from its ISBN with the Open Library API. Free, no key."
tags: ["Guide", "API"]
---

# Looking Up a Book by ISBN

**Stephanie Coulter · November 2026**

This guide walks through getting a book's title, author, and cover from its ISBN, using three Open Library APIs: [Books](https://openlibrary.org/dev/docs/api/books), [Authors](https://openlibrary.org/dev/docs/api/authors), and [Covers](https://openlibrary.org/dev/docs/api/covers). It's for developers adding book details to an app, and for librarians checking or filling in records. The APIs are free and need no key.

The examples use `curl` and *Fantastic Mr. Fox*, ISBN 9780140328721. Each example also has a link you can open in a browser. Responses are as of November 2026.

## Before You Start

Please send a `User-Agent` header with a name for your app or project and a contact email, as the [API guidelines](https://openlibrary.org/developers/api) ask. It's optional, but requests that include it can make 3 calls a second instead of 1.

```
$ curl -H "User-Agent: MyReadingList (you@example.com)" ...
```

Every example below includes this `User-Agent` header. Use your own name and email.

## Getting the Edition

An ISBN belongs to one edition of a book, not the book as a whole. The Books docs explain the difference in [Learnings about Works v Editions](https://openlibrary.org/dev/docs/api/books). Ask for the edition by ISBN:

```
$ curl -L -H "User-Agent: MyReadingList (you@example.com)" \
  https://openlibrary.org/isbn/9780140328721.json
```

In a browser: <https://openlibrary.org/isbn/9780140328721.json>

Open Library redirects this to the edition's own address, `/books/OL7353617M.json`. The `-L` tells `curl` to follow the redirect. Without it, the response is a `302 Found` redirect with an empty body.

The full response is long. These are the fields you'll use, trimmed from the full response:

```json
{
  "title": "Fantastic Mr. Fox",
  "authors": [{ "key": "/authors/OL34184A" }],
  "publishers": ["Puffin"],
  "publish_date": "October 1, 1988",
  "number_of_pages": 96,
  "isbn_10": ["0140328726"],
  "isbn_13": ["9780140328721"],
  "covers": [15152634, 8739161, -1]
}
```

The ISBN can be 10 or 13 digits, with or without hyphens. All three of these return the same edition: `9780140328721`, `0140328726`, `978-0-14-032872-1`.

If Open Library doesn't have the ISBN, the response is `404 Not Found`.

## Getting the Author's Name

The edition lists each author by a key, such as `/authors/OL34184A`, not by name. To get an author's name, request their key from the Authors API:

```
$ curl -H "User-Agent: MyReadingList (you@example.com)" \
  https://openlibrary.org/authors/OL34184A.json
```

In a browser: <https://openlibrary.org/authors/OL34184A.json>

The response, trimmed:

```json
{
  "name": "Roald Dahl",
  "birth_date": "13 September 1916",
  "death_date": "23 November 1990",
  "key": "/authors/OL34184A",
  ...
}
```

A book with three authors takes three calls, one for each author's key. The edition's `contributions` field, when it's there, names other people as plain text, such as illustrators: `"Tony Ross (Illustrator)"`.

## Getting the Cover

Covers come from a separate address, `covers.openlibrary.org`, as images, not JSON. Each cover comes in three sizes, set by the letter at the end of the address:

- `S`: small, for thumbnails. 38 × 58 pixels for this cover
- `M`: medium, for a book's details page. 180 × 275 pixels
- `L`: large. 326 × 500 pixels

Other covers have other dimensions, but the same three sizes.

The edition's `covers` field lists its cover IDs: `[15152634, 8739161, -1]`. Request the first ID in the list, `15152634`:

```
$ curl -H "User-Agent: MyReadingList (you@example.com)" \
  -o cover.jpg https://covers.openlibrary.org/b/id/15152634-M.jpg
```

In a browser: <https://covers.openlibrary.org/b/id/15152634-M.jpg>

You can also ask for a cover by ISBN, without getting the edition first:

```
$ curl -H "User-Agent: MyReadingList (you@example.com)" \
  -o cover.jpg "https://covers.openlibrary.org/b/isbn/9780140328721-M.jpg?default=false"
```

Use the cover ID when you have it. Cover lookups by ISBN are rate-limited, and cover lookups by cover ID aren't. See Gotchas.

## Gotchas

**An empty response from `/isbn/`.** The ISBN address answers with a `302 Found` redirect to the edition, and an empty body. Add `-L` so `curl` follows the redirect. Most HTTP libraries follow redirects by default; check yours.

**A missing cover looks like a working one.** When there's no cover, Open Library still returns `200 OK` with a blank 1-pixel image, 43 bytes. Add `?default=false` to get `404 Not Found` instead, so you can show your own placeholder.

**A `-1` in `covers`.** Some editions list `-1` as a cover ID. It isn't a cover; requesting it returns the same blank image. Skip it and use the next ID.

**`403 Forbidden` on covers.** Cover lookups by ISBN, OCLC, or LCCN are limited to 100 every 5 minutes per IP address. Lookups by cover ID aren't limited.

**Many ISBNs at once.** Please don't loop over thousands of ISBNs. The [API guidelines](https://openlibrary.org/developers/api) ask you to cache responses and to use the [monthly data dumps](https://openlibrary.org/developers/dumps) for bulk work.

