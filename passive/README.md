# Passive CSI collection

Listens passively for packets on channel 3 (same channel as both active_ap and active_sta). This channel can be changed in `main/main.c` depending on the channel of the device you wish to passively listen for.

The easiest way to evaluate this sub-project is to flash three ESP32s. One with active_ap, one with active_sta and finally one with this passive sub-project.

To use run `idf.py flash monitor` from a terminal.

*This clone is made for benchmarking purposes against other CSI firmware implementations.*

The original Hernadez passive version source repository contained an incomplete hardware, hence the need for this fork. 

To ensure a fair, identical, and functionally valid baseline comparison against the other firmwares, minimal core modifications were applied to Wi-ESP solely to enable hardware power-on and data serialization output. No algorithmic or performance optimizations were performed.

The total flash size of the firmware after these modifications is as extracted by the command `idf.py size` is:

```bash
Total sizes:
Used static DRAM:   33932 bytes ( 146804 remain, 18.8% used)
      .data size:   13444 bytes
      .bss  size:   20488 bytes
Used static IRAM:   86242 bytes (  44830 remain, 65.8% used)
      .text size:   85215 bytes
   .vectors size:    1027 bytes
Used Flash size :  769711 bytes
      .text     :  610183 bytes
      .rodata   :  159272 bytes
Total image size:  869397 bytes (.bin may be padded larger)
```

To find more details about the resource usage of the firmware such as CPU load (example: % time spent in CSI processing task) and RAM usage (heap + stack) during runtime, please use the `resources_usage` branch of this repository which contains the necessary code for measuring these metrics.

This implementation includes the code for acquiring the CSI (Channel State Information) using ESP32.
NOTE: This code is designed to be compatible with both Espressif version 4.3 and earlier versions.
