The [[CCVM]] runs on a custom bytecode format that I designed myself, its called CC-Binary and is stored in .ccb files. These files are essentially the .exe equivalent of the CCVM runtime.

---

## Header
The header of a CCB takes a grand total of 8 bytes, within you can find (in order)
- a 4 bit magic number used to identify that the file is a real .ccb file, without it, the CCVM will think the ccb is corrupted, the magic number should `DE AD BE EF`
- a 4 bit version number
	- 2 of which are used for the major version number
	- 2 of which are used for the minor version number

An example of a CCB file header is (when opened in a hex editor):
```
DEADBEEF 0001 0000
```

This CCB is meant for CCVM version 1.0 or later.

---

## After the header
After the header, the real program embedded within the CCB will start, this is essentially just a list of opcode instructions, varying in byte length. How these instructions are read, together with the full list of instructions is documented in [[Instructions]]