# Network Setup

## Lab Environment

This SOC lab uses two virtual machines:
| **Machine** | **Role**        | **IP Address** |
| Ubuntu      | Target / Server | 172.20.10.3    |
| Kali Linux  | Attacker        | 172.20.10.4    |

Both machines are connected to the same network:

`172.20.10.0/28`

## Connectivity Test

Connectivity between Kali Linux and Ubuntu was tested using ICMP:

```bash
ping -c 4 172.20.10.3
```

The purpose of this setup is to create an isolated environment where security testing and log analysis can be performed safely.
