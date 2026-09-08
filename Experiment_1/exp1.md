```python
def caesar_encrypt(plain_text,shift):
    res = ""
    shift = shift%26 
    for ch in plain_text:
        if ch.isalpha():
            if ch.isupper():
                base = ord("A")
            else:
                base = ord("a")   
            new_pos = (ord(ch)-base+shift)%26
            res += chr(new_pos + base)    
        else :
            res += ch
    return res


def caesar_decrypt(encrypted_text,shift):
    res = ""
    shift = shift%26
    for ch in encrypted_text:
        if ch.isalpha():
            if ch.isupper():
                base = ord("A")
            else:
                base = ord("a")    
            new_pos = (ord(ch)-base-shift)%26
            res += chr(new_pos + base)   
        else :
            res += ch
    return res

 
plain_text = input("enter text : ")
shift = int(input("enter no of shift : "))
key = input("enter plain_text key : ")
encrypted_text = caesar_encrypt(plain_text,shift)
print(f"encrypted : {encrypted_text}")
decrypted_text = caesar_decrypt(encrypted_text,shift)
print(f"decrypted : {decrypted_text}")
```

```python
def vigenere_encrypt(plain_text, key):

    result = ""
    key_idx = 0
    plain_text = plain_text.upper()
    key = key.upper()

    for ch in plain_text:
        key_ch = key[key_idx]

        text_pos = ord(ch) - ord("A")
        key_pos = ord(key_ch) - ord("A")

        new_pos = (text_pos + key_pos) % 26

        result += chr(new_pos + ord("A"))

        key_idx = key_idx + 1
        key_idx = key_idx % len(key)

    return result


decrypted_text = vigenere_encrypt(plain_text,shift)
print(f"decrypted : {decrypted_text}")
```
