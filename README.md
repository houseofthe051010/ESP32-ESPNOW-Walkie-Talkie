Source: 

<p align="center">
  <img src="Assets/readme/both-walkies-main.jpg" alt="Both ESP32 walkie talkies side by side" width="900">
</p>




## The Project

This is a ESP32 walkie talkie that uses WIFi (ESPNOW) for long range communication. It uses the esp32-wroom-32-U with an external U.fl connector, OLED 0.96 I2C display, I2S INMP441 microphone, I2S MAX98357A 3W speaker amplifier, 10k volume potentiometer, PTT button + 5 menu buttons, LASER, and LED. The aim of this walkie talkie was to not just serve as a walkie talkie, but sort of like a custom flipper zero that was more wireless oriented, although the walkie talkie comes with 3 female dupont pins that can be plugged in externally for a UART connection.

This device was framed as a walkie talkie but it can be used as a Wi-Fi/IoT device handheld controller platform. This is the main advantage with WIFI on esp32s as you can connect to a lot of places.



### Features

* ESP-NOW DIRECT VOICE (No router needed, multiple devices can connect)
* U.FL antenna for maximum range
* Tested to 600 meters of distance
* No acknowledge on ESPNOW, just shout and listen
* 16 kHz mono voice capture with IMA ADPCM compression
* No acknowledgement can be a problem with dropped packets so at weak ranges packets are automatically duplicated
* Built in black box logging with telemetry that can be uploaded to computer.
* OLED GUI with many features to control the walkie talkie and use as a remote for other wifi things.




<p align="center">
  <img src="Assets/readme/both-walkies-second.jpg" alt="Second side-by-side photo of both ESP32 walkie talkies" width="900">
</p>

## Walkie Talkie Hardware

The enclosure was designed to have enough space to solder every wire, but a custom PCB version was also made, scroll all the way down to learn more about fabricating PCB.

<p align="center">
  <img src="Assets/readme/grey-walkie-only.jpg" alt="Grey ESP32 walkie talkie" width="420">
  <img src="Assets/readme/black-walkie-only.jpg" alt="Black ESP32 walkie talkie" width="420">
</p>

### Electronics

* ESP32WROOM32 U.FL
* OLED I2C 0.96'
* I2S INMP441 MIC
* 10K Volume potentiometer.
* 2000 MAH LIPO
* 6 push buttons
* 5mm LED light
* 5V laser module
* Voltage divider for ADC battery voltage measurment
* Main power switch

## Assembly Process

### 1. Printed enclosure

All these parts contribute to the final product

* [`walkie_talkie_bottom_case.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_bottom_case.stl)
* [`walkie_talkie_top_cover.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_top_cover.stl)
* [`walkie_talkie_top_buttons_grid.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_top_buttons_grid.stl)
* [`walkie_talkie_OK_button.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_OK_button.stl)
* [`walkie_talkie_PTT_button.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_PTT_button.stl)
* [`walkie_talkie_PTT_button_insert.stl`](SOURCE%20CAD/INDIVIDUAL%20STLS/walkie_talkie_PTT_button_insert.stl)



### 2. Power system

The battery powers the TP4056 which gives power to a boost converter than powers the entire device

1. Wire th TP4056 through the battery to the main switch to the boost convert and then to the esp32 VIN rail.

### 3. Electronics wiring


1. To make it easy and not messy, wire every component listed in the schematic to their respected GPIO and some pins might have multiple wires to them, thats fine.
2. Make sure to use heat shrink tape to avoid short circuits. 

### 4. Front-panel assembly

1. The LED and laser press into their  holes.
2. The PTT, OK, and four navigation buttons sit in the front-panel openings.
3. Insert the OLED
4. Secure all with super glue. Make sure to apply around perimeter and not damage the electronics.

### 5. Internal packing

1. Insert the electronics. One at a type, placing the esp32 underneath the TP4056 mount, and glueing each part to their holes.
2. The enclosure has enough space to accodomate addition UART connections if you want to connect something else later on.

### 6. ESP-IDF firmware loading


1. Fork the project and config with ESP-IDF to upload the code
2. Make sure you have experience with using powershell, open it

3. Init the powershell

   ```powershell
   idf.py set-target esp32
   ```

4. Open project using

   ```powershell
   idf.py menuconfig
   ```

6. Compile using

   ```powershell
   idf.py build
   ```

7. Flash using

   ```powershell
   idf.py flash monitor
   ```

## Circuit Diagram


<p align="center">
  <img src="Assets/Walkie%20Talkie%20Circuit%20Diagram.png" alt="Walkie talkie circuit diagram" width="900">
</p>

### Device PINOUT (Use when soldering)

| Function             | ESP32 GPIO |
| -------------------- | ---------: |
| OLED SCL             |     GPIO18 |
| OLED SDA             |     GPIO19 |
| Speaker BCLK         |     GPIO32 |
| Speaker WS/LRC       |     GPIO33 |
| Speaker DIN          |     GPIO25 |
| Microphone BCLK      |     GPIO16 |
| Microphone WS        |     GPIO17 |
| Microphone SD        |      GPIO4 |
| OK button            |      GPIO0 |
| Bottom-left button   |     GPIO14 |
| Bottom-right button  |     GPIO15 |
| Laser                |     GPIO21 |
| Volume potentiometer |     GPIO34 |
| Battery divider      |     GPIO35 |


## My versions:

## Grey Walkie

<p align="center">
  <img src="Assets/readme/grey-walkie-internal.jpg" alt="Grey walkie internal circuitry" width="900">
</p>


This is my 2nd iteration with much cleaner wiring

## Black Walkie

<p align="center">
  <img src="Assets/readme/black-walkie-internal.jpg" alt="Black walkie internal circuitry" width="900">
</p>

This first iteration is much more messier



### User Interface

The user interface has a whole "apps" menu for different wifi connections and button use cases, you can code your own for your own custom use cases.

<p align="center">
  <img src="Assets/PTT%20home%20screen%20GUI.png" alt="Real OLED PTT home screen GUI" width="420">
  <img src="Assets/SCANNING%20CHANNEL%20GUI.png" alt="Real OLED scanning channel GUI" width="420">
</p>

<p align="center">
  
</p>

<p align="center">
  <img src="Assets/Increase%20MIC%20sense%20settings%20GUI.png" alt="Real OLED increase mic sensitivity settings GUI" width="420">
  <img src="Assets/LIGHT%20STROBE%20GUI.png" alt="Real OLED light strobe app GUI" width="420">
</p>

<p align="center">
  
</p>


### Black Box

You can debug or see what happend with the walkie in the field, this isn't really needed now that I have perfected the code though, but can be helpful if you're making your own changes.

Example of a JSON black box record:

```json
{"event":"radio_stats","t_ms":123456,"board":"BLACK","ch":1,"ptt":false,"link":true,"rssi_dbm":-82,"quality_pct":21,"jitter_frames":3,"vol_pct":50,"tx_audio":0,"tx_audio_dup":0,"tx_ctrl":2,"tx_no_mem":0,"tx_fail":0,"rx_audio":48,"rx_audio_dup":7,"rx_audio_old":0,"rx_plc":2,"rx_ctrl":1,"rx_wrong_peer":0,"rx_bad_proto":0,"rx_wrong_channel":0}
```



## Bill of Materials

| Category    | Quantity | Part                                 | Purchase Link                                                      | Estimated Price |
| ----------- | -------: | ------------------------------------ | ------------------------------------------------------------------ | --------------: |
| Fabricated  |        2 | Walkie-talkie enclosure              | [AliExpress](https://www.aliexpress.us/item/3256806989098121.html) |           $2.22 |
| Electronics |        2 | ESP32 development board              | [AliExpress](https://www.aliexpress.us/item/3256807617923920.html) |           $1.90 |
| Radio       |        2 | External antenna                     | [AliExpress](https://www.aliexpress.us/item/3256812004598286.html) |      $0.64 used |
| Display     |        2 | 0.96-inch OLED display               | [AliExpress](https://www.aliexpress.us/item/3256805954920554.html) |      $1.98 used |
| Audio       |        2 | I2S microphone                       | [AliExpress](https://www.aliexpress.us/item/3256810210666726.html) |           $6.45 |
| Audio       |        2 | I2S speaker amplifier                | [AliExpress](https://www.aliexpress.us/item/3256809715431644.html) |      $1.88 used |
| Audio       |        2 | Speaker                              | [AliExpress](https://www.aliexpress.us/item/3256805151989671.html) |           $0.99 |
| Control     |        2 | Volume potentiometer                 | [AliExpress](https://www.aliexpress.us/item/3256805703535495.html) |           $0.99 |
| Power       |        2 | Lithium battery                      | [AliExpress](https://www.aliexpress.us/item/3256811489152615.html) |     $10.96 used |
| Power       |        2 | Battery charger and protection board | [AliExpress](https://www.aliexpress.us/item/3256809139500038.html) |      $0.20 used |
| Power       |        2 | Boost converter                      | [AliExpress](https://www.aliexpress.us/item/3256811757076890.html) |      $1.88 used |
| Power       |        2 | Main power switch                    | [AliExpress](https://www.aliexpress.us/item/3256809823421130.html) |           $2.37 |
| Lighting    |        2 | Status LED                           | [AliExpress](https://www.aliexpress.us/item/3256807537207911.html) |      $0.02 used |
| Lighting    |        2 | Laser module                         | [AliExpress](https://www.aliexpress.us/item/3256808318801769.html) |           $0.99 |
| Control     |       12 | Momentary pushbutton                 | [AliExpress](https://www.aliexpress.us/item/3256810479380665.html) |           $0.99 |
| Optional RC |        2 | Continuous-rotation servo            | [AliExpress](https://www.aliexpress.us/item/3256804365417662.html) |           $9.28 |
| Measurement |        2 | 100 kΩ battery-divider resistor      | [AliExpress](https://www.aliexpress.us/item/3256802303553096.html) |      $0.02 used |
| Measurement |        2 | 220 kΩ battery-divider resistor      | [AliExpress](https://www.aliexpress.us/item/3256802303553096.html) |      $0.02 used |
| Wiring      |        1 | Signal and power wire                | [AliExpress](https://www.aliexpress.us/item/3256810394181790.html) | $0.99 allowance |


## Custom PCB Fabrication Option

If you want to avoid the hassle of soldering than fabricate your own PCB here: 

See [CUSTOM PCB FABRICATION/README.md](CUSTOM%20PCB%20FABRICATION/README.md) for the JLBPCB fabrication guide
