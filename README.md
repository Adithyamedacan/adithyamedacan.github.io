# GitHub Documentation Site

This is a Jekyll-based documentation site for sharing GitHub usage guidelines with clients.

## Structure

```
.
├── _config.yml              # Jekyll configuration
├── _layouts/                # Page layouts
│   └── default.html        # Main layout template
├── _includes/              # Reusable components
│   └── navigation.html     # Navigation menu
├── assets/                 # Static assets
│   └── css/
│       └── style.css       # Site styles
├── index.md                # Home page
├── getting-started.md      # Getting started guide
├── repository-basics.md    # Repository basics
├── branching-merging.md    # Branching and merging
├── pull-requests.md        # Pull requests guide
├── collaboration.md        # Collaboration guide
├── best-practices.md       # Best practices
└── Gemfile                 # Ruby dependencies

```

## Local Development

1. **Install Jekyll:**
   ```bash
   gem install jekyll bundler
   ```

2. **Install dependencies:**
   ```bash
   bundle install
   ```

3. **Run locally:**
   ```bash
   bundle exec jekyll serve
   ```

4. **View site:**
   Open http://localhost:4000 in your browser

## Deployment

This site is automatically deployed to GitHub Pages when you push to the `main` branch via the GitHub Actions workflow in `.github/workflows/jekyll.yml`.

## Adding New Pages

1. Create a new markdown file in the root directory (e.g., `new-page.md`)
2. Add front matter:
   ```yaml
   ---
   layout: default
   title: New Page
   ---
   ```
3. Add the page to navigation in `_config.yml`:
   ```yaml
   navigation:
     - title: New Page
       url: /new-page
   ```

## Customization

- **Site title:** Edit `title` in `_config.yml`
- **Navigation:** Edit `navigation` array in `_config.yml`
- **Styles:** Modify `assets/css/style.css`
- **Layout:** Edit `_layouts/default.html`
- **Navigation component:** Edit `_includes/navigation.html`

## Features

- Responsive navigation with mobile menu
- Clean, modern design
- Syntax highlighting for code blocks
- Card-based home page layout
- Cross-linked documentation pages
- Mobile-friendly responsive design

## License

This documentation is for internal use.
