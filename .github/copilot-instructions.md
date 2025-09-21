# SIVQ Static Website

SIVQ.github.io is a simple French-language static HTML/CSS website for "Société d'immatriculation ERLC" (ERLC Registration Society) that provides a landing page with server registry access.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Prerequisites and Environment Setup
- Ensure you have Python 3 installed (available by default on most systems)
- No additional dependencies, build tools, or package managers are required
- The site deploys automatically to GitHub Pages via `.github/workflows/static.yml`

### Development and Testing Workflow
- **Start local development server:**
  ```bash
  cd /home/runner/work/SIVQ.github.io/SIVQ.github.io
  python3 -m http.server 8080
  ```
  - Server starts immediately (< 5 seconds)
  - Access site at `http://localhost:8080`
  - Use Ctrl+C to stop the server

- **Test site functionality:**
  ```bash
  curl -s http://localhost:8080 | head -10  # Verify HTML loads
  curl -s http://localhost:8080/style.css | head -10  # Verify CSS loads
  ```

### Build Process
- **No build step required** - this is a static HTML/CSS site
- Files are served directly as-is
- GitHub Pages deployment happens automatically on push to main branch via `.github/workflows/static.yml`

### Testing and Validation
- **NEVER CANCEL: Manual validation takes 2-3 minutes** - Set timeout to 10+ minutes
- **Always test the complete user experience after making changes:**
  1. Start local server: `python3 -m http.server 8080`
  2. Open browser to `http://localhost:8080` 
  3. Verify page loads with proper styling (white background with dot pattern, neumorphic button)
  4. Check that logo image loads from external URL
  5. Verify footer displays "SIVQ - 2025"
  6. Test button hover and active states work
  7. Stop server when done

- **Use Playwright for automated testing:**
  ```bash
  # Start server in background for testing
  python3 -m http.server 8081 &
  SERVER_PID=$!
  
  # Run playwright tests (if available)
  # Take screenshot for visual validation
  
  # Stop server
  kill $SERVER_PID
  ```

### File Structure and Important Locations
```
/home/runner/work/SIVQ.github.io/SIVQ.github.io/
├── index.html                    # Main landing page (French language)
├── style.css                    # All styling including neumorphic design
├── .github/
│   └── workflows/
│       └── static.yml           # GitHub Pages deployment
└── Elements/                    # Referenced but missing directory
    └── SIVQ.png                # Missing favicon file
```

### Known Issues and Limitations
- **Missing favicon:** `Elements/SIVQ.png` is referenced in HTML but file doesn't exist (causes 404)
- **Broken link:** Button links to `file:///C:/Users/fromh/OneDrive/Desktop/SIVQ/Site%20Web/Registre%20Serveurs/listservers.html` which won't work on web
- **External image dependency:** Logo loads from `i.imgur.com` which may be blocked by some clients

## Validation Scenarios

### Manual Testing Checklist
**ALWAYS run these validation steps after making ANY changes:**

1. **Visual Validation (2-3 minutes):**
   - Start server: `python3 -m http.server 8080`
   - Take screenshot using Playwright or browser
   - Verify layout renders correctly with:
     - Gray background (#f0f0f0)
     - White container with dotted pattern background
     - Logo image (external URL)
     - Title "Bienvenue à la société d'immatriculation ERLC"
     - Neumorphic button with proper shadow effects
     - Fixed footer "SIVQ - 2025"

2. **Interactive Validation:**
   - Hover over button to see white border effect
   - Click button to see active shadow animation
   - Verify responsive layout on different screen sizes

3. **Code Validation:**
   - Check HTML syntax is valid HTML5
   - Ensure CSS follows existing patterns
   - Verify no broken internal links (external links expected to work)

### Deployment Validation
- **GitHub Pages deployment is automatic** - no manual steps required
- Workflow `.github/workflows/static.yml` runs on every push to main
- Deployment typically takes 1-2 minutes
- Site will be available at `https://felixcaron512.github.io/SIVQ.github.io/`

## Common Development Tasks

### Adding New Content
- Edit `index.html` for content changes
- Edit `style.css` for styling changes
- Always test locally before committing

### Styling Guidelines
- Follow existing neumorphic design pattern (soft shadows and highlights)
- Use consistent color scheme: #f0f0f0 (background), #e8e8e8 (elements), #242020 (text)
- Maintain French language content
- Keep layout centered and responsive

### Before Committing Changes
- **Always run validation steps** (2-3 minutes - NEVER CANCEL)
- Start local server and test manually
- Take screenshot to verify visual changes
- Check browser console for any new errors
- Verify both desktop and mobile layouts

## Troubleshooting

### Common Issues
- **Server won't start:** Check if port 8080 is already in use, try different port
- **Styles not loading:** Verify `style.css` exists and HTTP server is serving it correctly
- **Images not loading:** External image URLs may be blocked, favicon is missing (expected)
- **Deployment fails:** Check `.github/workflows/static.yml` syntax and GitHub Pages settings

### Performance
- Site loads instantly (static files only)
- No JavaScript or external dependencies except logo image
- Minimal CSS keeps page size small
- GitHub Pages provides global CDN for fast loading

## File Contents Reference

### Root Directory Listing
```
ls -la /home/runner/work/SIVQ.github.io/SIVQ.github.io/
total 24
drwxr-xr-x 4 runner runner 4096 Sep 21 23:09 .
drwxr-xr-x 3 runner runner 4096 Sep 21 23:09 ..
drwxrwxr-x 7 runner runner 4096 Sep 21 23:09 .git
drwxrwxr-x 3 runner runner 4096 Sep 21 23:09 .github
-rw-rw-r-- 1 runner runner  928 Sep 21 23:09 index.html
-rw-rw-r-- 1 runner runner 1411 Sep 21 23:09 style.css
```

### HTML Structure Summary
- DOCTYPE html5 with French Canadian locale (fr-CA)
- Responsive meta viewport tag
- External favicon and CSS references
- Logo from imgur.com external URL
- Single call-to-action button (currently broken link)
- Fixed position footer

### CSS Architecture
- Mobile-first responsive design
- Neumorphic design pattern with soft shadows
- Flexbox layout for centering
- Dotted background pattern on main container
- Smooth transitions for interactive elements