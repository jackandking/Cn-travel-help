# China Travel Help - Interactive Travel Checklists

China Travel Help is a lightweight static website providing interactive travel checklists for foreign travelers visiting China. Each checklist uses vanilla JavaScript with localStorage to persist user progress across browser sessions.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Local Development Setup
- **NO BUILD REQUIRED** - This is a pure static HTML/CSS/JavaScript site with no dependencies
- Serve locally for testing: `python3 -m http.server 8080`
- Navigate to: `http://localhost:8080`
- **NEVER CANCEL** the HTTP server - it starts instantly and runs continuously

### Core Validation Steps
After making any changes, ALWAYS run these validation scenarios:

1. **Start Local Server**:
   ```bash
   cd /home/runner/work/Cn-travel-help/Cn-travel-help
   python3 -m http.server 8080
   ```

2. **Test Homepage Navigation**:
   - Navigate to `http://localhost:8080`
   - Verify all checklist links work
   - Test feedback page link

3. **Test Checkbox Functionality** (CRITICAL):
   - Open any checklist page (e.g., Beijing-travel-checklist.html)
   - Check multiple checkboxes
   - Refresh the page - checkboxes MUST remain checked
   - Clear browser storage and verify checkboxes reset
   - This validates localStorage persistence functionality

4. **Mobile Responsiveness Test**:
   - Resize browser window to mobile width (< 768px)
   - Verify layout remains usable and readable

### File Structure
```
/
├── index.html                    # Main landing page with navigation
├── Beijing-travel-checklist.html # Beijing travel checklist
├── Shanghai-travel-checklist.html # Shanghai travel checklist  
├── China-travel-checklist.html   # General China travel checklist
├── Xi-an-travel-checklist.html   # Xi'an travel checklist
├── Cambridge-kid-checklist.html  # Kids' checklist
├── feedback.html                 # Feedback page with Google Form
├── .github/workflows/static.yml  # GitHub Pages deployment
└── .github/ISSUE_TEMPLATE/       # Issue templates
```

## Deployment

### GitHub Pages
- **Automatic deployment** via `.github/workflows/static.yml` 
- Triggers on push to `main` branch
- **NEVER CANCEL** deployment workflow - completes in under 2 minutes
- Live site: https://jackandking.github.io/Cn-travel-help/
- Custom domain: https://cn-travel-help.cn/

### Deployment Validation
After deployment, ALWAYS test:
1. Visit live site and verify all pages load
2. Test checkbox functionality on live site
3. Verify Google Analytics loads (check browser console for gtag events)

## Common Tasks

### Adding a New Checklist
1. **Copy existing checklist**:
   ```bash
   cp Beijing-travel-checklist.html New-city-checklist.html
   ```

2. **Edit the new file**:
   - Update `<title>` tag
   - Update `<h1>` heading
   - Replace checklist content in `<details>` sections
   - Ensure each checkbox has unique `data-id` or `id` attributes (different checklists use different approaches)

3. **Update navigation**:
   - Add link to new checklist in `index.html` navigation

4. **Validate new checklist**:
   - Test locally with HTTP server
   - Verify checkbox persistence works
   - Check mobile responsiveness

### Troubleshooting Checklist Issues
- **Checkboxes not persisting**: Check that either `data-id` or `id` attributes are unique and properly formatted
  - Note: Some checklists use `data-id` (Beijing, China, Xi'an), others use `id` (Shanghai)
- **JavaScript errors**: Open browser console and check for syntax errors in `<script>` tags
- **Layout broken**: Validate CSS in `<style>` sections, ensure proper HTML structure

## Validation Scenarios

### End-to-End User Journey Testing
ALWAYS run through this complete scenario after making changes:

1. **Homepage Flow**:
   - Start at `http://localhost:8080`
   - Click each checklist link
   - Verify all pages load correctly
   - Test feedback page Google Form loads

2. **Checklist Functionality**:
   - Open Beijing checklist
   - Check 3-5 different checkboxes across different sections
   - Note which items you checked
   - Refresh the browser page
   - Verify all previously checked items remain checked
   - Open a different checklist (Shanghai)
   - Verify independent localStorage (different checkboxes)

3. **Mobile Experience**:
   - Resize browser to mobile width (320px)
   - Test tapping checkboxes on mobile
   - Verify text remains readable
   - Test expanding/collapsing details sections

### Critical Tests That Must Pass
- ✅ All HTML files must load without 404 errors
- ✅ All checkboxes must persist state via localStorage
- ✅ Each checklist must have unique data-id or id values  
- ✅ Mobile layout must be usable on screens 320px+ wide
- ✅ Google Analytics must load (check Network tab)
- ✅ Checkbox state must persist after page refresh
- ✅ Different checklists must maintain independent localStorage

## Performance & Analytics

### Google Analytics
- Tracking ID: `G-QEBJRV187V`  
- Loads via gtag.js on all pages
- **Note**: May show blocked errors in development (normal)

### Google Forms Integration
- Feedback form: Embedded Google Form in `feedback.html`
- GitHub issue template: `.github/ISSUE_TEMPLATE/feedback.yml`

## Common Outputs

### Repository Root Listing
```
ls -la
.git/
.github/
.gitignore
Beijing-travel-checklist.html
CNAME
Cambridge-kid-checklist.html  
China-travel-checklist.html
README.md
Shanghai-travel-checklist.html
Xi-an-travel-checklist.html
feedback.html
index.html
```

### Typical Validation Console Output
```bash
# Start server
python3 -m http.server 8080
# Expected: Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...

# Test URL access  
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080
# Expected: 200

# Test checklist page
curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/Beijing-travel-checklist.html  
# Expected: 200
```

## GitHub Workflow

### Static Site Deployment
- File: `.github/workflows/static.yml`
- Trigger: Push to `main` branch or manual dispatch
- Action: Upload entire repository to GitHub Pages
- **NEVER CANCEL** - deployment completes in under 2 minutes
- Set timeout to 5+ minutes for safety

### Issue Templates  
- Feedback template in `.github/ISSUE_TEMPLATE/feedback.yml`
- Used by feedback page GitHub link
- Creates structured feedback issues