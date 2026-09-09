```python
import hashlib


def generate_sha256(filename):
    with open(filename, "rb") as file:
        data = file.read()

    return hashlib.sha256(data).hexdigest()

with open("sample.txt", "w") as file:
    file.write("This is my original file.")

trusted_hash = generate_sha256("sample.txt")
print("Trusted SHA-256:", trusted_hash)


with open("sample.txt", "w") as file:
    file.write("This is my original file!")

new_hash = generate_sha256("sample.txt")

print("New SHA-256:    ", new_hash)

if new_hash == trusted_hash:
    print("Data Integrity Verified")
else:
    print("Data has been Modified")
```
