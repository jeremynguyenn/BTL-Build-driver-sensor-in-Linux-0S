## Install Driver for Raspberry Pi to use TCS34725 sensor

To install the “tcs34725_driver” for the Raspberry Pi, follow these steps:

- Step 1:  Navigate to the “/boot” directory of the Raspberry Pi.

- Step 2: Convert the Raspberry Pi device tree blob (.dtb) file to a device tree source (.dts) file using the following command:

            “dtc -I dts -O dtb -o your_license_raspPi.dtb your_liscence_raspPi.dts”

Note: At this step, it is important to select the correct Raspberry Pi model to ensure compatibility with the corresponding .dtb file.

Example: Using raspberry Pi 3 with the following command:

            “dtc -I dtb -O dts -o bcm2710-rpi-3-b.dts bcm2710-rpi-3-b.dtb”
            
Note: Replace bcm2710-rpi-3-b.dtb with the appropriate .dtb file for your specific Raspberry Pi model.

- Step 3: To proceed with Step 3, after opening the .dts file created in Step 2, you need to search for the section where the I2C-1 is defined. Once found, add the necessary code snippet to enable the I2C-1 interface:
![image](https://github.com/user-attachments/assets/eade3492-2507-4dcd-b002-fb5a7a0104bb)

- Step 4: After editing the file, save the changes and recompile the .dts file back into .dtb. Finally, reboot the Raspberry Pi for the changes to take effect:

            “dtc -I dts -O dtb -o your_liscence_raspPi.dtb your_liscence_raspPi.dts”

Example: Using raspberry Pi 3 with the following command:

            “dtc -I dts -O dtb -o bcm2710-rpi-3-b.dtb bcm2710-rpi-3-b.dts”
then 
            “sduo reboot”

- Step 5: Makefile and install Driver into system

            + Ensure that the "driver" file and the Makefile are in the same folder. Then run the make command:  “make”
  
            + Once the make command completes successfully, the file driver.ko will be generated.
  
            + The next step is to install the driver into the Raspberry Pi using the following command:   "sudo insmod driver.ko”.

            + You can check the installation status using the dmesg command “dmesg”.
  
            + Similarly, if you want to remove the installed driver, use the following command: “sudo rmmod driver”.

## Installation and Usage of the TCS34725_lib Library for Reading the Sensor TCS34725
5.1	Install library TCS34725_lib
To complement the driver, the team has developed a dedicated library for the TCS34725 sensor. The “tcs34725_lib” library provides users with functions to configure the sensor and retrieve values from the four color channels: clear, red, green, and blue. To install and use the library, follow these steps:

- Step 1: Make sure that your “code_lib.c” and “tcs34725_library.h” files are in the same folder.
- Step 2: Proceed with installing the library by following these steps:
   +	Compile the file into position-independent code: “gcc -c -fPIC code_lib.c -o code.o”
     
   +	Create the shared library: “gcc -shared -o libtcs34725_library.so code.o”
  
   + 	Copy file tcs34725_library.h to usr/include and tcs34725_library.so to usr/lib
 	
   + 	Link your program with the library  “gcc file.c -L -ltcs34725_library -o newfile”
  
By completing the above steps, you have successfully installed the “tcs34725_lib” library on the Raspberry Pi. Details about the library are provided in section 4.2
