# INTERFACING-OF-STEPPER-MOTOR-WITH-ARM-PROCESSOR.
### Name : Mathan Kailash S
### Reg No : 212223060156
### Slot : 4x4-5
## AIM:
  To write an embedded c program to interface STEPPER MOTOR with ARM processor LPC1768.
 
## COMPONENTS REQUIRED:

### HARDWARE:
ARM LPC 1768 STEPPER MOTOR.
### SOFTWARE:
KEIL MICRO VISION 4.0 IDE

## PROCEDURE:

~~~
⮚	Open the Keil software and select the New uvision project from Project Menu as shown below.
⮚	Browse to your project folder and provide the project name and click on save.
⮚	Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK.
⮚	Select the controller (NXP: LPC1768) and click on OK.
⮚	As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.
⮚	Create a new file by file → new to write the program.
⮚	Type the code.
⮚	After typing the code save the file as main.c eg. (abc.c).
⮚	Right click target and Add the suitable files to source group1 and header for the project.
⮚	Add the main.c along with system_LPC17xx.c.
⮚	Build the project and fix the compiler errors/warnings if any.
⮚	Code is compiled with no errors. The .bin file is still not generated.
⮚	Right Click on Target Options to select the option for generating .bin file.
⮚	Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000- 0x2000 so application should start from 0x2000
⮚	Write	the	command	to	generate	the .bin file	from
.axf file
Command: fromelf --bin projectname.axf --output filename.bin
⮚	in c/c++ → include paths → desktop (00-libfiles).
⮚	.Bin file is generated after a rebuild.
⮚	Check the project folder for the generated .Bin file.
~~~

## ADD FILES:

### Target1:
Source group1:
Startuplpc17xx.s, main.c (t), delay.c (t), systemlpc17xx.c (t), gpio.c (t)
### Header:
Delay.h, stdutils.h, gpioi.h

## PIN DIAGRAM:
<img width="299" height="194" alt="image" src="https://github.com/user-attachments/assets/e75f377a-2bbc-4f20-a95e-a460c6abe028" />

~~~
P1[26]/MC1B/PWM1[6]/CAP0[0] 4
I/O P1[26] — General purpose digital input/output pin.
O MC1B	— Motor control PWM channel 1, output B.
O PWM1[6] — Pulse Width Modulator 1, channel 6 output.
I CAP0[0]	— Capture input for Timer 0, channel 0.
P1[27]/CLKOUT/USB_OVRCR/CAP0[1] 43[1]
I/O P1[27]	— General purpose digital input/output pin. O CLKOUT		— Clock output pin.
I USB_OVRCR — USB port Over-Current status.
(LPC1768/66/65 only).
I CAP0[1]	— Capture input for Timer 0, channel 1.
P1[20]/MCFB0/PWM1[2]/SCK034[1]
I/O P1[20]	— General purpose digital input/output pin.
I MCFB0	— Motor control PWM channel 0, feedback input. Also Quadrature Encoder Interface PHA input.
O PWM1[2]	— Pulse Width Modulator 1, channel 2 output. I/O SCK0	—  Serial clock for SSP0.
P1[21]/MCABORT/PWM1[3]/SSEL035[1]
I/O P1[21]	— General purpose digital input/output pin.
O MCABORT		— Motor control PWM, emergency abort.  PWM1[3]	— Pulse Width Modulator 1, channel 3 output.
I/O SSEL0	— Slave Select for SSP0.
P1[22]/MC0B/USB_PWRD/MAT1[0]36[1]
I/O P1[22]	— General purpose digital input/output pin. O MC0B	— Motor control PWM channel 0, output B.
I USB_PWRD — Power Status for USB port (host power switch, LPC1768/66/65 only).
O MAT1[0]	— Match output for Timer 1, channel 0.
P1[23]/MCFB1/PWM1[4]/MISO037[1]
I/O P1[23]	— General purpose digital input/output pin.
I MCFB1	— Motor control PWM channel 1, feedback input. Also Quadrature Encoder Interface PHB input.
O PWM1[4]	— Pulse Width Modulator 1, channel 4 output. I/O MISO0		— Master In Slave Out for SSP0.
~~~

## CIRCUIT DIAGRAM:
<img width="330" height="289" alt="image" src="https://github.com/user-attachments/assets/ff371b15-6c32-4016-855e-c70f658e2d5c" />

## PROGRAM:
~~~
#include<lpc17xx.h> #include "gpio.h" #define pin1 20
#define pin2 21
#define pin3 22
#define pin4 23
#define control LPC_GPIO1-
>FIOPIN
void cmotor1()
{
control |=(1<<pin1); control |=(1<<pin2); control &=~(1<<pin3); control &=~(1<<pin4);
}
void cmotor2()
{
control &=~(1<<pin1); control |=(1<<pin2); control |=(1<<pin3); control &=~(1<<pin4);
}
void cmotor3()
{
control &=~(1<<pin1); control &=~(1<<pin2); control |=(1<<pin3); control |=(1<<pin4);
 }
void cmotor4()
{
control |=(1<<pin1); control &=~(1<<pin2); control &=~(1<<pin3); control |=(1<<pin4);
}
void delay_ms(unsigned int ms)
{
unsigned int i,j;
for(i=0;i<ms;i++) for(j=0;j<20000;j++);
}
int main()
{
SystemInit();
//Clock and PLL configuration LPC_PINCON->PINSEL3 = 0x000000;
LPC_GPIO1->FIODIR
=(1<<pin1)|(1<<pin2)|(1<<pin3)
| (1<<pin4); while(1)
{
cmotor1(); delay_ms(50); cmotor2();
delay_ms(50);
cmotor3();
delay_ms(50);
cmotor4();
delay_ms(50);
}
}
~~~

## OUTPUT:
![WhatsApp Image 2025-11-11 at 21 11 25_1c0c5534](https://github.com/user-attachments/assets/98b7e3ea-2f3d-46a0-9c35-71e363bc9ebd)


## RESULT: 
  Thus interfacing STEPPER MOTOR with ARM processor LPC1768 is verified
