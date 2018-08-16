# modbus4dsys
This example was ported from the library published at https://github.com/smarmengol/Modbus-Master-Slave-for-Arduino. The original library is one of the best implementations of Modbus RTU for Arduino. It implements the Master and Slave function codes 1,2,3,4,5,6, 15 and 16 of Modbus RTU protocol. 
This port does not implement the slave functinality. Check TODOs section.
## Getting Started
This example was developed and tested on the Gen4-uLCD-32DT (https://www.4dsystems.com.au/product/gen4_uLCD_32D/). This intelligent display implements the Diablo16 processor. Rnning this code requires some specific Diablo16 internal functions and may not be compatible with other graphic processors of 4D Systems. 

This repository includes a complete example for VISI IDE. Modbus is implemented in the same example as a group of functions, contants and procedures.

### Prerequisites
- Gen4-uLCD-32DT or any other Diablo16 based display
- Programming interface Gen4-PA 
- Modbus slave device. I recommend a Modbus PLC emulator (http://www.plcsimulator.org/) for your first test.

### Testing
- Connect your Gen4-uLCD-32DT to your computer using the programming interface. 
- Set Mobus parameters in source code:

```
  SERIAL:=0; //serial port to USE  0 for defualt port , 1 for serial port 1
  SLAVE_ADDRESS :=1; //adress of slave device
  MOD_TIMEOUT := 3000; //  timeout read/write modbus in ms
  MOD_POOL_T := 350; // pooling time period modbus in ms
  MOD_BAUDRATE := 960; // 9600 bauds according to Diablo16 documentation
```  
 
- Compile and download the example to your display
- Launch the emulator and configure the same serial port used  on Workshop 4 for downloading the example.
- Set the correct baudrate (9600), no parity, 1 stop bit, 8 bit data, RTS control disabled.
- Open the serial port and test your application.


## Known issues
Since Modbus polls data continuously from slave an uses many background tasks, it consumes considerable resources of Diablo16 processor. I faced some instability of EVE virtual machine and even some crashes. I am pretty sure crashes are not related to bugs in Modbus implementation. I realized that incrementing the MOD_POOL_T period helps with stability, especially when many objects of the display are modified with data coming from Modbus slave. I am not an expert on 4D systems products, but I think Diablo16 is not able to manage a demanding USART communication and update the screen at the same time. However, this is not a big issue, I managed to develop a functional and responsive application connecting to real Koyo PLC (slave) using the parameters of the included example.

## TODOs
- Implement Modbus slave fucntionality, it may be ported from the original library.
- Improve comments and help
- Test the example with a RS485 connection. It was only tested with a point to point RS232.


## More information about Modbus
http://www.simplymodbus.ca/FAQ.htm


