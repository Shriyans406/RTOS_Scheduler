# RTOS Scheduler Analysis

This project is a Real-Time Operating System (RTOS) implementation for the STM32F103C8T6 microcontroller. It uses FreeRTOS to demonstrate task scheduling, priority management, and basic inter-task synchronization.

## Objective

The main goal of this project is to analyze how a real-time scheduler handles multiple tasks with different priorities. It provides a practical look at task preemption, timing, and communication in an embedded system.

## Project Details

- **Microcontroller**: STM32F103C8T6 (ARM Cortex-M3)
- **Operating System**: FreeRTOS (configured via CMSIS-RTOS V1 API)
- **Clock Speed**: 72 MHz (external 8 MHz crystal)
- **Communication Interface**: USART1 (115200 Baud Rate)

## Task Architecture

The project implements three primary tasks with varying priority levels to demonstrate the scheduler's behavior:

### 1. Task High (High Priority)
- **Function**: Executes a continuous incrementing counter.
- **Behavior**: This task has the highest priority. It performs a simple computation and prints its status to the UART console every 50,000 cycles.
- **Starvation Prevention**: It includes a short 1ms delay (`osDelay(1)`) to yield control and allow lower priority tasks to execute.

### 2. Task Normal (Normal Priority)
- **Function**: Handles data processing.
- **Behavior**: This task is designed to wait for data from a message queue. When a message is received, it prints the value to the UART console. It remains in a blocked state while waiting, consuming no CPU cycles.

### 3. Task Low (Low Priority)
- **Function**: System monitoring and heartbeat.
- **Behavior**: Executes once every second. It calculates the time difference between its executions using system ticks and prints the current tick count and delta time.

## Key RTOS Concepts Demonstrated

- **Task Preemption**: Higher priority tasks will interrupt lower priority ones when they transition from a blocked to a ready state.
- **Priority-Based Scheduling**: The RTOS ensures that the highest priority task ready to run always gets the CPU.
- **Task Blocking**: Using `osDelay` or message queue waits allows the CPU to run other tasks instead of wasting cycles in busy-wait loops.
- **Inter-Task Communication**: Placeholder implementation for message queues to pass data between threads safely.

## Project Structure

- **Core/Src/main.c**: Contains the main initialization code and the implementation of the three RTOS tasks.
- **Core/Src/freertos.c**: Contains FreeRTOS specific configurations and hook functions.
- **RTOS_Scheduler_Analysis_2.ioc**: STM32CubeMX configuration file.
- **RTOS_Scheduler_Analysis.pdsprj**: Proteus simulation file for testing the firmware without physical hardware.

## How to Build and Run

1. **Prerequisites**:
   - STM32CubeIDE or ARM-GCC toolchain.
   - Proteus (optional, for simulation).

2. **Compilation**:
   - Open the project in STM32CubeIDE.
   - Build the project to generate the `.hex` or `.bin` file.

3. **Running/Simulation**:
   - Load the generated firmware into an STM32F103C8T6 microcontroller.
   - Alternatively, open the Proteus project file and link the `.hex` file to the STM32 component.
   - Connect a Serial Monitor to UART1 (TX: PA9, RX: PA10) set to 115200 baud to view the scheduler output.
