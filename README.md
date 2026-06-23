# CS-30: Project One Vulnerability Assessment Report

## Project Summary & Client Objectives
The core focus of this project was to conduct a comprehensive security review and modernization assessment for **Artemis Financial**, a fast-growing financial services firm. The primary objective was to safeguard their web-based financial tracking application against rising external threats and ensure adherence to rigorous data security requirements. By auditing the client's current software ecosystem, I mapped out critical threat vectors and designed a comprehensive technical mitigation roadmap to protect consumer financial records, maintain institutional trust, and achieve full alignment with secure industry standards.


## Reflective Assessment Q&A

### 1. How did you interpret the client's commercial needs and align them with security requirements?
* **Value of Secure Communications:** Protecting financial transaction data is fundamentally critical to Artemis Financial's market position, as any breach would result in catastrophic reputational damage and severe legal liability.
* **Regulatory Compliance:** The assessment specifically accounted for stringent government restrictions and international transaction frameworks, ensuring data handling satisfies mandates like the **Gramm-Leach-Bliley Act (GLBA)** and **PCI DSS** standards for handling sensitive financial records.
* **Modernization Framework:** To defend against current and imminent external threats, the application layer requirements were upgraded from unencrypted, legacy paradigms to dynamic, zero-trust cryptographic architectures.

### 2. What specific vulnerabilities were identified, and what tools or techniques did you use to discover them?
The assessment utilized a combination of static code reviews, dependency graphing, and threat modeling to isolate systematic weaknesses across the codebase. The primary vulnerabilities identified included:
* **Insecure Transport Channels:** The application originally accepted cleartext HTTP communication, exposing sensitive customer transaction traffic to packet-sniffing and man-in-the-middle (MitM) interception.
* **Broken Object Encapsulation:** Critical fields within application data models lacked strict access control boundaries, rendering them vulnerable to accidental or malicious modification.
* **Missing Environmental Mitigations:** The framework lacked built-in defenses against web-based exploit patterns like Cross-Site Request Forgery (CSRF) and did not maintain comprehensive audit logging for security events.

### 3. How did you approach the remediation strategy to make the codebase secure?
Remediation required establishing a layered defense-in-depth architecture across the codebase:
* **Encapsulation Enforcement:** All sensitive fields within application classes were reconfigured to be strictly `private`, restricting data interaction exclusively through validated getters and setters featuring built-in access controls.
* **Transport Layer Hardening:** Strict HTTPS/TLS enforcement was integrated by configuring the server environment to block cleartext loops and forcefully redirect all traffic over secure, encrypted communication ports.
* **State & Event Safeguards:** Spring Security configurations were introduced to enable native Cross-Site Request Forgery (CSRF) protection, alongside a detailed security logging utility to track authentication attempts and critical data mutations.

### 4. What went particularly well, and what did you find challenging during this assessment?
* **Successes:** Translating abstract, high-level compliance needs (like regulatory data privacy laws) into concrete, actionable engineering steps inside the Java application layer was highly successful.
* **Challenges:** Balancing the enforcement of strict security boundaries (such as input validation and encryption handshakes) without degrading application performance or disrupting the existing business logic flow presented a significant technical hurdle.

### 5. How will you apply the secure programming mindsets and practices learned here to future projects?
This project cemented the mindset that **security is an active, continuous lifecycle** rather than a secondary phase added after development. Moving forward, I will implement static application security testing (SAST) tools early in the development pipeline, explicitly enforce strong access encapsulation as a baseline coding practice, and systematically leverage well-vetted, industry-standard cryptographic libraries rather than attempting custom implementations.


## Mitigations Matrix Reference
The following core security mitigations were established to transition Artemis Financial to a hardened operational baseline:

| Defense Level | Control Strategy | Security Objective |
| :--- | :--- | :--- |
| **Data Layer** | Object Encapsulation (`private` scopes) | Prevents unauthorized memory state modification. |
| **Network Layer** | Mandatory HTTPS/TLS Channel Restructuring | Eliminates eavesdropping and credential sniffing in transit. |
| **Session Layer** | Cryptographic CSRF Token Validation | Neutralizes malicious cross-site transaction hijacking. |
| **Operations Layer** | Automated Auditing & Security Event Logging | Establishes non-repudiation and immediate breach visibility. |
