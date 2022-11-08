# Hafta 05

 1. Dersteki ana kod!!
 ``` 
 #include <stdint.h>
#include <stdbool.h>
#include "inc/hw_types.h"
#include "inc/hw_memmap.h"
#include "inc/hw_ints.h"
#include "driverlib/sysctl.h"
#include "driverlib/gpio.h"
#include "inc/hw_gpio.h"
#include "driverlib/sysctl.c"
#include "driverlib/timer.h"
#include "driverlib/interrupt.h"

//int a=2;

int sn,dk,sa;

void timerkesmefonk(void){
    //a=~a;
    //GPIOPinWrite(GPIO_PORTF_BASE, 2, a);
    //GPIOPinWrite(GPIO_PORTF_BASE, 2, ~GPIOPinRead(GPIO_PORTF_BASE, 2));
    sn++;
    if(sn==60){
        sn=0;
        dk++;
        if(dk==60){
            dk=0;
            sa++;
            if(sa==24){
                sa=0;
            }
        }
    }
    TimerIntClear(TIMER0_BASE, TIMER_TIMA_TIMEOUT);
}
int main(void)
{
        sn=0; dk=0; sa=0;
        SysCtlClockSet(SYSCTL_SYSDIV_5|SYSCTL_USE_PLL|SYSCTL_XTAL_16MHZ|SYSCTL_OSC_MAIN); // 40mhz
        long a=SysCtlClockGet();
        SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);
        SysCtlPeripheralEnable(SYSCTL_PERIPH_TIMER0);

        GPIOPinTypeGPIOOutput(GPIO_PORTF_BASE, 14);

        IntMasterEnable();// setb ea
        IntEnable(INT_TIMER0A);

        TimerConfigure(TIMER0_BASE, TIMER_CFG_PERIODIC);// asagi sayici
        TimerLoadSet(TIMER0_BASE, TIMER_A,400000-1);// ilk degeri girdikk

        TimerIntEnable(TIMER0_BASE, TIMER_TIMA_TIMEOUT);//0daneksi1 olunca
        TimerIntRegister(TIMER0_BASE, TIMER_A, timerkesmefonk);
        TimerEnable(TIMER0_BASE, TIMER_A);//setb tr0

        while(1);


}
```

