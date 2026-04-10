# Remote Process Shellcode Loader in C
This repository features a lightweight and efficient Shellcode Loader written in C. It demonstrates low-level system programming techniques for injecting and executing shellcode within the address space of a remote Windows process.

## Technical Overview
The loader leverages the Windows API (WinAPI) to interact with the OS kernel, performing process enumeration, memory allocation, and remote thread execution. This project is intended for security researchers, Red Teamers, and developers interested in malware analysis and defensive engineering.

## Key Features
Process Enumeration: Automatically locates a target process (e.g., explorer.exe or notepad.exe) using the Toolhelp32 snapshot API.

- **Memory Injection:** Implements a classic injection workflow:

- **OpenProcess:** Acquires a handle to the target process.

- **VirtualAllocEx:** Allocates memory with executable permissions within the remote process.

- **WriteProcessMemory:** Writes the payload into the newly allocated memory space.

- **Remote Execution:** Utilizes CreateRemoteThread to initiate execution without interrupting the main thread of the host process.

- **Minimal Footprint:** Written in pure C to ensure a small binary size and minimal external dependencies.

## Execution Workflow
- **PID Discovery:** The loader scans the process list to find the Process ID (PID) of the specified target.

- **Handle Acquisition:** Requests necessary access rights from the Windows kernel.

- **Payload Deployment:** Allocates a buffer (typically PAGE_EXECUTE_READWRITE) and transfers the shellcode.

- **Thread Creation:** Instructs the remote process to spawn a new thread starting at the shellcode's memory address.

## Compilation
To compile the loader using MinGW, run:

```bash
gcc main.c -o loader.exe -lkernel32 -luser32
```
For Visual Studio (MSVC), ensure you include the Windows SDK and compile for the appropriate architecture (x64/x86) matching your shellcode.

## Disclaimer
**IMPORTANT:** This project is provided for educational and ethical security testing purposes only. Unauthorized access to computer systems is illegal. The developer assumes no liability for any misuse of this software or damage caused by its application. Use responsibly within authorized environments.
