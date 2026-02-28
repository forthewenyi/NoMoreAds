# NoMoreAds

Network-wide ad blocking and DNS privacy using a Raspberry Pi.

## How It Works

```
Your Devices -> Pi-hole (blocks ads) -> Unbound (resolves directly from root servers)
```

- **Pi-hole** blocks known ad/tracker/malware domains by returning `0.0.0.0`
- **Unbound** resolves everything else directly from root DNS servers — no third party involved

## What's Blocked

- **StevenBlack Hosts** — ads and trackers (~78k domains)
- **Hagezi TIF** — malware, phishing, scams, crypto mining (~600k domains)

## Stack

| Component | Role |
|-----------|------|
| Raspberry Pi OS | Headless, console only |
| Pi-hole v6 | DNS sinkhole + DHCP server |
| Unbound | Recursive DNS resolver (IPv4 + IPv6) |

## Recovery

1. Flash fresh Raspberry Pi OS
2. Install Pi-hole: `curl -sSL https://install.pi-hole.net | bash`
3. Copy `unbound/pi-hole.conf` to `/etc/unbound/unbound.conf.d/`
4. Add adlists from `pihole/adlists.txt` in Pi-hole settings
5. Run `pihole -g` to rebuild gravity
6. Set static IP and gravity cron: `echo "30 3 * * 0 /usr/local/bin/pihole -g" | sudo crontab -u pihole -`

## Links

- [Pi-hole Docs](https://docs.pi-hole.net/)
- [Unbound + Pi-hole Guide](https://docs.pi-hole.net/guides/dns/unbound/)
- [Hagezi Blocklists](https://github.com/hagezi/dns-blocklists)
- [StevenBlack Hosts](https://github.com/StevenBlack/hosts)
