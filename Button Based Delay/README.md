# Button Based Delay
## Objective
The objective of this lab was to use the Timer A peripheral and interrupts to enable a user to control the duration of the 
delay (time when LED is spent off during blinking) by holding down the button.
### How
First, the LED is initialized as an output with pull up and pull down resistors so that it may be toggled with a push of a
button. The button is still initialized as an input, similar as to Lab 2, but we also need to enable the interupt of 
the button by using the code P1IE |=BIT1;. Further we need to set the button as falling edge using the code P1IES |=BIT1
and finally we must clear the interrupt flag of the button utilizing the code P1IFG &=~(BIT1);

Then, Timer A was initialized by the code "TA0CTL = TASSELx + MC_x;" (x being 0,1,or2). The value of x determines 
whether the counter is in up mode, continous mode, or up/down mode. Variable x also specifies which clock is being 
used, whether it be ACLK, SMCLK or MCLK. TA0CCTL0 sets the mode to either capture or compare if up or up/down
is used. TA0CCR0 is the period of the counter and sets the speed of the blink because the frequency of the blink is 
determined by the speed of the clock/TA0CCR0.

Further, an interrupt is innitialized and an if else statment is written to determine what to do when the user is interacting
with the button. When the button is pressed we set the Timer to count up using "MC_2". We also set this to capture mode 
using "TA1CCTL0 = CAP;". An else if statement is used when the button is on the rising edge as well. We then set the 
TA0CCR0 equal to the value we obtained from TA1CCR0 in order to achieve the users input. In addition to this an 
additional function is used to calculate the number of cycles need to provide a 10Hz starting frequency.

### Board Differences
Pins all change of course, but the line of code "PM5CTL0 &= ~LOCKLPM5;"is required in order to disable the GPIO 
power-on default high-impedance mode for the 2311 and 6989. The 2311 has no TimerA so TimerB was used for that 
implementation. 