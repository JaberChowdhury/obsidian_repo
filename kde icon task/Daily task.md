

[ prompt ] : 
``` txt
i use arch linux with wayland and  KDE Plasma 6.4.5 . in this setup i can change each app icon manually . there are an option that create a custom color based on the wallpaper . 

here is what i want there are a tool called goowall[https://github.com/Achno/gowall.git] . this tool can generate color palate from an wallpaper and it also can apply theme and color palate on a wallpaper and it can be done on ico and icons too. so i want to make a bash script that convert my base icons to the curent theme oriented version where the theme or color palate will be generated from the current wallpaper . 
```



Alright Jaber, let’s write down our **whole workflow** like a blueprint 📜 — so you know which files/scripts/configs we’ll have, and what each step does.

---

# ⚡ Step-by-Step Algorithm

### **Step 1: Collect base icon packs**

1. Download Papirus, WhiteSur, and Tela.
    
2. Place them inside `~/IconBases/` like:
    
    ```
    ~/IconBases/papirus/
    ~/IconBases/WhiteSur/
    ~/IconBases/Tela/
    ```
    

---

### **Step 2: Merge themes → MasterBase**

- Run `merge-icons.sh`
    
- Algorithm:
    
    - For each source theme (Papirus → WhiteSur → Tela):
        
        - Traverse all icons (`*.svg`, `*.png`).
            
        - Copy into `MasterBase/` if not already present.
            
    - Result: `MasterBase` = combined super-collection.
        

---

### **Step 3: Detect wallpaper**

- KDE Plasma stores wallpaper in `~/.config/plasma-org.kde.plasma.desktop-appletsrc`.
    
- Extract with:
    
    ```bash
    grep -m1 "Image=" ~/.config/plasma-org.kde.plasma.desktop-appletsrc | cut -d'=' -f2-
    ```
    

---

### **Step 4: Generate color palette**

- Use `gowall`:
    
    ```bash
    gowall palette "$wallpaper" -o ~/.cache/gowall_palette.json
    ```
    
- Produces JSON with colors (primary, secondary, accent, etc.).
    

---

### **Step 5: Recolor icons**

- Apply palette to icons:
    
    ```bash
    gowall icons "$wallpaper" -i ~/IconBases/MasterBase -o ~/.local/share/icons/WallpaperTheme
    ```
    
- Result: new KDE theme `WallpaperTheme` (icons recolored to wallpaper).
    

---

### **Step 6: Apply theme in KDE**

- Update KDE setting:
    
    ```bash
    kwriteconfig6 --file kdeglobals --group Icons --key Theme "WallpaperTheme"
    qdbus6 org.kde.KWin /KWin reconfigure
    ```
    
- Plasma reloads → icons now match wallpaper.
    

---

### **Step 7: Automate (Optional)**

- Run `wallpaper-icons.sh` manually OR
    
- Add a **systemd user service** or **inotify watcher** that triggers script whenever wallpaper changes.
    

---

## 🗂️ Files You’ll Have

1. **merge-icons.sh** → create `MasterBase` once.
    
2. **wallpaper-icons.sh** → generate & apply recolored icons each time wallpaper changes.
    
3. **MasterBase/** → your giant merged icon set (can share).
    
4. **WallpaperTheme/** → dynamically recolored icons (changes with wallpaper).
    


---

