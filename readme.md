# Project XIX — Interactive Virtual Tour
**Phase 1 Prototype** · GitHub Pages · Zero Cost

---

## Deploy in 3 steps

```bash
# 1. Create a GitHub repo named: project-xix-tour
# 2. Push these files to main branch
git init
git add .
git commit -m "Project XIX virtual tour — Phase 1"
git remote add origin https://github.com/YOUR_ORG/project-xix-tour.git
git push -u origin main

# 3. In GitHub repo → Settings → Pages → Source: main / root
# Live in ~60 seconds at: https://YOUR_ORG.github.io/project-xix-tour/
```

---

## File structure

```
project-xix-tour/
  index.html          ← Everything. Deploy this.
  data/
    zones.json        ← Zone data (units, GFA, type)
  assets/             ← Create this folder
    plan-2d.jpg       ← Updated Masterplan render (from deck)
    plan-3d.jpg       ← 3D Massing render (from deck)
    panos/            ← Equirectangular panoramic images
      polo-field.jpg
      clubhouse.jpg
      villa-west.jpg
      villa-east.jpg
      loft-apts.jpg
      stables.jpg
      training.jpg
      paddock.jpg
```

---

## Step 1 — Add the plan images

Export from the ECAD presentation:
- Slide "UPDATED MASTER PLAN" → save as `assets/plan-2d.jpg` (min 2400px wide)
- Slide "3D MASSING" aerial view → save as `assets/plan-3d.jpg`

In `index.html`, find the two `<div class="plan-img ...">` elements and
replace them with `<img>` tags:

```html
<!-- Replace this -->
<div class="plan-img plan-2d-placeholder" id="plan-2d" ...>
<!-- With this -->
<img class="plan-img" id="plan-2d" src="assets/plan-2d.jpg" alt="Project XIX 2D Masterplan">
```

Same for plan-3d.

---

## Step 2 — Generate panoramic images (free)

### Option A: Skybox AI (best quality — recommended)
1. Go to https://skybox.blockadelabs.com
2. Select style: "Realistic"
3. Use these prompts for each zone:

**polo-field.jpg**
```
Equirectangular 360 panorama, standing at the centre of a lush international
standard polo field in Lagos Nigeria, surrounded by premium residential villas
and a white clubhouse pavilion in the distance, tropical palms, golden afternoon
light, ultra-realistic architectural photography
```

**clubhouse.jpg**
```
Equirectangular 360 panorama, standing on the spectator terrace of a modern
luxury polo clubhouse in Lagos, overlooking a vast green polo field, tiered
seating, warm evening light, white concrete and glass architecture,
Nigerian tropical landscape, ultra-realistic
```

**villa-west.jpg**
```
Equirectangular 360 panorama, standing on the private terrace of a luxury
3-bedroom villa overlooking a polo field in Lagos Nigeria, modern tropical
architecture, landscaped garden, palm trees, warm golden hour light,
ultra-realistic interior/exterior
```

**villa-east.jpg**
```
Equirectangular 360 panorama, standing on a luxury villa terrace overlooking
a polo estate lake in Lagos, lush landscaping, tropical palms, modern Nigerian
architecture, blue water reflection, sunset light
```

**loft-apts.jpg**
```
Equirectangular 360 panorama, rooftop terrace of a modern loft apartment
complex overlooking a polo estate in Lagos Nigeria, full estate view,
contemporary architecture, tropical palms, wide open sky, late afternoon
```

**stables.jpg**
```
Equirectangular 360 panorama, standing in the courtyard of luxury horse stables
in Lagos Nigeria, red brick and timber, polo ponies visible, lush tropical
greenery, cobblestone ground, warm morning light, ultra-realistic
```

**training.jpg**
```
Equirectangular 360 panorama, standing on a polo training field in Lagos
Nigeria, practice goals visible, green grass, tropical trees at perimeter,
academy building in background, early morning golden light
```

**paddock.jpg**
```
Equirectangular 360 panorama, standing in an open paddock at a luxury polo
estate in Lagos Nigeria, horses grazing, tropical palms, green grass,
white post-and-rail fencing, warm daylight
```

### Option B: Bing Image Creator (faster, free)
1. Go to https://www.bing.com/create
2. Use same prompts above — generate 4 variants per zone, pick the best
3. Note: Bing output is NOT equirectangular — use as flat images only
   (Pannellum will still load them as flat previews)

---

## Step 3 — Wire up panoramas in index.html

In the `ZONES` object, replace `null` with the image path:

```js
// Before:
panoImage: null,

// After:
panoImage: 'assets/panos/polo-field.jpg',
```

Repeat for each zone. Push to GitHub. Done.

---

## Calibrating zone hotspot positions

The SVG hotspot polygons are pre-positioned for the Updated Masterplan render.
If your exported image crops differently, adjust the `points` attributes on
each `<polygon class="zone-poly">` in index.html.

The SVG uses a `viewBox="0 0 1000 620"` coordinate space. To find correct
polygon coordinates:
1. Open your plan image in Figma or Photoshop
2. Resize canvas to 1000×620
3. Use the rectangle/polygon tool to trace each zone
4. Read the coordinates and paste into the `points` attribute

---

## Customisation quick-reference

| What | Where in index.html |
|------|---------------------|
| Brand colour (gold) | `--gold: #C9A84C` in `:root` |
| Brand colour (green) | `--green-deep: #1C3A2A` in `:root` |
| Loading screen tagline | `.loading-sub` text |
| Zone data (units, GFA) | `const ZONES = { ... }` object |
| CTA email address | `registerInterest()` function |
| CTA link (Formspree) | Replace `mailto:` with Formspree action URL |
| Pannellum auto-rotate speed | `autoRotate: -1.5` (negative = anticlockwise) |

---

## Phase 2 checklist (next steps)

- [ ] Drop in plan-2d.jpg and plan-3d.jpg
- [ ] Generate 8 panoramic images (Skybox AI)
- [ ] Wire panoImage paths in ZONES object
- [ ] Calibrate polygon hotspot coordinates to actual plan image
- [ ] Set up Formspree form (free, 50 submissions/month)
- [ ] Add custom domain in GitHub Pages settings
- [ ] Add Plausible or Umami analytics script

---

*Built for Mixta Africa · Project XIX · Lakowe, Ibeju-Lekki, Lagos · 2026*
