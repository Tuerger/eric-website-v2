# Eric Greuter Art Portfolio Website

A responsive, bilingual art portfolio website showcasing analog photography and oil paintings with an interactive rating system.

## 🎨 Features

### Core Features
- **Bilingual Support**: English and Dutch language switching
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **Random Animations**: Three different animations on homepage (video/GIFs)
- **Gallery Drawers**: Sliding galleries for Pictures and Paintings
- **5-Star Rating System**: Visitors can rate artworks (data sent to Formspree)
- **Contact Form**: Contact drawer with About Me section
- **Progressive Web App**: Installable with service worker and manifest

### Gallery System
- Photos and paintings with dynamic border colors
- Tooltips showing artwork descriptions
- Support for landscape, portrait, and square images
- Adaptive aspect ratios for optimal display

### Language System
- Desktop: Flag buttons in header
- Mobile: Expandable dropdown menu
- All text sourced from `captions.json`
- No hardcoded text in HTML

### Mobile Navigation
- Hamburger menu for primary navigation on mobile
- Language selector and hamburger aligned in header
- Menu closes on outside click or after navigation

## 📁 File Structure

```
website-v2/
├── index.html                  # Main HTML file
├── captions.json              # All text content (en/nl)
├── manifest.webmanifest       # PWA manifest
├── service-worker.js          # Service worker for PWA
├── css/
│   └── style.css              # All styles
├── images/
│   ├── logo-1.png             # Site logo
│   ├── Logo.ico               # Favicon
│   ├── flag-en.png            # English flag
│   ├── flag-nl.png            # Dutch flag
│   ├── pictures/
│   │   ├── pictures.json      # List of picture files
│   │   └── Picture *.jpg      # Photo gallery images
│   └── paintings/
│       ├── paintings.json     # List of painting files
│       └── Painting *.jpg     # Painting gallery images
└── Animations/
    ├── anim1_24fps_light.mp4  # Ballet video animation
    ├── puddle_outflow_reflect.gif  # Puddle animation (landscape)
    └── vuurtoren-fade-020220.gif   # Lighthouse animation (portrait)
```

## 🚀 Deployment

### Netlify Deployment
1. Connect your GitHub repository to Netlify
2. Build command: (none needed)
3. Publish directory: `/`
4. Deploy!

The website is static and requires no build process. All features work client-side.

### Local Development
```bash
# Start a local server
python -m http.server 8000

# Or use any static file server
npx http-server
```

## ⚙️ Configuration

### Rating System (Formspree)
The rating system uses Formspree to collect ratings. Current configuration:
- **Form ID**: `xjggrvek`
- **Endpoint**: `https://formspree.io/f/xjggrvek`

To change the Formspree endpoint:
1. Create a new form at [formspree.io](https://formspree.io)
2. Replace the form ID in `index.html` (search for `xjggrvek`)

Ratings are submitted with:
- `image`: Image file path
- `title`: Artwork title
- `rating`: 1-5 stars
- `timestamp`: ISO timestamp

### Language Configuration
Edit `captions.json` to modify text content. Structure:
```json
{
  "en": { /* English translations */ },
  "nl": { /* Dutch translations */ }
}
```

### Adding Gallery Images

**Pictures:**
1. Add JPG files to `images/pictures/` (format: `Picture N.jpg`)
2. Update `images/pictures/pictures.json` with filename
3. Add captions to `captions.json` under `pictures["Picture N"]`

**Paintings:**
1. Add JPG files to `images/paintings/` (format: `Painting N.jpg`)
2. Update `images/paintings/paintings.json` with filename
3. Add captions to `captions.json` under `paintings["Painting N"]`

### Animation System
Three animations are randomly selected on page load:
- **anim1**: Ballet video (700x400px frame, landscape)
- **anim2**: Puddle GIF (550x450px frame, landscape)
- **anim3**: Lighthouse GIF (450x550px frame, portrait)

To add more animations:
1. Add file to `Animations/` folder
2. Update JavaScript in `index.html` (search for `const animations = [...]`)
3. Add CSS rules with `data-selected-animation` selector if custom sizing needed

## 🎨 Styling

### CSS Variables
```css
:root {
  --accent: #60a5fa;   /* Blue accent color */
  --bg: #020220;       /* Dark background */
  --text: #111;        /* Text color */
}
```

### Responsive Breakpoints
- **Desktop**: > 768px
- **Tablet**: 640px - 768px
- **Mobile**: < 640px

### Z-Index Layers
- Header/Language Switcher: `1001`
- Drawers (Gallery/Contact): `1000`
- Modal Viewer: `100`

## 🔧 Technical Details

### Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- ES6+ JavaScript features used
- CSS Grid and Flexbox layout

### Mobile Drawer Sizing
- Contact and gallery drawers use dynamic viewport units (svh/dvh)
- Extra safe-area padding for iOS/Android browser UI
- Improved scroll behavior for mobile browsers

### PWA Orientation
- Orientation set to `any` (supports both portrait and landscape)

### Performance Optimizations
- Service worker for offline support
- Lazy-loaded captions
- Dominant color extraction for dynamic borders
- Optimized image loading with object-fit

### Key JavaScript Functions
- `loadCaptions()`: Fetches and applies language-specific text
- `updatePageText()`: Populates all UI elements
- `setLanguage(lang)`: Handles language switching
- `toggleGalleryDrawer(drawerId)`: Opens/closes gallery drawers
- `createGalleryItem()`: Generates gallery figure elements with ratings
- `getDominantColor()`: Extracts dominant color from images

### Security
- Images have user-select disabled
- No inline event handlers
- CORS headers set for API requests
- Form validation on Formspree side

## 📝 Content Management

### Updating Text
All visible text is in `captions.json`. Edit this file to change:
- Navigation labels
- Page titles and descriptions
- Gallery artwork titles and descriptions
- Contact information
- Footer content
- Form placeholders

### Animation Titles
Each animation has its own title in `captions.json`:
- `home.titleAnim1`: Ballet animation title
- `home.titleAnim2`: Puddle animation title
- `home.titleAnim3`: Lighthouse animation title

## 🐛 Troubleshooting

### Header Flickers on Refresh
The header is hidden until captions load to prevent text flickering. This is controlled by:
- CSS: `visibility: hidden` on header
- JavaScript: Adds `captions-ready` class when loaded

### Ratings Not Submitting
1. Check Formspree form ID is correct
2. Verify form is not in test mode
3. Check browser console for errors
4. Ensure CORS is enabled in Formspree settings

### Gallery Images Not Displaying
1. Verify file names match exactly in JSON files
2. Check file paths are correct (case-sensitive)
3. Ensure images are in correct folders
4. Check browser console for 404 errors

### Mobile Language Selector Not Working
1. Verify z-index is set correctly (1001)
2. Check that click outside handler is working
3. Ensure `.open` class toggles properly

## 📧 Support

For questions or issues:
- Check browser console for error messages
- Verify all file paths are correct
- Ensure Formspree account is active
- Test in different browsers

## 📄 License

Personal portfolio website for Eric Greuter.

---

**Last Updated**: January 2026  
**Version**: 2.0
