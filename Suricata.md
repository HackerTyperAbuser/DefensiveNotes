Validating Suricata configuration
```bash
suricata -T -c /etc/suricata/suricata.yaml
```
Post-mortem PCAP
```bash
suricata -r <PCAP>
```