# Create package .deb

## Download binary, ex (download tor browser)

[Last version](https://www.torproject.org/dist/torbrowser/11.0.10/tor-browser-linux64-11.0.10_en-US.tar.xz)

## Extract package

`tar -xvf tor-browser-linux64-11.0.10_en-US.tar.xz`
`mv tor-browser tor-browser`
`mkdir -p /tmp/tor-browser/opt && mv tor-browser /tmp/tor-browser/opt`

### Copy icon

`mkdir -p /tmp/tor-browser/usr/share/pixmaps`
`mv torbrowser.png /tmp/tor-browser/usr/share/pixmaps/`

### Create control (with one line empty)

`mkdir /tmp/tor-browser/DEBIAN`

    cat > /tmp/tor-browser/DEBIAN/control <<eol
    Package: torbrowser
    Version: 11.0.10
    Architecture: amd64
    Maintainer: Marcos Freitas <viniciusfreitasrj17@gmail.com>
    Installed-size: 245000
    Dependens: firefox
    Section: Network
    Priority: optional
    Description: Tor Browser, Privacy and Security

    eol

### Create torbrowser.desktop

`mkdir /tmp/tor-browser/usr/share/applications`

    cat > /tmp/tor-browser/usr/share/applications/torbrowser.desktop <<eol
    [Desktop Entry]
    Version=1.0
    Name=Tor Browser Setup
    Comment=Tor Browser is +1 for privacy and −1 for mass surveillance
    Type=Application
    Exec=sh -c '/opt/tor-browser/Browser/start-tor-browser --detach || ([ ! -x /opt/tor-browser/Browser/start-tor-browser ] && /opt/tor-browser/start-tor-browser --detach)' dummy %k
    Icon=/usr/share/pixmaps/torbrowser.png
    Categories=Network;WebBrowser;Security;
    Path=
    Terminal=false

    eol

### Create package

`dkpg -b /tmp/tor-browser`

### Install package

`dpkg -i /tmp/tor-browser.deb`
***or***
`apt install /tmp/tor-browser.deb`
