# Midjourney prompts — visual upgrades for thechadmin.com

Use these prompts in Midjourney if you want to push the visual further. Each is tuned for a specific asset slot in the site. Generated images go in `assets/`.

---

## 1. Premium parchment background (replacement for `assets/paper.png`)

Current paper.png is generated locally with ImageMagick — fine and uniform but plain. A Midjourney version would have more character. Save the result at 1600×1600 (square) and overwrite `assets/paper.png`.

```
Seamless aged parchment texture, warm ivory cream color with subtle sepia undertones,
extremely subtle paper grain barely visible, very faint warm vignette toward edges,
no visible borders or repeating pattern, archival manuscript quality, flat surface scan,
no objects no decorations no writing, soft natural diffused lighting,
museum-grade preservation, photorealistic, 8k texture --ar 1:1 --style raw --v 6.1
```

**Important after generation:**
- Crop to a clean square (1600×1600 or 2048×2048)
- If it still has visible darkening at edges, use the ImageMagick command in `_make_paper.ps1` to add a softer vignette
- Save as PNG (not JPEG) to preserve subtle gradients without compression artifacts

---

## 2. Ornate corner flourishes (for panel corners — adds option 2 vibe)

If you ever want to upgrade to the "with frame ornaments" option, generate four corner flourishes (top-left, top-right, bottom-left, bottom-right). They'd sit as small absolutely-positioned SVGs/PNGs on each panel.

```
Single ornate corner flourish, baroque filigree in dark navy and copper metallic accents
with small ruby red gemstone, intricate scrollwork curling inward from one corner,
isolated on pure transparent background, vector-style line art with metallic shading,
decorative element only no full frame, top-left corner orientation, illuminated manuscript
style, fine detail, symmetrical curves, no other elements in scene
--ar 1:1 --style raw --v 6.1 --no border, frame, background
```

Then in Midjourney:
- For top-right: add `--cref` of the top-left and prompt for "mirrored horizontally"
- For bottom corners: similarly mirror vertically
- Background-remove (e.g., remove.bg) or generate against pure black/white and key it out

**Drop into the site** by adding these CSS rules:
```css
.panel { position: relative; }
.panel::before,
.panel::after {
  content: "";
  position: absolute;
  width: 60px; height: 60px;
  background-size: contain;
  background-repeat: no-repeat;
  pointer-events: none;
  opacity: 0.7;
}
.panel::before { top: 4px; left: 4px;   background-image: url('assets/corner-tl.png'); }
.panel::after  { top: 4px; right: 4px;  background-image: url('assets/corner-tr.png'); transform: scaleX(-1); }
```

---

## 3. Custom AI badge upgrade (replace `assets/badge.png`)

Current badge is fine but generic. A custom one signed with your aesthetic could be striking.

```
Circular medieval scholar's seal, deep navy blue and copper metallic,
center features a stylized capital letter "C" intertwined with subtle circuit patterns,
encircled by raised text "CHAD DODSON · AI · AGENTIC · MCP · AITECH",
crisp embossed metal effect, illuminated manuscript meets modern technology,
isolated on transparent background, symmetrical, premium emblem design,
fine engraved detail, no shadow no background
--ar 1:1 --style raw --v 6.1
```

Save as PNG with transparency at 512×512 or 1024×1024.

---

## 4. Hero background accent (subtle illustrated map — option 2 territory)

If you want to commit harder to the fantasy-scholar aesthetic, replace the solid parchment behind the hero panel only with a subtle illustrated map. Use it as `background-image` on `.hero`, NOT the whole body.

```
Faded aged parchment map, warm sepia tones, very subtle mountain ranges and
coastline outlines drawn in fine brown ink, archaic cartography, low contrast and
extremely faded so it reads as background texture not a focal element,
no text no labels no compass rose, seamless usable as web background,
illustrated edges with soft fade to lighter center
--ar 16:9 --style raw --v 6.1
```

CSS to apply:
```css
.hero {
  background-image:
    linear-gradient(to bottom, rgba(242,232,208,0.85), rgba(242,232,208,0.85)),
    url('assets/hero-map.jpg');
  background-size: cover;
  background-position: center;
}
```

The double-gradient overlay keeps text readable — adjust the 0.85 alpha to taste.

---

## 5. Project section icons (replace generic Lucide icons)

The current project icons are generic Lucide SVGs (rocket, server, wand, GitHub). Could be replaced with custom illustrated icons matching the scholarly aesthetic.

```
Tiny illuminated manuscript icon of a [SUBJECT], copper and navy metallic finish,
medieval scholar's marginalia style, fine line art with subtle shading, square format,
isolated on transparent background, no shadow no extras, simple silhouette readable
at 40 pixels
--ar 1:1 --style raw --v 6.1 --no border, frame
```

Replace `[SUBJECT]` with:
- Kenshi MCP: "scroll wrapped around a glowing crystal"
- Foundry Bridge: "two scrolls connected by a chain"
- Foundry MCP Extensions: "wand crossed with quill"
- Windsurf framework: "spellbook with gears emerging"

---

## How to apply any of these once generated

1. Drop the file into `D:\WindSurf Projects\thechadmin-site\assets\`
2. If replacing `paper.png` or `badge.png`, just overwrite — the site references them by name
3. For new files (corner flourishes, custom icons), edit `index.html` and/or `styles.css` to reference them
4. Test locally: open `index.html` in a browser
5. Commit and push:
   ```powershell
   git add .
   git commit -m "Visual: <what changed>"
   git push
   ```
6. Cloudflare rebuilds within ~30 seconds

---

## My recommendation for first pass

Try prompt **#1** (premium parchment) first. It's the lowest-risk swap — purely cosmetic, doesn't change layout, and even a marginally better parchment makes the site feel more premium. The current locally-generated one is fine; a Midjourney version could be exquisite.

Save prompts **#2-#5** for if/when you decide to commit harder to the fantasy-scholar aesthetic.
