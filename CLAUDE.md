# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Michael Kumm's personal blog built with Hugo and the Blowfish theme. The site focuses on Elixir, software development, and life in Poland, and is deployed to Fly.io.

## Technology Stack

- **Static Site Generator**: Hugo (Go-based)
- **Theme**: Blowfish (Tailwind CSS-based theme)
- **CSS Framework**: Tailwind CSS 3.0
- **Deployment**: Fly.io (containerized with Docker)
- **Content**: Markdown files in the `content/` directory

## Common Development Commands

### Hugo Development Server
```bash
hugo server -D
```
Start the Hugo development server with drafts enabled. This will serve the site locally at `http://localhost:1313` with live reload.

### Building the Site
```bash
hugo --minify
```
Build the static site for production with minification. Output goes to `public/` directory.

### Theme Development (if working on Blowfish theme)
```bash
cd themes/blowfish
npm run dev
```
Start Tailwind CSS in watch mode for theme development.

### Building Theme CSS
```bash
cd themes/blowfish
npm run build
```
Build production CSS for the theme.

### Deployment
The site automatically deploys to Fly.io when changes are pushed to the main branch. Manual deployment:
```bash
fly deploy
```

## Project Structure

### Key Configuration Files
- `config/_default/hugo.toml` - Main Hugo configuration
- `config/_default/params.toml` - Blowfish theme parameters
- `config/_default/menus.en.toml` - Site navigation menus
- `config/_default/languages.en.toml` - Language settings
- `config/_default/markup.toml` - Markdown rendering configuration
- `fly.toml` - Fly.io deployment configuration
- `Dockerfile` - Container configuration for deployment

### Content Organization
- `content/posts/` - Blog posts (each in its own directory with index.md)
- `content/now/` - "Now" page sections (what the author is currently doing)
- `content/tags/` - Tag taxonomy pages
- `archetypes/` - Content templates for new posts

### Asset Structure
- `assets/css/custom.css` - Custom CSS overrides
- `assets/img/` - Site images and assets
- `static/` - Static files served directly (favicons, etc.)
- `public/` - Generated site output (not in git)

### Theme Integration
The site uses the Blowfish theme as a git submodule in `themes/blowfish/`. Theme customizations are done through:
- Configuration files in `config/_default/`
- Custom CSS in `assets/css/custom.css`
- Custom layouts in `layouts/` (if needed)

## Content Creation

### Creating New Blog Posts
```bash
hugo new posts/post-title/index.md
```
This creates a new post directory with the proper front matter template.

### Front Matter Structure
Posts use YAML front matter with fields like:
- `title` - Post title
- `date` - Publication date
- `draft` - Draft status (true/false)
- `tags` - Array of tags
- `description` - Meta description
- `featured` - Featured image (optional)

### Content Sections
- **Posts**: Technical blog posts about Elixir, development, etc.
- **Now**: Dynamic "what I'm doing now" content
- **Tags**: Automatic taxonomy pages for content categorization

## Deployment Architecture

The site is deployed as a static container on Fly.io:
1. Hugo builds the static site into `public/`
2. Docker container serves static files using `joseluisq/static-web-server`
3. Fly.io handles SSL, CDN, and global distribution
4. Domain redirects configured in `config.toml` for www → non-www

## Development Workflow

1. Create content using `hugo new` commands
2. Use `hugo server -D` for local development
3. Test theme changes in `themes/blowfish/` if needed
4. Commit changes to git
5. Deploy automatically triggers on push to main branch

## Important Notes

- The Blowfish theme has extensive documentation at https://blowfish.page/docs/
- Site uses "ocean" color scheme configured in `params.toml`
- Content is organized by taxonomy (tags, categories, series, authors)
- The site supports multiple content types and custom layouts through the Blowfish theme
- All theme customizations should be done through configuration files rather than modifying theme source