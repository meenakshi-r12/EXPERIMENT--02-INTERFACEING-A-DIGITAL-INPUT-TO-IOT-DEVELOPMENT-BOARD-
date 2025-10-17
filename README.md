###  DATE: 17.10.25

###  NAME: Meenakshi.R
###  ROLL NO :212224220062
###  DEPARTMENT: IT


# EXPERIMENT--02-INTERFACING-A-DIGITAL-INPUT-TO-IOT-DEVELOPMENT-BOARD-
 

## Aim: To Interface a Digital Input  (IR pair ) to ARM IOT development board and write a  program to obtain  the data 
## Components required: STM32 CUBE IDE, ARM IOT development board,  STM programmer tool.
## Theory 
The full form of an ARM is an advanced reduced instruction set computer (RISC) machine, and it is a 32-bit processor architecture expanded by ARM holdings. The applications of an ARM processor include several microcontrollers as well as processors. The architecture of an ARM processor was licensed by many corporations for designing ARM processor-based SoC products and CPUs. This allows the corporations to manufacture their products using ARM architecture. Likewise, all main semiconductor companies will make ARM-based SOCs such as Samsung, Atmel, TI etc.

 
 # IR pair 
 
 ![image](https://user-images.githubusercontent.com/36288975/227598600-730748bf-9884-4a33-95bf-a1fbfde518ed.png)

 IR technology is used in a wide range of wireless applications which includes remote controls and sensing. The infrared part in the electromagnetic spectrum can be separated into three main regions: near IR, mid-IR & far IR. The wavelengths of these three regions vary based on the application. For the near IR region, the wavelength ranges from 700 nm- 1400 nm, the wavelength of the mid-IR region ranges from 1400 nm – 3000 nm & finally for the far IR region, the wavelength ranges from 3000 nm – 1 mm.The near IR region is used on fiber optic & IR sensors, the mid-IR region is used for heat sensing and the far IR region is used in thermal imaging. The range of frequency for IR is maximum as compared to microwave and minimum than visible light.  
## Procedure:
 1. click on STM 32 CUBE IDE, the following screen will appear 
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)

 2. click on FILE, click on new stm 32 project 
 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)
3. select the target to be programmed  as shown below and click on next 

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

4.select the program name 
![image](https://user-images.githubusercontent.com/36288975/226189316-09832a30-4d1a-4d4f-b8ad-2dc28f137711.png)


5. corresponding ioc file will be generated automatically 
![image](https://user-images.githubusercontent.com/36288975/226189378-3abbdee2-0df6-470f-a3cd-79c74e3d3ad8.png)

6.select the appropriate pins as gipo, in or out, USART or required options and configure 
![image](https://user-images.githubusercontent.com/36288975/226189403-f7179f1a-3eae-4637-826b-ab4ec35ba1e1.png)
![image](https://user-images.githubusercontent.com/36288975/226189425-2b2414ce-49b3-4b61-a260-c658cb2e4152.png)


7.click on cntrl+S , automaticall C program will be generated 
![image](https://user-images.githubusercontent.com/36288975/226189443-8b43451d-0b14-47e4-a20b-cc09c6ad8458.png)
![image](https://user-images.githubusercontent.com/36288975/226189450-85ffa969-2ffb-4788-81e5-72d60fdda0f1.png)
8. edit the program and as per required 
![image](https://user-images.githubusercontent.com/36288975/226189461-a573e62f-a109-4631-a250-a20925758fe0.png)

9. use project and build all 
![image](https://user-images.githubusercontent.com/36288975/226189554-3f7101ac-3f41-48fc-abc7-480bd6218dec.png)
10. once the project is bulild 
![image](https://user-images.githubusercontent.com/36288975/226189577-c61cc1eb-3990-4968-8aa6-aefffc766b70.png)

11. click on debug option 
![image](https://user-images.githubusercontent.com/36288975/226189625-37daa9a3-62e9-42b5-a5ce-2ac63345905b.png)

12. connect the  iot board to power supply and usb 

13. After connecting open the STM cube programmer 
![image](https://user-images.githubusercontent.com/36288975/227599356-9c465b7e-6bd0-436b-b4e8-742ed25e06ce.png)

14. click on UART and click on connect 
![image](https://user-images.githubusercontent.com/36288975/227599458-26976d4a-f2d4-49f0-a49f-31f46eb15761.png)

15. once it is connected , click on Erasing and programming option 
![image](https://user-images.githubusercontent.com/36288975/227599531-f03d277e-440f-4f8a-8875-97f8e8058c71.png)

16. flash the bin or hex file as shown below by switching the switch to flash mode 

![image](https://user-images.githubusercontent.com/36288975/227599656-dc4a635f-b5f1-44c8-84c5-ee0a592fa184.png)


17. check for execution of the output by switching the board to run mode 



## STM 32 CUBE PROGRAM :
```
ENTRY(Reset_Handler)

/* Highest address of the user mode stack */
_estack = ORIGIN(RAM) + LENGTH(RAM); /* end of "RAM" Ram type memory */

_Min_Heap_Size = 0x200; /* required amount of heap  */
_Min_Stack_Size = 0x400; /* required amount of stack */

/* Memories definition */
MEMORY
{
  RAM    (xrw)   : ORIGIN = 0x20000000, LENGTH = 64K
  RAM2   (xrw)   : ORIGIN = 0x10000000, LENGTH = 32K
  FLASH   (rx)   : ORIGIN = 0x08000000, LENGTH = 256K
}

/* Sections */
SECTIONS
{
  /* The startup code into "FLASH" Rom type memory */
  .isr_vector :
  {
    . = ALIGN(4);
    KEEP(*(.isr_vector)) /* Startup code */
    . = ALIGN(4);
  } >FLASH

  /* The program code and other data into "FLASH" Rom type memory */
  .text :
  {
    . = ALIGN(4);
    *(.text)           /* .text sections (code) */
    *(.text*)          /* .text* sections (code) */
    *(.glue_7)         /* glue arm to thumb code */
    *(.glue_7t)        /* glue thumb to arm code */
    *(.eh_frame)

    KEEP (*(.init))
    KEEP (*(.fini))

    . = ALIGN(4);
    _etext = .;        /* define a global symbols at end of code */
  } >FLASH

  /* Constant data into "FLASH" Rom type memory */
  .rodata :
  {
    . = ALIGN(4);
    *(.rodata)         /* .rodata sections (constants, strings, etc.) */
    *(.rodata*)        /* .rodata* sections (constants, strings, etc.) */
    . = ALIGN(4);
  } >FLASH

  .ARM.extab (READONLY) : /* The READONLY keyword is only supported in GCC11 and later, remove it if using GCC10 or earlier. */
  {
    . = ALIGN(4);
    *(.ARM.extab* .gnu.linkonce.armextab.*)
    . = ALIGN(4);
  } >FLASH
  .ARM (READONLY) : /* The READONLY keyword is only supported in GCC11 and later, remove it if using GCC10 or earlier. */
  {
    . = ALIGN(4);
    __exidx_start = .;
    *(.ARM.exidx*)
    __exidx_end = .;
    . = ALIGN(4);
  } >FLASH

  .preinit_array (READONLY) : /* The READONLY keyword is only supported in GCC11 and later, remove it if using GCC10 or earlier. */
  {
    . = ALIGN(4);
    PROVIDE_HIDDEN (__preinit_array_start = .);
    KEEP (*(.preinit_array*))
    PROVIDE_HIDDEN (__preinit_array_end = .);
    . = ALIGN(4);
  } >FLASH

  .init_array (READONLY) : /* The READONLY keyword is only supported in GCC11 and later, remove it if using GCC10 or earlier. */
  {
    . = ALIGN(4);
    PROVIDE_HIDDEN (__init_array_start = .);
    KEEP (*(SORT(.init_array.*)))
    KEEP (*(.init_array*))
    PROVIDE_HIDDEN (__init_array_end = .);
    . = ALIGN(4);
  } >FLASH

  .fini_array (READONLY) : /* The READONLY keyword is only supported in GCC11 and later, remove it if using GCC10 or earlier. */
  {
    . = ALIGN(4);
    PROVIDE_HIDDEN (__fini_array_start = .);
    KEEP (*(SORT(.fini_array.*)))
    KEEP (*(.fini_array*))
    PROVIDE_HIDDEN (__fini_array_end = .);
    . = ALIGN(4);
  } >FLASH

  /* Used by the startup to initialize data */
  _sidata = LOADADDR(.data);

  /* Initialized data sections into "RAM" Ram type memory */
  .data :
  {
    . = ALIGN(4);
    _sdata = .;        /* create a global symbol at data start */
    *(.data)           /* .data sections */
    *(.data*)          /* .data* sections */
    *(.RamFunc)        /* .RamFunc sections */
    *(.RamFunc*)       /* .RamFunc* sections */

    . = ALIGN(4);
    _edata = .;        /* define a global symbol at data end */

  } >RAM AT> FLASH

  /* Uninitialized data section into "RAM" Ram type memory */
  . = ALIGN(4);
  .bss :
  {
    /* This is used by the startup in order to initialize the .bss section */
    _sbss = .;         /* define a global symbol at bss start */
    __bss_start__ = _sbss;
    *(.bss)
    *(.bss*)
    *(COMMON)

    . = ALIGN(4);
    _ebss = .;         /* define a global symbol at bss end */
    __bss_end__ = _ebss;
  } >RAM

  /* User_heap_stack section, used to check that there is enough "RAM" Ram  type memory left */
  ._user_heap_stack :
  {
    . = ALIGN(8);
    PROVIDE ( end = . );
    PROVIDE ( _end = . );
    . = . + _Min_Heap_Size;
    . = . + _Min_Stack_Size;
    . = ALIGN(8);
  } >RAM

  /* Remove information from the compiler libraries */
  /DISCARD/ :
  {
    libc.a ( * )
    libm.a ( * )
    libgcc.a ( * )
  }

  .ARM.attributes 0 : { *(.ARM.attributes) }
}
```


## Output  :
 
 
 <img width="500" height="395" alt="493192257-8069cd80-295b-44c6-b4d2-be90a94215e4" src="https://github.com/user-attachments/assets/333280ac-e7ce-4975-bf03-dbe792469959" />

 
## Result :
Interfacing a digital Input (ir pair) with ARM microcontroller based IOT development is executed and the results are verified.
