# Project Overview

This is a personal blog built with Jekyll, a static site generator. It uses the default "minima" theme. The blog is in its early stages, with most of the content being the default boilerplate from Jekyll.

## Building and Running

To work on this blog locally, you'll need to have Ruby and Jekyll installed.

1.  **Install dependencies:**
    ```bash
    bundle install
    ```

2.  **Run the local development server:**
    ```bash
    bundle exec jekyll serve --livereload
    ```
    This will start a local server, typically at `http://127.0.0.1:4000/`. The `--livereload` flag will automatically refresh the page when you make changes to the files.

## Development Conventions

*   **Content:** Blog posts are written in Markdown and stored in the `_posts` directory. The filename format for posts is `YYYY-MM-DD-title.markdown`.
*   **Customization:** The site's configuration can be modified in `_config.yml`. To customize the theme (e.g., layout, styles), you can override the theme's files. More information can be found in the [Jekyll documentation](https://jekyllrb.com/docs/themes/#overriding-theme-defaults).
*   **Pages:** New pages can be created by adding Markdown files to the root directory with the appropriate "front matter" (the block at the top of the file between the `---` lines).

---
*Managed by Gemini-CLI. Push access granted.*
