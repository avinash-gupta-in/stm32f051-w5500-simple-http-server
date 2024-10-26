# STM32 W5500 HTTP WebServer Example

The Wiznet IO (Ethernet Offload) library comes with a simple and small HTTP web server code. In this chapter we will understand its structure and working. Then we will use it to serve a small webpage from our STM32 to a web browser that is running on our PC.

![W5500 Web Server](https://extremeelectronics.co.in/github/w5500/stm32-w5500-http-server.png)

The HTTP Server Init function takes the number of sockets to use and an array of socket IDs. So, we define some constants and this array.

```
#define MAX_HTTPSOCK	6
uint8_t socknumlist[] = {2, 3, 4, 5, 6, 7};
```

The init function also need two statically allocated data buffers, one for RX and one for TX, both are 1KB long in the example program.

```
//name of this macro is important as it is used by httpservr module
#define DATA_BUF_SIZE 1024 //Both Rx and Tx
```

```
///////////////////////////////////////////////////////////////////////////
// Static Buffer for HTTP Server
///////////////////////////////////////////////////////////////////////////
uint8_t http_rx_buff[DATA_BUF_SIZE];
uint8_t http_tx_buff[DATA_BUF_SIZE];
```

## Initialize the HTTP Server

```
httpServer_init(http_tx_buff, http_rx_buff, MAX_HTTPSOCK, socknumlist);
reg_httpServer_cbfunc(NULL, NULL);
```

## Hardware Details
The code is written to run on a STM32F051 ARM Cortex M0 MCU. The W5500 is attached to the SPI Port and shown in table below.

| W5500    | STM32   |
| -------- | ------- |
| MISO     | PA6     |
| MOSI     | PA7     |
| SCLK     | PA5     |
| SCS      | PA1     |
| RST      | PA0     |
| INT      | NC      |

NC=No Connection
SCS=Chip Select (Active Low)

To view the debug output of the program we need a USB to Serial convertor like FT232RL (3.3V Version only)
The debug messages comes out on the TX pin of the USART2 peripheral of the STM32F051. This is **PA2**.
The baud rate is 38400. User RealTerm to view the outputs.

![real term showing output of http webserver](https://extremeelectronics.co.in/github/w5500/w5500-webserver-realterm.png)

You will need ![STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) (Free from ST Microelectronics) to compile, build, flash (burn) and debug this project.

![STM32CubeIDE Popup](https://www.st.com/en/development-tools/stm32cube_ide.png)

## More information
To learn more about w5500 Ethernet controller and its interface with STM32, please subsribe to our course on Udemy.
[Udemy's course on W5500 Interfacing](https://www.udemy.com/course/ethernet-on-stm32-using-w5500/)
