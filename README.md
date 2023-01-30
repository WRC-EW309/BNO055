# BNO055
Repository for BNO055 IMU customized for EW309



#include "mbed.h"
#include "BNO055/BNO055.h"

// Blinking rate in milliseconds
#define BLINKING_RATE     50ms

// Create BNO055 object with I2C (SDA,SCL) pins
BNO055 imu(D0,D1);

int main()
{
    // Initialise the digital pin LED1 as an output
    DigitalOut led(LED1);
    imu.setmode(OPERATION_MODE_IMUPLUS); //Set Mode to IMU with relative Heading
    imu.set_angle_units(RADIANS); // Set Angle Units to radians
    imu.set_anglerate_units(RAD_PER_SEC); //Set Gyro units to rad/s
    
    while (true) {
        led = !led;
        imu.get_angles();
        imu.get_gyro();
        printf("%f,%f,%f,%f,%f,%f\n\r",imu.euler.pitch,imu.euler.yaw,imu.gyro.y,imu.gyro.z);
        ThisThread::sleep_for(BLINKING_RATE);
    }
}
