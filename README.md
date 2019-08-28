# FlexSPI Flash Programming Algorithm for NXP RT106x

### Customize algorithm for different FlexSPI flash:

Set the **FLEXSPI_OPTION0** macro to **FLEXSPI_xxx** in the FlashPrg.c file according to your flash type. If predefined parameters not meet your device, please set **FLEXSPI_OPTION0** and **FLEXSPI_OPTION1** to the correct value of your flash type. Reference to the end of chapter 8, System Boot, in the  i.MXRT1060 RM for the definition of two options.

```
# define FLEXSPI_QSPI        0xC0000008

# define FLEXSPI_QSPIDDR     0xc0100003

# define FLEXSPI_HYPER1V8    0xc0233009

# define FLEXSPI_HYPER3V0    0xc0333006

# define FLEXSPI_MXICOPIDDR  0xc0333006

# define FLEXSPI_MCRNOCT     0xc0600006

# define FLEXSPI_MCRNOPI     0xc0603008

# define FLEXSPI_MCRNOPIDDR  0xc0633008

# define FLEXSPI_ADSTOPI     0xc0803008

# define FLEXSPI_OPTION0     FLEXSPI_QSPI  /* Change it accordign to your device */

# define FLEXSPI_OPTION1     0x00000000		/* Change it accordign to your device */
```

If you want to change the default parameters of flash, such as device size and page size, change them in the FlashDev.c file.

```
struct FlashDevice const FlashDevice  =  {
   FLASH_DRV_VERS,             // Driver Version, do not modify!
   "MIMXRT106x 8mB QuadSPI NOR Flash",   // Device Name 
   EXTSPI,                    // Device Type
   0x60000000,                 // Device Start Address
   0x800000,                   // Device Size in Bytes (8mB)
   256,                        // Programming Page Size
   0,                          // Reserved, must be 0
   0xFF,                       // Initial Content of Erased Memory
   100,                        // Program Page Timeout 100 mSec
   5000,                       // Erase Sector Timeout 5000 mSec

// Specify Size and Address of Sectors
   0x001000, 0x000000,         // Sector Size  4kB 
   SECTOR_END
};
```



### References:

For more information, refer to the documentation available at:

http://arm-software.github.io/CMSIS_5/Pack/html/flashAlgorithm.html

The initial CMSIS flash programming algorithm template is available at:

https://github.com/ARM-software/CMSIS_5/tree/develop/Device/_Template_Flash

How to add the Algorithm to RT1050 DFP, refer to the document available at:

http://arm-software.github.io/CMSIS_5/Pack/html/flashAlgorithm.html#AddFPA

