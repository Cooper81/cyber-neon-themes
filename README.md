# Cyber ​​& Neon Themes for Home Assistant

Two dark themes for Home Assistant dashboards:

| Theme | Look |
|---|---|
| **Cyber** | Cyberpunk HUD: beveled corners, scanlines, moving scan bar, Orbitron font, neon grid background; sections optionally available in specific colors (cyan / pink / yellow / violet) |
| **Neon** | Glass-style cards with blur, cyan border with magenta glow, hover effect, dark gradient background (cyan / magenta / violet) |

Both themes automatically style all cards—no `card_mod` is required within the dashboard itself. ### Cyber

![Cyber](https://raw.githubusercontent.com/Cooper81/cyber-neon-themes/main/images/cyber.png)

### Neon

![Neon](https://raw.githubusercontent.com/Cooper81/cyber-neon-themes/main/images/neon.png)

*Preview images: Snippets from a real dashboard.*

## Prerequisites

1. **[card-mod](https://github.com/thomasloven/lovelace-card-mod)** (install via HACS → Frontend)
2. For **Cyber**: the *Orbitron* font as a dashboard resource
*Settings → Dashboards → ⋮ → Resources → Add resource*
- URL: `https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&family=Share+Tech+Mono&display=swap`
- Type: **Stylesheet**
3. Themes from the `themes` folder must be loaded in `configuration.yaml`:

```yaml
frontend:
themes: !include_dir_merge_named themes
```

## Installation via HACS

1. **HACS → ⋮ (top right) → Custom repositories**
2. Repository: `https://github.com/Cooper81/cyber-neon-themes` – Type: **Theme** → Add
3. Search for **Cyber ​​& Neon Themes** in HACS → **Download**
4. Run **Developer Tools → Actions → `frontend.reload_themes`** (or restart Home Assistant)
5. **Profile → Theme** → Select `Cyber` or `Neon`

## Manual Installation

Copy the files from `themes/` into the `config/themes/` folder of your Home Assistant installation and run `frontend.reload_themes`. ## Customization

The accent colors are defined as RGB values ​​at the top of each file:

```yaml
cyber-accent-rgb: '0, 255, 234'    # Borders, scan bars
cyber-accent2-rgb: '255, 0, 170'   # Heading shadows
cyber-accent3-rgb: '252, 238, 10'  # Page titles
```

### Cyber: Colored sections

By default, all cards are cyan. To assign a different neon color to a specific section, add the following to the cards in that section:

```yaml
card_mod:
style: "ha-card { --cyber-sec-rgb: var(--cyber-color-2); }"
```

`1` = Cyan, `2` = Pink, `3` = Yellow, `4` = Violet – the heading, border, glow effect, and scan bar will adopt the selected color.

Individual cards can still be overridden using `card_mod` – the themes intentionally do not use `!important`.

## Notes

- A theme applies either per device/browser (profile setting) or to individual views by specifying `theme: Cyber` within the view configuration.
- Views or cards with their own fixed `theme` or custom `card_mod` styling will not be altered by the theme.