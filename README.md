# Compiling and Loading Software to AVR Microcontrollers #

Using avr-gcc compiler and AVRDUDESS loader on Windows, with ATMega8535 microcontroller.


1. Install avr-gcc compiler.[1]
    1. Download and extract relevant file (avr8-gnu-toolchain-3.7.0.1796-win32.any.x86_64.zip) from [2].
    2. Add bin folder to path variable.<br>
OR use a .bat file that adds it to path just for a cmd session[6].<br>
OR just use bin folder as current working directory in cmd later. <<<


2. Install AVRDUDESS (gui for avrdude).[1]
    1. Download and run relevant file (AVRDUDESS-2.18-setup.exe) from [7].<br>
OR, download and extract the portable zip from [7]. <<<


3. Compile example blink program, blink.c.[1][8]<br>
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

run in cmd:<br>
`avr-gcc -mmcu=atmega8535 -Wall -Os -o blink.elf blink.c`

`-mmcu` option selects microcontroller;[3] pg103, [4]<br>
`-Os` optimizes for size;[3] pg110, [5]<br>
-[3] pg49 links to gcc user manual[9]<br>
`-Wall` enables all warnings[10]<br>
`-o` is followed by name of output file; blink.c is input file[11]


4. Plug USBasp programmer into USB port. Windows automatically installs a driver.

5. Change driver.
    1. Run zadig-2.4.exe [6][12] (from [13] or [15]) (no install, just runs).
    2. Select USBasp and libusb-win32. [12]

6. Connect USBasp to microcontroller.[1], [14] pg251

7. Load program with AVRDUDESS.[12]
    1. Run avrdudess.exe .
    2. Select programmer: usbasp , select microcontroller: ATMega8535, select blink.elf file.
    3. Click Program! button.



## References ##

[1] https://github.com/m3y54m/start-avr<br>
[2] https://www.microchip.com/en-us/tools-resources/develop/microchip-studio/gcc-compilers<br>
[3] avr8-gnu-toolchain-win32_x86_64\doc\avr-libc\avr-libc-user-manual.pdf<br>
^ file within zip file downloaded from [2]<br>
[4] https://www.nongnu.org/avr-libc/user-manual/using_tools.html#using_avr_gcc_mach_opt<br>
[5] https://www.nongnu.org/avr-libc/user-manual/using_tools.html#using_sel_gcc_opts<br>

[6] https://tinusaur.com/guides/avr-gcc-toolchain/

[7] https://github.com/ZakKemble/AVRDUDESS/releases

[8] https://toastedcornflakes.github.io/articles/avr_getting_started.html

[9] https://gcc.gnu.org/onlinedocs/<br>
[10] https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wall<br>
[11] https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Overall-Options.html

[12] https://media.jaycar.com.au/product/resources/XC4627_manualMain_86841.pdf<br>
[13] https://media.jaycar.com.au/product/resources/XC4627_softwareMain_74679.zip

[14] https://ww1.microchip.com/downloads/en/DeviceDoc/doc2502.pdf	ATMega8535 datasheet

[15] https://zadig.akeo.ie/

