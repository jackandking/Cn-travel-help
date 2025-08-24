# China Travel Help - Static Website

China Travel Help is a static website featuring interactive travel checklists for foreign travelers visiting China. The site includes checklists for major Chinese cities (Beijing, Shanghai, Xi'an, Guangzhou) with both adult and kids versions, plus a general China travel checklist.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Quick Start
- Validate all HTML files: `cd /home/runner/work/Cn-travel-help/Cn-travel-help && for file in *.html; do tidy -quiet -errors "$file" >/dev/null 2>&1 && echo "$file: OK" || echo "$file: ERRORS"; done` -- takes <1 second
- Start local development server: `cd /home/runner/work/Cn-travel-help/Cn-travel-help && python3 -m http.server 8080` -- starts immediately
- Test website functionality: Open `http://localhost:8080` in browser
- Deploy to GitHub Pages: Push to `main` branch -- automatic via GitHub Actions

### Dependencies & Setup
- **NO build tools required** - This is a pure static website
- **NO package.json** - No Node.js dependencies  
- **NO compilation step** - HTML/CSS/JavaScript files are served directly
- Install HTML validator: `sudo apt-get update && sudo apt-get install -y tidy` -- takes 30-60 seconds
- **Python 3** is pre-installed and used for local development server

## Validation & Testing

### HTML Validation
Always validate HTML syntax before committing changes:
```bash
cd /home/runner/work/Cn-travel-help/Cn-travel-help
tidy -quiet -errors index.html
tidy -quiet -errors Beijing-travel-checklist.html
# Or validate all files at once (takes <1 second):
for file in *.html; do tidy -quiet -errors "$file" >/dev/null 2>&1 && echo "$file: OK" || echo "$file: ERRORS"; done
```

**Note**: Some HTML files have minor validation warnings due to structural inconsistencies (e.g., content outside proper head/body tags). These do not affect functionality but should be noted when making changes.

### Local Testing
Always test functionality with local server:
```bash
cd /home/runner/work/Cn-travel-help/Cn-travel-help
python3 -m http.server 8080 &
# Test in browser at http://localhost:8080
# Kill server when done: kill %1
```

### Interactive Functionality Testing
**CRITICAL**: Always manually test these user scenarios after making changes:
1. **Navigation**: Click between index.html and checklist pages - all links must work
2. **Expandable sections**: Click summary headers to expand/collapse details sections
3. **Checkbox persistence**: 
   - Check several checkboxes in different sections
   - Refresh the page or navigate away and back
   - Verify checkboxes remain checked (localStorage persistence)
4. **Mobile responsiveness**: Test at different screen sizes

### Browser Testing Commands
```bash
# Start server for browser testing
cd /home/runner/work/Cn-travel-help/Cn-travel-help && python3 -m http.server 8080 &
# Test main functionality in browser at http://localhost:8080
# Stop server: kill %1
```

**EXPECTED BROWSER ERRORS**: Google Analytics and AdSense resources will show `net::ERR_BLOCKED_BY_CLIENT` errors in local development - this is normal and expected. These work correctly in production.

## Repository Structure

### File Organization
```
/home/runner/work/Cn-travel-help/Cn-travel-help/
├── index.html                          # Main navigation page
├── China-travel-checklist.html         # General China travel checklist
├── Beijing-travel-checklist.html       # Beijing adult checklist
├── Beijing-kids-checklist.html         # Beijing kids checklist
├── Shanghai-travel-checklist.html      # Shanghai adult checklist
├── Shanghai-kids-checklist.html        # Shanghai kids checklist
├── Xi-an-travel-checklist.html         # Xi'an adult checklist
├── Xi-an-kids-checklist.html           # Xi'an kids checklist
├── Guangzhou-travel-checklist.html     # Guangzhou adult checklist
├── Guangzhou-kids-checklist.html       # Guangzhou kids checklist
├── Zhangjiajie-travel-checklist.html   # Zhangjiajie adult checklist
├── Zhangjiajie-kids-checklist.html     # Zhangjiajie kids checklist
├── Hangzhou-travel-checklist.html      # Hangzhou adult checklist
├── Hangzhou-kids-checklist.html        # Hangzhou kids checklist
├── Nanjing-travel-checklist.html       # Nanjing adult checklist
├── Nanjing-kids-checklist.html         # Nanjing kids checklist
├── Chengdu-travel-checklist.html       # Chengdu adult checklist
├── Chengdu-kids-checklist.html         # Chengdu kids checklist
├── Chongqing-travel-checklist.html     # Chongqing adult checklist
├── Chongqing-kids-checklist.html       # Chongqing kids checklist
├── Jiaxing-travel-checklist.html       # Jiaxing adult checklist
├── Jiaxing-kids-checklist.html         # Jiaxing kids checklist
├── Wuzhen-travel-checklist.html        # Wuzhen adult checklist
├── Wuzhen-kids-checklist.html          # Wuzhen kids checklist
├── Cambridge-kid-checklist.html        # Cambridge kids checklist
├── forbidden-city.html                 # Special Forbidden City guide
├── about.html                          # About page
├── contact.html                        # Contact page
├── faq.html                            # Frequently asked questions
├── privacy-policy.html                 # Privacy policy
├── terms-of-service.html               # Terms of service
├── feedback.html                       # User feedback form
├── CNAME                               # Custom domain: cn-travel-help.cn
├── README.md                           # Project documentation
├── .gitignore                          # Git ignore rules
└── .github/
    ├── workflows/static.yml            # GitHub Pages deployment
    └── ISSUE_TEMPLATE/feedback.yml     # Issue template
```

### Key Files Content Summary

#### index.html
- Main navigation hub with links to all checklists
- Includes Google Analytics (`G-QEBJRV187V`) and AdSense
- Mobile-responsive design
- Simple CSS styling embedded

#### Checklist HTML files (e.g., Beijing-travel-checklist.html)
- Interactive checklists using `<details>` and `<summary>` elements
- Checkboxes with `data-id` attributes for localStorage
- Embedded JavaScript for persistence functionality
- Consistent styling and navigation

## Development Workflows

### Adding a New Checklist
1. **Copy existing file**: `cp Beijing-travel-checklist.html NewCity-travel-checklist.html`
2. **Edit content**: Update title, checklist items, and data-id attributes  
3. **Update navigation**: Add link in `index.html` nav section
4. **Validate**: Run `tidy -quiet -errors NewCity-travel-checklist.html`
5. **Test**: Start local server and verify all functionality works
6. **Deploy**: Commit and push to `main` branch

### Modifying Existing Checklists
1. **Edit HTML file directly** - no build step required
2. **Validate HTML syntax**: `tidy -quiet -errors filename.html`
3. **Test locally**: Start server and verify changes work
4. **Test persistence**: Check/uncheck boxes, refresh page, verify localStorage works
5. **Commit changes** when validated

### Troubleshooting Common Issues

#### Checkbox State Not Persisting
- **Check data-id attributes**: Must be unique across the page
- **Verify JavaScript**: Look for `localStorage.getItem` and `localStorage.setItem` calls
- **Test in browser**: Open browser console and check for JavaScript errors

#### Links Not Working  
- **Check file paths**: All links are relative paths (e.g., `Beijing-travel-checklist.html`)
- **Verify file exists**: `ls -la filename.html`
- **Test navigation**: Click all links in local development server

#### Google Analytics/AdSense Errors
- **Expected in local development**: External resources are blocked in local testing
- **Error message**: `net::ERR_BLOCKED_BY_CLIENT` for Google Analytics and AdSense URLs 
- **Normal behavior**: These work fine when deployed to production
- **Do not fix**: These errors are expected and do not affect functionality

## Deployment & CI/CD

### GitHub Pages Deployment
- **Automatic**: Pushes to `main` branch trigger deployment
- **Workflow file**: `.github/workflows/static.yml`
- **NEVER CANCEL**: GitHub Actions deployment takes 2-5 minutes - let it complete
- **Live URLs**: 
  - `https://jackandking.github.io/Cn-travel-help/`
  - `https://cn-travel-help.cn/` (custom domain)

### Deployment Testing
After deployment, always test:
1. Visit both live URLs to ensure they load correctly
2. Test interactive functionality on the live site
3. Verify Google Analytics is working (not blocked)
4. Check mobile responsiveness on actual mobile devices if possible

## Technical Details

### JavaScript Implementation
Each checklist page includes this localStorage functionality:
```javascript
document.querySelectorAll('input[type="checkbox"]').forEach(cb => {
  const id = cb.dataset.id;
  cb.checked = localStorage.getItem(id) === 'true';
  cb.addEventListener('change', () => {
    localStorage.setItem(id, cb.checked);
  });
});
```

### CSS Styling
- **Embedded CSS** in each HTML file head section
- **Mobile-first responsive design**
- **Consistent styling** across all pages
- **No external CSS dependencies**

### Firebase Integration (Optional)
Some checklist pages (Beijing, Shanghai) include Firebase-based star rating systems:
- **Firebase configuration**: Stored in individual HTML files
- **Anonymous authentication**: Users can rate pages without accounts
- **Fallback**: Works offline with localStorage if Firebase unavailable
- **Setup guide**: See `FIREBASE_SETUP.md` for configuration details

## Common Tasks Reference

### Quick Commands
```bash
# Navigate to repository
cd /home/runner/work/Cn-travel-help/Cn-travel-help

# List all HTML files
ls -la *.html

# Count total checklist files
ls -1 *.html | wc -l

# Validate all HTML files (takes <1 second)
for file in *.html; do tidy -quiet -errors "$file" && echo "$file: VALID"; done

# Start local development server
python3 -m http.server 8080

# Check Git status
git status

# View current branch
git branch
```

### File Patterns to Remember
- **Checklist files**: `[City]-travel-checklist.html` and `[City]-kids-checklist.html`
- **Navigation structure**: All pages link back to `index.html` 
- **Data attributes**: Each checkbox needs unique `data-id="section-item"`
- **Consistent headers**: Each checklist page has same navigation structure

## Validation Checklist
Before committing any changes, ensure:
- [ ] HTML validates with `tidy -quiet -errors filename.html`
- [ ] Local server starts successfully with `python3 -m http.server 8080`
- [ ] All page links work correctly in browser
- [ ] Checkbox functionality works (check, refresh page, still checked)
- [ ] Page displays correctly on mobile and desktop
- [ ] No JavaScript console errors in browser
- [ ] All new files added to navigation in `index.html`

## Performance Notes
- **HTML validation**: <1 second (for all files)
- **Local server startup**: Immediate (starts immediately)
- **Page load time**: Nearly instant (static files)
- **GitHub Pages deployment**: 2-5 minutes (NEVER CANCEL)
- **Full manual testing**: 5-10 minutes for complete validation

**Remember**: This is a static website with no build process. Changes are immediate after saving HTML files. Always test locally before deploying to ensure the user experience is maintained.