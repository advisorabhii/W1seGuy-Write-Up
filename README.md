# W1seGuy XOR Solver (Pure Python)

def xor_bytes(data, key):
    result = b""
    for i in range(len(data)):
        result += bytes([data[i] ^ key[i % len(key)]])
    return result


# 🔹 Paste XOR hex from nc here
cipher_hex = "022c290e3f6705081b3b131c10343b2250071e2c170a16462e3a281d1d1a24101d453a241c2b0732"

cipher = bytes.fromhex(cipher_hex)

# Known plaintext
known = b"THM{"

# Recover first 4 key characters
key_first4 = bytes([cipher[i] ^ known[i] for i in range(4)])

# Recover 5th key character using '}'
key_5th = bytes([cipher[-1] ^ ord('}')])

# Full key
key = key_first4 + key_5th

# Decrypt full flag
plaintext = xor_bytes(cipher, key)

print("[+] Recovered key:", key.decode())
print("[+] Decrypted flag:", plaintext.decode())
