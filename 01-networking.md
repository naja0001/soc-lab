# Network Setup

## Lab Environment

This SOC lab uses two virtual machines:

| **Machine**    | **Role**          | **IP Address** |
| Ubuntu         | Target / Server   | `172.20.10.6` |
| Kali Linux     | Attacker          | `172.20.10.7` |

Both machines are connected to the same network:

```text
172.20.10.0/28
```

## Connectivity Test

Connectivity between Kali Linux and Ubuntu was tested using ICMP.

From Kali Linux:

```bash
ping -c 4 172.20.10.6
```

The test confirmed that Kali Linux can communicate with the Ubuntu server.

## Purpose

The network setup provides an isolated environment where security testing, attack simulation, log collection and security monitoring can be performed safely.

Kali Linux is used as the attacker machine, while Ubuntu is used as the target/server machine.
