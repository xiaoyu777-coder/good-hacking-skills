---
name: fix-vmp-iat
description: fix vmprotected iat
---

# fix-vmp-iat

VMP modifies the original IAT calls to a format of `call virtual section + one junk instruction` (often padded with nop), and decrypts them at runtime.

Recommended workflow:

1. Support specifying pid, module name, or raw memory range.
2. Optionally build a new IAT section before dumping, resulting in a PE file suitable for static analysis.

Signature search hints (x64):

- Original form: `call [iat]` / `mov reg, [iat];` call reg` / `jmp [iat]`
- After protection: uniformly converted to `call virtual segment` + padding with invalid bytes.
