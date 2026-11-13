# EXPERIMENT DETAILS

**EXP:** CONTINUOUS LAB EVALUATION 7

**DATE:** 24/08/2026 (Week 6)

**NAME OF EXP:** 16×2 LCD Driver Development and Dynamic Display Control

**HARDWARE SETUP / PLATFORM:** Keil MDK + 8051 Development Board (AT89S52) + 16×2 Character LCD + Hardware Debugger

---

## TASK 7A – LCD Initialization and Character/String Display

### 1. Circuit Diagram

The experiment demonstrates interfacing a 16×2 character LCD with the AT89S52 microcontroller using a 4-bit GPIO-based communication interface. An embedded C LCD driver is developed to initialize the LCD, send commands, transmit character data, and display strings.

- **Development Board:** 8051 Development Board
- **Microcontroller IC:** AT89S52
- **Display Device:** 16×2 Character LCD (HD44780 Compatible)
- **Communication Interface:** 4-bit GPIO-based interface
- **LCD Data Port:** Port 3 (P3.4–P3.7)
- **Register Select Pin (RS):** P3.2
- **Enable Pin (E):** P3.3

**Connections:**

| LCD Pin | AT89S52 Pin   | Description                      |
| ------- | ------------- | -------------------------------- |
| D4      | P3.4          | Data bit 4                       |
| D5      | P3.5          | Data bit 5                       |
| D6      | P3.6          | Data bit 6                       |
| D7      | P3.7          | Data bit 7                       |
| RS      | P3.2          | Selects command or data register |
| E       | P3.3          | Enable signal for LCD            |
| RW      | GND           | Selects write operation          |
| VSS     | GND           | Ground connection                |
| VDD     | +5V           | LCD power supply                 |
| V0      | Potentiometer | LCD contrast adjustment          |

**Working Configuration:**

- The LCD is configured in 4-bit communication mode.
- The display operates in 2-line mode with 5×8 character font.
- P3.4–P3.7 are used for transmitting data and commands.
- P3.2 is configured as the Register Select (RS) control signal.
- P3.3 is configured as the Enable (E) control signal.
- The RW pin is connected to GND to enable write-only operation.
- The LCD is initialized using the function set, display control, entry mode, and clear display commands.
![alt text](<circuit.png>)
### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates interfacing a 16×2 LCD with the AT89S52 microcontroller using a 4-bit GPIO-based communication method.

The LCD data pins D4–D7 are connected to Port 3 pins P3.4–P3.7. The RS and Enable control pins are connected to P3.2 and P3.3, respectively.

Initially, the microcontroller waits for 20 ms to allow the LCD to stabilize after power-up. The LCD is then initialized in 4-bit mode using the command `0x20`.

The function `lcd_cmd()` is used to transmit LCD instructions. It sets RS to LOW, indicating command mode, and sends the higher and lower nibbles of the command separately.

The function `lcd_data()` is used to transmit individual characters to the LCD. It sets RS to HIGH, indicating data mode, and sends the character in two 4-bit portions.

The function `lcd_send_nibble()` transfers the upper four bits of the given value to Port 3 pins P3.4–P3.7 while preserving the lower four port bits. The Enable signal is generated using the `lcd_enable()` function to latch the transmitted nibble into the LCD.

The LCD is configured using the following commands:

- `0x28` – Configures the LCD in 4-bit mode, 2-line display, and 5×8 font.
- `0x0C` – Turns ON the display and turns OFF the cursor.
- `0x06` – Configures the entry mode to increment the cursor position automatically.
- `0x01` – Clears the display.

After initialization, the microcontroller continuously transmits the characters of the string **"HELLO FROM 8051"** using the `lcd_data()` function.

After transmitting the characters and additional spaces, the display is cleared using `lcd_cmd(0x01)`, and the process repeats continuously.

**Pseudocode:**

1. Include the 8051 microcontroller header file `reg51.h`.
2. Define Port 3 as the LCD data port.
3. Assign P3.2 as the RS control pin.
4. Assign P3.3 as the Enable control pin.
5. Implement a delay function using nested loops.
6. Implement the `lcd_enable()` function to generate the Enable pulse.
7. Implement the `lcd_send_nibble()` function to transmit 4-bit data.
8. Implement the `lcd_cmd()` function to send LCD commands:
   - Set RS = 0.
   - Send the higher nibble.
   - Send the lower nibble.
9. Implement the `lcd_data()` function to transmit characters:
   - Set RS = 1.
   - Send the higher nibble.
   - Send the lower nibble.
10. Implement the `lcd_init()` function to initialize the LCD:
    - Wait for 20 ms.
    - Configure 4-bit mode.
    - Configure 2-line display.
    - Turn ON the display.
    - Configure automatic cursor increment.
    - Clear the display.
11. Call `lcd_init()` from the `main()` function.
12. Enter the infinite loop.
13. Display the characters of the string "HELLO FROM 8051" using `lcd_data()`.
14. Clear the LCD using `lcd_cmd(0x01)`.
15. Repeat the process continuously.

**Code Base:**

The LCD interfacing is implemented using the following Embedded C functions:

- `delay_ms()` – Generates the required time delay for LCD initialization and data transmission.
- `lcd_enable()` – Generates the Enable pulse to latch commands and data into the LCD.
- `lcd_send_nibble()` – Sends a 4-bit data or command nibble through Port 3.
- `lcd_cmd()` – Sends LCD control commands by transmitting higher and lower nibbles.
- `lcd_data()` – Sends individual character data to the LCD.
- `lcd_init()` – Initializes the LCD in 4-bit, 2-line mode.
- `main()` – Performs LCD initialization and continuously displays the predefined character sequence.

**LCD Control Signals:**

| Control Signal | Microcontroller Pin | Function                       |
| -------------- | ------------------- | ------------------------------ |
| RS             | P3.2                | LOW = Command, HIGH = Data     |
| E              | P3.3                | Enable pulse for data transfer |
| RW             | GND                 | Write operation                |
| D4             | P3.4                | Data bit 4                     |
| D5             | P3.5                | Data bit 5                     |
| D6             | P3.6                | Data bit 6                     |
| D7             | P3.7                | Data bit 7                     |

**LCD Command Configuration:**

| Command             | Hexadecimal Value | Function                             |
| ------------------- | ----------------- | ------------------------------------ |
| Function Set        | `0x28`            | 4-bit mode, 2-line display, 5×8 font |
| Display ON/OFF      | `0x0C`            | Display ON, cursor OFF               |
| Entry Mode Set      | `0x06`            | Automatic cursor increment           |
| Clear Display       | `0x01`            | Clears the LCD display               |
| Initial 4-bit Setup | `0x20`            | Selects 4-bit interface              |

**LCD Driver Functions:**

| Function            | Description                    |
| ------------------- | ------------------------------ |
| `delay_ms()`        | Generates software delays      |
| `lcd_enable()`      | Generates the LCD Enable pulse |
| `lcd_send_nibble()` | Sends 4-bit data               |
| `lcd_cmd()`         | Transmits LCD commands         |
| `lcd_data()`        | Transmits character data       |
| `lcd_init()`        | Initializes the LCD            |

**Expected Output:**

The 16×2 LCD should display the following message:

```text
HELLO FROM 8051
```

The program continuously transmits the characters using the 4-bit interface and clears the display after completing the transmission.

The LCD should operate in 4-bit mode with automatic cursor increment and display control enabled.



### 3. Inference

The AT89S52 microcontroller successfully interfaces with the 16×2 character LCD using a 4-bit GPIO-based communication interface.

The LCD is initialized using the required control commands, and the higher and lower nibbles of each command and character are transmitted separately through Port 3.

The RS and Enable control signals are used to distinguish between command and data operations and to synchronize the communication between the microcontroller and LCD.

The program continuously transmits the message **"HELLO FROM 8051"** using the `lcd_data()` function and clears the display using the `lcd_cmd()` function.

Thus, 4-bit LCD interfacing, LCD initialization, command transmission, character display, and Embedded C driver development for the AT89S52 microcontroller are demonstrated successfully.
