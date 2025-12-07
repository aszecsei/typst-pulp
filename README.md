# Pulp Novel Template

A Typst template for creating mass-market paperback novels with 1990s pulp fiction aesthetics.

## Project Structure

```
typst-pulp/
├── template/
│   ├── config.typ          # Configuration and font settings
│   ├── page-setup.typ      # Page dimensions, margins, and text styling
│   ├── headers.typ         # Page header functions and chapter tracking
│   ├── content.typ         # Chapter, part, scene break, and epigraph functions
│   ├── front-matter.typ    # Half-title, title page, copyright, dedication
│   ├── back-matter.typ     # About author, also-by, teaser, advertisement pages
│   └── template.typ        # Main template module (imports everything)
└── example.typ             # Example document using the template
```

## Quick Start

### Using the Example

Compile the example document:

```bash
typst compile example.typ
```

### Creating Your Own Book

1. Create a new `.typ` file
2. Import the template modules:

```typst
#import "template/config.typ": default-config
#import "template/headers.typ": apply-headers
#import "template/content.typ": chapter, part, scene-break, epigraph
#import "template/front-matter.typ": *
#import "template/back-matter.typ": *
```

3. Configure your book:

```typst
#let config = (
  title: "Your Book Title",
  subtitle: "A Thriller",
  author: "Your Name",
  publisher: "Your Publisher",
  year: "2025",
  isbn: "0-555-12345-6",
)
```

4. Build your book structure:

```typst
// Front matter
#half-title-page(config.title)
#title-page(config.title, subtitle: config.subtitle, config.author, config.publisher)
#copyright-page(config.title, config.author, config.publisher, config.year, config.isbn)
#dedication[Your dedication text]
#table-of-contents()

// Enable headers and page numbers
#show: apply-headers(config)
#counter(page).update(1)

// Main content
#part("ONE", "Part Title")
#chapter(1, title: "Chapter Title")

#chapter-opening[
Your opening paragraph here. The first three words will be in ALL CAPS automatically.
]

Your story content continues here...

#scene-break()

More content...

// Back matter
#set page(numbering: none)
#also-by(config.author, ("Book 1", "Book 2"))
#about-author[Your bio]
```

## Available Functions

### Front Matter
- `half-title-page(title)` - Half title page
- `title-page(title, subtitle, author, publisher)` - Full title page
- `copyright-page(title, author, publisher, year, isbn)` - Copyright/legal page
- `dedication(content)` - Dedication page
- `table-of-contents()` - Styled table of contents

### Content
- `chapter(number, title: none)` - Chapter heading
- `chapter-opening(content)` - Opening paragraph with no indent
- `part(number, title)` - Part divider (no headers)
- `scene-break()` - Scene break marker (∗ ∗ ∗)
- `epigraph(quote, attribution)` - Epigraph/quote

### Back Matter
- `about-author(bio)` - Author biography
- `also-by(author, books)` - List of other books
- `teaser-page(content)` - Preview/teaser page
- `ad-page(headline, body)` - Advertisement page

## Features

- **Page Headers**:
  - Left pages: Book title (centered) with page number (left-aligned)
  - Right pages: Chapter title (centered) with page number (right-aligned)
  - No headers on part pages

- **Page Layout**: Mass-market paperback size (4.25" x 6.87")

- **Styling**: Classic pulp fiction typography with justified text, proper indentation, and vintage fonts

## Customization

### Fonts

Edit `template/config.typ` to change fonts:

```typst
#let display-font = "Your Display Font"  // Chapter headings
#let header-font = "Your Header Font"    // Page headers
#let body-font = "Your Body Font"        // Main text
```

### Page Dimensions

Edit `template/page-setup.typ` to change page size and margins.

### Header Style

Edit `template/headers.typ` to customize header appearance and spacing.

## License

This template is provided as-is for creating pulp fiction novels.
