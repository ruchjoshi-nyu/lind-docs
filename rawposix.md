# RawPOSIX

RawPOSIX provides an in-process OS with POSIX-like interface implemented on top of standard POSIX Linux system calls, enabling safe execution of isolated applications.

## Purpose

The primary goal is to enable execution of both legacy and modern multi-process applications safely and efficiently within the same address space, maintaining identical behavior to applications running on native Linux.

## Core Features

### System Call Support
- Signals
- Fork/exec operations
- Threading capabilities
- File system operations
- Networking functionality
- Independent management of FDs and threads per cage

### Key Components

**Memory Management**
- Tailored to runtime environment
- Leverages VMMap-related system calls
- Enables per-cage memory management

**Process Management**
- Wait and waitpid functionality
- Fork and exec operations
- Signal handling
- Updates cage structure and data structures
- Maintains process isolation

## Project Structure

### Source Directory (src/)
- **syscalls.rs**: Defines and implements supported system calls
- **cage.rs**: Contains cage data structure definitions and lifecycle management

### Additional Directories
- **tests/**: Contains test cases and validation scripts
- **docs/**: Documentation and setup instructions

## Implementation Details

### System Call Types
1. **Raw Syscalls**: Direct interactions with Linux kernel for low-level operations
2. **Userspace Syscalls**: Abstractions for runtime-specific needs (WASM/Native Client)

### Cage Structure
- Handles per-process information
- Provides required memory management
- Maintains isolation between processes

## Testing Framework

RawPOSIX includes comprehensive testing capabilities:
- Validates core functionality
- Covers normal usage scenarios
- Tests error conditions
- Ensures proper component operation
