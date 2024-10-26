The Wiznet IO (Ethernet Offload) library comes with a simple and small HTTP web server code. In this chapter we will understand its structure and working. Then we will use it to serve a small webpage from our STM32 to a web browser that is running on our PC.

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

##Initialize the HTTP Server

```
httpServer_init(http_tx_buff, http_rx_buff, MAX_HTTPSOCK, socknumlist);
reg_httpServer_cbfunc(NULL, NULL);
```

##More information
To learn more about w5500 Ethernet controller and its interface with STM32, please subsribe to our course on Udemy.
[Udemy's course on W5500 Interfacing](https://www.udemy.com/course/ethernet-on-stm32-using-w5500/)
