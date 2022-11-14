# Hafta 06

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
#include "driverlib/adc.h"


int main(void)
 {

        SysCtlClockSet(SYSCTL_SYSDIV_5|SYSCTL_USE_PLL|SYSCTL_XTAL_16MHZ|SYSCTL_OSC_MAIN); // 40mhz
        long a=SysCtlClockGet();
        SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);
        SysCtlPeripheralEnable(SYSCTL_PERIPH_TIMER0);
        SysCtlPeripheralEnable(SYSCTL_PERIPH_ADC0);


        ADCSequenceConfigure(ADC0_BASE, 2, ADC_TRIGGER_PROCESSOR, 0);// seq 2 kullanilacak
        ADCSequenceStepConfigure(ADC0_BASE, 2, 0, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 1, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 2, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 3, ADC_CTL_TS|ADC_CTL_IE|ADC_CTL_END);
        ADCSequenceEnable(ADC0_BASE, 2);

        uint32_t gelendeger[4];
        long ort,temp;
        while(1){
            ADCProcessorTrigger(ADC0_BASE, 2); // CEVRIM BASLADI
            while(!ADCIntStatus(ADC0_BASE, 2, false)){}
            ADCSequenceDataGet(ADC0_BASE, 2, gelendeger);
            ort=(gelendeger[0]+gelendeger[1]+gelendeger[2]+gelendeger[3])/4;
            temp=(1475-((2475*ort)/4096))/10;
            ADCIntClear(ADC0_BASE, 2);
        }


}

```

2. Dersteki ana kod!!
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
#include "driverlib/adc.h"


uint32_t gelendeger[4];
long ort,temp;

void adckesme(){
    ADCSequenceDataGet(ADC0_BASE, 2, gelendeger);
    ort=(gelendeger[0]+gelendeger[1]+gelendeger[2]+gelendeger[3])/4;
    ADCIntClear(ADC0_BASE, 2);
    ADCProcessorTrigger(ADC0_BASE, 2);
}




int main(void)
 {
        SysCtlClockSet(SYSCTL_SYSDIV_5|SYSCTL_USE_PLL|SYSCTL_XTAL_16MHZ|SYSCTL_OSC_MAIN); // 40mhz
        long a=SysCtlClockGet();
        SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);
        SysCtlPeripheralEnable(SYSCTL_PERIPH_TIMER0);
        SysCtlPeripheralEnable(SYSCTL_PERIPH_ADC0);

        IntMasterEnable();
        IntEnable(INT_ADC0SS2);

        ADCSequenceConfigure(ADC0_BASE, 2, ADC_TRIGGER_PROCESSOR, 0);// seq 2 kullanilacak
        ADCSequenceStepConfigure(ADC0_BASE, 2, 0, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 1, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 2, ADC_CTL_TS);
        ADCSequenceStepConfigure(ADC0_BASE, 2, 3, ADC_CTL_TS|ADC_CTL_IE|ADC_CTL_END);
        ADCIntClear(ADC0_BASE, 2);
        ADCIntRegister(ADC0_BASE, 2, adckesme);
        ADCIntEnable(ADC0_BASE, 2);


        ADCSequenceEnable(ADC0_BASE, 2);

        ADCProcessorTrigger(ADC0_BASE, 2); // CEVRIM BASLADI

        while(1){

        }


}

```

