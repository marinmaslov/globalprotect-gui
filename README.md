# Simple GlobalProtectGUI
 
GlobalProtectGUI is simple tray app to connect, disconnect and monitor 
globalprotect VPN connection.

## Installation

Required before starting script:
```
pip3 install pgi
sudo apt update
sudo apt install gir1.2-appindicator3
sudo apt install xterm
```

Clone this repo and run `python3 globalprotect-gui.py` and tray icon will appear.

To run this on start you can setup  ~/.config/autostart/*.desktop (the XDG Autostart specification), 
or through ~/.xprofile (a regular shell script),
e.g.
`sudo vi ~/.config/autostart/globalprotect-gui.desktop`
with content:
```
[Desktop Entry]
Name=GlobalProtectGUI
Type=Application
Exec=python3 [PATH_TO_REPO]/globalprotect-gui.py
```
# Preview

### Connected:
![Connected](docs/connected.png)

### Disconnected:
![Disconnected](docs/disconnected.png)

### Dropdown:
![Dropdown](docs/dropdown.png)

### Connecting:
![Connecting](docs/connecting.png)

## Troubleshooting

- DBus/session bus required: The tray indicator needs a running DBus user session. If you see warnings like "Unable to get the session bus" or mentions of `dbus-launch`, install a user-session DBus and AppIndicator libraries, then log out and back in:
	```bash
	sudo apt update
	sudo apt install dbus-user-session libayatana-appindicator3-1 gir1.2-appindicator3-0.1 python3-gi xterm
	# For legacy X11 setups that expect dbus-launch:
	sudo apt install dbus-x11
	```
	If the session bus is running but the environment variable is missing, you can export it manually before starting the app:
	```bash
	export DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/$(id -u)/bus"
	python3 globalprotect-gui.py
	```

- Deprecation warnings: The app now avoids Gtk/AppIndicator deprecations by using keyword labels for menu items and `set_icon_full` for the tray icon. If you still see warnings, ensure you’re running with GTK 3 and recent `gir1.2-` packages.