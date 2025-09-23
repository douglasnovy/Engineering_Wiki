---
title: Communication_Protocols
consolidated: true
sources: 2
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
**Secure Communications Between StackVision and 8864 Devices**

---

## Overview
Secure communications between StackVision servers and 8864 devices are critical for ensuring data integrity, confidentiality, and reliable remote access in industrial monitoring and control environments. Beginning with firmware version 5.02, the 8864 supports a secure communication method based on SSH reverse tunneling, eliminating the need for inbound firewall penetration. This approach, combined with strong encryption, authentication, and key management practices, provides a robust framework for secure data exchange.

---

## Key Concepts

### Reverse SSH Tunneling
- **Definition**: A secure communication method where the client (8864) initiates and maintains an SSH tunnel to the server (StackVision).
- **Purpose**: Enables secure, port-specific VPN-like connections without requiring inbound firewall rules.
- **Directionality**: Connection is initiated outbound from the 8864 to the StackVision server.

### Public/Private Key Authentication
- **RSA-2048 Keys**: Used for mutual authentication between the 8864 and StackVision server.
- **Key Exchange**: Public keys are exchanged and installed on both ends; private keys remain secure and are never transmitted.
- **Security Implication**: Public keys can be distributed over insecure channels, but installation must be strictly controlled.

### Encryption and Integrity
- **AES-128 Encryption**: Ensures confidentiality of transmitted data.
- **HMAC-SHA256 Signing**: Provides message integrity verification.
- **Diffie-Hellman Key Exchange**: Used for establishing session keys securely.

---

## Technical Details

1. **Connection Establishment**:
   - On boot, the 8864 device initiates an outbound SSH connection to the StackVision server.
   - The reverse tunnel acts as a secure conduit for specific ports, similar to a VPN.

2. **Firewall Considerations**:
   - No inbound ports need to be opened on the firewall between the 8864 and StackVision server.
   - Only outbound connections from the 8864 are required, reducing attack surface.

3. **Authentication Process**:
   - Each 8864 has a unique RSA-2048 key pair.
   - The public key of the 8864 must be installed on the StackVision server’s SSH configuration.
   - The StackVision server’s public key must be installed on each 8864.
   - Keys must be monitored to prevent unauthorized access.

4. **Encryption and Signing**:
   - Data is encrypted using AES-128.
   - Messages are signed with HMAC-SHA256 for integrity.
   - Diffie-Hellman is used for secure session key negotiation.

5. **Port Configuration**:
   - StackVision server inbound ports for Modbus communication may be configured depending on client/server roles.
   - If unused, certain ports can be closed to further enhance security.

---

## Best Practices

- **Key Management**:
  - Maintain strict control over key installation and updates.
  - Regularly audit installed keys to detect and remove rogue entries.

- **Firewall Configuration**:
  - Ensure outbound SSH connections from the 8864 are permitted.
  - Keep unused ports closed to minimize exposure.

- **Encryption Standards**:
  - Use AES-128 for data encryption and HMAC-SHA256 for integrity checks.
  - Ensure Diffie-Hellman parameters are strong and up-to-date.

- **Firmware Updates**:
  - Keep 8864 firmware updated to leverage the latest security features.
  - Verify compatibility between StackVision server and 8864 firmware versions.

- **Monitoring and Logging**:
  - Enable logging of SSH tunnel connections for auditing and troubleshooting.
  - Monitor for unusual connection patterns that may indicate security issues.

---

## Source Attribution

- **Document 1 (Mark Shell, 2021)**:  
  Provided detailed explanation of reverse SSH tunneling implementation in 8864 firmware v5.02, key installation procedures, firewall considerations, and RSA-2048 authentication.

- **Document 2 (2016)**:  
  Contributed encryption and signing specifications (AES-128, HMAC-SHA256), Diffie-Hellman key exchange details, and port configuration guidelines for StackVision network connections.

---

Would you like me to also include a **diagram** showing the reverse SSH tunnel architecture between the 8864 and StackVision server? This could make the consolidated entry more visually clear.

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
