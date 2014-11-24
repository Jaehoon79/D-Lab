/**
  @page HID_Standalone USB Device Humain Interface (HID) example
  
  @verbatim
  ******************** (C) COPYRIGHT 2014 STMicroelectronics *******************
  * @file    USB_Device/HID_Standalone/readme.txt 
  * @author  MCD Application Team
  * @version V1.0.0
  * @date    18-June-2014
  * @brief   Description of the USB HID example.
  ******************************************************************************
  *
  * Licensed under MCD-ST Liberty SW License Agreement V2, (the "License");
  * You may not use this file except in compliance with the License.
  * You may obtain a copy of the License at:
  *
  *        http://www.st.com/software_license_agreement_liberty_v2
  *
  * Unless required by applicable law or agreed to in writing, software 
  * distributed under the License is distributed on an "AS IS" BASIS, 
  * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  * See the License for the specific language governing permissions and
  * limitations under the License.
  *
  ******************************************************************************
  @endverbatim

@par Example Description 

This example is a part of the USB Device Library package using STM32Cube firmware. It describes how to 
use USB device application based on the Humain Interface (HID) on the STM32f3xx devices.

This is a typical example on how to use the USB peripheral in Device mode with HID class V1.11 
following the "Device Class Definition for Human Interface Devices (HID) Version 1.11 
Jun 27, 2001". The example is built around the USB device library and emulate the Mouse directions 
using Joystick buttons mounted on the STM32373C-EVAL board.

This example supports the remote wakeup feature (the ability to bring the USB suspended bus back
to the active condition), and the Key button is used as the remote wakeup source. 
   
By default, in Windows OS, the USB mouse Power Management feature is turned off. This setting 
is different from classic PS/2 computer functionality. To enable the Wake up from  standby 
option, user has to manually turn on the Power Management feature for the USB mouse.

To enable the wake from standby option for the USB mouse, the following steps have to be followed: 
 - Start "Device Manager",
 - Select "Mice and other pointing devices",
 - Select the "HID-compliant mouse" device (make sure that PID &VID are equal to 0x5710 & 0x0483 respectively) 
 - Right click and select "Properties", 
 - Select "Power Management" tab,
 - Finally click to select "Allow this device to wake the computer" check box.

At the beginning of the main program the HAL_Init() function is called to reset all the peripherals,
initialize the Flash interface and the systick. The user is provided with the SystemClock_Config()
function to configure the system clock (SYSCLK) to run at 72 MHz. The Full Speed (FS) USB module uses
internally a 48-MHz clock, which is generated from an integrated PLL. 
 
It is possible to remappe the USB interrupts (USB_LP and USB_WKUP) on interrupt lines 75 and 76.
User can select USB line Interrupt through macro defined in main.h. 
(USE_USB_INTERRUPT_DEFAULT and USE_USB_INTERRUPT_REMAPPED)

@note The application needs to ensure that the SysTick time base is set to 1 millisecond
      to have correct HAL configuration.

@note To reduce the example footprint, the toolchain dynamic allocation is replaced by a static allocation
      by returning the address of a pre-defined static buffer with the HID class structure size. 
	  
@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in SysTick ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@par Directory contents

  - USB_Device/HID_Standalone/Src/main.c                  Main program
  - USB_Device/HID_Standalone/Src/system_stm32f3xx.c      STM32f3xx system clock configuration file
  - USB_Device/HID_Standalone/Src/stm32f3xx_it.c          Interrupt handlers
  - USB_Device/HID_Standalone/Src/usbd_conf.c             General low level driver configuration
  - USB_Device/HID_Standalone/Src/usbd_desc.c             USB device HID descriptor
  - USB_Device/HID_Standalone/Inc/main.h                  Main program header file
  - USB_Device/HID_Standalone/Inc/stm32f3xx_it.h          Interrupt handlers header file
  - USB_Device/HID_Standalone/Inc/stm32f3xx_hal_conf.h    HAL configuration file
  - USB_Device/HID_Standalone/Inc/usbd_conf.h             USB device driver Configuration file
  - USB_Device/HID_Standalone/Inc/usbd_desc.h             USB device MSC descriptor header file  

	
@par Hardware and Software environment

  - This example runs on STM32F373xx devices.
    
  - This example has been tested with STMicroelectronics STM32373C-EVAL
    evaluation boards and can be easily tailored to any other supported device 
    and development board.

  - STM32373C-EVAL Rev B Set-up
    - Connect the STM32373C-EVAL board to the PC through 'USB Type A-Male 
      to A-Male.
              
@par How to use it ?

In order to make the program work, you must do the following:
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example
 
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
  