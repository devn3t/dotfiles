dotfiles
========

My dotfiles for various Linux window managers.

This repository contains configuration files for an Openbox-based desktop setup using a lightweight set of desktop tools:

- Openbox
- Plank
- Stalonetray
- tint2

The purpose of these dotfiles is to provide a simple, fast, and clean desktop environment with a custom menu, panel, tray, dock, and startup behavior.

Repository layout
-----------------

- `openbox/` — Openbox window manager configuration
- `plank/` — Plank dock configuration and launcher items
- `stalonetray/` — Stalonetray system tray configuration
- `tint2/` — tint2 panel configuration and tintwizard defaults

Openbox
-------

The `openbox/` folder contains the primary configuration for the Openbox window manager, which handles the overall desktop layout, window behavior, keyboard shortcuts, and application launching.

### `openbox/autostart`

This script runs when Openbox starts and launches the rest of the desktop environment.

Key actions in this file:

- Disables screen blanking and DPMS:
  - `xset -dpms`
  - `xset s off`
- Starts compositing:
  - `compton -CGb`
- Restores the wallpaper:
  - `nitrogen --restore`
- Launches the desktop panel/dock stack:
  - `plank`
  - `stalonetray`
- Starts audio mixer support:
  - `pnmixer`
- Starts Conky for system information:
  - `conky -c /home/devnet/.conky/Fold/fold`
- Updates `obmenu-generator` paths for the current user home directory

This file is the “startup glue” for the desktop session.

### `openbox/menu.xml`

This file defines the Openbox root menu and uses `obmenu-generator` as the menu backend.

It is a simple XML file that points Openbox to:

- `obmenu-generator -i`

This lets the menu be generated dynamically from installed desktop applications, rather than being manually maintained by hand.

### `openbox/rc.xml`

This is the main Openbox configuration file. It controls the behavior of the window manager itself.

Key sections and settings include:

- Desktops:
  - number of desktops
  - desktop names
  - popup timeout
- Focus behavior:
  - focus new windows
  - follow mouse
  - focus last used window
- Placement:
  - Smart window placement
  - center new windows
  - monitor preferences
- Theme:
  - `ManjaroFlatDark` theme
  - fonts for active and inactive windows, menu items, and on-screen displays
- Dock settings:
  - position
  - auto-hide
  - hide delay
  - move button
- Keyboard shortcuts:
  - desktop switching
  - launching terminal, file manager, dmenu, logout, screenshots
  - media key controls for brightness and volume

This file is the main configuration for how Openbox behaves.

Openbox project: https://openbox.org/

Plank
-----

The `plank/` directory contains configuration for Plank, a lightweight dock.

### `plank/dock1/settings`

This file contains the Plank dock preferences.

Important settings include:

- `CurrentWorkspaceOnly=false`
  - Shows items from all workspaces, not just the current one
- `IconSize=48`
  - Dock icon size
- `HideMode=1`
  - Smart auto-hide
- `Position=3`
  - Dock is placed on the bottom edge
- `Alignment=3`
  - Centered alignment
- `Theme=Transparent`
  - Uses a transparent theme
- `DockItems=...`
  - The list of applications pinned to the dock
- `LockItems=false`
  - Items are not locked in place
- `PinnedOnly=false`
  - Allows regular dynamic docking behavior
- `AutoPinning=true`
  - Plank may auto-pin useful applications

### `plank/dock1/launchers/`

This directory contains the individual Plank launcher item definitions for apps pinned to the dock.

Current launcher items:

- `chromium.dockitem`
  - Launches Chromium
- `deadbeef.dockitem`
  - Launches DeaDBeeF
- `geany.dockitem`
  - Launches Geany
- `lxterminal.dockitem`
  - Launches LXTerminal
- `pidgin.dockitem`
  - Launches Pidgin
- `vlc.dockitem`
  - Launches VLC

Each `.dockitem` file points Plank at the matching system desktop entry for that application.

Plank project: https://launchpad.net/plank

Stalonetray
-----------

The `stalonetray/` folder contains configuration for Stalonetray, the system tray used for small status icons and notification applets.

### `stalonetray/stalonetrayrc`

This file configures the tray’s behavior and appearance.

Key settings include:

- `background "#777777"`
  - Tray background color
- `decorations none`
  - No window decorations
- `dockapp_mode none`
  - Normal tray mode
- `geometry 1x1+0+0`
  - Tiny tray geometry
- `icon_size 24`
  - Size of tray icon slots
- `skip_taskbar true`
  - Hides the tray from the taskbar
- `sticky true`
  - Keeps the tray visible across desktops
- `tint_color white`
  - White tint color
- `transparent false`
  - No transparency enabled
- `window_type dock`
  - Treats the tray like a dock-type window
- `window_strut auto`
  - Lets the tray reserve space properly

This gives the desktop a minimal tray that works well with Openbox.

Stalonetray project: https://stalonetray.sourceforge.net/

Tint2
-----

The `tint2/` folder contains the panel/taskbar configuration for tint2, an alternative lightweight panel.

### `tint2/tint2rc`

This is the main tint2 panel configuration.

Important settings include:

- `panel_position = bottom center`
  - Panel sits across the bottom center of the screen
- `panel_size = 100% 34`
  - Full-width panel with a height of 34 pixels
- `taskbar_mode = single_desktop`
  - One taskbar for the current desktop
- `task_icon = 1`
  - Shows task icons
- `task_text = 1`
  - Shows task text
- `task_width = 150`
  - Width for each task entry
- `task_font = sans 8`
  - Task font style
- `task_font_color = #ffffff 70`
  - Task text color at 70% opacity
- `task_active_font_color = #ffffff 100`
  - Active task text color at full opacity
- `clock_font_color = #ffffff 100`
  - Clock text color
- `clock_rclick_command = gsimplecal`
  - Right-clicking the clock opens gsimplecal
- `mouse_scroll_up = toggle`
- `mouse_scroll_down = iconify`
  - Custom mouse behavior on task entries

This file gives tint2 a clean black-and-white panel with a simple clock and minimal taskbar behavior.

### `tint2/tintwizard.conf`

This file is a small configuration template used by tintwizard.

It contains the default color, background, font, and foreground placeholders:

- `borderColor = None`
- `bgColor = None`
- `font = None`
- `fgColor = None`
- `bgCount = None`

This is not the main runtime panel config for this setup, but it is useful as a starting point for tint2 styling.

Tint2 project: https://gitlab.com/o9000/tint2

How these files fit together
----------------------------

This desktop setup uses:

- Openbox as the window manager
- Plank as the dock
- Stalonetray as the system tray
- tint2 as the panel/taskbar

The startup file brings everything together and launches the selected components automatically.

Notes
-----

This repository is designed to be copied into the appropriate user configuration locations on a Linux system.

Typical placement:

- `openbox/` files → `~/.config/openbox/`
- `plank/dock1/` → `~/.config/plank/dock1/`
- `stalonetray/stalonetrayrc` → `~/.stalonetrayrc`
- `tint2/tint2rc` → `~/.config/tint2/tint2rc`

This is a curated set of dotfiles for a lightweight Openbox desktop environment with multiple desktop components working together.
