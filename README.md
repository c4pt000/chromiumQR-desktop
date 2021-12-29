# chromiumQR-desktop

# update, I've removed the little bastard out of the share QR code image to match the desktop version
# semi working proto-type treat as extemely unstable

https://drive.google.com/file/d/12YJjWcDCWiM2Bh_VDnwnJPv7oCHuWCo6/view?usp=sharing


![s1](https://raw.githubusercontent.com/c4pt000/chromiumQR-desktop/main/Screenshot_20211229-042443-122.png)

```
~/chromium/chromium/src/chrome/browser

share/qr_code_generation_request.cc:  request->render_dino = false;
ui/views/qrcode_generator/qrcode_generator_bubble.cc:  request->render_dino = false;
ui/views/webauthn/authenticator_qr_sheet_view.cc:    request->render_dino = false;
```

# reference google developer notes for building android versions
https://github.com/c4pt000/chromiumQR-desktop/raw/main/Checking%20out%20and%20building%20Chromium%20for%20Android.pdf

# gdrive download (google chrome source 35GB src folder) requires 60~GB+ free space


# WIP build instructions confusing enough even for me, fedora 35 yum packages actually build natively docker image just for reference to use ubuntu or debian
```
mkdir /root/chromium/chromium
cd /root/chromium/chromium
place chromium.src.tar here . https://drive.google.com/file/d/1hep4Vh1D6x2IKXVbY9liMLi0io4CzXPg/view?usp=sharing

# 1GB download (place chromium.src.tar in /root/chromium/chromium which is 35GB and untar)
# if you decide to make a docker image with a virtual mount to use ubuntu or debian here otherwise ignore this
docker run -it --net host -d -v /root/chromium/chromium:/root/chromium/chromium -v /opt/chromiumQR-desktop:/opt/CHROMEQR c4pt/chrome-qr-source-builder

cd /root/chromium/chromium
tar -xvf chromium.src.tar
cd src/

copying over files will break from desktop to android versions (i remember now from looking at the source its just a boolean to disable the dino logo render as false for dino_render = true)
ignore this will break android versions -> cp -rf /opt/chrome-QR/qrcode_generator_* chrome/browser/ui/views/qrcode_generator/

when using docker ubuntu or debian
Ubuntu / Debian 
apt-get update
apt install python3 build-essential libprotobuf-dev git lsb-release sudo nano -y


when using fedora 35 natively or fedora 35 docker
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

set export PATH to depot_tools folder where it is on the drive in this case as part of chromeQR yours might differ
provides chrome build tools like gclient and fetch and gn

git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git

export PATH=$PATH:/opt/chromeQR/depot_tools

gclient sync


ignore using this script to install deps when using fedora or fedora as a docker image
bash build/install-build-deps-android.sh

gclient runhooks

gn args out/Default


* still experimental for final output

target_os = "android"
target_cpu = "x86"
use_lld = false
is_component_build = true


autoninja -C out/Default chrome_public_apk

```

```
where the actual 1:1 source code for chromium "src" lives instead of using fetch --nohooks --no-history android
git clone https://chromium.googlesource.com/chromium/src
```

```

requires resizing tmpfs on the fly with the 60gb of free disk space including 35gb of bloated chrome raw source
can be added to /root/.bashrc with source /root/.bashrc

mount -oremount,size=20G /dev
 mount -oremount,size=20G tmpfs

the boolean which draws a dino png or svg logo in the QR
just change render_dino = false 

changes from desktop version not for android version but very similar:
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

# LONG TERM GOALS FOR "SHARE QR" CODE
![qr-code](https://raw.githubusercontent.com/c4pt000/chromiumQR-desktop/main/IBM-polymorphic-QR-code.gif)

just a would be design of a QR code in motion (from a concept design that I made using an ATM screen) can be replaced in chromium for chromium to support QR codes in motion
see semi working mod at http://radiopool.me/QR that I implemented of actually putting the QR code pin dots physically in motion (not the background picture in motion support but the actual QR code pin dots)

<p align="center"><img src="https://github.com/c4pt000/a-PROTECTED_QR_CODE-QR-code-Encryption-layer-for-QR-codes-in-plainsight-and-machine-vision/releases/download/gif/PIN-protected-for-QR-import-to-phone.gif" width="800"></p>
