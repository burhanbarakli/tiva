# Hafta 03

 1. Dersin videosu [Tıkla1](https://www.youtube.com/watch?v=rH7ts8izUqk&list=PL-eKWUr5h4myBzqmyVgmhaZztvl7gbR4E&index=5)
 2. Dersteki ana kod!!
 ``` #include <stdint.h>
#include <stdbool.h>
#include "inc/hw_types.h"
#include "inc/hw_gpio.h"
#include "driverlib/pin_map.h"
#include "driverlib/sysctl.h"
#include "driverlib/gpio.h"
#include "inc/hw_memmap.h"

void SetInitSettings();

void main(void)
{
    //ilk ayarlar
    SetInitSettings();

    int sayac=0;

    while(1) // ana döngü
    {
        int a=GPIOPinRead(GPIO_PORTF_BASE,GPIO_PIN_4|GPIO_PIN_0);

        if (GPIOPinRead(GPIO_PORTF_BASE,GPIO_PIN_4|GPIO_PIN_0)==0)
        {
            while(GPIOPinRead(GPIO_PORTF_BASE,GPIO_PIN_4|GPIO_PIN_0)==0){}
            SysCtlDelay(1000000);
            GPIOPinWrite(GPIO_PORTF_BASE, GPIO_PIN_1, GPIO_PIN_1);
            GPIOPinWrite(GPIO_PORTF_BASE, GPIO_PIN_2, 0);
        }

        else if (GPIOPinRead(GPIO_PORTF_BASE,GPIO_PIN_4|GPIO_PIN_0)==0)
        {
            while(GPIOPinRead(GPIO_PORTF_BASE,GPIO_PIN_4|GPIO_PIN_0)==0){}
            SysCtlDelay(1000000);
            GPIOPinWrite(GPIO_PORTF_BASE, GPIO_PIN_2, GPIO_PIN_2);
            GPIOPinWrite(GPIO_PORTF_BASE, GPIO_PIN_1, 0);
        }
    }
}


void SetInitSettings()
{
    long aaaaa=SysCtlClockGet();
    SysCtlClockSet(SYSCTL_SYSDIV_5|SYSCTL_USE_PLL|SYSCTL_XTAL_16MHZ|SYSCTL_OSC_MAIN);
    SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);

    HWREG(GPIO_PORTF_BASE + GPIO_O_LOCK) = GPIO_LOCK_KEY;
    HWREG(GPIO_PORTF_BASE + GPIO_O_CR) |= 0x01;

    GPIOPinTypeGPIOOutput(GPIO_PORTF_BASE,GPIO_PIN_1|GPIO_PIN_2|GPIO_PIN_3);
    GPIOPinTypeGPIOInput(GPIO_PORTF_BASE,GPIO_PIN_4 | GPIO_PIN_0);
    GPIOPadConfigSet(GPIO_PORTF_BASE, GPIO_PIN_4| GPIO_PIN_0, GPIO_STRENGTH_8MA, GPIO_PIN_TYPE_STD_WPU);
}
```

 3. 
 ![Fonksiyonlarin ve parametreler nerden geliyor](https://i.imgur.com/2EUgdqy.jpg)
 
 4. 
 ![enter image description here](https://i.imgur.com/ed4yzDD.png)
