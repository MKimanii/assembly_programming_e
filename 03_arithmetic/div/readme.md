
## Flag Analysis: `div1.asm`
### 1. Division Operation Point (`div bl` / `div ebx`)
- **State at `_start+14`:** `eax = 0x20e` (526), `ebx = 0x7`, `edx = 0x0`
- **EFLAGS:** `0x212` `[ AF IF ]`
**AF** (Auxiliary Carry)| Retained or left undefined by the x86 architecture during the division instruction. 
**IF** (Interrupt Flag) | Hardware interrupts are enabled by default
### 2. Exit Logic Point (`xor ebx, ebx`)
- **State at `_start+21`:** `eax = 0x1` (sys_exit), `ebx = 0x0`
- **EFLAGS:** `0x246` `[ PF ZF IF ]`
**ZF** (Zero Flag)  The bitwise XOR operation (`ebx ^ ebx`) cleared the destination register to exactly `0`
**PF** (Parity Flag)| The lowest 8 bits of the result (`0x00`) contain zero `1` bits, which is counted as even parity. 
**IF** (Interrupt Flag) | Hardware interrupts remain enabled


## Flag Analysis: `div2.asm`
### 1. Division Operation Point (`div ebx`)
- **State at `_start+23`:** `eax = 0xa6` (Quotient: 166), `edx = 0xc8` (Remainder: 200), `ebx = 0x12c` (Divisor: 300)
- **EFLAGS:** `0x212` `[ AF IF ]`
**AF** (Auxiliary Carry) | Left in an undefined state by the architecture. Per the Intel x86 specification
**IF** (Interrupt Flag)| Hardware interrupts are enabled by the operating system by default.
### 2. Exit Logic Point (`xor ebx, ebx`)
- **State at `_start+30`:** `eax = 0x1` (sys_exit), `ebx = 0x0`
- **EFLAGS:** `0x246` `[ PF ZF IF ]`
**ZF** (Zero Flag)The bitwise XOR operation (`ebx ^ ebx`) yields an exact result of `0` in `ebx`
**PF** (Parity Flag) |The lowest 8 bits of the result (`0x00`) contain an even number (zero) of set `1` bits
**IF** (Interrupt Flag) |System interrupts remain enabled by default