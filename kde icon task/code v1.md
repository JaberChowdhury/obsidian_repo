``` bash 
#!/usr/bin/env bash
set -e

# === CONFIG ===
sources=(
    "$HOME/IconBases/papirus"
    "$HOME/IconBases/WhiteSur"
    "$HOME/IconBases/Tela"
)
icons_dir="$HOME/.local/share/icons"

# === 1. Get current wallpaper ===
wallpaper=$(grep -m1 "Image=" ~/.config/plasma-org.kde.plasma.desktop-appletsrc | cut -d'=' -f2-)
[ -z "$wallpaper" ] && { echo "❌ Could not detect wallpaper"; exit 1; }

# === 2. Generate palette ===
gowall palette "$wallpaper" -o ~/.cache/gowall_palette.json

# === 3. Build temporary merged base ===
tmp_base=$(mktemp -d)
for theme in "${sources[@]}"; do
  find "$theme" -type f \( -name "*.svg" -o -name "*.png" \) | while read -r f; do
    rel="${f#$theme/}"
    dest="$tmp_base/$rel"
    if [ ! -f "$dest" ]; then
      mkdir -p "$(dirname "$dest")"
      cp "$f" "$dest"
    fi
  done
done

# === 4. Recolor to new KDE theme ===
theme_name="WallpaperTheme-$(date +%Y%m%d%H%M%S)"
output_theme="$icons_dir/$theme_name"

gowall icons "$wallpaper" -i "$tmp_base" -o "$output_theme"

# Add index.theme (KDE requires it)
cat > "$output_theme/index.theme" <<EOF
[Icon Theme]
Name=$theme_name
Comment=Wallpaper-based dynamic icon theme
Inherits=Papirus
EOF

# === 5. Apply theme in KDE ===
kwriteconfig6 --file kdeglobals --group Icons --key Theme "$theme_name"
qdbus6 org.kde.KWin /KWin reconfigure

echo "✅ Installed and applied theme: $theme_name"

```