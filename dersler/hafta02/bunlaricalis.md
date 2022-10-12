# Çalış

 1. Bir while döngüsünde ilk önde red, sonra blue ve ardından green ledlerini sırasıyla sonsuza kadar yak söndür.
 2. İlk adımı bu sefer for döngüsünde yap.
``` 
#include <stdint.h>
#include <stdbool.h>
#include "inc/hw_types.h"
#include "inc/hw_gpio.h"
#include "driverlib/pin_map.h"
#include "driverlib/sysctl.h"
#include "driverlib/gpio.h"
#include "driverlib/gpio.c"
#include "inc/hw_memmap.h"
#include "math.h"
```
 3. Aşağıdaki döngüleri tamamla
```
void main(void)
{
    //ilk ayarlar
    SetInitSettings();

    while(1) // ana döngü
    {
        // kirmizi ledi 20 kez yakan dongu
        // mavi ledi 10 kez yakan dongu
        // yesil ledi 15 kez yakan dongu
    }
}

void SetInitSettings()
{
    SysCtlClockSet(SYSCTL_SYSDIV_5|SYSCTL_USE_PLL|SYSCTL_XTAL_16MHZ|SYSCTL_OSC_MAIN);
    SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);
    GPIOPinTypeGPIOOutput(GPIO_PORTF_BASE,GPIO_PIN_1|GPIO_PIN_2|GPIO_PIN_3); // pin 123 output
}
```

 4. Aşağıdaki fonksiyonları tamamla
```
 #include "math.h"
//.......
void kirmizilediyaksondur(int deger){
    // gelen deger kadar ledi yak sondur
}

void mavilediyaksondur(int deger){
    // gelen deger kadar ledi yak sondur
}

void yesillediyaksondur(int deger){
    // gelen deger kadar ledi yak sondur
}

void main(void)
{
    //ilk ayarlar
    SetInitSettings();

    while(1) // ana döngü
    {
        kirmizilediyaksondur(20);
        mavilediyaksondur(10);
        yesillediyaksondur(15);
    }
}
```

 5. Aşağıdaki döngüleri tamamla
```
void lediyaksondur(int pin,int deger){
    // gelen pini, deger kadar ledi yak sondur
}


int ilkSayi=0;

void main(void)
{
    //ilk ayarlar
    SetInitSettings();

    while(1) // ana döngü
    {
        lediyaksondur(2,20); //kirmizi
        lediyaksondur(4,10); //mavi
        lediyaksondur(8,15); //yesil
    }
}
```
 5. Aşağıdaki döngüleri tamamla
```
void lediyaksondur(int pin,int deger){
    // gelen pini, deger kadar ledi yak sondur
}


int ilkSayi=0;

void main(void)
{
    //ilk ayarlar
    SetInitSettings();

    while(1) // ana döngü
    {
        lediyaksondur(1,20); //pin1,20kez
        lediyaksondur(2,10); //pin2,10kez
        lediyaksondur(3,15); //pin3,15kez
    }
}
```

 
