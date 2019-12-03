<p align="center">
  <a href="https://www.espressif.com/en/products/hardware/esp32/resources">
    <img alt="Espressif" src="https://www.espressif.com/sites/all/themes/espressif/logo.svg" width="500" />
  </a>
  <a href="https://www.arduino.cc/en/main/software">
    <img alt="Arduino" src="https://www.arduino.cc/en/pub/skins/arduinoWide/img/ArduinoAPP-01.svg" width="100" />
  </a>
</p>
<h1 align="center">
  ESP32 CameraWebServer example sketch<br><i>made more tinker friendly</i>.
</h1>

This is the CameraWebServer example sketch that comes with the ESP32 framework for the IDE. However, this sketch is a bit, well, _sketchy_.

The main html pages are stored in a header file, which would be bad enough, except it is written out in array initializer notation, one agonizing byte at a time. Ridiculous? What if I told you it was gzipped, too? Now how much would you pay?

And, yes, the browser knows how to unzip stuff. That's not the point. My editor don't do gzip, yo.

So, I converted the header file mess into files, and then unzipped them (call me stubborn). They now reside in the `data` folder as `index_ov2640.html` and `index_ov3660.html` and will be uploaded to the board's SPIFFS filesystem. The proper one will be selected and served depending on the camera model. Mine was an OV2640.

## ⚙️ Gear you need

### 🛠 Hardware

You need an ESP32 development board with a camera. I used an [ESP32-cam](https://www.amazon.com/gp/product/B07Q56LGG6/ref=ppx_od_dt_b_asin_title_s01?ie=UTF8&psc=1). That one comes with the OV2640 camera already installed with sample code preloaded. I found this example sketch while trying to find the source for the preloaded code. Since I just wanted to play with some code, I was satisfied to hack the example!

### 📀 Software

You need the [Arduino IDE](https://www.arduino.cc/en/main/software), of course. It must be set up for ESP32 development, including the sketch data uploader. Check out [my guide](https://pmcg31.netlify.com/esp32-set-up-on-arduino/) if you need help!

You will also need the ArduinoJSON library. I have a [guide that includes downloading and setting that up](https://pmcg31.netlify.com/esp32-webserver-with-websockets/), too!

## 🧩 Getting set up

Once you have this project downloaded there are still a couple of things to do.

### 📡 WiFi credentials

You will need to rename the file `sample.config.json` to `config.json` and move it to the `data` directory. Edit the file to reflect the ssid and key for your network. The ESP32 will connect to this network and attempt to establish an mDNS responder.

Speaking of that mDNS responder, there is a key to control the responder name in `config.json`. In case you want multiple cameras. You're welcome!

## 🚀 Launching the project

Upload sketch data to the board first, then upload the sketch. Watch the serial monitor for WiFi to connect. If the mDNS responder was set up successfully, browse to the camera URL shown in the serial monitor ([http://espcam.local](http://espcam.local) by default). If the mDNS didn't work, it will spit its IP to the serial monitor instead. However you get there, this will let you see the (not gzipped) UI from the example. It lets you do a bunch of stuff with the camera, including face detection and recognition! 🤯

<p align="center" style="padding-top: 50">🍀 Good Luck! 🍀
