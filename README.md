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
apt install python3 -y

# build for android apk
autoninja -C out/Default chrome_public_apk

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
