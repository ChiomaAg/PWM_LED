# STM32 PWM LED Brightness Control

This project demonstrates how to control LED brightness using PWM (Pulse Width Modulation) with TIM1 on an STM32 microcontroller. The LED brightness alternates between two levels (75% and 25%) every second.

##  Project Overview

- **MCU Series**: STM32 (tested with STM32L4, configurable for other STM32 families)
- **Timer Used**: TIM1, Channel 1
- **PWM Frequency**: 1 kHz
- **Duty Cycles**: 75% and 25%, alternating every second
- **Clock Source**: MSI @ 4 MHz
- **Prescaler**: 3
- **Period**: 999 (for 1 kHz PWM cycle)

##  Peripherals Configuration

### Clock
- System Clock: 4 MHz using MSI (RCC_MSIRANGE_6)
- No PLL

### Timer Configuration
| Parameter      | Value        |
|----------------|--------------|
| Prescaler      | 3            |
| Period         | 999          |
| Counter Mode   | Up           |
| PWM Mode       | PWM1         |
| Output Compare | Channel 1    |

### GPIO
- **Pin**: PA8
- **Mode**: Alternate Function Push-Pull (AF for TIM1_CH1)
- **Speed**: Low/Medium
- **Connected to**: LED + resistor (220–470 Ω)

## 📋 Code Behavior

- The LED brightness is controlled by varying the duty cycle.
- In the main loop, the duty cycle is updated every second:
  ```c
  __HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_1, 750); // 75% duty
  HAL_Delay(1000);
  __HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_1, 250); // 25% duty
  HAL_Delay(1000);
