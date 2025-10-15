# App Icons

## Current Status

The PWA manifest references `icon-192.png` and `icon-512.png`, but these need to be generated.

## Generating Icons

You can use the provided `icon.svg` to generate PNG icons:

### Using ImageMagick:
```bash
# Install ImageMagick if needed: brew install imagemagick
convert -background none icon.svg -resize 192x192 icon-192.png
convert -background none icon.svg -resize 512x512 icon-512.png
```

### Using online tools:
- Upload `icon.svg` to https://cloudconvert.com/svg-to-png
- Convert to 192x192 and 512x512 sizes

### Using Figma/Sketch/Design tools:
- Open `icon.svg` in your design tool
- Export as PNG at 192x192 and 512x512

## Design

The icon features a purple gradient background (matching the app theme) with a white pound sterling symbol (£).

Feel free to customise the design in `icon.svg` before generating the PNG files.
