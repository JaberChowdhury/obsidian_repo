```json
{

"$schema": "https://github.com/fastfetch-cli/fastfetch/raw/master/doc/json_schema.json",

"logo": "arch2",

"display": {

"separator": ": ", // Separator between keys and values

"color": {

"keys": "blue", // Key color

"title": "red" // Title color

},

"key": {

"width": 12, // Aligns keys to this width

"type": "string" // string, icon, both, or none

},

"bar": {

"width": 10, // Width of percentage bars

"char": {

"elapsed": "■", // Character for elapsed portion

"total": "-" // Character for total portion

}

},

"percent": {

"type": 9, // 1=number, 2=bar, 3=both, 9=colored number

"color": {

"green": "green",

"yellow": "light_yellow",

"red": "light_red"

}

}

},

"modules": [

{

"type": "title",

"key": "󰌽 System",

"keyColor": "red"

},

// "separator",

  

// ─────────── OS / SYSTEM ───────────

{

"type": "os",

"key": "󰣇 OS",

"keyColor": "green"

},

{

"type": "disk",

"key": "󱦟 OS Age",

"folders": "/",

"format": "{days} days",

"keyColor": "cyan"

},

{

"type": "host",

"key": "󰌢 Host",

"keyColor": "magenta"

},

{

"type": "kernel",

"key": "󰒓 Kernel",

"keyColor": "red"

},

{

"type": "uptime",

"key": "󰔚 Uptime",

"keyColor": "blue"

},

{

"type": "packages",

"key": "󰏖 Packages",

"keyColor": "yellow"

},

// "separator",

  

// ─────────── SHELL / UI ───────────

{

"type": "shell",

"key": " Shell",

"keyColor": "green"

},

{

"type": "display",

"key": "󰍹 Display",

"keyColor": "cyan"

},

{

"type": "de",

"key": "󰠲 DE",

"keyColor": "blue"

},

{

"type": "wm",

"key": "󱂬 WM",

"keyColor": "red"

},

{

"type": "wmtheme",

"key": "󰉼 WM Theme",

"keyColor": "magenta"

},

{

"type": "theme",

"key": "󰉼 GTK Theme",

"keyColor": "magenta"

},

{

"type": "icons",

"key": "󰀻 Icons",

"keyColor": "yellow"

},

{

"type": "font",

"key": " Font",

"keyColor": "cyan"

},

{

"type": "cursor",

"key": "󰇀 Cursor",

"keyColor": "blue"

},

{

"type": "terminal",

"key": " Terminal",

"keyColor": "green"

},

{

"type": "terminalfont",

"key": " Terminal Font",

"keyColor": "cyan"

},

// "separator",

  

// ─────────── HARDWARE ───────────

{

"type": "cpu",

"key": " CPU",

"keyColor": "yellow"

},

{

"type": "gpu",

"key": "󰍛 GPU",

"keyColor": "red"

},

{

"type": "memory",

"key": "󰑭 Memory",

"keyColor": "green"

},

{

"type": "swap",

"key": "󰓡 Swap",

"keyColor": "blue"

},

{

"type": "disk",

"key": "󰋊 Disk",

"keyColor": "magenta"

},

// "separator",

  

// ─────────── NETWORK & POWER ───────────

{

"type": "localip",

"key": "󰩠 Local IP",

"keyColor": "cyan"

},

{

"type": "battery",

"key": "󰁹 Battery",

"keyColor": "yellow"

},

{

"type": "poweradapter",

"key": "󰂄 Adapter",

"keyColor": "green"

},

{

"type": "locale",

"key": "󰌌 Locale",

"keyColor": "blue"

},

// "separator",

  

// ─────────── FINISH ───────────

{

"type": "break"

},

{

"type": "custom",

// "key": "󰏘 keyColors",

"key": "󰏘 ",

"format": "{#red}{#} {#green}{#} {#yellow}{#} {#blue}{#} \n {#magenta}{#} {#cyan}{#} {#white}{#} {#bright_black}{#} "

}

]

}
```