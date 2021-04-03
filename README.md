# linux-from-scratch
Eine (kurze) Dokumentation meiner Arbeit an meinem eigenen [Linux from Scratch](https://www.linuxfromscratch.org/) System (LFS).

Nach insgesamt fast 90 Stunden und zwei Anläufen bin ich mit dem LFS System (bzw. [BLFS](http://www.linuxfromscratch.org/blfs/) (= Beyond Linux From Scratch)) zufrieden, was ich schließlich vollenden konnte.

Das System befindet sich auf einer virtuellen Maschine mit einer Gesamtgröße von ca. 9,4 GB (da die Datei für die Festplatte jedoch 20 GB groß sein muss, ist es schwierig das System zu teilen). Es hat eine grafische Oberfläche, die auf [X11](https://www.x.org/wiki/) basiert und verwendet als Window Manager [bspwm](https://github.com/baskerville/bspwm), einen Tiling-Window-Manager, d.h. Fenster werden fliesenartig angeordnet und der Großteil der Navigation funktioniert über Keybinds durch [sxhkd](https://github.com/baskerville/sxhkd), statt durch Benutzung der Maus, wobei das auch möglich ist.

Das System ist insgesamt sehr minimalistisch nur mit den Basispaketen ausgestattet, die zwingend benötigt werden und jedes Programm, was auf dem System läuft, wurde vorher auch auf dem System selbst kompiliert, wodurch einige Programme und Bibliotheken besser an das spezifische System angepasst sind.
Dies hat natürlich auch den Effekt, dass die Kompilierung einzelner wichtiger Programme die manuelle Installation aller Abhängigkeiten und damit einhergehende Schwierigkeiten bspw. durch unpassende Versionen oder andere Fehler beim Kompilieren der Abhängigkeiten mit sich bringt. Z.B. war die Kompilierung von Firefox so aufwendig und fehlerreich, dass ich sie aus Zeitmangel abgebrochen habe.

Ich konnte trotz - oder vielleicht wegen - dieser vielen Schwierigkeiten viel aus dem Projekt lernen und verstehe jetzt zu großen Teil, was einzelne Untersysteme in einem Linux Betriebssystem machen und wodurch sich einzelne Distributionen unterscheiden. Ich habe auch eine Routine entwickelt, wie ich verschiedene Programme von den Quelldateien auf kompilieren und installieren kann und wie ich Fehler bei der Kompilierung lösen kann. Ich denke, dass ich tatsächlich in Zukunft weitere LFS Systeme aufbauen werde, wobei ich allerdings mehr Wert auf die Automatisierung der einzelnen Prozesse legen werde, weil es mir unerwarteter Weise Spaß macht solche grundlegenden Systeme und Scripts für deren Erstellung zusammenzubauen.

# Dokumentation

Im folgenden noch einmal die Dokumentation meines Arbeitsprozesses, die ich parallel während meiner Arbeit stichwortartig geführt habe:
>Informatik - LFS
>
>Ziel: ein Linux From Scratch (LFS) System auf einer VM zu installieren
>
>12.11.(ca. 90 min):
>    - Informationen sammeln, LFS E-Book anfangen (https://linuxfromscratch.org/lfs/downloads/stable/LFS-BOOK-10.0.html)
>    - Lesen von "Beginners' Guide to Installing from Source", "Building and Installing Software Packages for Linux" 
>12.11. - Zuhause(ca. 45 min):
>    - Aufsetzen einer Virtuellen Maschine mit VirtualBox, auf der zuerst ein Linux Host System für LFS läuft, in diesem Fall "Endeavour OS", später wird hier das >LFS System installiert
>13.11. - Zuhause (ca. 1 h):
>    - LFS bis Kapitel 4.6 durchgearbeitet
>14.11. - Zuhause (ca. 2.5 h):
>    - Cross-compiler Toolchain erstellt
>    - M4, Ncurses, Bash (cross-) kompiliert und auf dem LFS-System installiert
>17.11. - Zuhause (ca. 1.5 h):
>    - Coreutils, Diffutils, File, Findutils, Gawk, Grep, Gzip, Make, Patch, Sed, Tar, Xz, Binutils, GCC (cross-) kompiliert und auf dem LFS-System installiert
>18.11. - Zuhause (ca. 1 h):
>    - Chroot in das Dateisystem und Erstellen wichtiger Ordnerstrukturen und Systemdateien
>    - Installation der Basis Pakete
>19.11.(ca. 1 h):
>    - Lesen von versch. Package Management Methoden, speziell "fakeroot"
>    - Installation von... und tcl (bis 8.4.1)
>23.11. - Zuhause(ca. 1 h):
>    - Installation von expect, Fehlerbehebung von nicht vorhandenen virtuellen Geräten
>24.11.(45 min):
>    - weiter bis Glibc Kompilierung nr. 3
>3.12.(ca. 90 min):
>    - Kompilierung: Zlib, Bzip2, Xz, Zstd, File, Readline
>8.12.(ca. 45 min):
>    - Kompilierung: M4, Bc, Flex
>9.12. - Zuhause(ca. 1 h):
>    - Kompilierung: Binutils (Fehlerbehebung, weil Probleme mit VM), GMP (Beginn)
>10.12.(ca. 90 min):
>    - Kompilierung: GMP, MPFR, MPC, Attr, Acl, Libcap, Shadow, GCC, Pkg-config, Ncurses, Sed, Psmisc, Gettext, Bison, Grep, Bash, Libtool, GDBM, Gperf, Expat, >Inetutils, Perl (Beginn)
>17.12. - Zuhause (ca. 3 h):
>    - Kompilierung: Perl (Ende), XML-Parser (mit Fixes), Intltool, Autoconf, Automake, Kmod, Libelf, Libffi, OpenSSL, Python, Ninja, Meson, Coreutils
>18.12. - Zuhause (ca. 4 h):
>    - Kompilierung: Check, Diffutils, Gawk, Findutils, Groff, GRUB, Less, Gzip, IPRoute2, Kbd, Libpipeline, Make, Patch, Man-DB, Tar, Texinfo, Vim, Eudev, Procps-ng, Util-linux, E2fsprogs, Sysklogd, Sysvinit
>    - Erarbeitung bis 9.5
>---- bisher ca. 22 h 45 min ----
>25.12. - Zuhause:
>    - Initialisierung Udev rules, Geräteeinrichtung übersprungen, da keine besonderen Geräte vorhanden
>01.01. - Zuhause (ca. 1h):
>    - Netzwerkkonfigurationsdateien
>    - Konfiguration des Boot Vorgangs mit SysVinit, Konfiguration der Uhrzeit beim Booten nach 9.6.4 und http://www.linuxfromscratch.org/hints/downloads/files/time.txt
>02.01. - Zuhause (ca. 4 h - 4.5 h):
>    - Konfiguration der Konsole (Layout, Schriftart, etc.)
>    - Weitere Anpassungen der Bootparameter von SysVinit in /etc/sysconfig/rc.site
>    - Umgebungsvariable für Sprache in /etc/profile setzen, um die interaktive Shell (hier Bash) mit deutschem Charset verwenden zu können
>    - Readline Konfiguration für Editor in /etc/inputrc
>    - Shells (sh und bash) in /etc/shells eintragen (später soll auch noch zsh (="Zshell") installiert und hier eingefügt werden)
>    - Erstellung von /etc/fstab, um alle benötigten realen und virtuellen Geräte zu mounten
>    - Kernel
>        - Basis Konfigurierung an das Host System angepasst mit "make defconfig"
>        - Konfigurierung von Kernel Modulen u.ä. für später eventuell benötigte Packages aus http://www.linuxfromscratch.org/blfs/view/10.0/longindex.html#kernel-config-index (ALSA, Automounter, bluez, DHCP, dosfstools, gpm, Wireless Devices, libevdev, libinput, lm_sensors, NetworkManager, pm-utils, wpa-supplicant, xorg-amdgpu-driver, xorg-ati-driver, xorg-nouveau-driver, xorg-intel-driver)
>        - Kompilierung (43 min) und Installation der Kernel Module
>        - Installation des Kernels in /boot
>    - Im Host System grub-mkconfig ausführen, um über os-prober das neue Betriebssystem zum Bootloader hinzuzufügen
>--- Bootable Linux From Scratch System fertig nach ca. 28 h 20 min ---
>02.01. - Zuhause (ca. 3 h):
>    - Installation von wget und Requirements, um Dateien aus dem Internet herunterladen zu können (vom Host-System aus)
>    - Internet auf dem System herstellen (vom Host aus):
>        - Installation dhcpcd (http://www.linuxfromscratch.org/blfs/view/10.0/basicnet/dhcpcd.html)
>        - Installation dhclient (http://www.linuxfromscratch.org/blfs/view/10.0/basicnet/dhcp.html)
>        - Konfiguration der Pakete und Netzwerkadapter über ifconfig
>    - (sehr viele Probleme, aber am Ende nach mehrmaligem Überarbeiten eine funktionierende Internetverbindung)
>03.01. - Zuhause (ca. 6 h):
>    - Installation der VBoxGuestAdditions für die virtuelle Maschine, dafür benötigt, Installation von dbus und Dependencies. Unter anderem Xorg Libraries, die später verwendet werden, um ein grafisches Interface zu ermöglichen (6 Stunden, weil sehr viele Dependencies mit komplexer Installation, mehrere Fehler bei manchen Installationen, circular dependencies (=> Programme, die sich gegenseitig benötigen und dadurch auf spezielle Weise mehrfach kompiliert werden müssen) und Neukompilierung des Kernels) (http://www.linuxfromscratch.org/blfs/downloads/stable/BLFS-BOOK-10.0-nochunks.html#dbus)
>04.01. - 05.01. - Zuhause (ca. 8 h):
>    - Installation von Lynx (terminalbasierter Internet Browser), von Linux-PAM als authentication control und von Xorg-Server als Grafikserver für das Betriebssystem (erneut komplexe Zusammenhänge von Dependencies, viel Konfiguration) (http://www.linuxfromscratch.org/blfs/downloads/stable/BLFS-BOOK-10.0-nochunks.html#xorg-server)
>06.01. - Zuhause (ca. 3 h):
>    - Installation der Xorg Treiber, allerdings Fehler beim Starten von Xorg mit "startx", Fehler: "no devices detected"
>07.01. - 08.01. - Zuhause (ca. 5 h):
>    - Versuche den Fehler auf verschiedene Arten zu beheben:
>        - Neukompilierung des Kernels mit aktiviertem Modul für VirtualBox Grafiktreiber
>        - Installation verschiedener Treiber, die für virtuelle Grafikkarten benötigt werden
>        - Änderung des virtuellen Grafikchips in VMSVGA, VBoxVGA oder VBoxSVGA
>        - Neuinstallation der VirtualBox GuestAdditions
>    - Bisher jedoch kein Erfolg
>    - (wiederholte Versuche von kleinen Konfigurationsänderungen, aber keine Erfolge)
>
>26.01. Neuanfang diesmal LFS mit Systemd (Service-System, was von vielen Distributionen verwendet wird) 
>    - komplette Installation bis Bootable (Kapitel 11) in ca. 12 h bis 27.01. (http://linuxfromscratch.org/lfs/downloads/stable-systemd/LFS-BOOK-10.0-systemd.pdf)
>03.02. (2h):
>    - Setup von Internetverbindung mit dhcpcd und wget
>05.02. (ca. 2h 30 min):
>    - Installation und Konfigurierung von Linux PAM und Requirements
>09.02. (ca. 2h): 
>    - Rebuild von Systemd mit Linux PAM für volles Funktionspotential von Systemd (Zumindest ist das das Ziel...)
>    - Build von GLib-2.64.4 und Requirements (einige Fehler bei der Installation von docbook-xsl, docbook-xml)
>    - Neuinstallation von docbook-xml und Konfiguration
>16.02. :
>    - Neuinstallation von docbook-xsl
>23.02. (45 min):
>    - Scripts vorschreiben zur Kompilierung zuhause (u.a. Systemd, Ziel Xorg System)
>25.02. (90 min):
>    - Scripts bis Xorg-Libraries fertig
>01.03. (ca. 2h) - Zuhause:
>    - Kompilierung der Pakete durch die Scripts bis Xorg-Libraries
>04.03. (ca. 4h) - Zuhause:
>    - Kompilierung und Konfigurierung Xorg komplett (mit VMWare Grafiktreibern und VBoxSVGA simulierter Grafikkarte) (auch funktionstüchtig! => Neuinstallation war erfolgreich) 
>-- Grundlage Grafikoberfläche fertig nach ca. 26 h --
>
>11.03.:
>    - Installation von Pango failed, evtl fix durch Herunterladen von https://download.gnome.org/sources/pango/1.46/pango-1.46.0.tar.xz
>    - TODO:
>        - gdk-pixbuf (Fehler, reinstall docbook-xsl?)
>            (- libjpeg-turbo
>                - yasm)
>            - librsvg
>                - rustc
>                    - libssh2
>                - vala
>                    - graphviz
>           (- libtiff)
>        - imagemagick
>        - https://github.com/devnev/libxdg-basedir
>        - dbus
>            - circular dependency: elogind
>        - gtk+ 3 (aufwendig, optional) 
>        
>15.03. - 22.03. (insg. ca. 8h - 10h) :
>    - Installation von Pango erfolgreich, Ziel awesomeWM (Window manager für Grafikinterface) kompilieren, installieren (https://github.com/awesomeWM/awesome)
>    - Installation Dependencies von AwesomeWM (https://github.com/awesomeWM/awesome/blob/master/docs/10-building-and-testing.md) (sehr aufwendig)
>    - Kompilierung von AwesomeWM, mehrfach Fehler wegen unpassenden Lua Versionen (versucht mit 5.2, 5.3, 5.4; nur 5.4 funktioniert scheinbar mit LGI (testing) und awesome)
>    - Versuche verschiedene vorgefertigte AwesomeWM Konfigurationen zu verwenden (https://github.com/archias-lnx/awesome-possum, https://github.com/JavaCafe01/dotfiles)
>    - Immer wieder Fehler und nicht funktionierende Teilaspekte der Konfigurationen
>    
>27.03. - 02.04. (insg. ca. 10h) :
>    - Entscheidung doch nicht AwesomeWM zu verwenden, Alternative bspwm (https://github.com/baskerville/bspwm) (auch ein tiling window manager)
>    - Kompilierung deutlich simpler (https://github.com/baskerville/bspwm/blob/master/doc/INSTALL.md), allerdings zusätzlich Polybar (taskbar) und sxhkd (keybinds) benötigt
>    - Konfiguration mit Anpassung aus meinem Main-setup übernommen (siehe https://github.com/maxicraftone/linux-from-scratch/tree/main/config)
>    - Kompilierung von Firefox versucht, allerdings mehrere Fehler, Kompilierung + Installation von Atom als Code/Text Editor
>    - Erstellung der Liste an Sources (siehe https://github.com/maxicraftone/linux-from-scratch/blob/main/sources.list) und anschließend Löschung der Sourcedateien, um Platz zu sparen
>    - Erstellung von Beispiel Screenshots des fertigen Systems

# Screenshots
Hier nochmal einige Screenshots des fertigen Systems (mehr [hier](https://github.com/maxicraftone/linux-from-scratch/tree/main/Screenshots))

Fertiger Desktop
![desktop](https://raw.githubusercontent.com/maxicraftone/linux-from-scratch/main/Screenshots/desktop.png)

Die Konfiguration des Window Managers
![bspwm config file in Atom](https://raw.githubusercontent.com/maxicraftone/linux-from-scratch/main/Screenshots/bspwmrc.png)

Mein eigenes Wallpaper setter script, was Hintergrundbilder von Reddit herunterladen kann und Systemfarben anpasst
![wallpaper changer](https://raw.githubusercontent.com/maxicraftone/linux-from-scratch/main/Screenshots/wallpaper-change.png)
Noch einmal Atom mit geänderten Farben
![wallpaper changed](https://raw.githubusercontent.com/maxicraftone/linux-from-scratch/main/Screenshots/changed-system-colors.png)
