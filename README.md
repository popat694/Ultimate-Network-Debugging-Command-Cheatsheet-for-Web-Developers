# Ultimate Network Debugging Command Cheatsheet for Web Developers

## Basic Connectivity Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ping <host>` | Test basic connectivity to host | `ping google.com` | Add `-c 4` to limit to 4 packets |
| `ping -6 <host>` | Test IPv6 connectivity | `ping -6 ipv6.google.com` | Verify IPv6 connectivity |
| `traceroute <host>` | Show network path to host | `traceroute example.com` | Linux/macOS command |
| `tracert <host>` | Windows version of traceroute | `tracert example.com` | Windows command |
| `mtr <host>` | Combine ping and traceroute in real-time monitoring | `mtr github.com` | More comprehensive than traceroute |
| `pathping <host>` | Windows alternative to mtr | `pathping example.com` | Windows advanced traceroute |
| `curl -I <URL>` | Fetch HTTP headers only | `curl -I https://example.com` | Quick way to check status code |
| `wget -S <URL>` | Fetch and show server response headers | `wget -S https://example.com` | Alternative to curl |

## DNS Troubleshooting

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `dig <domain>` | Query DNS records | `dig example.com` | Linux/macOS command |
| `dig <domain> <record_type>` | Query specific DNS record | `dig example.com MX` | Check mail records |
| `dig +short <domain>` | Show only the answer | `dig +short example.com` | Simplified output |
| `dig +trace <domain>` | Follow entire DNS resolution path | `dig +trace example.com` | Debug DNS delegation |
| `dig @<nameserver> <domain>` | Query specific nameserver | `dig @8.8.8.8 example.com` | Test against Google DNS |
| `dig -x <IP>` | Reverse DNS lookup | `dig -x 93.184.216.34` | Get hostname from IP |
| `nslookup <domain>` | Interactive DNS queries | `nslookup example.com` | Works on Windows too |
| `nslookup -type=<record_type> <domain>` | Query specific record | `nslookup -type=TXT example.com` | Check TXT records |
| `host <domain>` | Simple DNS lookup | `host example.com` | Quick output format |
| `whois <domain>` | Look up domain registration info | `whois example.com` | Registration details |
| `dnsmasq-leases` | Check DHCP leases (if using dnsmasq) | `cat /var/lib/misc/dnsmasq.leases` | Local DNS debugging |

## Network Configuration

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ifconfig` | Display network interfaces (legacy) | `ifconfig` | Being deprecated |
| `ip addr` | Modern way to display network interfaces | `ip addr show` | Preferred over ifconfig |
| `ipconfig` | Windows network interface info | `ipconfig /all` | Windows equivalent |
| `ip route` | Show routing table | `ip route show` | Linux routing info |
| `route` | Legacy way to display routing table | `route -n` | Works on older systems |
| `route print` | Windows routing table | `route print` | Windows routing info |
| `netstat -tuln` | List active listening ports | `netstat -tuln` | Legacy command |
| `ss -tuln` | Modern alternative to netstat | `ss -tuln` | More efficient than netstat |
| `sudo lsof -i :<port>` | Find process using a port | `sudo lsof -i :3000` | Identify port usage |
| `netstat -anb` | Windows command to find process using port | `netstat -anb` | Requires admin |
| `arp -a` | Show ARP cache | `arp -a` | View IP-to-MAC mappings |
| `ip neigh` | Modern way to show ARP cache | `ip neigh show` | Neighbor table |

## Advanced Network Analysis

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `tcpdump -i <interface>` | Capture packets on interface | `tcpdump -i eth0 port 80` | Powerful packet capture |
| `tcpdump -i <interface> -w <file>` | Capture to file | `tcpdump -i eth0 -w capture.pcap` | For Wireshark analysis |
| `tcpdump host <host>` | Filter by host | `tcpdump host 192.168.1.1` | Target specific host |
| `tcpdump port <port>` | Filter by port | `tcpdump port 443` | Target specific port |
| `tshark -i <interface>` | CLI version of Wireshark | `tshark -i eth0 -f "port 80"` | Rich filtering options |
| `nmap <target>` | Scan ports and services | `nmap 192.168.1.1` | Basic host scan |
| `nmap -sV <target>` | Detect service versions | `nmap -sV example.com` | Service fingerprinting |
| `nmap -p 1-65535 <target>` | Scan all ports | `nmap -p 1-65535 192.168.1.1` | Comprehensive scan |
| `nmap -A <target>` | Aggressive scan (OS, versions, scripts) | `nmap -A 192.168.1.1` | Detailed scan |
| `netcat -zv <host> <port>` | Test if specific port is open | `netcat -zv example.com 443` | Basic port check |
| `nc -zv <host> <port-range>` | Check range of ports | `nc -zv example.com 20-25` | Scan port range |
| `openssl s_client -connect <host:port>` | Test SSL/TLS connections | `openssl s_client -connect example.com:443` | TLS debugging |

## HTTP Analysis and API Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -v <URL>` | Verbose HTTP request details | `curl -v https://example.com` | See request/response |
| `curl -vk <URL>` | Verbose with SSL certificate bypass | `curl -vk https://self-signed.example.com` | For SSL issues |
| `curl -I <URL>` | Show response headers only | `curl -I https://example.com` | Quick status check |
| `curl -o /dev/null -w "%{http_code}" <URL>` | Return only HTTP status code | `curl -o /dev/null -w "%{http_code}" https://example.com` | Status code only |
| `curl -X POST -d "data" <URL>` | POST request with data | `curl -X POST -d "name=test" https://example.com/api` | Basic POST |
| `curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' <URL>` | POST JSON data | `curl -X POST -H "Content-Type: application/json" -d '{"user":"test"}' https://api.example.com/users` | API testing |
| `curl --compressed <URL>` | Request compressed content | `curl --compressed https://example.com` | Gzip support |
| `httpie <URL>` | User-friendly HTTP client | `http POST api.example.com/users name=John` | Easier than curl |
| `httpie -v <URL>` | Verbose mode with httpie | `http -v GET api.example.com/users` | Colored output |
| `curl -w "@curl-format.txt" <URL>` | Custom timing data (with format file) | `curl -w "@curl-format.txt" https://example.com` | Detailed timings |

## Performance Analysis

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `iperf3 -c <server>` | Measure network throughput | `iperf3 -c iperf.example.com` | Bandwidth test |
| `iperf3 -c <server> -R` | Measure download throughput | `iperf3 -c iperf.example.com -R` | Download test |
| `iperf3 -c <server> -u` | UDP bandwidth test | `iperf3 -c iperf.example.com -u` | Test UDP performance |
| `time curl -s <URL> > /dev/null` | Simple response time test | `time curl -s https://example.com > /dev/null` | Quick performance check |
| `httping -c 10 <URL>` | HTTP ping to measure latency | `httping -c 10 https://example.com` | HTTP-specific latency |
| `siege -c 10 -t 30S <URL>` | Website load testing | `siege -c 10 -t 30S https://example.com` | Concurrent connections |
| `ab -n 100 -c 10 <URL>` | Apache Bench load testing | `ab -n 100 -c 10 https://example.com/` | Basic load test |
| `wrk -t12 -c400 -d30s <URL>` | Modern HTTP benchmarking | `wrk -t12 -c400 -d30s https://example.com` | More powerful than ab |
| `vegeta attack -rate=10 -duration=30s -targets=targets.txt` | HTTP load testing | Create targets.txt with URLs first | Scriptable load testing |
| `k6 run script.js` | Advanced load testing | Create script.js with test scenarios | Full testing framework |

## Content Debugging and Manipulation

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl <URL> \| jq` | Fetch JSON and pretty print | `curl https://api.example.com/users \| jq` | JSON prettifier |
| `curl <URL> \| jq '.property'` | Extract specific JSON field | `curl https://api.example.com/users \| jq '.[0].name'` | JSON parsing |
| `curl <URL> \| python -m json.tool` | Alternative JSON pretty printing | `curl https://api.example.com/users \| python -m json.tool` | Without jq |
| `curl -L <URL>` | Follow redirects | `curl -L http://example.com` | Trace redirect chains |
| `curl -A "UserAgent" <URL>` | Set custom user agent | `curl -A "Mozilla/5.0" https://example.com` | Browser simulation |
| `curl -e "Referer" <URL>` | Set referer header | `curl -e "https://google.com" https://example.com` | Test referer policies |
| `curl -b "name=value" <URL>` | Send cookies | `curl -b "session=abc123" https://example.com` | Session testing |
| `curl -c cookies.txt <URL>` | Save cookies to file | `curl -c cookies.txt https://example.com/login` | Cookie persistence |
| `curl -H "X-Custom-Header: value" <URL>` | Add custom header | `curl -H "Authorization: Bearer token123" https://api.example.com` | API auth testing |

## Proxy and Security Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -x http://proxy:port <URL>` | Use HTTP proxy | `curl -x http://10.0.0.1:8080 https://example.com` | Through HTTP proxy |
| `curl --proxy-ntlm -x http://proxy:port <URL>` | NTLM proxy auth | `curl --proxy-ntlm -x http://proxy:8080 https://example.com` | Corporate proxies |
| `curl --socks5 proxy:port <URL>` | Use SOCKS5 proxy | `curl --socks5 127.0.0.1:9050 https://example.com` | Through SOCKS |
| `curl -k <URL>` | Skip SSL certificate verification | `curl -k https://self-signed.example.com` | Dev environments |
| `curl --cert cert.pem --key key.pem <URL>` | Client certificate authentication | `curl --cert client.pem --key client.key https://example.com` | Mutual TLS |
| `openssl s_client -connect <host:port> -servername <hostname>` | Test SNI support | `openssl s_client -connect example.com:443 -servername secure.example.com` | SNI debugging |
| `openssl s_client -connect <host:port> -showcerts` | Show certificate chain | `openssl s_client -connect example.com:443 -showcerts` | Cert chain debugging |
| `openssl x509 -in cert.pem -text -noout` | View certificate details | `openssl x509 -in certificate.crt -text -noout` | Inspect certificates |
| `mitmproxy -p 8080` | Interactive HTTPS proxy | `mitmproxy -p 8080` | API debugging |
| `bettercap` | Network attack framework | `sudo bettercap -iface eth0` | Security testing |

## HTTP/2 and HTTP/3 Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl --http2 -I <URL>` | Test HTTP/2 support | `curl --http2 -I https://example.com` | HTTP/2 headers |
| `curl --http2-prior-knowledge <URL>` | Force HTTP/2 | `curl --http2-prior-knowledge https://example.com` | Skip negotiation |
| `curl --http3 <URL>` | Test HTTP/3 support (if compiled with HTTP/3) | `curl --http3 https://example.com` | QUIC protocol |
| `curl --alt-svc alt-svc.cache <URL>` | Use Alt-Svc cache | `curl --alt-svc alt-svc.cache https://example.com` | HTTP/3 discovery |
| `nghttp -nv <URL>` | HTTP/2 debugging tool | `nghttp -nv https://example.com` | HTTP/2 details |
| `nghttp -v <URL>` | Verbose HTTP/2 debug | `nghttp -v https://example.com` | Protocol analysis |
| `h2load <URL>` | HTTP/2 load testing | `h2load -n 100 -c 10 https://example.com` | HTTP/2 benchmarking |

## Websocket Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `websocat ws://host:port` | Connect to WebSocket server | `websocat ws://localhost:8080/socket` | Interactive websocket |
| `websocat --text ws://host:port` | Text mode for WebSockets | `websocat --text ws://localhost:8080/socket` | Human-readable |
| `websocat -v ws://host:port` | Verbose websocket connection | `websocat -v ws://localhost:8080/socket` | Debug connection |
| `wscat -c ws://host:port` | Alternative WebSocket client | `wscat -c ws://localhost:8080` | Node.js tool |
| `wscat --auth user:pass -c ws://host:port` | Websocket with basic auth | `wscat --auth admin:password -c ws://api.example.com/socket` | Authentication |
| `curl -i -N -H "Connection: Upgrade" -H "Upgrade: websocket" <URL>` | Raw WebSocket handshake | `curl -i -N -H "Connection: Upgrade" -H "Upgrade: websocket" -H "Sec-WebSocket-Key: SGVsbG8sIHdvcmxkIQ==" -H "Sec-WebSocket-Version: 13" https://ws.example.com` | Manual handshake |

## CDN and Cache Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -H "Pragma: no-cache" <URL>` | Bypass cache | `curl -H "Pragma: no-cache" https://example.com` | Force origin request |
| `curl -H "Cache-Control: no-cache" <URL>` | Modern cache bypass | `curl -H "Cache-Control: no-cache" https://example.com` | HTTP/1.1 cache control |
| `curl -s -w "%{time_connect} - %{time_starttransfer} - %{time_total}\n" <URL>` | Timing breakdown | `curl -s -w "%{time_connect} - %{time_starttransfer} - %{time_total}\n" https://example.com` | Performance metrics |
| `curl -H "X-Cache-Debug: 1" <URL>` | CDN cache debugging | `curl -H "X-Cache-Debug: 1" https://example.com` | Works with some CDNs |
| `curl -r 0-0 <URL>` | Check if server supports range requests | `curl -r 0-0 https://example.com/large-file.zip` | Partial content |
| `curl -I <URL> && curl -I <URL>` | Compare multiple requests | `curl -I https://example.com && curl -I https://example.com` | Check cache headers |

## Mobile and Responsive Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -A "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X)" <URL>` | Simulate iPhone | `curl -A "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X)" https://example.com` | Mobile user agent |
| `curl -A "Mozilla/5.0 (Linux; Android 10)" <URL>` | Simulate Android | `curl -A "Mozilla/5.0 (Linux; Android 10)" https://example.com` | Android user agent |
| `lighthouse <URL>` | Google Lighthouse CLI | `lighthouse https://example.com --output json --output-path ./report.json` | Performance analysis |
| `curl -H "Save-Data: on" <URL>` | Test Save-Data support | `curl -H "Save-Data: on" https://example.com` | Data saving mode |

## Container and Microservices Networking

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `docker network ls` | List Docker networks | `docker network ls` | Container networking |
| `docker network inspect <network>` | Inspect Docker network | `docker network inspect bridge` | Network details |
| `kubectl get services` | List Kubernetes services | `kubectl get services` | K8s networking |
| `kubectl describe service <service>` | Describe K8s service | `kubectl describe service frontend` | Service details |
| `kubectl port-forward <pod> <localport:podport>` | Forward pod port | `kubectl port-forward mypod 8080:80` | Local access |
| `istioctl analyze` | Analyze Istio configuration | `istioctl analyze` | Service mesh |

## API Gateway and Service Mesh

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -H "debug: true" <URL>` | Debug headers for API gateways | `curl -H "debug: true" https://api.example.com` | Works with some gateways |
| `grpcurl -plaintext localhost:50051 list` | List gRPC services | `grpcurl -plaintext localhost:50051 list` | gRPC introspection |
| `grpcurl -plaintext localhost:50051 describe` | Describe gRPC service | `grpcurl -plaintext localhost:50051 describe example.Service` | Service details |
| `linkerd check` | Check Linkerd service mesh | `linkerd check` | Service mesh health |
| `linkerd top deployment/<name>` | Realtime metrics | `linkerd top deployment/web` | Traffic analysis |

## Web Application Debugging

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -H "Accept-Encoding: gzip" --compressed <URL>` | Test gzip compression | `curl -H "Accept-Encoding: gzip" --compressed https://example.com` | Compression check |
| `curl -H "Accept-Encoding: br" --compressed <URL>` | Test Brotli compression | `curl -H "Accept-Encoding: br" --compressed https://example.com` | Brotli support |
| `curl -w 'Response: %{size_download} bytes, Time: %{time_total}s\n' <URL>` | Basic performance metrics | `curl -w 'Response: %{size_download} bytes, Time: %{time_total}s\n' https://example.com` | Quick stats |
| `lighthouse <URL> --only-categories=performance` | Performance audit | `lighthouse https://example.com --only-categories=performance` | Web perf analysis |
| `curl -H "Origin: https://example.org" -I <URL>` | Test CORS headers | `curl -H "Origin: https://example.org" -I https://api.example.com` | CORS debugging |
| `curl -X OPTIONS -H "Origin: https://example.org" <URL>` | CORS preflight check | `curl -X OPTIONS -H "Origin: https://example.org" https://api.example.com` | Preflight request |

## DNS Over HTTPS (DoH) and DNS Over TLS (DoT)

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -H 'accept: application/dns-json' 'https://dns.google/resolve?name=example.com&type=A'` | Query DoH | `curl -H 'accept: application/dns-json' 'https://dns.google/resolve?name=example.com&type=A'` | Google DoH |
| `kdig @8.8.8.8 +tls example.com` | Query DoT | `kdig @8.8.8.8 +tls example.com` | Knot DNS utility |
| `doggo example.com @https://cloudflare-dns.com/dns-query` | Modern DNS client | `doggo example.com @https://cloudflare-dns.com/dns-query` | Supports DoH |

## Server Push and Resource Hints

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `nghttp -ns <URL>` | View HTTP/2 server push | `nghttp -ns https://example.com` | Server push analysis |
| `curl -I <URL>` | Check for Link headers | `curl -I https://example.com` | Preload/prefetch hints |

## GraphQL API Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -X POST -H "Content-Type: application/json" -d '{"query": "{ viewer { login } }"}' <URL>` | Basic GraphQL query | `curl -X POST -H "Content-Type: application/json" -d '{"query": "{ viewer { login } }"}' https://api.github.com/graphql` | Simple query |
| `curl -X POST -H "Content-Type: application/json" -d @query.json <URL>` | GraphQL from file | `curl -X POST -H "Content-Type: application/json" -d @query.json https://api.example.com/graphql` | Complex queries |

## Security Headers and CSP Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -I <URL> \| grep -i "content-security-policy"` | Check CSP header | `curl -I https://example.com \| grep -i "content-security-policy"` | Security policy |
| `curl -I <URL> \| grep -i "strict-transport-security"` | Check HSTS header | `curl -I https://example.com \| grep -i "strict-transport-security"` | HTTPS enforcement |
| `curl -I <URL> \| grep -i "x-frame-options"` | Check X-Frame-Options | `curl -I https://example.com \| grep -i "x-frame-options"` | Clickjacking protection |
| `curl -I <URL> \| grep -i "x-content-type-options"` | Check X-Content-Type-Options | `curl -I https://example.com \| grep -i "x-content-type-options"` | MIME sniffing protection |

## Service Worker and PWA Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -I <URL>/sw.js` | Check service worker | `curl -I https://example.com/sw.js` | SW availability |
| `curl -I <URL>/manifest.json` | Check web manifest | `curl -I https://example.com/manifest.json` | PWA manifest |
| `lighthouse <URL> --only-categories=pwa` | PWA audit | `lighthouse https://example.com --only-categories=pwa` | PWA compliance |

## WebRTC Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `webrtc-internals` | Chrome WebRTC debug | Open in Chrome browser: chrome://webrtc-internals/ | In-browser tool |
| `stun-client stun.l.google.com 19302` | Test STUN connectivity | `stun-client stun.l.google.com 19302` | NAT traversal |

## Cross-browser Network Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36" <URL>` | Chrome user agent | `curl -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36" https://example.com` | Browser simulation |
| `curl -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:93.0) Gecko/20100101 Firefox/93.0" <URL>` | Firefox user agent | `curl -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:93.0) Gecko/20100101 Firefox/93.0" https://example.com` | Firefox simulation |
| `curl -A "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)" <URL>` | Googlebot user agent | `curl -A "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)" https://example.com` | SEO testing |

## Frontend Performance Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `curl -w "@curl-format.txt" -o /dev/null -s <URL>` | Detailed timing metrics | Create curl-format.txt with timing variables | Performance analysis |
| `webpagetest <URL>` | WebPageTest CLI | `webpagetest test https://example.com` | Comprehensive testing |
| `pagespeed <URL>` | Google PageSpeed CLI | `pagespeed https://example.com` | Performance suggestions |


## SSH Basic Commands

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh <user>@<host>` | Connect to remote host | `ssh user@example.com` | Basic connection |
| `ssh -p <port> <user>@<host>` | Connect on non-standard port | `ssh -p 2222 user@example.com` | Custom port |
| `ssh -i <key_file> <user>@<host>` | Connect using identity file | `ssh -i ~/.ssh/id_rsa user@example.com` | Key authentication |
| `ssh -v <user>@<host>` | Verbose connection (debugging) | `ssh -v user@example.com` | Basic debugging |
| `ssh -vv <user>@<host>` | More verbose output | `ssh -vv user@example.com` | Detailed debugging |
| `ssh -vvv <user>@<host>` | Maximum verbosity | `ssh -vvv user@example.com` | Full debug output |
| `ssh -4 <user>@<host>` | Force IPv4 | `ssh -4 user@example.com` | IPv4 only |
| `ssh -6 <user>@<host>` | Force IPv6 | `ssh -6 user@example.com` | IPv6 only |

## SSH Authentication & Key Management

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh-keygen` | Generate SSH key pair | `ssh-keygen` | Creates RSA key by default |
| `ssh-keygen -t ed25519` | Generate Ed25519 key (more secure) | `ssh-keygen -t ed25519` | Modern algorithm |
| `ssh-keygen -t rsa -b 4096` | Generate 4096-bit RSA key | `ssh-keygen -t rsa -b 4096` | Strong RSA key |
| `ssh-keygen -p -f <key_file>` | Change passphrase | `ssh-keygen -p -f ~/.ssh/id_rsa` | Update protection |
| `ssh-copy-id <user>@<host>` | Copy public key to server | `ssh-copy-id user@example.com` | Setup key auth |
| `ssh-copy-id -i <key_file.pub> <user>@<host>` | Copy specific key | `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@example.com` | Install specific key |
| `ssh-add <key_file>` | Add key to SSH agent | `ssh-add ~/.ssh/id_rsa` | Cache credentials |
| `ssh-add -l` | List keys in SSH agent | `ssh-add -l` | View loaded keys |
| `ssh-add -D` | Delete all keys from agent | `ssh-add -D` | Clear agent |
| `ssh-add -t <seconds> <key_file>` | Add key with timeout | `ssh-add -t 3600 ~/.ssh/id_rsa` | Temporary auth |
| `ssh-keygen -lf <key_file>` | Display key fingerprint | `ssh-keygen -lf ~/.ssh/id_rsa.pub` | Verify key |
| `ssh-keygen -R <hostname>` | Remove host from known_hosts | `ssh-keygen -R example.com` | Reset host key |

## SSH Configuration & Security

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh -o "IdentitiesOnly=yes" <user>@<host>` | Use only specified keys | `ssh -o "IdentitiesOnly=yes" -i key.pem user@example.com` | Prevent agent keys |
| `ssh -o "PubkeyAuthentication=no" <user>@<host>` | Disable public key auth | `ssh -o "PubkeyAuthentication=no" user@example.com` | Password only |
| `ssh -o "StrictHostKeyChecking=no" <user>@<host>` | Bypass host key checking | `ssh -o "StrictHostKeyChecking=no" user@example.com` | Security risk! |
| `ssh -o "ServerAliveInterval=60" <user>@<host>` | Keep connection alive | `ssh -o "ServerAliveInterval=60" user@example.com` | Prevent timeouts |
| `ssh -o "ConnectTimeout=10" <user>@<host>` | Set connection timeout | `ssh -o "ConnectTimeout=10" user@example.com` | Faster failures |
| `ssh -o "UserKnownHostsFile=/dev/null" <user>@<host>` | Don't save host keys | `ssh -o "UserKnownHostsFile=/dev/null" user@example.com` | Ephemeral connections |
| `chmod 600 <key_file>` | Set correct permissions for key | `chmod 600 ~/.ssh/id_rsa` | Required security |
| `chmod 700 ~/.ssh` | Set correct permissions for .ssh | `chmod 700 ~/.ssh` | Directory protection |

## SSH File Transfer & Port Forwarding

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `scp <file> <user>@<host>:<path>` | Copy file to remote host | `scp file.txt user@example.com:~/` | Basic file transfer |
| `scp <user>@<host>:<path> <local_path>` | Copy from remote host | `scp user@example.com:~/file.txt ./` | Download file |
| `scp -r <directory> <user>@<host>:<path>` | Copy directory recursively | `scp -r ./docs user@example.com:~/` | With subdirectories |
| `scp -P <port> <file> <user>@<host>:<path>` | SCP on custom port | `scp -P 2222 file.txt user@example.com:~/` | Non-standard port |
| `scp -i <key_file> <file> <user>@<host>:<path>` | SCP with identity file | `scp -i key.pem file.txt user@example.com:~/` | Key authentication |
| `scp -C <file> <user>@<host>:<path>` | SCP with compression | `scp -C large-file.zip user@example.com:~/` | Faster transfers |
| `scp -l <limit> <file> <user>@<host>:<path>` | Limit bandwidth (Kbit/s) | `scp -l 1000 file.txt user@example.com:~/` | Throttle transfer |
| `ssh -L <local_port>:<target_host>:<target_port> <user>@<host>` | Local port forwarding | `ssh -L 8080:localhost:80 user@example.com` | Forward local port |
| `ssh -R <remote_port>:<target_host>:<target_port> <user>@<host>` | Remote port forwarding | `ssh -R 8080:localhost:3000 user@example.com` | Reverse tunnel |
| `ssh -D <port> <user>@<host>` | Dynamic port forwarding (SOCKS proxy) | `ssh -D 1080 user@example.com` | Local SOCKS proxy |
| `ssh -N -L <local_port>:<target_host>:<target_port> <user>@<host>` | Port forwarding only (no shell) | `ssh -N -L 8080:internal-server:80 user@jumphost.com` | Quiet tunneling |
| `ssh -J <jumphost> <destination>` | ProxyJump (SSH through bastion) | `ssh -J user@jumphost.com user@internal-server` | Jump host connection |

## SSH Client Configuration

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `vim ~/.ssh/config` | Edit SSH config file | Various host configurations | Client config |
| `chmod 600 ~/.ssh/config` | Set correct config permissions | `chmod 600 ~/.ssh/config` | Required security |

## SSH Config File Examples

```
# Basic host configuration
Host example
    HostName example.com
    User username
    Port 22
    IdentityFile ~/.ssh/id_rsa

# Jump host configuration
Host internal
    HostName internal-server
    User admin
    ProxyJump jumpuser@jumphost.com

# Keep connections alive
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 120

# Port forwarding in config
Host tunnel
    HostName example.com
    User username
    LocalForward 8080 localhost:80
```

## SFTP Basic Commands

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `sftp <user>@<host>` | Connect to SFTP server | `sftp user@example.com` | Interactive session |
| `sftp -P <port> <user>@<host>` | Connect on non-standard port | `sftp -P 2222 user@example.com` | Custom port (capital P) |
| `sftp -i <key_file> <user>@<host>` | Connect using identity file | `sftp -i ~/.ssh/id_rsa user@example.com` | Key authentication |
| `sftp -o "IdentitiesOnly=yes" -i <key_file> <user>@<host>` | Use only specified key | `sftp -o "IdentitiesOnly=yes" -i key.pem user@example.com` | Force specific key |
| `sftp -b <batch_file> <user>@<host>` | Batch mode using commands file | `sftp -b commands.txt user@example.com` | Automated transfers |
| `echo "put file.txt" | sftp user@example.com` | Pipe commands to sftp | Uploads file.txt | One-liner operation |

## SFTP Interactive Commands

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ls` | List remote directory contents | `ls` | View files |
| `lls` | List local directory contents | `lls` | Local files |
| `cd <dir>` | Change remote directory | `cd uploads` | Remote navigation |
| `lcd <dir>` | Change local directory | `lcd Downloads` | Local navigation |
| `pwd` | Print remote working directory | `pwd` | Remote location |
| `lpwd` | Print local working directory | `lpwd` | Local location |
| `get <remote_file> [local_file]` | Download file | `get data.csv` | Basic download |
| `get -r <directory>` | Download directory recursively | `get -r project` | Download folder |
| `put <local_file> [remote_file]` | Upload file | `put report.pdf` | Basic upload |
| `put -r <directory>` | Upload directory recursively | `put -r images` | Upload folder |
| `mkdir <directory>` | Create remote directory | `mkdir backups` | Make directory |
| `rmdir <directory>` | Remove remote directory | `rmdir old_backups` | Remove directory |
| `rm <file>` | Delete remote file | `rm obsolete.txt` | Delete file |
| `chmod <mode> <file>` | Change permissions | `chmod 644 config.txt` | File permissions |
| `chown <owner>:<group> <file>` | Change ownership | `chown www:www index.html` | Change owner |
| `rename <old> <new>` | Rename remote file | `rename old.txt new.txt` | Rename file |
| `!<command>` | Execute local shell command | `!ls -la` | Run local command |
| `bye` or `exit` or `quit` | Exit SFTP session | `exit` | Close connection |
| `help` | Show available commands | `help` | Command reference |

## SFTP Automation

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `echo -e "cd /upload\nput file.txt" > commands.txt` | Create batch file | Creates SFTP script | Line by line commands |
| `sftp -b commands.txt user@example.com` | Execute batch file | Automated operation | Non-interactive |
| `lftp -c "open -u user,password sftp://example.com; mirror -R local remote"` | Mirror directory (upload) | Syncs local to remote | Using lftp (alternative) |
| `lftp -c "open -u user,password sftp://example.com; mirror remote local"` | Mirror directory (download) | Syncs remote to local | Using lftp (alternative) |

## SMTP Basic Verification Commands

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `dig MX <domain>` | Look up mail exchange records | `dig MX example.com` | Find mail servers |
| `dig +short MX <domain>` | Concise MX lookup | `dig +short MX example.com` | Prioritized list |
| `nslookup -type=MX <domain>` | Alternative MX lookup | `nslookup -type=MX example.com` | Works on Windows |
| `host -t MX <domain>` | Simple MX record query | `host -t MX example.com` | Quick check |
| `dig TXT <domain>` | Look up TXT records (SPF, DKIM, DMARC) | `dig TXT example.com` | Mail authentication |
| `dig +short TXT <domain>` | Concise TXT lookup | `dig +short TXT example.com` | Readable format |
| `dig TXT _dmarc.<domain>` | Look up DMARC record | `dig TXT _dmarc.example.com` | DMARC policy |
| `nslookup -type=TXT <domain>` | Alternative TXT lookup | `nslookup -type=TXT example.com` | Windows alternative |
| `host -t TXT <domain>` | Simple TXT record query | `host -t TXT example.com` | Quick check |

## SMTP Server Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `telnet <mail_server> 25` | Connect to SMTP server | `telnet smtp.example.com 25` | Basic connection |
| `openssl s_client -connect <mail_server>:465` | Connect to SMTPS (SSL) | `openssl s_client -connect smtp.example.com:465` | Secure connection |
| `openssl s_client -starttls smtp -connect <mail_server>:587` | Connect with STARTTLS | `openssl s_client -starttls smtp -connect smtp.example.com:587` | TLS upgrade |
| `openssl s_client -connect <mail_server>:465 -showcerts` | View certificate chain | `openssl s_client -connect smtp.gmail.com:465 -showcerts` | SSL verification |
| `swaks --to user@example.com --from test@example.com --server smtp.example.com` | Test email sending | Simple test email | SMTP Swiss Army Knife |
| `swaks --to user@example.com --from test@example.com --server smtp.example.com --tls` | Test with TLS | Secure test email | TLS testing |
| `swaks --to user@example.com --from test@example.com --server smtp.example.com --auth LOGIN --auth-user user --auth-password pass` | Test with authentication | Authenticated test | With credentials |

## Manual SMTP Conversation

```
# After connecting with telnet or openssl:

EHLO example.com
# View supported capabilities

MAIL FROM:<sender@example.com>
# Set sender address

RCPT TO:<recipient@example.com>
# Set recipient address

DATA
# Start message content
Subject: Test Message

This is a test message.
.
# End with a single period on its own line

QUIT
# End session
```

## Email Verification and Validation

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `echo "VRFY user@example.com" | nc <mail_server> 25` | Verify mailbox exists | `echo "VRFY john@example.com" | nc smtp.example.com 25` | May be disabled |
| `echo "EXPN listname" | nc <mail_server> 25` | Expand mailing list | `echo "EXPN sales" | nc smtp.example.com 25` | Often disabled |
| `emailhippo check <email>` | Online verification API | `emailhippo check test@example.com` | Third-party service |
| `mailcheck <email>` | Email verification tool | `mailcheck user@example.com` | Command line tool |

## SPF, DKIM, and DMARC Validation

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `dig +short TXT <domain>` | Check SPF record | `dig +short TXT example.com` | Look for "v=spf1" |
| `dig +short TXT _dmarc.<domain>` | Check DMARC record | `dig +short TXT _dmarc.example.com` | DMARC policy |
| `dig +short TXT selector._domainkey.<domain>` | Check DKIM record | `dig +short TXT default._domainkey.example.com` | DKIM public key |
| `opendkim-testkey -d <domain> -s <selector> -vvv` | Test DKIM key | `opendkim-testkey -d example.com -s default -vvv` | Validate DKIM |
| `swaks --to test@example.com --from user@yourdomain.com --server smtp.example.com --header "DKIM-Signature: testing"` | Test with DKIM header | For testing only | Headers testing |

## Mail Queue Management

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `mailq` | Display mail queue (Postfix/Sendmail) | `mailq` | View outgoing queue |
| `postqueue -p` | Display Postfix mail queue | `postqueue -p` | Postfix specific |
| `postsuper -d ALL` | Delete all messages in queue | `postsuper -d ALL` | Postfix purge |
| `postsuper -d <queue_id>` | Delete specific message | `postsuper -d 8F3D94C67` | Remove message |
| `postcat -q <queue_id>` | View message content | `postcat -q 8F3D94C67` | Postfix content |
| `exim -bp` | Display Exim mail queue | `exim -bp` | Exim specific |
| `exim -M <message_id>` | Force delivery attempt | `exim -M 1a2b3c-0004c2-Ty` | Exim retry |
| `qshape` | Show Postfix queue by domains | `qshape` | Queue analysis |

## Mail Server Logs

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `tail -f /var/log/mail.log` | Monitor mail log | `tail -f /var/log/mail.log` | Common location |
| `tail -f /var/log/maillog` | Monitor mail log (RHEL/CentOS) | `tail -f /var/log/maillog` | RHEL systems |
| `grep "recipient@example.com" /var/log/mail.log` | Search for recipient | `grep "user@example.com" /var/log/mail.log` | Track message |
| `grep "status=sent" /var/log/mail.log` | Find successful deliveries | `grep "status=sent" /var/log/mail.log` | Sent messages |
| `grep "status=bounced" /var/log/mail.log` | Find bounced messages | `grep "status=bounced" /var/log/mail.log` | Failed deliveries |
| `zgrep "recipient@example.com" /var/log/mail.log.*` | Search compressed logs | `zgrep "user@example.com" /var/log/mail.log.*` | Historical search |

## Email Security Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `smtp-user-enum -M VRFY -U users.txt -t <mail_server>` | Enumerate users | `smtp-user-enum -M VRFY -U users.txt -t smtp.example.com` | Security testing |
| `nmap --script smtp-commands <mail_server>` | Check SMTP commands | `nmap --script smtp-commands smtp.example.com` | Server capabilities |
| `nmap --script smtp-open-relay <mail_server>` | Test for open relay | `nmap --script smtp-open-relay smtp.example.com` | Security check |
| `nmap --script smtp-enum-users <mail_server>` | Enumerate users | `nmap --script smtp-enum-users smtp.example.com` | User discovery |
| `checktls --smtp <mail_server>` | Test TLS configuration | `checktls --smtp smtp.example.com` | Security assessment |

## Advanced SSH Techniques

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh -T git@github.com` | Test SSH keys with GitHub | `ssh -T git@github.com` | Repository access |
| `ssh-keyscan <host>` | Get host's public keys | `ssh-keyscan github.com` | Key fingerprints |
| `ssh-keyscan -t rsa <host>` | Get specific key type | `ssh-keyscan -t rsa example.com` | RSA keys only |
| `ssh -Q cipher` | List supported ciphers | `ssh -Q cipher` | Security options |
| `ssh -Q mac` | List supported MACs | `ssh -Q mac` | Message auth codes |
| `ssh -Q kex` | List supported key exchanges | `ssh -Q kex` | KEX algorithms |
| `ssh -Q key` | List supported key types | `ssh -Q key` | Public key types |
| `ssh-audit <host>` | Audit SSH server security | `ssh-audit example.com` | Security assessment |
| `ssh <user>@<host> 'bash -s' < local_script.sh` | Run local script on remote host | `ssh user@example.com 'bash -s' < backup.sh` | Remote execution |
| `ssh <user>@<host> "cat > remote_file" < local_file` | Transfer file via SSH | `ssh user@example.com "cat > config.txt" < local_config.txt` | Simple transfer |
| `tar czf - folder | ssh <user>@<host> "tar xzf - -C /dest"` | Transfer directory via tar+SSH | `tar czf - docs | ssh user@example.com "tar xzf - -C /var/www"` | Efficient transfer |
| `ssh -o ControlMaster=auto -o ControlPath=~/.ssh/control:%h:%p:%r -o ControlPersist=yes <user>@<host>` | Enable connection sharing | Multiple connections use single TCP connection | Performance |

## SSH Agent Forwarding

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh -A <user>@<host>` | Enable agent forwarding | `ssh -A user@example.com` | Security risk! |
| `ssh-add -c` | Add key with confirmation | `ssh-add -c ~/.ssh/id_rsa` | Safer forwarding |
| `ssh -o ForwardAgent=yes <user>@<host>` | Alternative agent forwarding | `ssh -o ForwardAgent=yes user@example.com` | Config option |

## SSH X11 Forwarding

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh -X <user>@<host>` | Enable X11 forwarding | `ssh -X user@example.com` | Run GUI apps |
| `ssh -Y <user>@<host>` | Trusted X11 forwarding | `ssh -Y user@example.com` | Less secure |
| `ssh -o ForwardX11=yes <user>@<host>` | Alternative X11 forwarding | `ssh -o ForwardX11=yes user@example.com` | Config option |

## SFTP Advanced Examples

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `sftp -o "IdentityFile=~/.ssh/id_rsa" -o "Port=2222" user@example.com` | Multiple options | Connect with custom settings | Combined options |
| `sftp -l 1000 <user>@<host>` | Limit bandwidth (KB/s) | `sftp -l 1000 user@example.com` | Throttle transfer |
| `lftp sftp://user@example.com` | Alternative SFTP client | Interactive with more features | Advanced client |
| `lftp -e "mirror -R localdir remotedir" sftp://user@example.com` | Mirror directories with lftp | Upload directory | Synchronization |
| `rsync -avz -e ssh ./localdir/ user@example.com:/remotedir/` | Rsync over SSH | Efficient directory sync | Better than sftp |
| `sshfs user@example.com:/remote/dir /local/mountpoint` | Mount remote filesystem | `sshfs user@example.com:/home/user/docs ~/remote-docs` | FUSE mounting |
| `fusermount -u /local/mountpoint` | Unmount sshfs filesystem | `fusermount -u ~/remote-docs` | Cleanup |

## SSH Jump Hosts & Proxy Commands

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `ssh -J <jumphost> <destination>` | SSH via jump host | `ssh -J user@jumphost.com user@internal-server` | Multi-hop SSH |
| `ssh -J <jump1>,<jump2> <destination>` | Multiple jump hosts | `ssh -J user@jump1.com,user@jump2.com user@destination` | Chain connections |
| `ssh -o ProxyCommand="ssh -W %h:%p jumpuser@jumphost.com" user@destination` | ProxyCommand alternative | `ssh -o ProxyCommand="ssh -W %h:%p jumpuser@jumphost.com" user@internal-server` | Pre-OpenSSH 7.3 |
| `ssh -o ProxyCommand="nc -X 5 -x proxy:1080 %h %p" user@destination` | SSH via SOCKS proxy | `ssh -o ProxyCommand="nc -X 5 -x localhost:1080 %h %p" user@example.com` | Through SOCKS |
| `ssh -o ProxyCommand="corkscrew http-proxy 8080 %h %p" user@destination` | SSH via HTTP proxy | `ssh -o ProxyCommand="corkscrew proxy.company.com 8080 %h %p" user@example.com` | Through HTTP proxy |

## SMTP Common Errors & Troubleshooting

| Error | Description | Troubleshooting |
|-------|-------------|----------------|
| `Connection refused` | Server not accepting connections | Check firewall, server running, correct port |
| `Connection timed out` | No response from server | Network issues, server down, firewall blocking |
| `501 5.1.7 Bad sender address syntax` | Invalid sender email | Check email format, quotation marks |
| `550 5.1.1 User unknown` | Recipient does not exist | Verify email address, check for typos |
| `550 5.7.1 Relay denied` | Not authorized to relay | Authentication required, use SMTP auth |
| `454 4.7.1 Temporary authentication failure` | Auth problem | Check credentials, TLS requirements |
| `535 5.7.8 Authentication failed` | Wrong username/password | Verify credentials, check for app passwords |
| `421 4.7.0 Too many concurrent SMTP connections` | Connection limit reached | Reduce simultaneous connections |
| `452 4.2.2 Mailbox full` | Recipient's mailbox full | Contact recipient |
| `451 4.4.1 SMTP server is busy` | Temporary server issue | Retry later, check server status |
| `550 5.7.1 Message rejected as spam` | Content flagged as spam | Check content, sender reputation |
| `554 5.7.1 Relay access denied` | Not allowed to send | Use authenticated SMTP |

## Common Mail Server Ports

| Port | Protocol | Description | Notes |
|------|----------|-------------|-------|
| 25 | SMTP | Standard email submission (unencrypted) | Often blocked by ISPs |
| 465 | SMTPS | SMTP over SSL | Implicit SSL/TLS |
| 587 | Submission | Modern email submission (with STARTTLS) | Preferred for sending |
| 110 | POP3 | Post Office Protocol (unencrypted) | Mail retrieval |
| 995 | POP3S | POP3 over SSL | Secure mail retrieval |
| 143 | IMAP | Internet Message Access Protocol (unencrypted) | Mail access |
| 993 | IMAPS | IMAP over SSL | Secure mail access |

## SMTP Status Codes

| Code | Meaning | Example |
|------|---------|---------|
| 2xx | Success | 250 OK |
| 3xx | Partial success, more actions needed | 354 Start mail input |
| 4xx | Temporary failure | 421 Service not available |
| 5xx | Permanent failure | 550 Mailbox unavailable |

## Email Authentication Tools

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `spfquery --ip=<IP> --sender=<email> --helo=<domain>` | Check SPF | `spfquery --ip=192.0.2.1 --sender=user@example.com --helo=mail.example.com` | SPF validation |
| `opendkim-testkey -d <domain> -s <selector> -k <keyfile>` | Test DKIM key | `opendkim-testkey -d example.com -s mail -k /etc/dkim/mail.private` | DKIM verification |
| `opendmarc-check <email_file>` | Check DMARC | `opendmarc-check message.eml` | DMARC validation |
| `dkimproxy-verify < email.eml` | Verify DKIM signature | `dkimproxy-verify < message.eml` | Signature check |
| `policyd-spf-perl < email.eml` | Check SPF policy | `policyd-spf-perl < message.eml` | Policy validation |

## SMTP Load Testing

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `smtp-source -s <sessions> -l <message_size> -m <message_count> -f <from> -t <to> <server>` | Load test SMTP server | `smtp-source -s 10 -l 1000 -m 100 -f sender@example.com -t recipient@example.com smtp.example.com:25` | Generate load |
| `swaks --to recipient@example.com --from sender@example.com --server smtp.example.com --auth-user user --auth-password pass --header-X-Test "Load Test" --threads 10 --pipe /dev/null` | Concurrent testing | Multiple connections | Stress testing |
| `msmtp-queue -R` | Process msmtp queue | `msmtp-queue -R` | Flush queue |

## SSH Troubleshooting Tips

| Problem | Command/Solution | Notes |
|---------|------------------|-------|
| Permission denied (publickey) | `ssh -v user@host` to debug | Check key path, permissions |
| | `chmod 600 ~/.ssh/id_rsa` | Correct key permissions |
| | `chmod 700 ~/.ssh` | Correct directory permissions |
| | `ssh-add -l` | Verify key loaded in agent |
| Host key verification failed | `ssh-keygen -R hostname` | Remove old host key |
| | `ssh -o StrictHostKeyChecking=no user@host` | Bypass check (security risk!) |
| Connection times out | `ping host` | Check basic connectivity |
| | `telnet host 22` | Check if port is open |
| | `traceroute host`
