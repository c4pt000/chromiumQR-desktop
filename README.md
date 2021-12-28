# chromiumQR-desktop


# gdrive download (google chrome source 35GB src folder)

```
mkdir /root/chromium/chromium
cd /root/chromium/chromium
place chromium.src.tar here . https://drive.google.com/file/d/1hep4Vh1D6x2IKXVbY9liMLi0io4CzXPg/view?usp=sharing

# 1GB download (place chromium.src.tar in /root/chromium/chromium which is 35GB and untar)
docker run -it --net host -d -v /root/chromium/chromium:/root/chromium/chromium -v /opt/chromiumQR-desktop:/opt/CHROMEQR c4pt/chrome-qr-source-builder
cd /root/chromium/chromium
tar -xvf chromium.src.tar
cd src/
cp -rf /opt/chrome-QR/qrcode_generator_* chrome/browser/ui/views/qrcode_generator/

Ubuntu / Debian 
apt-get update
apt install python3 build-essential libprotobuf-dev git lsb-release sudo nano -y

# Fedora 35 from the README.md build instructions

Instead of running build/install-build-deps.sh , run:
su -c 'yum install git python bzip2 tar pkgconfig atk-devel alsa-lib-devel \
bison binutils brlapi-devel bluez-libs-devel bzip2-devel cairo-devel \
cups-devel dbus-devel dbus-glib-devel expat-devel fontconfig-devel \
freetype-devel gcc-c++ glib2-devel glibc.i686 gperf glib2-devel \
gtk3-devel java-1.*.0-openjdk-devel libatomic libcap-devel libffi-devel \
libgcc.i686 libgnome-keyring-devel libjpeg-devel libstdc++.i686 libX11-devel \
libXScrnSaver-devel libXtst-devel libxkbcommon-x11-devel ncurses-compat-libs \
nspr-devel nss-devel pam-devel pango-devel pciutils-devel \
pulseaudio-libs-devel zlib.i686 httpd mod_ssl php php-cli python-psutil wdiff \
xorg-x11-server-Xvfb'

export EDITOR=nano

# build for android apk

gclient sync

bash build/install-build-deps-android.sh

gclient runhooks

gn args out/Default

target_os = "android"
target_cpu = "x64"
use_lld = false
is_component_build = true


autoninja -C out/Default trichrome_library_apk

```

git clone https://chromium.googlesource.com/chromium/src

```
changes:
https://github.com/c4pt000/chromiumQR-desktop/blob/main/qrcode_generator_bubble.cc
https://github.com/c4pt000/chromiumQR-desktop/blob/main/qrcode_generator_icon_view.cc

-> chrome/browser/ui/views/qrcode_generator/qrcode_generator_bubble.cc
-> chrome/browser/ui/views/qrcode_generator/qrcode_generator_icon_view.cc

```

* rebase of current chromium src to make the qr code button as part of the menu bar

<br>
https://github.com/c4pt000/chromiumQR-desktop/releases
<br>
ot-export as raw html for embedding into html?-> secondary button or right click for download button
<br>
to do: open on mouse hover
<br>
add right click copy link as QR code export
<br>


* chromiumQR-desktop<p align="center"><img src="https://raw.githubusercontent.com/c4pt000/chromiumQR-desktop/main/chromiumQR-desktop-browser.png" width="800"></p>

removal of the dinosaur QR center

* chromiumQR-desktop-upper-right<p align="center"><img src="https://raw.githubusercontent.com/c4pt000/chromiumQR-desktop/main/chromiumQR-desktop-default.png" width="800"></p>

https://github.com/c4pt000/mojo-vison-OT

just a would be design of a QR code in motion (from a concept design that I made using an ATM screen) can be replaced in chromium for chromium to support QR codes in motion
see semi working mod at http://radiopool.me/QR that I implemented of actually putting the QR code pin dots physically in motion (not the background picture in motion support but the actual QR code pin dots)

<p align="center"><img src="https://github.com/c4pt000/a-PROTECTED_QR_CODE-QR-code-Encryption-layer-for-QR-codes-in-plainsight-and-machine-vision/releases/download/gif/PIN-protected-for-QR-import-to-phone.gif" width="800"></p>
