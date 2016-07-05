#CAN-BUS Shield
----
##Introduction

CAN-BUS is a common industrial bus because of its long travel distance, medium communication speed and high reliability. It is commonly found on modern machine tools and as an automotive diagnostic bus. 

This CAN-BUS Shield adopts MCP2515 CAN Bus controller with SPI interface and MCP2551 CAN transceiver to give your Arduino/Seeeduino CAN-BUS capibility. With an OBD-II converter cable added on and the OBD-II library imported, you are ready to build an onboard diagnostic device or data logger.

![](https://github.com/SeeedDocument/CAN_BUS_Shield/blob/master/image/Can_bus_shield_all.jpg?raw=true)

##Features

- Implements CAN V2.0B at up to 1 Mb/s
- SPI Interface up to 10 MHz
- Standard (11 bit) and extended (29 bit) data and remote frames
- Two receive buffers with prioritized message storage
- Industrial standard 9 pin sub-D connector
- LED indicators

##Hardware Overview

![](https://github.com/SeeedDocument/CAN_BUS_Shield/blob/master/image/hardware_overview_1.png?raw=true)

1. **DB9 Interface** - to connect to OBDII Interface via a DBG-OBD Cable.
2. **V_OBD** - If get power from OBDII Interface(from DB9)
3. **Led Indicator**:
    - **PWR**: power
    - **TX**: blink when the data is sending
    - **RX**: blink when there's data coming
    - **INT**: data interrupt
4. **Terminal** - CAN_H and CAN_L
5. Arduino UNO pin out
6. Serial Grove connector
7. I2C Grove connector
8. ICSP pins
9. **IC** - MCP2551, a high-speed can transceiver ([datasheet](https://github.com/SeeedDocument/CAN_BUS_Shield/raw/master/resource/Mcp2551.pdf))
10. **IC** - MCP2515, stand-alone CAN controller wth SPI interface ([datasheet](https://github.com/SeeedDocument/CAN_BUS_Shield/raw/master/resource/MCP2515.pdf))


!!!warning
    When you use more than two CAN Bus Shield in one net, you should think about the impedance.
    You can just cut P1 in the PCB with a knife, or just remove R3 on the PCB.

###Digital Pin Used

|Arduino Pin|Function               |
|-----------|-----------------------|
|D0         |Not Used               |
|D1	        |Not Used               |
|D2		    |**Receive Interrupt**  |
|D3     	|Not Used               |
|D4	        |Not_Used               |
|D5	        |Not Used               |
|D6	        |Not Used               |
|D7	        |Not Used               |
|D8	        |Not Used               |
|D9	        |**SPI_CS(default)**    |
|D10        |**SPI_CS(selectable)** |
|D11        |**SPI_MOSI(default)**  |
|D12        |**SPI_MISO(default) ** |
|D13        |**SPI_SCK(default) **  |

###Analog Pin Used


|Arduino Pin|Function|
|-----------|--------|
|A0	        |Not_Used|
|A1	        |Not_Used|
|A2	        |Not_Used|
|A3	        |Not_Used|
|A4	        |Not Used|
|A5	        |Not Used|
