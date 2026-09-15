```python
import hashlib
import secrets

# Shared secret key
secret_key = "mysecret"

# Generate a challenge
challenge = secrets.token_hex(8)

print("Server Challenge:", challenge)

# Client generates response
response = hashlib.sha256(
    (challenge + secret_key).encode()
).hexdigest()

print("Client Response:", response)

# Server verifies response
expected_response = hashlib.sha256(
    (challenge + secret_key).encode()
).hexdigest()

if response == expected_response:
    print("Authentication Successful")
else:
    print("Authentication Failed")

# Replay attack simulation
print("\nReplay Attack Simulation")

if challenge == challenge:
    print("Replay Attack Detected")
```
