# Button Interrupt
## Objective
The objective of this lab was to use interrupts to implement the toggle of an LED with the input of a button, as opposed 
to using Polling in Lab 2
### How
First, the LED is initialized as an output with pull up and pull down resistors so that it may be toggled with a push of a
button. The button is still initialized as an input, similar as to Lab 2, but we also need to enable the interupt of 
the button by using the code P1IE |=BIT1;. Further we need to set the button as falling edge using the code P1IES |=BIT1
and finally we must clear the interrupt flag of the button utilizing the code P1IFG &=~(BIT1);

The major difference between toggling the LED with a button in Lab 2 as compared to now comes in the form of the 
pragma vector interrupt that is placed underneath all of the initializations and below the main section. Interrupts also 
allow us to enable low power mode which is done here as well using "_BIS_SR(LPMx + GIE)". The GIE part of the 
code enables interrupts. The interrupt occurs upon the press of a button and then the code inside the pragma vector is 
executed.

### Board Differences
Pins all change of course, but the line of code "PM5CTL0 &= ~LOCKLPM5;"is required in order to disable the 
GPIO power-on default high-impedance mode for the 2311 and 6989.