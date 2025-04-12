Mobile Application Security Assessment: InsecureBankv2

Introduction

In this project, I performed a security assessment on the InsecureBankv2 Android application. The goal was to identify and exploit common security vulnerabilities, specifically in insecure data storage, insecure communication, and insecure authentication mechanisms. The assessment was conducted using Android Studio, ADB (Android Debug Bridge), and Burp Suite.

Objective:
•	Identify common security vulnerabilities in the InsecureBankv2 app.
•	Exploit the vulnerabilities to demonstrate how they can be used to compromise the application’s security.
•	Provide recommendations for securing the application.

Tools Used
•	Android Studio: IDE for Android app development and debugging.
•	ADB (Android Debug Bridge): A command-line tool used for managing Android devices and performing tasks such as installing apps, extracting data, and interacting with the emulator.
•	Burp Suite: A web vulnerability scanner and interception proxy used to analyze and manipulate web traffic for testing insecure communication.

1. Insecure Data Storage

Vulnerability Identified:
Insecure storage of sensitive information such as user credentials (username and password) in SharedPreferences was identified. This data was being stored in plaintext, making it vulnerable to unauthorized access.

Exploit:
•	Data Stored in SharedPreferences: The app stored sensitive data such as usernames and passwords in SharedPreferences without proper encryption.
•	Using Android Studio and ADB, I accessed the data stored in SharedPreferences from the emulator:
o	Opened the Device File Explorer in Android Studio.
o	Navigated to /data/data/com.insecurebankv2/shared_prefs/ directory.
o	Extracted the mySharedPreferences.xml file, which contained sensitive user data.

![Image](https://github.com/user-attachments/assets/8d17b7c8-e50e-452e-a38f-a2df6e9b2d76)

Recommendation:
•	Use EncryptedSharedPreferences instead of plain SharedPreferences to securely store sensitive data.
•	Encrypt passwords and other sensitive information before storing them in any form of persistent storage.

2. Insecure Communication

Vulnerability Identified:
The application communicates with the backend server without proper encryption (i.e., using HTTP instead of HTTPS), making it vulnerable to man-in-the-middle (MITM) attacks.

Exploit:
•	Burp Suite was configured as an interception proxy to capture the network traffic between the app and the server.
•	I configured the Android emulator's proxy settings to route traffic through Burp Suite.
•	After inspecting the traffic, I was able to capture sensitive information such as login credentials sent in plaintext over HTTP.

Steps to intercept traffic using Burp Suite:
1.	Set Burp Suite’s proxy listener to listen on port 8080.
2.	Configure the Android Emulator’s Wi-Fi proxy settings to route traffic through Burp Suite (IP 10.0.2.2 and port 8080).
3.	Install Burp Suite's CA certificate on the Android emulator to intercept HTTPS traffic.
4.	Capture the HTTP requests and responses to identify any sensitive data being sent in clear text.

![Image](https://github.com/user-attachments/assets/0f62c17b-bb03-4d2f-8b1c-059a70fa127b)

Recommendation:
•	Always use HTTPS for communication between the app and the server to protect data in transit.
•	Ensure the app properly validates server certificates to prevent man-in-the-middle (MITM) attacks.

3. Insecure Authentication Mechanisms

Vulnerability Identified:
The application lacked robust authentication mechanisms. There were issues with password storage, login bypass, and brute-force attacks.

Exploit:
•	Weak Password Handling: Passwords were stored in plaintext and sent over the network without encryption.
•	I used Burp Suite to test for login bypass by manipulating request parameters in HTTP traffic and replaying requests to test authentication bypass.

Testing:
•	I attempted brute-force login attempts using Burp Suite’s Intruder tool to test the strength of the login mechanism.
•	The application did not have protections against brute-force attacks (such as rate-limiting or CAPTCHAs), making it susceptible to an attack.

![Image](https://github.com/user-attachments/assets/b73ed1cf-ff57-4e8e-9c88-10826afd7e0e)

Recommendation:
•	Implement secure password hashing (e.g., using bcrypt or PBKDF2) for storing passwords.
•	Use multi-factor authentication (MFA) to improve security during the login process.
•	Implement rate-limiting and CAPTCHA to protect against brute-force attacks.

Conclusion
The security assessment of the InsecureBankv2 Android application revealed several critical vulnerabilities related to insecure data storage, insecure communication, and insecure authentication mechanisms. These vulnerabilities can potentially allow an attacker to compromise sensitive user data and gain unauthorized access to the application.

Key Recommendations:
1.	Secure Data Storage: Use EncryptedSharedPreferences for storing sensitive information such as passwords.
2.	Secure Communication: Ensure that all communication between the app and the server is done over HTTPS with proper certificate validation.
3.	Strong Authentication: Use secure password hashing algorithms and implement multi-factor authentication (MFA) to strengthen the authentication mechanism.

Next Steps:
•	Apply the recommended security measures to the application.
•	Conduct further security testing to ensure the implementation of proper security practices.

Code Modification

Before: I decompiled the application and looked at the strings. There is a setting called is_admin, and it is set to no.

![Image](https://github.com/user-attachments/assets/56988e75-14fc-4318-9c97-871024671ca3)

AFTER: What about if I set it to yes and recompile the application?

![Image](https://github.com/user-attachments/assets/f9454701-1f8b-40c7-a84e-3605abe7a157)

![Image](https://github.com/user-attachments/assets/b1cfd83d-283a-45e1-8765-ddd0378a8cf7)

As you can see, the create user button appeared

How to Run This Security Assessment
To replicate this security assessment, follow these steps:
1.	Set up the InsecureBankv2 app on an Android Emulator:
o	Clone the repository: git clone https://github.com/dineshshetty/Android-InsecureBankv2.git.
o	Open the project in Android Studio and set up the environment.
2.	Set up Burp Suite to intercept traffic:
o	Install Burp Suite on your machine.
o	Configure the Android Emulator to use Burp Suite as a proxy.
o	Install Burp's CA certificate on the emulator to intercept HTTPS traffic.
3.	Perform the security tests:
o	Test insecure data storage using ADB and Android Studio.
o	Test insecure communication using Burp Suite.
o	Test insecure authentication by manipulating requests in Burp Suite.
________________________________________



