# Instalacja i konfiguracja systemu Debian wraz z Fluxbox

## 1. Instalacja

### Pobieranie obrazu iso:

Pobieramy obraz ze strony: [link](https://www.debian.org/distrib/)

### Wstępna instalacja:

#### Ustawienia językowe:

Ustawiamy w większości domyślne ustawienia zmieniamy jedynie strefę czasową i układ klawiatury.

#### Nazwa Hosta:

``` int033 ```

#### Domena:

``` s3 ```

#### Hasło root:

``` root_int01 ```

#### Nazwa i Hasło domyślnego użytkownika:

Nazwa: ``` userint01 ```

Hasło: ``` user_int01 ```

#### Ustawienia partycji

``` Guided - use entire disk => *wybierz dysk* => Separate /home partition => Finish partitioning and write changes to disk ```

#### Serwer lustrzany

``` ftp.pl.debian.org ```

#### Proxy http:

Klikamy dalej

## 2. Wstępna konfiguracja użytkownika:
 
### Dodajemy użytkownika do grupy sudo oraz instalujemy sudo

``` usermod -aG sudo userint01 ```

``` apt install sudo ```

###  Zezwalamy na użycie shutdown użytkownikowi userint01:

``` sudo visudo ```

Dodajemy ta linie przed ``` @includedir ```

```
userint01 int033=NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot
```

## 3. Instalujemy serwer Xorg

#### Instalacja

``` apt update ``` - aktualizujemy cache

``` apt install xserver-xorg xbase-clients xfonts-base xterm ``` - instalujemy podstawowe paczki potrzebne do środowiska graficznego

##### Możemy teraz wypróbować czy wszystko do tej pory działa

```
startx
```

Powinniśmy zobaczyć "okno" emulatora terminala rozpoznamy to po zmienionej czcionce i teraz mamy myszkę
 
Plik: ``` /etc/X11/xorg.conf ``` jest pusty.

Możemy wygenerować szkielet takiego pliku przez komendę:
``` Xorg :0 -configure ```
poczym utworzony zostanie plik ```xorg.conf.new```

Który może wyglądać tak (notka: Przykład z linuxa poza maszyną wirtualną):


<details>

```r 
Section "ServerLayout"
	Identifier     "X.org Configured"
	Screen      0  "Screen0" 0 0
	Screen      1  "Screen1" RightOf "Screen0"
	Screen      2  "Screen2" RightOf "Screen1"
	Screen      3  "Screen3" RightOf "Screen2"
	InputDevice    "Mouse0" "CorePointer"
	InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
	ModulePath   "/usr/lib/xorg/modules"
	FontPath     "/usr/share/fonts/misc"
	FontPath     "/usr/share/fonts/TTF"
	FontPath     "/usr/share/fonts/OTF"
	FontPath     "/usr/share/fonts/Type1"
	FontPath     "/usr/share/fonts/100dpi"
	FontPath     "/usr/share/fonts/75dpi"
EndSection

Section "Module"
	Load  "vnc"
	Load  "glx"
EndSection

Section "InputDevice"
	Identifier  "Keyboard0"
	Driver      "kbd"
EndSection

Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "auto"
	Option	    "Device" "/dev/input/mice"
	Option	    "ZAxisMapping" "4 5 6 7"
EndSection

Section "Monitor"
	Identifier   "Monitor0"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Monitor"
	Identifier   "Monitor1"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Monitor"
	Identifier   "Monitor2"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Monitor"
	Identifier   "Monitor3"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "AccelMethod"        	# <str>
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "TearFree"           	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "VariableRefresh"    	# [<bool>]
	Identifier  "Card0"
	Driver      "amdgpu"
	BusID       "PCI:6:0:0"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "AccelMethod"        	# <str>
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "TearFree"           	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "VariableRefresh"    	# [<bool>]
	Identifier  "Card1"
	Driver      "amdgpu"
	BusID       "PCI:7:0:0"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "AccelMethod"        	# <str>
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "TearFree"           	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "VariableRefresh"    	# [<bool>]
	Identifier  "Card2"
	Driver      "amdgpu"
	BusID       "PCI:8:0:0"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "AccelMethod"        	# <str>
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "TearFree"           	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "VariableRefresh"    	# [<bool>]
	Identifier  "Card3"
	Driver      "amdgpu"
	BusID       "PCI:8:0:1"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0"
	Monitor    "Monitor0"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

Section "Screen"
	Identifier "Screen1"
	Device     "Card1"
	Monitor    "Monitor1"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

Section "Screen"
	Identifier "Screen2"
	Device     "Card2"
	Monitor    "Monitor2"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

Section "Screen"
	Identifier "Screen3"
	Device     "Card3"
	Monitor    "Monitor3"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

```

</details>

## 4. Instalacja i konfiguracja Środowiska graficznego fluxbox:

### Instalacja

``` apt install fluxbox ```

Teraz jak uruchomimy ``` startx	``` powinniśmy zostać powitani przez nowy pulpit

### Instalacja dodatkowego oprogramowania

#### Xpdf oraz lynx:

``` apt install xpdf lynx ```

#### Iceweasel:

Iceweasel jest przestarzała i została podmieniona przez inną paczkę ``` firefox-esr ``` dlatego nie ma jej w repozytorium debiana 11.
Musimy ją pobrać z internetu lub z repo debiana 10
link:
``` 
http://ftp.pl.debian.org/debian/pool/main/f/firefox-esr/iceweasel_78.14.0esr-1~deb10u1_all.deb
```
Pobieramy plik .deb i instalujemy go za pomocą:

``` apt install ./iceweasel*.deb ```

albo

``` 
dpkg -i ./iceweasel*.deb
apt install -f
```

#### OpenOffice:

Idziemy na stronę pobierania openoffice i wybieramy wersję pakowaną w plik .deb:

``` https://www.openoffice.org/pl/download/index.html ```

Pobieramy plik *.tar.gz i rozpakowujemy go za pomocą komendy:

``` tar -xf Apache_OpenOffice*.tar.gz ```

następnie przechodzimy do folderu ``` <język np. pl>/DEBS/ ``` i instalujemy wszystkie paczki deb tam zawarte.

``` apt install ./*.deb && apt install ./desktop-integration/*.deb ```

## Konfiguracja FluxBoxa:

### Autostart

Dodajemy na końcu pliku ``` ~/.fluxbox/startup ``` linijkę:
``` exec xterm ```
Oraz podmieniamy ``` exec fluxbox ``` na ``` fluxbox ```

### Ikony na pulpicie

Instalujemy PCman-FM oraz nitrogen

``` apt install pcmanfm nitrogen ```

Dodajemy w pliku ``` ~/.fluxbox/startup ``` przed ``` exec xterm ``` linijkę:

``` pcmanfm --desktop && nitrogen --restore ```

### Dodajemy skróty do pulpitu

np.
``` cp /usr/share/applications/firefox-esr.desktop ~/Desktop ```
i powtarzamy to dla wszystkich pożądanych aplikacji:
- debian-xterm.desktop
- xpdf.desktop
- firefox-esr.desktop
- openoffice4-base.desktop

### Tapeta

Pobieramy wybraną tapetę z internetu i wykonujemy polecenie:

```
nitrogen <nazwa folderu z tapetami>
``` 

## 5. Pliki konfiguracyjne:

### ``` /etc/fstab ```

<details>

``` yml

# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/vda2 during installation
UUID=61de23a3-d0aa-4646-8f9c-642a68ebf412 /               ext4    errors=remount-ro 0       1
# /boot/efi was on /dev/vda1 during installation
UUID=349B-FDBA  /boot/efi       vfat    umask=0077      0       1
# /home was on /dev/vda4 during installation
UUID=808c7ea3-da60-4da1-b241-348d75ed0534 /home           ext4    defaults        0       2
# swap was on /dev/vda3 during installation
UUID=0b0ac72f-e983-4414-9417-90595bcfd372 none            swap    sw              0       0
/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0
```
</details>


### ``` /etc/passwd ```

<details>

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:101:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:104:110::/nonexistent:/usr/sbin/nologin
userint01:x:1000:1000:userint01,,,:/home/userint01:/bin/bash
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
usbmux:x:105:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin

```

</details>

### ``` /etc/shadow ```

<details>

```perl

root:$y$j9T$ycs1HBhnANt.Iixp961jT1$2xDtT0wkukRX17OobFoHU7tDuznwApzjWNw1O2qoggC:19063:0:99999:7:::
daemon:*:19063:0:99999:7:::
bin:*:19063:0:99999:7:::
sys:*:19063:0:99999:7:::
sync:*:19063:0:99999:7:::
games:*:19063:0:99999:7:::
man:*:19063:0:99999:7:::
lp:*:19063:0:99999:7:::
mail:*:19063:0:99999:7:::
news:*:19063:0:99999:7:::
uucp:*:19063:0:99999:7:::
proxy:*:19063:0:99999:7:::
www-data:*:19063:0:99999:7:::
backup:*:19063:0:99999:7:::
list:*:19063:0:99999:7:::
irc:*:19063:0:99999:7:::
gnats:*:19063:0:99999:7:::
nobody:*:19063:0:99999:7:::
_apt:*:19063:0:99999:7:::
systemd-timesync:*:19063:0:99999:7:::
systemd-network:*:19063:0:99999:7:::
systemd-resolve:*:19063:0:99999:7:::
messagebus:*:19063:0:99999:7:::
userint01:$y$j9T$4SSuNP1Ht3P.HArtYBI7W1$WtZWDNs18cLR7QAlHwldgKmgv/hRWpzdTmZsOmeJ2oD:19063:0:99999:7:::
systemd-coredump:!*:19063::::::
usbmux:*:19063:0:99999:7:::

```

</details>

### ``` /etc/group ```

<details>

```perl
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:userint01
floppy:x:25:userint01
tape:x:26:
sudo:x:27:userint01
audio:x:29:userint01
dip:x:30:userint01
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:userint01
sasl:x:45:
plugdev:x:46:userint01
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-timesync:x:101:
systemd-journal:x:102:
systemd-network:x:103:
systemd-resolve:x:104:
input:x:105:
kvm:x:106:
render:x:107:
crontab:x:108:
netdev:x:109:userint01
messagebus:x:110:
ssh:x:111:
userint01:x:1000:
systemd-coredump:x:999:
lpadmin:x:112:

```

</details>

### ``` /etc/network/interfaces ```

<details>

```sh
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug ens3
iface ens3 inet dhcp

```

</details>

### ``` /etc/resolv.conf ```

<details>

```
nameserver 10.1.0.1
```

</details>

### ``` /etc/sudoers ```

<details>

```sh
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root	ALL=(ALL:ALL) ALL

# Allow members of group sudo to execute any command
%sudo	ALL=(ALL:ALL) ALL
userint01 int033=NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot
# See sudoers(5) for more information on "@include" directives:

@includedir /etc/sudoers.d

```

</details>
