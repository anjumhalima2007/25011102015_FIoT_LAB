# EXPERIMENT DETAILS

**EXP:** CONTINUOUS LAB EVALUATION 8

**DATE:** 18/09/2026 (Week 7)

**NAME OF EXP:** STM32 GPIO Bring-Up and Switch-Controlled LED

**HARDWARE SETUP / PLATFORM:** CubeMX + Keil MDK + STM32 Development Board (Blue Pill STM32F103C8T6) + Push Button + Onboard LED

---

## TASK 8A – GPIO Input/Output

### 1. Circuit Diagram

The experiment demonstrates GPIO input and output interfacing using the STM32 Blue Pill development board. A push button is connected to the GPIO input pin, and the onboard LED is controlled based on the button state.

- **Development Board:** STM32 Blue Pill
- **Microcontroller IC:** STM32F103C8T6
- **Input Device:** Push Button
- **Output Device:** Onboard LED
- **GPIO Input Pin:** PA3
- **GPIO Output Pin:** PC13
- **Communication:** GPIO-based digital input/output

**Connections:**

| Component | STM32 Blue Pill Pin | Description |
|---|---|---|
| Push Button | PA3 | Reads button state |
| Push Button | GND | Common connection |
| Onboard LED | PC13 | LED output control |
| Internal Pull-up | PA3 | Keeps input HIGH when button is released |
| GND | GND | Common Ground |

**Working Configuration:**

- PA3 is configured as a GPIO input with an internal pull-up resistor.
- PC13 is configured as a GPIO output.
- When the push button is pressed, PA3 becomes LOW.
- The onboard LED turns ON when PC13 is driven LOW.
![alt text](<circuit.png>)
### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates GPIO-based communication between an input device and an output device using the STM32 Blue Pill.

The push button is connected to GPIO pin PA3, which is configured as an input with an internal pull-up resistor. When the button is not pressed, the input remains HIGH. When the button is pressed, the input becomes LOW.

The STM32 continuously monitors the button state using `HAL_GPIO_ReadPin()`. When a LOW signal is detected, a small delay of 20 ms is introduced to reduce the effect of switch bouncing. The button state is checked again to confirm the press.

If the button remains pressed, the onboard LED connected to PC13 is turned ON using `HAL_GPIO_WritePin()`. Otherwise, the LED is turned OFF.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO pins.
4. Configure PA3 as GPIO input with an internal pull-up resistor.
5. Configure PC13 as GPIO output.
6. Continuously read the push-button state using `HAL_GPIO_ReadPin()`.
7. If PA3 reads LOW:
   - Introduce a delay of 20 ms.
   - Read the button state again.
   - If it is still LOW, turn ON the LED.
   - Otherwise, turn OFF the LED.
8. If PA3 reads HIGH, turn OFF the LED.
9. Repeat the process continuously.

**Code Base:**

The GPIO interfacing is implemented using the following STM32 HAL functions:

- `HAL_Init()` – Initializes the HAL library.
- `SystemClock_Config()` – Configures the system clock.
- `MX_GPIO_Init()` – Initializes and configures the GPIO pins.
- `HAL_GPIO_ReadPin()` – Reads the push-button input state from PA3.
- `HAL_GPIO_WritePin()` – Controls the onboard LED connected to PC13.
- `HAL_Delay()` – Introduces a 20 ms delay for basic switch debouncing.
- `Error_Handler()` – Handles initialization errors.

**GPIO Configuration:**

| GPIO Pin | Mode | Pull Configuration | Function |
|---|---|---|---|
| PA3 | Input | Pull-up | Push-button input |
| PC13 | Output Push-Pull | Pull-up (as configured in code) | Onboard LED control |

**Expected Output:**

| Push Button State | PA3 Input | PC13 Output | LED Status |
|---|---|---|---|
| Released | HIGH | SET | OFF |
| Pressed | LOW | RESET | ON |

### 3. Inference

The STM32 Blue Pill successfully detects the push-button state through GPIO pin PA3 and controls the onboard LED connected to PC13 accordingly.

When the push button is pressed, the input pin reads LOW, and the LED turns ON after a 20 ms delay and a second input check. When the button is released, the input pin reads HIGH, and the LED turns OFF.

Thus, GPIO input/output interfacing and basic switch debouncing using STM32 HAL libraries are demonstrated successfully.