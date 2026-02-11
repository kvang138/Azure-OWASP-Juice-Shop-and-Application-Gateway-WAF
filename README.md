# Securing an extremely vulnerable web application with a WAF

## 📖Introduction
In this project, I explored how to secure a vulnerable web application such the OWASP Juice Shop using a Web Application Firewall (WAF). The exercise bridges both offensive and defensive security perspectives: first, understanding how real-world attackers exploit flawed and vulnerable code, and then observing how a properly configured Azure WAF can significantly mitigate the risk without requiring any modifications to the application itself.

## 🛠️⚙️Components
- OWASP Juice Shop as an Azure containerized instance (ACI).
- Application Gateway (WAF)
- Log Analytics Workspace
- Microsoft Sentinel

## ❌🛡️Before Implementing the Compensating Control
Prior to the WAF implementation, the application exhibited critical authentication vulnerabilities and multiple exploitable attack surfaces. (See screenshot below for an example of a successful unauthorized access attempt.)


## 🔐🛡️After Implementing the Compensating Control
By placing the vulnerable OWASP Juice Shop application behind an Azure WAF (configured in prevention mode with the OWASP ruleset enabled), I observed effective real-time blocking of common attacks, including:
 - SQL injection
 - Cross-site scripting (XSS)
 - Command injection
 - Path traversal / local/remote file inclusion
 - Insecure deserialization attempts
 - And many other OWASP Top 10 vulnerabilities.

The WAF intercepted and blocked malicious payloads that previously succeeded against the unprotected application, returning HTTP 403 responses or otherwise denying access. (See screenshots below.)

## Screenshots
Before implementing the WAF.
![Before implementing the WAF.](https://github.com/kvang138/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF/blob/main/Screenshots/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF%201.png)

![Before implementing the WAF.](https://github.com/kvang138/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF/blob/main/Screenshots/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF%202.png)

After implementing the WAF.
![Before implementing the WAF.](https://github.com/kvang138/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF/blob/main/Screenshots/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF%203.png)

The Application Gateway Firewall log showing the attack getting blocked.
![The Application Gateway Firewall log showing the attack getting blocked.](https://github.com/kvang138/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF/blob/main/Screenshots/Azure-OWASP-Juice-Shop-and-Application-Gateway-WAF%204.png)

## Conclusion
It is worth noting that even an extremely vulnerable web application's attack surfaces can be dramatically reduced when placed behind a properly configured WAF. This compensating control provides substantial protection without necessitating code changes, patches, or refactoring—making it especially valuable for legacy systems or applications in rapid deployment scenarios. That said, a WAF is not 100% foolproof. Sophisticated or novel attack techniques may evade signature-based or rules-based detection, and zero-day vulnerabilities or logic flaws beyond the scope of typical WAF capabilities can still pose risks. True security requires a defense-in-depth strategy, combining WAF protection with secure coding practices, regular vulnerability scanning, input validation, least-privilege access controls, monitoring, and timely patching.
This project highlights the practical value of WAFs as a strong layer in modern application security—especially when time or resources for full remediation are limited.
