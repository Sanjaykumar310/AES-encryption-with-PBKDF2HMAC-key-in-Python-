# 🔐 AES & RSA Encryption Toolkit with API Integration

This repository provides a complete solution for symmetric and asymmetric encryption using AES (CBC/GCM) and RSA. It includes a Python module for local encryption/decryption, benchmarking support for large messages, and seamless API integration with a remote server for RSA operations.

---

## 📚 Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Usage](#usage)
- [Large Input Support](#large-input-support)
- [API Integration](#api-integration)
  - [RSA Key Fetching](#rsa-key-fetching)
  - [Encrypt and Decrypt via API](#encrypt-and-decrypt-via-api)
- [API Endpoint Overview](#api-endpoint-overview)
- [Sample Output](#sample-output)
- [Performance and Memory Monitoring](#performance-and-memory-monitoring)
- [Edge Case Testing](#edge-case-testing)
- [Security Considerations](#security-considerations)
- [Acknowledgements](#acknowledgements)

---

## 🚀 Features

- 🔐 AES-256 Encryption in CBC and GCM modes.
- 🛡️ RSA Encryption via Public Key API.
- 📡 Remote Encryption & Decryption using HTTP APIs.
- 📊 Benchmarking and memory profiling with `memory_profiler`.
- 📁 Secure large-message handling (50MB+).
- ✅ Unit tests for encryption/decryption integrity and failure scenarios.

---

## 🏗️ Architecture

                        |
                        V
              +--------------------------+
              |       RSA API Server     |
              |                          |
              | GET /get-rsa-key         |
              | POST /encrypt-rsa        |
              | POST /decrypt-rsa        |
              | POST /encrypt-aes        |
              | POST /decrypt-aes        |
              +--------------------------+

---

## 🧑‍💻 Usage

```python
from encryption import AESCipher

# AES CBC Encryption Example
cipher = AESCipher("my_secure_password", os.urandom(16), mode="CBC")
encrypted = cipher.encrypt("Hello, World!")
decrypted = cipher.decrypt(encrypted)
run_aes_operations(mode='CBC', iteration_count=2)

length = 5 * 10**7  # 50 million characters
message = ''.join(random.choices(string.ascii_letters, k=length))
run_aes_operations(mode='GCM', iteration_count=1, custom_message=message, message_print_limit=10)

response = requests.get(f"{API_URL}/v1/encryption/get-rsa-key")
public_key_pem = b64decode(response.json()['publicKey'])

# Encrypt
requests.post(f"{API_URL}/v1/encryption/encrypt-rsa", json={"message": msg, "publicKey": b64encode(pub_key).decode()})

# Decrypt
requests.post(f"{API_URL}/v1/encryption/decrypt-rsa", json={"encryptedMessage": encrypted_msg})

Original Message (CBC): CBC secret message
Encrypted (CBC): ... base64 string ...
Decrypted (CBC): CBC secret message
Elapsed Time (CBC): 0.001234 seconds
Memory Usage: 0.050Mb
