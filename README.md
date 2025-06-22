# STM32 PWM LED Fading with TIM1

This project demonstrates how to fade an LED smoothly using PWM (Pulse Width Modulation) and a `for` loop on an STM32 microcontroller. The LED gradually brightens from off to full brightness, then dims back down — creating a breathing effect.

##  Project Overview

- **MCU Series**: STM32 (tested with STM32L4, configurable for others)
- **Timer Used**: TIM1, Channel 1
- **PWM Frequency**: 1 kHz
- **Duty Cycle Range**: 0% to 100%, updated incrementally
- **Clock Source**: MSI @ 4 MHz
- **Prescaler**: 3
- **Period**: 999 (1 ms PWM period)

## Peripherals Configuration

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

- The LED fades **up** and **down** by adjusting the PWM duty cycle gradually in a loop.
  
```c
while (1)
{
  // Fade in
  for (int i = 0; i <= 999; i += 10)
  {
    __HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_1, i);
    HAL_Delay(10);
  }

  // Fade out
  for (int i = 999; i >= 0; i -= 10)
  {
    __HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_1, i);
    HAL_Delay(10);
  }
}
