# PF Firewall

This repository contains a PF (Packet Filter) firewall script for enhancing the security of your system. PF is a powerful firewall included with macOS that allows you to control network traffic and protect your system from unauthorized access.

## Features

- **Strict Filtering**: The firewall script implements a set of rules to block unwanted network traffic, preventing unauthorized access to your system.
- **Customizable**: You can easily modify the script to add or remove rules according to your specific security requirements.
- **Easy Integration**: The script is designed to be seamlessly integrated with the PF firewall utility on macOS, making it easy to apply and manage.

## Breakdown

These rules aim to provide a baseline level of security by allowing essential network services and blocking potentially malicious or unwanted traffic. However, it's important to review and customize the rules based on your specific needs and security requirements.

Options: This section specifies various configuration options for the firewall, such as the block policy, fingerprints file, skipping interfaces, and state policy.

Normalization: The "scrub in all no-df" rule enables packet scrubbing for incoming packets. This helps to normalize and sanitize the packets by removing any IP options and ensuring they don't have the "Don't Fragment" (DF) flag set.

Queueing: This section is empty in the provided script.

Translation: This section is empty in the provided script.

Filtering: The remaining rules focus on filtering network traffic:

Antispoof: The "antispoof" rule logs and quickly blocks any traffic with spoofed source addresses. It helps prevent attackers from using fake or forged IP addresses.

Block by default: The "block in log" rule blocks incoming traffic and logs it. This acts as a default deny rule, ensuring that only explicitly allowed traffic is permitted.

Block to/from illegal destinations or sources: The "block in log quick from no-route to any" rule blocks incoming traffic from illegal or unreachable destinations. It prevents traffic from sources that are not part of a valid route table.

Allow critical system traffic: The "pass in quick inet proto udp from any port 67 to any port 68" rule allows DHCP traffic, which is essential for network configuration.

Allow DNS traffic: The "pass in log inet proto { udp, tcp } from any port 53 to any" rule allows incoming DNS (Domain Name System) traffic, both UDP and TCP. It enables DNS queries to be processed by the system.

Allow outgoing web traffic: The "pass out inet proto tcp from any to any port { 80, 443 } keep state" rule permits outgoing web traffic over HTTP (port 80) and HTTPS (port 443).

Allow outgoing DNS traffic: The "pass out inet proto udp from any to any port 53 keep state" rule allows outgoing DNS queries from the system.

Allow outgoing VPN traffic: The "pass out inet proto udp from any to any port 51820 keep state" rule permits outgoing VPN (WireGuard) traffic over UDP on port 51820.

Allow MDNS traffic: The "pass in log inet proto udp from any to any port 5353 keep state" rule allows incoming MDNS (Multicast DNS) traffic, which is used for service discovery on local networks.

Limit inbound traffic: The "block in log" rule logs and blocks inbound traffic that doesn't match any of the preceding allow rules.


## Usage

To apply the PF firewall script on your macOS system, follow these steps:

1. Open a terminal window.
2. Copy the entire script and save it to `pf.conf`. Usually found in the /etc/ directory (/etc/pf.conf)
3. Run the following command to load the firewall script `sudo pfctl -ef pf.conf`

Note: You will be prompted to enter your administrator password.

## Contributing

Contributions to the PF Firewall project are welcome. If you find any issues or have suggestions for improvement, feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE). See the LICENSE file for more details.

## Disclaimer

This firewall script is provided as-is, without any warranties or guarantees. Use it at your own risk. The author and the contributors are not responsible for any damages or losses resulting from the use of this script.

---
**Note**: The effectiveness of a firewall depends on proper configuration and regular updates. It is recommended to consult with security professionals and keep the firewall rules up to date to ensure the highest level of security for your system.

