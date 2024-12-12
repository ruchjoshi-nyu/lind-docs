# RawPOSIX

RawPOSIX provides an in-process OS with POSIX-like interface implemented on top of standard POSIX Linux system calls, enabling safe execution of isolated applications[1].

## Purpose

The primary goal is to enable execution of both legacy and modern multi-process applications safely and efficiently within the same address space, maintaining identical behavior to applications running on native Linux[1].

## Core Features

### System Call Support
- Signals
- Fork/exec operations
- Threading capabilities
- File system operations
- Networking functionality
- Independent management of FDs and threads per cage[1]

### Key Components

**Memory Management**
- Tailored to runtime environment
- Leverages VMMap-related system calls
- Enables per-cage memory management[1]

**Process Management**
- Wait and waitpid functionality
- Fork and exec operations
- Signal handling
- Updates cage structure and data structures
- Maintains process isolation[1]

## Project Structure

### Source Directory (src/)
- **syscalls.rs**: Defines and implements supported system calls
- **cage.rs**: Contains cage data structure definitions and lifecycle management[1]

### Additional Directories
- **tests/**: Contains test cases and validation scripts
- **docs/**: Documentation and setup instructions[1]

## Implementation Details

### System Call Types
1. **Raw Syscalls**: Direct interactions with Linux kernel for low-level operations
2. **Userspace Syscalls**: Abstractions for runtime-specific needs (WASM/Native Client)[1]

### Cage Structure
- Handles per-process information
- Provides required memory management
- Maintains isolation between processes[1]

## Testing Framework

RawPOSIX includes comprehensive testing capabilities:
- Validates core functionality
- Covers normal usage scenarios
- Tests error conditions
- Ensures proper component operation[1]
