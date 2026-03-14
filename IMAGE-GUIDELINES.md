# Visuelles Marketing für Mlivo Workflow

## LinkedIn Bildgrößen

### Profil
- **Profilbild**: 400 x 400 px (1:1)
- **Banner**: 1584 x 396 px (4:1)

### Posts
- **Einzelbild**: 1200 x 1200 px (1:1) oder 1200 x 627 px (1.91:1)
- **Karussell**: 1080 x 1080 px (1:1)
- **Video**: 1920 x 1080 px (16:9)

### Artikel
- **Header**: 1200 x 644 px (1.86:1)

## Website Bilder

### Hero-Banner
- **Desktop**: 1920 x 600 px
- **Mobile**: 768 x 400 px
- **Format**: JPG (Qualität 80%), WebP

### Icons
- **Größe**: 64 x 64 px
- **Format**: SVG (vektorbasiert)
- **Farbe**: #1e3a5f (Mlivo Blau)

## Bildkonvertierung

### Mit ImageMagick
```bash
# Größe ändern
convert input.jpg -resize 1200x1200 output.jpg

# WebP erstellen
convert input.jpg -quality 80 output.webp

# Mehrere Größen für responsive
convert input.jpg -resize 1920x600 hero-large.jpg
convert input.jpg -resize 768x400 hero-mobile.jpg
```

### Mit Python (Pillow)
```python
from PIL import Image

# Bild öffnen
img = Image.open('input.jpg')

# Größe ändern
img_resized = img.resize((1200, 1200), Image.Resampling.LANCZOS)

# Speichern
img_resized.save('output.jpg', quality=80, optimize=True)
```

## Branding Assets

### Logo-Varianten
```
logo/
├── logo.svg          # Master (vektorbasiert)
├── logo.png          # 500x500px
├── logo-small.png    # 64x64px (Favicon)
└── logo-white.png    # Für dunkle Hintergründe
```

### Farbpalette
- **Primär**: #1e3a5f (Dunkelblau)
- **Sekundär**: #48bb78 (Grün)
- **Akzent**: #667eea (Lila)
- **Text**: #333333
- **Hintergrund**: #f8f9fa

## Screenshot-Workflow

### Für Dokumentation
```bash
# Screenshot mit Annotation
convert screenshot.png -pointsize 30 -fill red \
  -gravity center -annotate +0+0 "WICHTIG" \
  annotated.png
```

### Für Social Media
```bash
# Geräte-Frame hinzufügen
convert screenshot.png -resize 800x600 \
  device-frame.png -gravity center -composite \
  social-ready.png
```

## Automatisierung

### Batch-Verarbeitung
```bash
#!/bin/bash
# batch-resize.sh

for img in *.jpg; do
  convert "$img" -resize 1200x1200 "optimized/$img"
done
```

### Website-Optimierung
```python
import os
from PIL import Image

def optimize_for_web(input_dir, output_dir):
    """Alle Bilder für Web optimieren"""
    
    for filename in os.listdir(input_dir):
        if filename.endswith(('.jpg', '.png')):
            img = Image.open(os.path.join(input_dir, filename))
            
            # WebP erstellen
            webp_filename = filename.rsplit('.', 1)[0] + '.webp'
            img.save(os.path.join(output_dir, webp_filename), 
                    'WEBP', quality=80)
            
            # JPG optimieren
            img.save(os.path.join(output_dir, filename), 
                    'JPEG', quality=80, optimize=True)

optimize_for_web('raw-images/', 'website/images/')
```

## Bild-SEO

### Dateinamen
```
❌ IMG_2024_001.jpg
✅ excel-automatisierung-ingenieure.jpg
```

### Alt-Text
```html
<img src="excel-makro.jpg" 
     alt="Excel-Makro für automatische Lastberechnungen">
```

### Lazy Loading
```html
<img src="image.jpg" 
     loading="lazy" 
     alt="Beschreibung">
```
