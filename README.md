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
