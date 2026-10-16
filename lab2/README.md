# Laborator 2

## Exercitiul 1

**DOS Header**
- La `0x3C`: `F0 00 00 00`
- `e_lfanew = 0xF0` (little-endian)

**PE Signature si COFF Header**

Semnatura PE la `0xF0`:
- Signature: `50 45 00 00` (`PE\0\0`)

COFF Header incepe la `0xF4`:
- Machine: `0x014C` (x86)
- NumberOfSections: `5`
- TimeDateStamp: `0x6AD21529` (16.10.2026, 12:14:33 UTC)

**Optional Header**
- Offset: `0x108` (`0xF0 + 4 + 20`)
- Magic: `0x010B` (PE32)
- AddressOfEntryPoint: `0x125A`
- ImageBase: `0x400000`

**Section Table**
- Offset: `0x1E8`
- Prima sectiune: `.text`
- VirtualAddress: `0x1000`
- PointerToRawData: `0x400`

**Entry Point**
- File offset: `0x125A - 0x1000 + 0x400 = 0x65A`
- VA: `0x400000 + 0x125A = 0x40125A`

La Entry Point apare un `call` (`E8`), urmat de un `jmp` (`E9`), deci pare sa fie compilat cu MSVC.

## Exercitiul 2

**Teste:**
- `valid`: 5/5 rezultate identice cu cele din `expected`
- `malformed`: 6 fisiere au afisat erori, iar 2 au putut fi parsate

Cele doua fisiere care au putut fi parsate:
- `ep_outside.exe`: Entry Point in afara sectiunilor
- `wx_section.exe`: sectiunea `.data` are permisiuni `RWX`