# Using-tools-like-John-the-Ripper-for-password-cracking 

## AIM:
To crack password hashes using John the Ripper in Kali Linux.
## REQUIREMENTS:
- **Operating System:** Kali Linux / Ubuntu / Windows (with JtR binaries)
- **Tools:**
    - John the Ripper (Community/Pro version)
    - Hash generating tools (e.g., openssl, unshadow)
- **Test Data:**
    - /etc/shadow file (Linux hashed passwords)
    - Custom password-protected file (ZIP, RAR, etc.)
## ARCHITECTURE DIAGRAM:
```mermaid
flowchart TD
    A[Password Protected File / Hash] --> B[John the Ripper]
    B --> C[Select Attack Mode: Dictionary or Brute Force]
    C --> D[Load Wordlist / Charset Rules]
    D --> E[Password Cracking Process]
    E --> F[Recovered Passwords]
```
## DESIGN STEPS:
### Step 1: Install John the Ripper
```bash
sudo apt update
sudo apt install john -y
```

### Step 2: Prepare Hash File
- Extract hashes (Linux example):
```
unshadow /etc/passwd /etc/shadow > myhashes.txt
```
- For a ZIP file:
```
zip2john secret.zip > ziphash.txt
```
### Step 3: Run John the Ripper
- Dictionary Attack:
```
john --wordlist=/usr/share/wordlists/rockyou.txt myhashes.txt
```
- Brute Force (Incremental Mode):
```
john --incremental myhashes.txt
```
### Step 4: Show Cracked Passwords
```
john --show myhashes.txt
```
## PROGRAM:
 **Install the John Ripper**
  ```bash
  sudo apt install john
  ```
- **Create a Password-Protected ZIP File**
   Archive a normal file (secret.txt) into a password-protected ZIP file
   ```bash
   zip --password 123abc secret.txt.zip secret.txt
   ```
 - **Extract the Hash from the ZIP File**
   ```bash
   zip2john secret.txt.zip > zip_hash.txt
   ```
- **Crack the ZIP Password using John**
  ```bash
  john --format=zip zip_hash.txt
  ```
- **Show the Cracked Password**
  ```bash
  john --show zip_hash.txt

## OUTPUT:
### Create a Password-Protected ZIP File
![image](https://github.com/user-attachments/assets/38aafaf5-1e19-437e-b081-e65d7b87faaf)


### Extract the Hash from the ZIP File
![1](https://github.com/user-attachments/assets/f56d14b3-308b-46d1-a881-2949f3130fbf)

### Crack the ZIP Password using John
![2](https://github.com/user-attachments/assets/b5150b03-086b-4a42-b23c-6f6c2e19dea4)

![Screenshot 2025-04-25 130110](https://github.com/user-attachments/assets/e6726360-d5ea-44d2-8564-0e428a49a5d8)

### Show the Cracked Password
![Screenshot 2025-04-25 130116](https://github.com/user-attachments/assets/e212ed80-74a0-4532-ba3e-6bd015cde111)

## RESULT:
The password hashes were successfully cracked using John the Ripper.

