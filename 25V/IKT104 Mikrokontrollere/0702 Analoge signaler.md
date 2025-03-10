Digital vs Analoge signaler
**Digital**, 1 eller på, bunn 0 eller av. 
Overfører bits. Eller skru noe av eller på.

**Analog**:
Sinuskurve, variabel spenning, -120v til + 120v f.eks. 0-3.3v hos oss. Sende ut alle verdiene mellom minimum og maksimum.

Digi
1 på 2.5 og opp.
Burde ikke ligge i mellom området siden man ikke vet hva man får.

Analoge er ikke like nøyaktige sånn sett.

Digital brukes for ren data.

Analog, vifte, sensorer, rotering, harddisk.  Ofte litt av begge deler
.
Analog krever ADC analog digital converter. 
0-1023
0 is 0v, 1023 is 3.3v

Analoge inputs sue cases.
Components
That have multiple steps
- turnable knobs (styre en motstand, helt åpen da kommer 3.3V, øke motstanden, spenningsfall)
- Levers
- Push buttons with depth sensing (R2).
Sensors:
Mikrophone
temperature sensor.
Humidity sensors
Light intensity Sensors.

**ADC** Kan ofte konfigurere oppløsning på den. ofte 10 eller 12 bit, for høyere og lavere nøyaktighet. Hastigheten avhenger av det. 
STM32L4xx er det 12-bit default. 0-4095. Microcontroller might have higher or lower internal resolution than the default. 

Analoge outputs - use cases
- Setting speed or intensity of another component. 
- LED brightness
- Screen brightness
- Motor speed, Motor kontroller Gir analog input, også styrer chippen motoroen.
![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdACt0k8t0vGKWZiA42eS4jED4plPGoPHZyqAEsf99hb8_aFLRP8JmAPhmTmIzEj7P73qDpIKt_qfUB34S8wymWFqCth6HiaMq_4mePT9RaHab1TWfpcVoSRMt7hI2zCIvQRFpa=s2048?key=L6Vc0XISLPY16DM8Cr22o9P2)
AnalogOut::write()
Sample ofte, høyere frekvenser, 44.1 KHz sampling kan du gjenskape halvparten. Opp tik 22KHz.

```cpp
#include "mbed.h"

  

#define WAIT_TIME_MS 1000

  

AnalogIn ain(A0, 3.3f); // PC_5

AnalogOut aout(PA_4); // PA_4

  

int main() {

  printf("ADC reference voltage %.1f\n", ain.get_reference_voltage());

  

  while (true) {

    printf("ADC value read %.1f, %u 12-bit converted to 16-bit, %.1f volt\n",

           ain.read(), ain.read_u16(), ain.read_voltage());

  

    printf("Set DAC output to %.1f volt\n", ain.read_voltage());

    aout.write(ain.read()); // Shorthand aout = ain;

  

    thread_sleep_for(WAIT_TIME_MS);

  }

}
```

### PWM
Pulse Width Modulation
- Not all microcontrollers have DAC, and those that do have few.
- PWM is a method of approximating an analoug output with digital signal. 
- Turn it on and off really fast, styre styrke.
- The % of on time is called the duty cycle
- o % duty is off, 100% is always on.
- Control speed of motors or brighness of LED.
![[firefox 2025.02.07 NeKxPqbYzbT.png]]
```cpp
#include "mbed.h"

  

#define WAIT_TIME_MS 1000

  

AnalogIn ain(A0, 3.3f); // PC_5

PwmOut pwm(D9); // PA_15

  

int main() {

  // Set PWM periode to 100Hz, i.e. 10 milliseconds

  pwm.period_ms(10 );

  

  printf("ADC reference voltage %.1f\n", ain.get_reference_voltage());

  

  while (true) {

    printf("ADC value read %.1f, %u 12-bit converted to 16-bit, %.1f volt\n",

           ain.read(), ain.read_u16(), ain.read_voltage());

  

    printf("Set PWM duty cycle to %d%%\n", (int)(ain.read() * 100));

    pwm.write(ain.read());// Shorthand pwm = ain; 
    // Glemt å gange med 100
  

    thread_sleep_for(WAIT_TIME_MS);

  }

}
```

0 -> 0%

range() -> 100%

range()/range()