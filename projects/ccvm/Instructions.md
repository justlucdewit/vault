CCB files that are ran within the CCVM should have a certain executable format. as explain in [[Bytecode format]], a ccb starts with a 8byte header, followed by the program code.

This program code is nothing but a list of instructions. These instructions are 1 byte indicating the type of instruction (this is called the 'opcode'), optionally followed by a set of argument bytes, depending on which opcode was used.

---

## Example

lets say there is an opcode `AB` which should be followed by a `register argument`, and a `literal argument`. Register arguments are 1 byte long and should only be `00`, `01`, `02`, `03`, .... , `07`.

An example of this would be the following instruction:

```ccb
03 01 00000003
```

Which does opcode 03 with register 01, and the number literal 3. In CC Assembly this might be expressed with:

```cca
SMTNG r1, 3 ; SMTNG would be 0x03
```

## Opcode list

| Opcode | Asm mnemonic | Arguments | Description                       |
| ------ |:------------ |:--------- |:--------------------------------- |
| 0x00   | STP          |           | Stops execution of the program    |
| 0x10   | MOV          | reg lit   | moves a literal to a register     |
| 0x10   | MOV          | reg reg   | moves a register to a register    |
| 0x12   | PSH         | lit       | pushes a literal to the stack     |
| 0x13   | PSH         | reg       | pushes a register to the stack    |
| 0x14   | POP          | reg       | pops from the stack to a register |

## CCB Example
The following is an example of a CCB for V1.0, that puts the literal `1` into register 1, and then clones it to register 2, and then stops the program. At the end both register 1 and 2 will have the number 1 in it.

```ccb
DEADBEEF 00010000
10 01 00000001
11 02 01
00
```

The following CCA assembly code represents this CCB file:
```cca
MOV r1, 1
MOV r2, r1
STP
```