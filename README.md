# mbed_ES410_simpleSpeedMeasurement
ES410 Simple Speed Measurement

```C++
#include "mbed.h"
#include "MotCon.h"
#include "QEI.h"

QEI enc1(p24,p23,NC,800, QEI::X4_ENCODING); //Global Motor 800 cpr w x4 encoding
MotCon motor(p26, p28);       //pwm output, direction

int main() {
    long e[210];     // vector to save encoder readings
    int k;    
    
    motor.mot_control(0.5);   // sets motor voltage duty cucle, example  25% (12*0.25=3 V)
    
    for(k=1;k<=100;k++){ // take x=100 readings
        e[k]=enc1.getPulses();    // read the encoder
        wait(.050);   // wait x=50 ms between the readings         
    }
    motor.mot_control(0.0);
    for(k=1;k<=100;k++){   // print readings to screen so you can import to MATLAB
        printf("%d\r\n",e[k]);
    }    
}//main
```
