# ezpy
1. 已知该文件为`pyc`文件,利用工具对该文件进行反编译,得到python代码:
    ```py
    # Visit https://www.lddgo.net/string/pyc-compile-decompile for more information
    # Version : Python 3.8


    def caesar_cipher_encrypt(text, shift):
        result = []
        for char in text:
            if char.isalpha():
                if char.islower():
                    new_char = chr(((ord(char) - ord('a')) + shift) % 26 + ord('a'))
                elif char.isupper():
                    new_char = chr(((ord(char) - ord('A')) + shift) % 26 + ord('A'))
                result.append(new_char)
                continue
            result.append(char)
        return ''.join(result)

    user_input = input('please input your flag：')
    a = 1
    if a != 1:
        plaintext = user_input
        shift = 114514
        encrypted_text = caesar_cipher_encrypt(plaintext, shift)
        if encrypted_text == 'wyomdp{I0e_Ux0G_zim}':
            print('Correct!!!!')
    ```
2. 运行该代码,发现要求输入flag
   ![01](./picture/01.png)
   对该部分代码进行分析,发现为凯撒加密,由此写出解密代码
    ```py
    def caesar_cipher_decrypt(text, shift):
        return caesar_cipher_encrypt(text, -shift)

    def caesar_cipher_encrypt(text, shift):
        result = []
        for char in text:
            if char.isalpha():
                if char.islower():
                    new_char = chr(((ord(char) - ord('a')) + shift) % 26 + ord('a'))
                elif char.isupper():
                    new_char = chr(((ord(char) - ord('A')) + shift) % 26 + ord('A'))
                result.append(new_char)
                continue
            result.append(char)
        return ''.join(result)

    ciphertext = 'wyomdp{I0e_Ux0G_zim}'
    shift = 114514
    effective_shift = shift % 26

    plaintext = caesar_cipher_decrypt(ciphertext, effective_shift)
    print(plaintext)
    ```
    解得flag为`moectf{Y0u_Kn0W_pyc}`