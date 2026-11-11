# EXPERIMENT DETAILS

**EXP:** CONTINUOUS LAB EVALUATION 8

**DATE:** 18/09/2026 (Week 7)

**NAME OF EXP:** STM32 GPIO Event-Based Control – Push Button Controlled LED Toggle with Debouncing

**HARDWARE SETUP / PLATFORM:** CubeMX + Keil MDK + STM32 Development Board (Blue Pill STM32F103C8T6) + Push Button + Onboard LED

---

## TASK 8B – Event-Based Control

### 1. Circuit Diagram

The experiment demonstrates event-based GPIO control using the STM32 Blue Pill development board. A push button is interfaced with the STM32 GPIO input pin, and the onboard LED is controlled by toggling its state whenever a valid button press is detected.

- **Development Board:** STM32 Blue Pill
- **Microcontroller IC:** STM32F103C8T6
- **Input Device:** Push Button
- **Output Device:** Onboard LED
- **GPIO Input Pin:** PA3
- **GPIO Output Pin:** PC13
- **Control Method:** Event-based GPIO control
- **Debouncing Method:** Software debouncing using a 50 ms delay

**Connections:**

| Component | STM32 Blue Pill Pin | Description |
|---|---|---|
| Push Button | PA3 | Reads push-button state |
| Push Button | GND | Common connection |
| Onboard LED | PC13 | LED toggle control |
| Internal Pull-up | PA3 | Maintains HIGH state when button is released |
| GND | GND | Common Ground |

**Working Configuration:**

- PA3 is configured as GPIO input with an internal pull-up resistor.
- PC13 is configured as GPIO output push-pull.
- When the button is released, PA3 reads HIGH.
- When the button is pressed, PA3 reads LOW.
- The onboard LED is active-low, so writing RESET turns it ON and writing SET turns it OFF.
![alt text](<CIRCUIT DIAGRAM.png>)
### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates event-based control of an LED using a push button and GPIO pins of the STM32 Blue Pill.

The push button is connected to GPIO pin PA3, which is configured as an input with an internal pull-up resistor. The onboard LED is connected to GPIO pin PC13.

The STM32 continuously monitors the push-button state using `HAL_GPIO_ReadPin()`. When the button is pressed, the input pin reads LOW. A delay of 50 ms is introduced to eliminate unwanted transitions caused by mechanical switch bouncing.

After the delay, the button state is checked again. If the input is still LOW, the LED state is changed using `HAL_GPIO_TogglePin()`. A `while` loop then waits until the button is released before accepting another press.

This ensures that one valid button press produces only one LED toggle, preventing multiple toggles due to switch bouncing or a continuously pressed button.

**Pseudocode:**

1. Initialize the HAL library.
2. Configure the system clock.
3. Initialize GPIO pins.
4. Configure PA3 as GPIO input with an internal pull-up resistor.
5. Configure PC13 as GPIO output.
6. Continuously monitor the push-button state using `HAL_GPIO_ReadPin()`.
7. If PA3 reads LOW:
   - Introduce a 50 ms delay for debouncing.
   - Check the button state again.
   - If it is still LOW, toggle the LED using `HAL_GPIO_TogglePin()`.
8. Wait until the push button is released.
9. Return to the beginning of the loop to detect the next button press.
10. Repeat the process continuously.

**Code Base:**

The GPIO event-based control is implemented using the following STM32 HAL functions:

- `HAL_Init()` – Initializes the HAL library.
- `SystemClock_Config()` – Configures the system clock.
- `MX_GPIO_Init()` – Initializes and configures the GPIO pins.
- `HAL_GPIO_ReadPin()` – Reads the push-button input state from PA3.
- `HAL_GPIO_TogglePin()` – Toggles the onboard LED state connected to PC13.
- `HAL_Delay()` – Introduces a 50 ms delay for software debouncing.
- `Error_Handler()` – Handles initialization errors.

**GPIO Configuration:**

| GPIO Pin | Mode | Pull Configuration | Function |
|---|---|---|---|
| PA3 | Input | Pull-up | Push-button input |
| PC13 | Output Push-Pull | Pull-up (as configured in code) | Onboard LED control |

**Expected Output:**

| Push Button Action | PA3 Input | LED Behaviour |
|---|---|---|
| Button released | HIGH | No change |
| First valid press | LOW | LED toggles ON |
| Button released again | HIGH | LED retains its state |
| Second valid press | LOW | LED toggles OFF |
| Third valid press | LOW | LED toggles ON |

**Software Debouncing:**

- A 50 ms delay is introduced after detecting a LOW input.
- The button state is checked again to confirm a valid press.
- The program waits until the button is released before accepting another press.
- This prevents repeated LED toggling while the button remains pressed.

### 3. Inference

The STM32 Blue Pill successfully detects valid push-button press events through GPIO pin PA3 and toggles the onboard LED connected to PC13.

A 50 ms software debounce delay is implemented to eliminate unwanted transitions caused by mechanical switch bouncing. The program also waits for the button to be released before detecting the next press.

Thus, event-based GPIO control and software debouncing are successfully demonstrated using STM32 HAL libraries. Each valid push-button press produces exactly one LED toggle.