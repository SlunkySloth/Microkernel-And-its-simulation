# 🖥️ Microkernel OS Simulation

A web-based interactive simulation of a **Microkernel Operating System architecture**. This project visualizes how a minimal kernel handles Inter-Process Communication (IPC) and Process Scheduling to coordinate between user-space applications and system servers.

## 🚀 Live Demo
[Click here to view the simulation](#) *(Or simply open the `index.html` file in your browser)*

## 📖 Overview

Unlike Monolithic kernels (like Linux/Windows) where file systems and drivers run in kernel mode, a **Microkernel** keeps the kernel code minimal. It pushes services like File Systems, Drivers, and Networking into "User Space" as separate processes.

**This project simulates:**
1.  **The Kernel:** Handles *only* scheduling and passing messages.
2.  **IPC (Inter-Process Communication):** The mechanism processes use to talk to each other.
3.  **The Servers:** Separate processes for File System, Input Drivers, and Logging.

## ✨ Features

* **Visualized State:** Real-time view of Kernel, Scheduler, and Process states.
* **Round-Robin Scheduling:** Watch the scheduler cycle through processes (highlighting the active one).
* **Message Passing System:** See messages move from `App` → `Kernel` → `Server` and back.
* **Interactive Controls:**
    * Request file reads from the virtual File System.
    * Send keystrokes to the virtual Keyboard Driver.
* **Process Logs:** Individual logs for every process to track execution flow.

## 🛠️ Architecture

The system mimics a standard microkernel design pattern:

```mermaid
sequenceDiagram
    participant UserApp as User Application
    participant Kernel as Microkernel
    participant FS as FileSystem Server
    
    Note over UserApp, FS: Example: Reading a File
    UserApp->>Kernel: IPC_SEND: {to: 'fs_server', type: 'READ'}
    Note over Kernel: Context Switch (Scheduler)
    Kernel->>FS: Dispatch Message
    Note over FS: Process Request
    FS->>Kernel: IPC_SEND: {to: 'app', type: 'CONTENT'}
    Note over Kernel: Context Switch (Scheduler)
    Kernel->>UserApp: Dispatch Message
