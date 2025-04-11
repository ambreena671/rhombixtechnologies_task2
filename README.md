# rhombixtechnologies_task2

# InsecureBankv2 Security Assessment

This repository contains the security assessment report and findings for the **InsecureBankv2** mobile application. The security assessment identifies and exploits vulnerabilities in **insecure data storage**, **insecure communication**, and **insecure authentication mechanisms**.

## Tools Used:
- **Android Studio**: IDE for Android development.
- **ADB**: Android Debug Bridge for interacting with the emulator.
- **Burp Suite**: Web vulnerability scanner and interception proxy for testing network communication.

## Findings:
- **Insecure Data Storage**: User credentials stored in plain text in SharedPreferences.
- **Insecure Communication**: Unencrypted traffic sent over HTTP.
- **Insecure Authentication**: Weak authentication with no brute-force protection.

## Recommendations:
1. Use **EncryptedSharedPreferences** for sensitive data storage.
2. Use **HTTPS** for secure communication.
3. Implement **multi-factor authentication** and **rate-limiting** for secure authentication.


