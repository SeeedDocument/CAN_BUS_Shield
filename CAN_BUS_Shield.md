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

##Getting Started

// to be continue


##APIs

###1. Set the Baudrate

This function is used to initialize the baudrate of the CAN Bus system.

The available baudrates are listed as follws:

	#define CAN_5KBPS    1
	#define CAN_10KBPS   2
	#define CAN_20KBPS   3
	#define CAN_25KBPS   4 
	#define CAN_31K25BPS 5
	#define CAN_33KBPS   6
	#define CAN_40KBPS   7
	#define CAN_50KBPS   8
	#define CAN_80KBPS   9
	#define CAN_83K3BPS  10
	#define CAN_95KBPS   11
	#define CAN_100KBPS  12
	#define CAN_125KBPS  13
	#define CAN_200KBPS  14
	#define CAN_250KBPS  15
	#define CAN_500KBPS  16
	#define CAN_666kbps  17
	#define CAN_1000KBPS 18

###2. Set Receive Mask and Filter

There are **2** receive mask registers and **5** filter registers on the controller chip that guarantee you get data from the target device. They are useful especially in a large network consisting of numerous nodes.

We provide two functions for you to utilize these mask and filter registers. They are:

**Mask:**

	init_Mask(unsigned char num, unsigned char ext, unsigned char ulData);

**Filter:**

	init_Filt(unsigned char num, unsigned char ext, unsigned char ulData);


- **num** represents which register to use. You can fill 0 or 1 for mask and 0 to 5 for filter.
- **ext** represents the status of the frame. 0 means it's a mask or filter for a standard frame. 1 means it's for a extended frame.
- **ulData** represents the content of the mask of filter.

###3. Check Receive
The MCP2515 can operate in either a polled mode, where the software checks for a received frame, or using additional pins to signal that a frame has been received or transmit completed. 

Use the following function to poll for received frames.

    INT8U MCP_CAN::checkReceive(void);

The function will return 1 if a frame arrives, and 0 if nothing arrives.

###4. Get CAN ID
When some data arrive, you can use the following function to get the CAN ID of the "send" node.

    INT32U MCP_CAN::getCanId(void)

###5. Send Data

    CAN.sendMsgBuf(INT8U id, INT8U ext, INT8U len, data_buf);

It is a function to send data onto the bus. In which:

* **id** represents where the data come from.
* **ext** represents the status of the frame. '0' means standard frame. '1' means extended frame.
* **len** represents the length of this frame.
* **data_buf** is the content of this message.

For example, In the 'send' example, we have:

    unsigned char stmp[8] = {0, 1, 2, 3, 4, 5, 6, 7};
    CAN.sendMsgBuf(0x00, 0, 8, stmp); //send out the message 'stmp' to the bus and tell other devices this is a standard frame from 0x00.

###6. Receive Data

The following function is used to receive data on the 'receive' node:

    CAN.readMsgBuf(unsigned char len, unsigned char buf);
In conditions that masks and filters have been set. This function can only get frames that meet the requirements of masks and filters.

* **len** represents the data length.
* **buf** is where you store the data.

##Generate a New BaudRate

We had provided many frequently-used baud rate, as below:

	#define CAN_5KBPS    1
	#define CAN_10KBPS   2
	#define CAN_20KBPS   3
	#define CAN_25KBPS   4 
	#define CAN_31K25BPS 5
	#define CAN_33KBPS   6
	#define CAN_40KBPS   7
	#define CAN_50KBPS   8
	#define CAN_80KBPS   9
	#define CAN_83K3BPS  10
	#define CAN_95KBPS   11
	#define CAN_100KBPS  12
	#define CAN_125KBPS  13
	#define CAN_200KBPS  14
	#define CAN_250KBPS  15
	#define CAN_500KBPS  16
	#define CAN_666kbps  17
	#define CAN_1000KBPS 18

Yet you may still can't find the rate you want. Here we provide a software to help you to calculate the baud rate you need.

Click here to download the software, it's in Chinese, but never mind, it's easy to use. And the software support Windows only.

