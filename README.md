# Compiling and Loading Software to AVR Microcontrollers #

Using avr-gcc compiler and AVRDUDESS loader on Windows.


1. Install avr-gcc compiler.[1]
 1. Download and extract relevant file (avr8-gnu-toolchain-3.7.0.1796-win32.any.x86_64.zip) from [2].
 2. Add bin folder to path variable.
OR use a .bat file that adds it to path just for a cmd session[4].
OR just use bin folder as current working directory in cmd later.


2. Install avrdudess (gui for avrdude).[1]
 1. Download and run relevant file (AVRDUDESS-2.18-setup.exe) from [5].
OR, download and extract the portable zip from [5].


3. Compile example blink program.[1][6]
blink.c:
```c
#define F_CPU 1000000UL

#include <avr/io.h>
#include <util/delay.h>

int main(void) {
	DDRB |= (1 << PB0);

	while (1) {
		PORTB |= (1 << PB0);
		_delay_ms(2000);
		PORTB &= ~(1 << PB0);
		_delay_ms(2000);
	}

	return 0;
}
```

 1. run in cmd:
`avr-gcc -mmcu=atmega8535 -Wall -Os -o blink.elf blink.c`

^ from [3]:
pg103: `-mmcu` option selects microcontroller
pg110: `-Os` optimizes for size
pg49: link to gcc manual[7]
^ from [8]: `-Wall` enables all warnings
^ from [9]: `-o` indicates name of output ; blink.c is input file


4. Plug USBasp programmer into USB port. Windows automatically installs a driver.

5. Change driver.
 1. Run zadig-2.4.exe [4][10] (from [11] or [13]) (no install, just runs).
 2. Select USBasp and libusb-win32. [10]

6. Connect USBasp to microcontroller.[1][12]

7. Load program with AVRDUDESS.
 1. Run avrdudess.exe .
 2. Select programmer: usbasp , select microcontroller: ATMega8535, select blink.elf file.
 3. Click Program! button.



## References ##

[1] https://github.com/m3y54m/start-avr
[2] https://www.microchip.com/en-us/tools-resources/develop/microchip-studio/gcc-compilers
[3] avr8-gnu-toolchain-win32_x86_64\doc\avr-libc\avr-libc-user-manual.pdf
^ file within zip file downloaded from [2]

[4] https://tinusaur.com/guides/avr-gcc-toolchain/

[5] https://github.com/ZakKemble/AVRDUDESS/releases

[6] https://toastedcornflakes.github.io/articles/avr_getting_started.html

[7] https://gcc.gnu.org/onlinedocs/
[8] https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wall
[9] https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Overall-Options.html

[10] https://media.jaycar.com.au/product/resources/XC4627_manualMain_86841.pdf
[11] https://media.jaycar.com.au/product/resources/XC4627_softwareMain_74679.zip

[12] https://ww1.microchip.com/downloads/en/DeviceDoc/doc2502.pdf	ATMega8535 datasheet

[13] https://zadig.akeo.ie/

