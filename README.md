```markdown
# Logstash FortiGate Pipeline

Logstash configuration for ingesting FortiGate firewall logs into Elasticsearch with automatic categorization.

## Indices

| Index | Description                                             |
|-------|---------------------------------------------------------|
| `fortigate-traffic-*` | Forward, local, and snat traffic logs   |
| `fortigate-vpn-*`     | SSL-VPN and IPsec tunnel logs           |
| `fortigate-users-*`   | Authentication and captive portal logs  |
| `fortigate-utm-*`     | Antivirus, web filter, IPS, app control |
| `fortigate-event-*`   | System, HA, and endpoint events         |
| `fortigate-other-*`   | Uncategorized logs                      |

## Requirements

- Logstash 8.x
- Elasticsearch 8.x
- GeoIP database (bundled with Logstash)

## FortiGate Configuration

config log syslogd setting
    set status enable
    set server "<LOGSTASH_IP>"
    set port 5515
    set mode udp
    set format default
end

## Features

- Parses FortiGate `key=value` log format
- Routes logs into separate daily indices by category
- GeoIP enrichment for source and destination IPs
- Timestamp normalization from FortiGate `eventtime`
- Handles slash-separated numeric values (e.g. `251/203`)
```
