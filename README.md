micropython-lorawan-heltec-v4.2.bin is AS923 for Heltec LoRa bot V.3.2 and 4.2.

Example

import lorawan,time
import tbeam
lw = lorawan.LoRaWAN(
    region=lorawan.AS923,
    lorawan_version=lorawan.V1_0_4,
    radio="sx1262",
    spi_id=2,
    sclk=9,
    mosi=10,
    miso=11,
    cs=8,
    reset=12,
    irq=14,
    busy=13,
)

print("b..")
if not lw.joined():
    lw.join_otaa(
        dev_eui=bytes.fromhex("70B3D57ED00683AA"),
        join_eui=bytes.fromhex("0000000000000000"),
        app_key=bytes.fromhex("78164A6458CF125EFCD4BE75EB6E00AA"),
        timeout=60,
    )

while True:
    lw.send(b"Hello", port=1)
    print("Sent!")
    time.sleep(5)

