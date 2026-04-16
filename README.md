# Binary & Hex String to Decimal Converter DLL (P09)

A Windows Dynamic Link Library (DLL) written in x86 Assembly (MASM) that provides two functions to convert string representations of numbers into decimal integers:

- Binary strings (up to 8 bits)
- Hexadecimal strings (up to 4 characters)

**Author:** DN MBOYI  
**Student Number:** 222019179  
**Subject:** CSC03B3  
**Practical:** P09  
**Year:** 2025  

---

## Problem Description

This DLL exports two functions:

1. **`binStringToDecimal(pString)`**  
   Converts a binary string (e.g., `"00000101"`, `"1010"`, `"11111111"`) to its decimal equivalent.  
   Maximum length: **8 characters**.  
   Returns **-1** if the string contains invalid characters or exceeds 8 bits.

2. **`hexStringToDecimal(pString)`**  
   Converts a hexadecimal string (e.g., `"1A3F"`, `"ff"`, `"A"`) to its decimal equivalent.  
   Maximum length: **4 characters**.  
   Supports both uppercase (`A-F`) and lowercase (`a-f`) letters.  
   Returns **-1** if the string contains invalid characters or exceeds 4 digits.

---

## Features

- Robust input validation for binary (`0` and `1` only) and hexadecimal (`0-9`, `A-F`, `a-f`) characters
- Efficient bit-shifting for binary conversion (`SHL EDX, 1`)
- Efficient nibble-shifting for hex conversion (`SHL EDX, 4`)
- Proper handling of variable-length strings (shorter than maximum allowed)
- Returns `-1` on invalid input (as per specification)
- Clean stack frame management and register preservation
- Exported via `.def` file for easy integration with C/C++ or other languages

---

## Technologies Used

- **x86 Assembly Language**
- **MASM** (Microsoft Macro Assembler)
- **DLL Development** with module definition (`.def`) file
- String processing and character validation
- `LibMain` entry point for DLL loading

---

## Files Included

- `222019179_P09.asm` – Main assembly source containing both conversion functions
- `P09.def` – Module definition file exporting the two functions
- `README.md`

---

## How to Build

1. Create a new **Win32 DLL** project in Visual Studio with MASM support.
2. Add `222019179_P09.asm` and configure it for assembly.
3. Add `P09.def` to the project.
4. Build the solution → This generates `P09.dll` and the import library.

These functions can then be called from C/C++, C#, or another assembly program using `LoadLibrary` / `GetProcAddress` or by linking against the `.lib` file.

---

## Example Usage

```c
// Pseudocode examples
int result1 = binStringToDecimal("00000101");   // Returns 5
int result2 = binStringToDecimal("11111111");   // Returns 255
int result3 = hexStringToDecimal("1A3F");       // Returns 6719
int result4 = hexStringToDecimal("ff");         // Returns 255
int result5 = hexStringToDecimal("XYZ");        // Returns -1 (invalid)
