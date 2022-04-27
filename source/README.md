# Create package .deb

## Download source code, ex (download joe editor)

[Last version](https://sourceforge.net/projects/joe-editor/files/JOE%20sources/joe-4.6/joe-4.6.tar.gz/download)

## Create directory

`mkdir /tmp/joe-4.6`

## Extract package

`tar -xvf joe-4.6.tar.gz && cd joe-4.6`

## Configure and Compile Package in diretory where are file downloaded

`./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var`
`make`
`sudo make install DESTDIR=/tmp/joe-4.6`

### Copy icon

`mv joe.ico /tmp/joe-4.6/usr/share/pixmaps/`

### Create control (with one line empty)

    cat > /tmp/joe-4.6/DEBIAN/control <<eol
      Package: joe-4.6
      Version: 4.6
      Architecture: all
      Maintainer: Marcos Freitas <viniciusfreitasrj17@gmail.com>
      Installed-size: 1900
      Dependens: xterm
      Section:
      Priority: optional
      Description: Text editor CLI

    eol

### Create postint (execute after installation)

    cat > /tmp/joe-4.6/DEBIAN/postint <<eol
      #!/bin/bash

      chmod +x /usr/bin/joe
    eol

### Create joe.desktop

    cat > /tmp/joe-4.6/usr/share/applications/joe.desktop <<eol
      [Desktop Entry]
      Version=1.0
      Name=Joe's Own Editor
      GenericName=Text Editor
      Comment=View and edit files
      Exec=/usr/bin/joe %F
      TryExec=joe
      Icon=/usr/share/pixmaps/joe.ico
      Type=Application
      Terminal=true
      Categories=Utility;TextEditor;

    eol

### Create package

`dkpg -b /tmp/joe-4.6`

### Install package

`dpkg -i /tmp/joe-4.6.deb`
***or***
`apt install /tmp/joe-4.6.deb`
