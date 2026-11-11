# EXPERIMENT DETAILS

**EXP:** CONTINUOUS ASSESSMENT 9

**DATE:** 28/09/2026

**NAME OF EXP:** STM32 UART Character Reception and Echo

**HARDWARE SETUP / PLATFORM:** STM32CubeMX + Keil MDK + STM32 Development Board Blue Pill STM32F103C8T6

---

## TASK 9A – UART Character Reception and Echo

### 1. Circuit Diagram

The experiment uses UART communication between the STM32 Blue Pill development board and a PC terminal.

- **Development Board:** STM32 Blue Pill
- **Microcontroller IC:** STM32F103C8T6
- **UART Peripheral:** USART2
- **UART TX Pin:** PA2
- **UART RX Pin:** PA3
- **Communication Interface:** USB-to-TTL Serial Converter
- **Baud Rate:** 115200 bps

The TX pin of the USB-to-TTL converter is connected to the RX pin of the STM32, and the RX pin of the converter is connected to the TX pin of the STM32. Both devices share a common GND connection.
![alt text](<CIRCUIT DIAGRAM-1.png>)
### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates UART character reception and echo communication using the STM32 HAL library. USART2 is configured with a baud rate of 115200, 8 data bits, no parity, and 1 stop bit.

A character is received from the PC terminal using `HAL_UART_Receive()`. The received character is then immediately transmitted back to the PC terminal using `HAL_UART_Transmit()`. This process is repeated continuously.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO and USART2 peripherals.
4. Configure UART with 115200 baud rate and 8N1 configuration.
5. Declare a variable to store the received character.
6. Receive one character from the PC terminal.
7. Transmit the received character back to the PC terminal.
8. Repeat the process continuously.

**Code Base:**

The UART communication is performed using the following STM32 HAL functions:

- `HAL_UART_Init()` – Initializes USART2.
- `HAL_UART_Receive()` – Receives a character from the PC terminal.
- `HAL_UART_Transmit()` – Sends the received character back to the PC terminal.

### 3. Inference

The STM32 Blue Pill successfully receives characters entered through the PC terminal and transmits the same characters back. This demonstrates UART data reception, transmission, and echo communication using STM32 HAL functions.
