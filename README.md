# Cyber ​​& Neon Themes for Home Assistant

Two dark themes for Home Assistant dashboards:

| Theme | Look |
|---|---|
| **Cyber** | Cyberpunk HUD: beveled corners, scanlines, moving scan bar, Orbitron font, neon grid background, sections automatically color-coded (Cyan / Pink / Yellow / Violet) |
| **Neon** | Glass-style cards with blur, cyan border with magenta glow, hover effect, dark gradient background (Cyan / Magenta / Violet) |

Both themes automatically style all cards—no `card_mod` is required within the dashboard itself.

### Cyber

![Cyber](https://raw.githubusercontent.com/Cooper81/cyber-neon-themes/main/images/cyber.png)

### Neon

![Neon](https://raw.githubusercontent.com/Cooper81/cyber-neon-themes/main/images/neon.png)

*Preview images: Cropped sections of a real dashboard.*

## Prerequisites

1. **[card-mod](https://github.com/thomasloven/lovelace-card-mod)** (install via HACS → Frontend)
and additionally load it as a frontend module in `configuration.yaml` (see step 3)—
without this, themes relying on card-mod will have limited functionality. 2. For **Cyber**: the *Orbitron* font as a dashboard resource
*Settings → Dashboards → ⋮ → Resources → Add Resource*
- URL: `https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&family=Share+Tech+Mono&display=swap`
- Type: **Stylesheet**
3. Load themes from the `themes` folder in `configuration.yaml` and register `card-mod` as a module,
then **restart** Home Assistant:

```yaml
frontend:
themes: !include_dir_merge_named themes
extra_module_url:
- /hacsfiles/lovelace-card-mod/card-mod.js
```

> Tip: Under *Settings → Dashboards → ⋮ → Resources*, you can find the `card-mod` URL including the `?hacstag=…` parameter.
> Enter this exact URL (including `?hacstag=…`) for `extra_module_url` to prevent `card-mod` from loading twice.

## Installation via HACS

1. **HACS → ⋮ (top right) → Custom repositories**
2. Repository: `https://github.com/Cooper81/cyber-neon-themes` – Type: **Theme** → Add
3. Search for **Cyber ​​& Neon Themes** in HACS → **Download**
4. Run **Developer Tools → Actions → `frontend.reload_themes`** (or restart Home Assistant)
5. **Profile → Theme** → Select `Cyber` or `Neon`

## Manual Installation

Copy the files from `themes/` into the `config/themes/` folder of your Home Assistant installation and run `frontend.reload_themes`. ## Customization

The accent colors are defined at the top of each file as RGB values:

```yaml
cyber-accent-rgb: '0, 255, 234'    # Borders, scan bars
cyber-accent2-rgb: '255, 0, 170'   # Heading shadows
cyber-accent3-rgb: '252, 238, 10'  # Page titles
```

### Cyber: Colorful Sections

The sections of a view—or the columns of a masonry view—automatically cycle through Cyan, Pink, Yellow, and Violet.
Headings, borders, glows, and scan bars adopt the respective color. The four colors can be modified at the top
of `Cyber.yaml` (`cyber-color-1` … `cyber-color-4`).

Individual cards can be assigned a specific color using `card_mod` (either RGB values ​​or one of the section colors):

```yaml
card_mod:
style: "ha-card { --cyber-sec-rgb: 40, 120, 255; }"   # or: var(--cyber-color-2)
```

> The automatic section colors utilize `:host-context()`—a feature supported by Chrome, Edge, and the Android app.
> In Safari (iPhone/iPad, iOS app) and Firefox, all cards appear cyan; however, the `card_mod` line shown above still works.

Individual cards can still be overridden using `card_mod`, as the designs intentionally avoid using `!important`.

## Notes

- A theme applies either per device/browser (via profile settings) or to specific views by setting `theme: Cyber` within the view configuration. - Views or cards with their own fixed `theme` or custom `card_mod` styling are not altered by the design.