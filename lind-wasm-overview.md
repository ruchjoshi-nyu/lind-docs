# Lind-Wasm

Lind is a single-process sandbox that provides an option to safely execute programs. Lind executes applications using software fault isolation and a kernel microvisor to limit the potential of reaching bugs or security flaws in the application[1].

In Old Norse, Old High German and Old English a "lind" is a shield constructed with two layers of linden wood. Linden wood shields are lightweight, and do not split easily, an appropriate metaphor for a sandboxing system which employs two technologies[1].

## Core Concepts

- **Cage**: Lightweight isolation boundary within a process
  - Can run legacy code (may need recompilation)
  - Protects and isolates memory[1]
- **Microvisor**: Small POSIX compliant kernel within a process
  - Provides a POSIX interface
  - Distinct isolation between cages[1]
- **3i (three eye)**: Capability-based POSIX interfaces between cages[1]

## Technology Overview

### Cages
Memory and bookkeeping that encapsulates the idea of a typical OS process, encompassing applications as well as grates[1].

### Grates
Can perform trusted operations on descendant cages without requiring code in the microvisor's TCB. Grates can run arbitrary code, with restrictions only placed by grates beneath them. The microvisor implements a grate with access to call into the Linux kernel[1].

**Inheritance Properties**:
- A child inherits system calls from parent on fork
- If cage A was forked by cage B, cage A will have the same system call handlers as cage B
- If grate A was forkinterpose()'d by grate B, grate A inherits B's system call behavior changes[1]

### 3i System
The 3i system serves as:
- Central point for all communication between cages
- Table container for system call routing
- Security control mechanism for system call interception
- Privilege management system for blocking unnecessary calls[1]

## Components

### Wasmtime
Wasmtime is a fast and secure runtime for WebAssembly designed by Bytecode Alliance. Lind-wasm uses wasmtime as a runtime with added support for multi-processing via Asyncify[1].

### lind-glibc
Modified version of glibc compiled to wasm bytecode with the following changes[1]:

1. System Call Mechanism: Routes through `rawposix` using:
```c
MAKE_SYSCALL(syscallnum, "syscall|callname", arg1, arg2, arg3, arg4, arg5, arg6)
```

2. Assembly Code Elimination: Removed assembly components and rewrote in C
3. Generated Files Handling: Manually implemented system calls in C files[1]

### RawPOSIX
Provides normal POSIX system calls including:
- Signals
- Fork/exec
- Threading
- File system
- Networking
- Separate handling of cages' fds and threads[1]

### 3i Implementation
The iPC (intra-process call) interposable interface enables secure and efficient cage communication with function call-like speed. It provides POSIX interfaces between cages with interposition capabilities, enabling fine-grained security and access control while maintaining program behavior[1].
