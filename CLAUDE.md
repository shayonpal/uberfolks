# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

UberFolks is a static website showcasing a digital agency that creates web and mobile applications. The site features a clean, professional design with adaptive theming and smooth interactions.

## Technology Stack

- **Frontend**: Vanilla HTML, CSS, and JavaScript (no framework dependencies)
- **Deployment**: Cloudflare Pages via Wrangler
- **Build Tool**: Wrangler (Cloudflare's CLI tool)
- **CI/CD**: GitHub Actions for automated deployment

## Key Architecture Decisions

### Static Site Architecture
- Single-page application with no external dependencies
- Theme system supports light, dark, and auto (system preference) modes
- Responsive design optimized for mobile and desktop

### Theme System
The site implements a sophisticated theming system:
- **CSS Custom Properties**: All colors and styles use CSS variables for easy theme switching
- **Three Theme Modes**: Light (GitHub-inspired), Dark (Nord-inspired), and Auto (follows system preference)
- **JavaScript Theme Controller**: Persists user preference in localStorage and handles system preference changes
- **SVG Logo Adaptation**: Logo automatically adjusts colors based on the active theme

### Design System
- **Color Palettes**: GitHub Light and Nord Dark color schemes
- **Typography**: System fonts for optimal performance across platforms
- **Grid Layouts**: CSS Grid for responsive feature cards and stats
- **Animations**: Smooth transitions and floating background elements
- **Backdrop Effects**: CSS backdrop-filter for modern glassmorphism effects

## Development Commands

### Local Development
```bash
# Serve locally using Wrangler
wrangler pages dev .

# Alternative: Use any static file server
python -m http.server 8000
# or
npx serve .
```

### Deployment
```bash
# Deploy to production
wrangler pages deploy . --project-name=uberfolks

# Deploy to preview environment
wrangler pages deploy . --project-name=uberfolks-preview
```

### Configuration Management
```bash
# View current Wrangler configuration
wrangler pages project list

# View deployment history
wrangler pages deployment list --project-name=uberfolks
```

## File Structure

- `index.html` - Main HTML file with embedded CSS and JavaScript
- `global.css` - Global CSS styles and theme definitions
- `wrangler.toml` - Cloudflare Pages configuration
- `images/` - Logo assets (PNG and SVG formats)
- `.github/workflows/deploy.yml` - GitHub Actions deployment configuration

## Configuration Files

### wrangler.toml
Defines Cloudflare Pages deployment settings:
- Production environment: `uberfolks`
- Preview environment: `uberfolks-preview`
- Build output directory: `.` (current directory)

### GitHub Actions
Automated deployment triggered on:
- Push to `main` branch
- Pull requests to `main` branch

Required secrets:
- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

## Development Guidelines

### Code Organization
- Keep the single-file architecture for simplicity
- Use CSS custom properties for all theme-related values
- Maintain semantic HTML structure for accessibility
- Follow mobile-first responsive design principles

### Theme Development
When modifying themes:
1. Update CSS custom properties in the `:root` declaration
2. Ensure all three theme modes (light, dark, auto) are properly defined
3. Test theme switching functionality across different system preferences
4. Verify logo visibility and contrast in all theme modes

### Performance Considerations
- All assets are inlined to minimize HTTP requests
- Images are optimized and served in multiple formats (PNG/SVG)
- CSS and JavaScript are minified in production builds
- System fonts are used to avoid external font loading

### Accessibility
- Semantic HTML structure throughout
- Proper contrast ratios maintained across all themes
- Keyboard navigation support for theme switcher
- Screen reader friendly content structure

## Deployment Process

The site automatically deploys via GitHub Actions when changes are pushed to the main branch. The deployment process:

1. Checks out the repository
2. Uses Wrangler to deploy static files to Cloudflare Pages
3. Updates both production and preview environments based on branch

## Common Tasks

### Adding New Content Sections
1. Create semantic HTML structure
2. Add corresponding CSS styles using existing design tokens
3. Ensure responsive behavior across all breakpoints
4. Test theme compatibility

### Modifying Theme Colors
1. Update CSS custom properties in `global.css`
2. Test across all three theme modes
3. Verify logo and content contrast
4. Check mobile responsiveness

### Performance Optimization
1. Inline critical CSS and JavaScript
2. Optimize images in the `images/` directory
3. Use system fonts when possible
4. Minimize external dependencies