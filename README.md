

> Network traffic capture and analysis CLI with protocol distribution, top talkers, and bandwidth visualization.

*This is a quick overview — security theory, architecture, and full walkthroughs are in the [learn modules](#learn).*

## What It Does

- Capture live network traffic on any interface with configurable packet counts
- Real-time protocol distribution analysis with percentage breakdowns
- Top talkers identification showing most active IP addresses by traffic volume
- Bandwidth calculation with bytes sent/received per endpoint
- Verbose mode displays individual packet flow with source/destination details
- Built on Scapy for deep packet inspection and protocol parsing

## Quick Start

```bash
uv tool install netanal
sudo netanal capture -i eth0 -c 100
```

> [!TIP]
> This project uses [`just`](https://github.com/casey/just) as a command runner. Type `just` to see all available commands.
>
> Install: `curl -sSf https://just.systems/install.sh | bash -s -- --to ~/.local/bin`

## Commands

| Command | Description |
|---------|-------------|
| `netanal capture` | Live packet capture with protocol analysis, top talkers, and bandwidth stats |

## Learn

This project includes step-by-step learning materials covering security theory, architecture, and implementation.

| Module | Topic |
|--------|-------|
| [00 - Overview](learn/00-OVERVIEW.md) | Prerequisites and quick start |
| [01 - Concepts](learn/01-CONCEPTS.md) | Security theory and real-world breaches |
| [02 - Architecture](learn/02-ARCHITECTURE.md) | System design and data flow |
| [03 - Implementation](learn/03-IMPLEMENTATION.md) | Code walkthrough |
| [04 - Challenges](learn/04-CHALLENGES.md) | Extension ideas and exercises |

![Capture Summary](screenshots/capture-summary.png)
![Packet Flow](screenshots/packet-flow.png)
![First Capture](screenshots/first-capture.png)
## License

AGPL 3.0
