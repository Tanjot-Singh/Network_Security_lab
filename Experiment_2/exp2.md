```python
import hashlib


def generate_sha256(filename):
    with open(filename, "rb") as file:
        data = file.read()

    return hashlib.sha256(data).hexdigest()


# 1. Create sample.txt with known content
with open("sample.txt", "w") as file:
    file.write("This is my original file.")


# 2. Generate and record the trusted SHA-256 hash
trusted_hash = generate_sha256("sample.txt")

print("Trusted SHA-256:", trusted_hash)


# 3. Change one character
with open("sample.txt", "w") as file:
    file.write("This is my original file!")


# Calculate hash again
new_hash = generate_sha256("sample.txt")

print("New SHA-256:    ", new_hash)


# 4. Compare against trusted reference hash
if new_hash == trusted_hash:
```
    print("Data Integrity Verified")
else:
    print("Data has been Modified")
