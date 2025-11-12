AUTOMATIC-LED-CONTROL-IR-SENSOR
AIM
To design and implement a system using the STM32 microcontroller where an LED automatically turns ON or OFF based on the input from an IR sensor.

Components Required
STM32 Nucleo or Discovery Board (e.g., Nucleo-G071RB)
IR Sensor Module
LED (5mm Green or any color)
Jumper wires
Breadboard
Theory
An IR sensor detects the presence of an object by emitting and receiving infrared light.

IR Sensor Behavior
When an object is detected, the IR sensor output goes LOW (0V).
When no object is detected, the output stays HIGH (3.3V).
Microcontroller Response
If IR output = LOW → LED ON
If IR output = HIGH → LED OFF
Procedure
Open STM32CubeIDE. image

Click File → New STM32 Project. image

image
Select the target microcontroller or board and click Next. image

Name the project. image

The corresponding .ioc file will be generated automatically.

image
Configure the pins as GPIO (Input/Output), USART, etc. as needed. image
image
Save the configuration (Ctrl + S) – the base C program will be generated automatically. image

Edit the generated main program as required. image

image
Click Project → Build All. image

Link the HEX file using the post-build process. image

Click Debug and connect the STM Nucleo Board. image

Click Run to execute the program.

💻 Program
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
OUTPUT
CASE 1: LED ON image CASE 2: LED OFF image
RESULT
The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.

