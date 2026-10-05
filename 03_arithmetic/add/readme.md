
## Flag Analysis: `add1.asm`
- **Operation:** `add al, [num2]` (`120 + 10 = 130`)
- **Hex Result:** `0x82`
- **Binary Result:** `10000010b`
- **EFLAGS Register:** `0xa96` `[ PF AF SF IF OF ]`
**SF** (Sign Flag) | Bit 7 (the MSB of an 8-bit value) is `1` (`10000010b`), indicating a negative number (`-126`) in signed two's complement[cite: 1].
**OF** (Overflow Flag) |  A signed overflow occurred; adding two positive numbers (`+120` and `+10`) exceeded the maximum signed 8-bit limit (`+127`) and wrapped into negative[cite: 1].
**AF** (Auxiliary Carry) | A carry occurred from bit 3 into bit 4 across the lower nibble boundary (`0x8 + 0xA = 0x12`).
**PF** (Parity Flag) | The lowest byte (`10000010b`) contains an even number of `1` bits (exactly two `1`s)[cite: 1].


## Flag Analysis: `add2.asm`
- **Operation:** `32000 + 500 = 32500`
- **Hex Result:** `0x7EF0` (in `ax`)
- **Binary Result:** `0111 1110 1111 0000b`
- **EFLAGS:** `[ zF,PF,IF ]` 
**ZF** (Zero Flag) | **SET** | The result of `xor ebx, ebx` is exactly `0`. 
**PF** (Parity Flag) | **SET** | The lowest 8 bits (`0x00`) contain zero `1` bits, which satisfies even parity. 
**IF** (Interrupt Flag) | **SET** | System interrupts remain enabled by default.