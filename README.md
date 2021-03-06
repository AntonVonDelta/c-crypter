# c-crypter

This is a project meant for encrypting c-strings from C++ code. It works as a quick fix for hiding text from mediocre so-called hackers or script kiddies that have no basic knowledge in assembly language but use tools for probing executables.

The code is written in javascript and uses extensively regex for pattern matching. The code also provides feedback to the user about possible errors or success.

The program needs two sources: the code(entire code..the program contains a parser that can diferentiate between executable code and strings) whose strings to be encrypted and an additional code that will include all defines and functions needed for decryption. This last code can be put into an obfus.h file.

Test here: https://antonvondelta.github.io/c-crypter/
### Input
The user must input some values for the encryption:
- encryption key
- null character replacement
- source code
- 'obfus' code (default provided)

It not necessary to reset obfus code to default for every program that needs to be encrypted. New encrypted strings are added to obfus section without any interaction needed.

### Encryption
The encryption algorithm is a simple one. The key is defined by the user and every character found in every string is XORed with that key. The code can diferentiate between a declared string-array `char arr[][]={"string1","string2"}` up to two dimensions  and simple strings used as parameteres in function calls `strlen("string")`.
As an extra security measure the null charcater is replaced with the specified code which is also encrypted. At runtime this is reversed.

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
- Unicode strings are not supported. E.g: `L"string"`
- some strings are not encrypted on purpose: all smaller than 5 characters or those that don't contain characters in [a-zA-Z0-9] range
