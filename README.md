# c-crypter

This is a project meant for encrypting c-strings from C++ code. It works as a quick fix for hiding text from mediocre so-called hackers or script kiddies that have no basic knowledge in assembly language but use tools for probing executables.

The code is written in javascript and uses extensively regex for pattern matching. The code also provides feedback to the user about possible errors or success.

The program needs two sources: the code whose strings to be encrypted and an additional code that will include all defines and functions needed for decryption. This last code can be put into an obfus.h file.

### Input
The user must input some values for the encryption:
- encryption key
- null character replacement
- source code
- 'obfus' code (default provided)


### Encryption
The encryption algorithm is a simple one. The key is defined by the user and every character found in every string is XORed with that key. The code can diferentiate between a declared string-array `char arr[][]={"string1","string2"}` up to two dimensions  and simple strings used as parameteres in function calls `strlen("string")`.

### Encrypted format
For string arrays the program will do the following:
- add the original line as a comment
- transform all strings into hex arrays of the encrypted characters
- add the decryption function call

For inline-used strings:
- create a define for the string using a custom generator: `#define str_<generated-short-name>_<string-hash> <string-index>`. This is stored in obfus code.
 - add encrypted string to `content` array in obfus code.
 - replace original string with a function call to the decrypting method.
 
### Attention:
- It is important to make sure that strings are not split between lines. No multiline-string support.

