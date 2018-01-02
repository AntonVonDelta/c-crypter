# c-crypter

This is a project meant for encrypting c-strings from C++ code. It works as a quick fix for hiding text from mediocre so-called hackers or script kiddies that have no basic knowledge in assembly language but use tools for probing executables.

The code is written in javascript and uses extensively regex for pattern matching. The code also provides feedback to the user about possible errors or success.

### Input
The user must input some values for the encryption:
- encryption key
- null character replacement
- source code
- 'obfus' code

### Encryption
The encryption alghoritm is a simple one. The key is defined by the user and every character found in every string is XORed with that key. The code can diferentiate between a declared string-array `char arr[][]={"string1","string2"}` up to two dimensions  and simple strings used as parameteres in function calls `strlen("string")`.


### Attention:
- It is important to make sure that strings are not split between lines. No multiline-string support.

