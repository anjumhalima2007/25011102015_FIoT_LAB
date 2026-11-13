# EXPERIMENT DETAILS

**EXP:** CONTINUOUS ASSESSMENT 9

**DATE:** 28/09/2026

**NAME OF EXP:** STM32 UART Character Transmission

**HARDWARE SETUP / PLATFORM:** STM32CubeMX + Keil MDK + STM32 Development Board Blue Pill STM32F103C8T6

---

## TASK 9A – UART Character Transmission

### 1. Circuit Diagram

The experiment uses UART communication between the STM32 Blue Pill development board and a PC terminal.

- **Development Board:** STM32 Blue Pill
- **Microcontroller IC:** STM32F103C8T6
- **UART Peripheral:** USART2
- **UART TX Pin:** PA2
- **Communication Interface:** USB-to-TTL Serial Converter
- **Baud Rate:** 115200 bps

The TX pin of the STM32 is connected to the RX pin of the USB-to-TTL converter, with a common GND connection.
![alt text](<circuit.png>)
### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates UART character transmission using the STM32 HAL library. USART2 is configured with a baud rate of 115200, 8 data bits, no parity, and 1 stop bit.

The character `'t'` is stored in a variable and continuously transmitted to the PC terminal using `HAL_UART_Transmit()`. A delay of 1 second is introduced between successive transmissions using `HAL_Delay(1000)`.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO and USART2 peripherals.
4. Configure UART with 115200 baud rate and 8N1 configuration.
5. Store the character `'t'` in a variable.
6. Transmit the character to the PC terminal.
7. Introduce a delay of 1 second.
8. Repeat the transmission continuously.

**Code Base:**

The UART transmission is performed using the following STM32 HAL functions:

- `HAL_UART_Init()` – Initializes USART2.
- `HAL_UART_Transmit()` – Transmits the character to the PC terminal.
- `HAL_Delay()` – Introduces a delay between transmissions.

### 3. Inference

The STM32 Blue Pill successfully transmits the character `'t'` continuously to the PC terminal at one-second intervals. This demonstrates UART initialization and character transmission using STM32 HAL functions.
