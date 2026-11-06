# cross-platform-network-diagnostics
Two person hands-on ICMP ping and traceroute analysis between macOS and Windows.
# Cross-Platform Network Diagnostics: Ping & Traceroute Analysis

## Project Overview

This project explores network connectivity between two devices running different operating systems: macOS and Windows 11.

Using command-line networking utilities, I tested bidirectional communication, measured network latency and packet loss, and compared UDP-based and ICMP-based traceroute methods.

The experiment was conducted on a shared Wi-Fi network with permission from both device users.

## Objectives

- Identify local IPv4 addresses on macOS and Windows.
- Test bidirectional network connectivity using ICMP Echo Requests.
- Measure round-trip latency and packet loss.
- Investigate how traceroute identifies network paths.
- Compare the results of UDP and ICMP traceroute probes.

## Tools & Technologies

| Tool | Purpose |
|---|---|
| macOS Terminal | Execute networking commands |
| Windows Command Prompt | Perform Windows network diagnostics |
| `ipconfig` | Identify local IPv4 addresses |
| `ping` | Test connectivity and latency |
| `traceroute` | Trace network paths from macOS |
| ICMP | Send Echo Requests and receive Echo Replies |
| UDP | Default probe method for macOS traceroute |

## Network Environment

Two laptops were connected to the same campus Wi-Fi network.

- Device A: Apple MacBook Air running macOS
- Device B: HP laptop running Windows
- Network: Shared campus Wi-Fi
- IP addressing: Private IPv4 addresses

*Actual IP addresses have been replaced with placeholders for privacy.*

## Experiment 1: Identifying IP Addresses

On macOS, I executed:

```bash
ipconfig getifaddr en0
```

On Windows, my partner executed:

```powershell
ipconfig
```

These commands allowed us to identify each device's IPv4 address.

## Experiment 2: Testing Bidirectional Connectivity

From macOS to Windows:

```bash
ping -c 5 <WINDOWS_IP>
```

From Windows to macOS:

```powershell
ping <MAC_IP>
```

### Results

| Metric | macOS → Windows | Windows → macOS |
|---|---|---|
| Packets Sent | 5 | 4 |
| Packets Received | 5 | 4 |
| Packet Loss | 0% | 0% |
| Minimum Latency | 9.804 ms | 9 ms |
| Average Latency | 39.819 ms | 89 ms |
| Maximum Latency | 76.397 ms | 131 ms |

### Analysis

Both devices successfully exchanged ICMP Echo Requests and Replies.

Neither test experienced packet loss, demonstrating successful bidirectional ICMP connectivity.

However, the average latency differed between the two tests. Possible contributing factors include wireless interference, network congestion, device processing, and background network activity.

## Experiment 3: UDP Traceroute

I first executed the following command from macOS:

```bash
traceroute -n -m 10 -w 1 <WINDOWS_IP>
```

### Results

All ten tested hops displayed:

```text
* * *
```

The probes did not receive responses within the configured timeout.

This may occur when network devices or host firewalls filter traceroute traffic. The results alone do not establish the exact cause.

## Experiment 4: ICMP Traceroute

To investigate further, I changed the traceroute method to ICMP:

```bash
traceroute -I -n -m 10 -w 2 <WINDOWS_IP>
```

### Results

```text
1  <WINDOWS_IP>  40.479 ms  10.355 ms  9.273 ms
```

The destination responded at the first reported hop.

Unlike the original UDP traceroute, the ICMP-based traceroute successfully received replies from the target device.

### Technical Explanation

The difference between these tests demonstrates that network diagnostic results can depend on the protocol and probe method used.

The successful ICMP traceroute confirms that the destination responded to ICMP probes. It does not conclusively establish why the UDP probes received no replies.

## Key Findings

1. Successful ping replies confirmed bidirectional ICMP connectivity between macOS and Windows.
2. Both ping tests achieved 0% packet loss.
3. Round-trip latency varied between the two directions.
4. UDP traceroute received no responses within the tested hop limit.
5. ICMP traceroute successfully reached the destination at the first reported hop.
6. Different network diagnostic methods can produce different results on the same network.

## Skills Demonstrated

- TCP/IP networking fundamentals
- IPv4 addressing
- ICMP Echo Request and Echo Reply analysis
- Network latency and packet-loss measurement
- Cross-platform command-line troubleshooting
- Traceroute diagnostics
- Technical documentation

## Conclusion

This project provided hands-on experience analyzing network communication between macOS and Windows.

By performing ping tests and comparing traceroute methods, I gained a better understanding of network reachability, latency, packet loss, and how protocol differences affect diagnostic results.

The project reinforced foundational networking concepts relevant to cybersecurity, cloud infrastructure, and IT systems administration.

## Future Improvements

- Analyze authorized ICMP traffic using Wireshark.
- Compare connectivity over different network types.
- Investigate how firewalls affect network diagnostics.
- Explore DNS resolution and TCP connectivity testing.

---

**Project Type:** Networking / Cybersecurity Fundamentals  
**Experience Level:** Beginner  
**Environment:** macOS, Windows 11, Campus Wi-Fi
