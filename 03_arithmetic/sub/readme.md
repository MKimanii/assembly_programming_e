## Flag Analysis: `sub1.asm`
### 1. Subtraction Arithmetic Point (`sub al, ...`)
- **State at `_start+11`:** `eax = 0xe2` (226), `ebx = 0x0`, `edx = 0x0`
- **Hex Result in `al`:** `0xe2`
- **Binary Result:** `11100010b`
- **EFLAGS:** `0x287` `[ CF PF SF IF ]`
**CF** (Carry Flag) | An unsigned borrow occurred. The subtracted value was larger than the initial value in `al`, causing a borrow past the most significant bit (bit 7). 
**SF** (Sign Flag) | Bit 7 (the MSB of an 8-bit value) is `1` (`11100010b`), indicating a negative result (`-30`) in signed two's complement. 
**PF** (Parity Flag)| The lowest 8 bits (`11100010b`) contain exactly four `1` bits, which satisfies even parity.
**IF** (Interrupt Flag) | System hardware interrupts are enabled by default
### 2. Exit Logic Point (`xor ebx, ebx`)
- **State at `_start+23`:** `eax = 0x1` (sys_exit), `ebx = 0x0`
- **EFLAGS:** `0x246` `[ PF ZF IF ]`
**ZF** (Zero Flag)| The bitwise XOR operation (`xor ebx, ebx`) cleared the register to exactly `0`
**PF** (Parity Flag)| The lowest 8 bits (`0x00`) contain zero `1` bits, which counts as even parity
**IF** (Interrupt Flag) | Hardware interrupts remain enabled by default


## Flag Analysis: `sub2.asm`
### 1. Subtraction Operation Point (`sub ax, ...`)
- **State at `_start+13`:** `eax = 0xfc18` (64536 in `ax`, or `-1000` signed), `edx = 0x0`, `ebx = 0x0`
- **Hex Result in `ax`:** `0xfc18`
- **Binary Result (`ax`):** `1111 1100 0001 1000b`
- **EFLAGS:** `0x287` `[ CF PF SF IF ]`
**CF** (Carry Flag) | An unsigned borrow occurred across the highest bit (bit 15). The value being subtracted was larger than the original unsigned 16-bit minuend in `ax`. 
 **SF** (Sign Flag) | Bit 15 (the most significant bit of a 16-bit word) is `1` (`1111 1100 0001 1000b`), representing a negative value (`-1000`) in signed two's complement. |
**PF** (Parity Flag)| The lowest 8 bits (`al = 0x18` / `00011000b`) contain exactly two `1` bits, satisfying even parity. 
**IF** (Interrupt Flag) | Hardware interrupts remain enabled by default
