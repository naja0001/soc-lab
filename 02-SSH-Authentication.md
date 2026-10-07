# SSH Authentication

## Objective

The purpose of this exercise was to configure and test SSH authentication between the Kali Linux attacker machine and the Ubuntu target machine.

The exercise also provides a security event that can later be monitored and investigated using Wazuh.

## Lab Environment

| **Machine** | **Role** | **IP Address** |
| **Kali Linux** | **Attacker** | **`172.20.10.7`** |
| **Ubuntu** | **Target / Server** | **`172.20.10.6`** |

SSH is configured to use port `22123`.

## SSH Configuration

The Ubuntu server was configured to allow SSH connections on port `22123`.

Password authentication was disabled:

```text
PasswordAuthentication no
```

Public key authentication was enabled:

```text
PubkeyAuthentication yes
```

This means that users authenticate using an SSH key instead of a password.

## Authentication Test

A connection was initiated from Kali Linux to the Ubuntu server using an ED25519 SSH key:

```bash
ssh -i ~/.ssh/id_ed25519 naja@172.20.10.6 -p 22123
```

The authentication was successful.

## Authentication Log

The successful authentication generated the following events on the Ubuntu server:

```text
Accepted publickey for naja from 172.20.10.7
pam_unix(sshd:session): session opened
```

## Log Analysis

| **Field** | **Value** |
|---|---|
| **Event** | **Successful SSH authentication** |
| **Username** | **`naja`** |
| **Source IP** | **`172.20.10.7`** |
| **Destination IP** | **`172.20.10.6`** |
| **Authentication method** | **Public key** |
| **SSH port** | **`22123`** |
| **Result** | **Successful** |

From a SOC perspective, the source IP, username, authentication method and result are important when determining whether a login was legitimate or suspicious.

## Failed Authentication Event

During the configuration process, an unsuccessful SSH authentication event was also recorded:

```text
User naja from 172.20.10.7 not allowed
Connection closed by invalid user naja
```

The issue was caused by an SSH configuration restriction requiring users to belong to the `group13` group.

The user was added to the required group, after which public-key authentication worked successfully.

## SOC Perspective

SSH authentication logs can provide useful information for security monitoring, including:

- Successful logins
- Failed login attempts
- Source IP addresses
- User accounts
- Authentication methods
- Repeated authentication failures

Repeated failed SSH authentication attempts could indicate activities such as brute-force attacks or password spraying.

These events will later be monitored using Wazuh as part of the SOC detection and investigation process.

## Next Step

The next step is to configure Wazuh to monitor the Ubuntu server and collect security events.

The planned workflow is:

```text
Kali Linux
    ↓
SSH Activity
    ↓
Ubuntu
    ↓
Wazuh Agent
    ↓
Wazuh Server
    ↓
Wazuh Dashboard
    ↓
Detection & Investigation
```
