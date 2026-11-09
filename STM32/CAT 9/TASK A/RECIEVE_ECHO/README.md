# EXPERIMENT DETAILS

**EXP:** CONTINUOUS ASSESSMENT 9

**DATE:** 28/09/2026

**NAME OF EXP:** STM32 UART Communication – Character Transmission and Echo

**HARDWARE SETUP / PLATFORM:** STM32CubeMX + Keil MDK + STM32 Development Board Blue Pill STM32F103C8T6

---

## TASK 9A – Basic UART Communication

### 1. Circuit Diagram

The experiment uses UART communication between the STM32 Blue Pill development board and a PC terminal.

- **Development Board:** STM32 Blue Pill
- **Microcontroller IC:** STM32F103C8T6
- **Peripheral:** USART2
- **UART TX Pin:** PA2
- **UART RX Pin:** PA3
- **Communication Interface:** USB-to-TTL Serial Converter
- **Baud Rate:** 115200 bps
- **Serial Configuration:** 8 Data Bits, No Parity, 1 Stop Bit (8N1)

The TX pin of the STM32 is connected to the RX pin of the USB-to-TTL converter, and the RX pin is connected to the TX pin. The GND pins are connected together to establish a common reference.

### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates UART serial communication using the STM32 HAL library. USART2 is configured using STM32CubeMX with a baud rate of 115200, 8-bit data, no parity, and 1 stop bit.

Two operations are performed:

**A. Transmit a Character:**

The STM32 continuously transmits the character `'t'` to the PC terminal using `HAL_UART_Transmit()`. A delay of 1 second is introduced between successive transmissions using `HAL_Delay(1000)`.

**B. Receive and Echo:**

The STM32 receives a character from the PC terminal using `HAL_UART_Receive()`. The received character is immediately transmitted back to the PC using `HAL_UART_Transmit()`, demonstrating echo communication.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO and USART2 peripherals.
4. Configure UART with a baud rate of 115200, 8 data bits, no parity, and 1 stop bit.
5. For character transmission:
   - Store the character `'t'` in a variable.
   - Transmit the character to the PC terminal.
   - Introduce a delay of 1 second.
   - Repeat continuously.
6. For character reception and echo:
   - Receive one character from the PC terminal.
   - Transmit the received character back to the PC.
   - Repeat continuously.

**Code Base:**

The UART communication operations are performed using the following STM32 HAL functions:

- `HAL_UART_Init()` – Initializes the USART2 peripheral.
- `HAL_UART_Transmit()` – Transmits a character to the PC.
- `HAL_UART_Receive()` – Receives a character from the PC.
- `HAL_Delay()` – Introduces a delay between transmissions.

### 3. Inference

UART communication between the STM32 Blue Pill board and the PC terminal is successfully demonstrated. The STM32 continuously transmits the character `'t'` at one-second intervals, and in the receive-and-echo operation, every character entered in the PC terminal is received and transmitted back by the STM32.

Thus, the experiment demonstrates basic serial communication, character transmission, character reception, and echo functionality using the STM32 HAL library.
