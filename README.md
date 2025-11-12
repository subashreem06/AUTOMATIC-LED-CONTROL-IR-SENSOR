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
1.Open STM32CubeIDE. 
<img width="1050" height="591" alt="image" src="https://github.com/user-attachments/assets/d38b1d48-eb07-476c-a86e-76cccfcb06aa" />

2.Click File → New STM32 Project.
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/bc1874da-52c8-4714-918a-0e4db4aba25c" />
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/041ab692-a5bf-4b74-9f85-19600cf4dde2" />

3.Select the target microcontroller or board and click Next.
<img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/453470ba-5924-43b4-9da8-a16c8109c357" />
<img width="533" height="588" alt="image" src="https://github.com/user-attachments/assets/3fb0f9cc-84c7-4479-bbf6-5c6738738fdb" />




4.Name the project. 

5.The corresponding .ioc file will be generated automatically.
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/d3a8fbca-de2d-401f-b914-32c6cdd9f6ca" />
<img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/b845a742-0676-4a53-bd6d-67bfc503ced9" />



6.Configure the pins as GPIO (Input/Output), USART, etc. as needed.
<img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/84d00a29-5036-4bcc-a6c6-a3d1222ba5b9" />
<img width="1104" height="621" alt="image" src="https://github.com/user-attachments/assets/bbabca10-64d4-44d8-8f41-5f6db765bddc" />


7.Save the configuration (Ctrl + S) – the base C program will be generated automatically. 
<img width="1053" height="465" alt="image" src="https://github.com/user-attachments/assets/d3c3993d-36d0-45cd-9515-19620edc4163" />


8.Edit the generated main program as required.
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/86a6fa47-7f88-4bcc-9a9d-a91f02e84e74" />
<img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/a1f0593b-1606-4f6e-9355-b353cb23b70c" />
9.Click Project → Build All.
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/c80997e1-385f-4362-acc4-a93d50281988" />

10.Link the HEX file using the post-build process.
![Uploading image.png…]()


11.Click Debug and connect the STM Nucleo Board. 
![Uploading image.png…]()


12.Click Run to execute the program.

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

