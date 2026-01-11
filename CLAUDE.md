# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

UberFolks is a static website for a software development studio, built as a single-page application using vanilla HTML, CSS, and JavaScript. The site showcases the company's expertise in building web and mobile applications with a focus on user experience and problem-solving.

## Architecture

This is a **static web application** with the following structure:

- **Frontend**: Single HTML file (`index.html`) with embedded JavaScript
- **Styling**: CSS custom properties with dual-theme system (GitHub Light + Nord Dark)
- **Deployment**: Cloudflare Pages via GitHub Actions
- **No Build Process**: Pure HTML/CSS/JS - no bundler or package manager required

### Key Components

1. **Theme System** (`ThemeSwitcher` class in `index.html:124-178`):
   - Supports light/dark themes with automatic OS preference detection
   - Persists theme choice in localStorage
   - Uses CSS custom properties for seamless theme switching

2. **Styling Architecture** (`global.css`):
   - CSS custom properties for consistent theming
   - GitHub Light theme for light mode
   - Nord color palette for dark mode
   - Responsive design with mobile-first approach

3. **Visual Elements**:
   - Custom SVG logo with lightbulb and checkmark design
   - Floating animated elements for visual interest
   - Gradient backgrounds and smooth animations

## Development Commands

Since this is a static site with no build process, development is straightforward:

### Local Development
```bash
# Serve locally (any static server works)
python -m http.server 8000
# or
npx serve .
# or
php -S localhost:8000
```

### Deployment
```bash
# Deploy to Cloudflare Pages (automatic via GitHub Actions)
git push origin main

# Manual deployment via Wrangler CLI
npx wrangler pages deploy . --project-name=uberfolks
```

### Custom Domains
The site is accessible via two custom domains:
- **Primary**: https://uberfolks.ca (Canada)
- **Secondary**: https://uberfolks.in (India)

Both domains are configured in the Cloudflare Pages dashboard to point to the same deployment. Domain configuration is NOT in code - it's managed in Cloudflare's UI under:
`Pages → uberfolks → Custom domains`

### Theme Development
- Light theme colors defined in `:root` and `[data-theme="light"]`
- Dark theme colors defined in `[data-theme="dark"]`
- Test theme switching functionality with the toggle button

## Configuration Files

- **`wrangler.toml`**: Cloudflare Pages configuration with production and preview environments
- **`.github/workflows/deploy.yml`**: Automated deployment to Cloudflare Pages on push to main
- **`.gitignore`**: Standard ignores for Node.js projects (despite no package.json)

## Code Conventions

- **HTML**: Semantic markup with accessibility considerations
- **CSS**: Custom properties for theming, BEM-like naming for components
- **JavaScript**: ES6+ classes, modern APIs (localStorage, matchMedia)
- **SVG**: Inline SVG for the logo to allow CSS theming

## Key Features to Maintain

1. **Theme Switching**: Ensure new features respect the dual-theme system
2. **Performance**: Keep the site lightweight - no external dependencies
3. **Accessibility**: Maintain semantic HTML and proper contrast ratios
4. **Mobile Responsiveness**: Test on various screen sizes
5. **Browser Compatibility**: Modern browsers (ES6+ support assumed)

## Working with this Codebase

- All styles are in `global.css` - no CSS preprocessing
- JavaScript is embedded in `index.html` - consider extracting to separate files if it grows
- Images stored in `/images/` directory
- No package manager or dependencies - keep it simple
- Test theme switching in both light and dark OS preferences