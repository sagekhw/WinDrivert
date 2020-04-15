# WinDrivert
### flowtrack.c: A network flow tracking application.
### netdump.c: A simple packet capture and dump application.
### netfilter.c: A simple firewall application.
### passthru.c: A skeleton WinDivert application with multi-threading.
### socketdump.c: Dumps socket operations.
### streamdump.c: Redirects TCP streams to a local proxy server.
### webfilter.c: A simple URL blacklist filter.

- flowtrack.c: usage: flowtrack.exe [filter]

- netdump.c: usage: netdump.exe windivert-filter [priority]
 - This is a simple traffic monitor.  It uses a WinDivert handle in SNIFF mode.
 - The SNIFF mode copies packets and does not block the original.
 
- netfilter.c: usage: netfilter.exe windivert-filter [priority]
 - This is a simple traffic filter/firewall using WinDivert.
 - Any traffic that matches the windivert-filter will be blocked using one of
 - the following methods:
 - - TCP: send a TCP RST to the packet's source.
 - - UDP: send a ICMP(v6) "destination unreachable" to the packet's source.
 - - ICMP/ICMPv6: Drop the packet.

- passthru.c: usage: passthru.exe [windivert-filter] [num-threads] [batch-size] [priority]
 - This program does nothing except divert packets and re-inject them.  This is
 - useful for performance testing.

- socketdump.c:usage: socketdump.exe [filter]
                      socketdump.exe --block [filter]

- streamdump.c: usage: streamdump.exe port
 - This program demonstrates how to handle streams using WinDivert.
 - The program works by "reflecting" outbound TCP connections into inbound
 - TCP connections that are handled by a simple proxy server.

- webfilter.c: 
 - This is a simple web (HTTP) filter using WinDivert.
 - It works by intercepting outbound HTTP GET/POST requests and matching
 - the URL against a blacklist.  If the URL is matched, we hijack the TCP
 - connection, reseting the connection at the server end, and sending a
 - blockpage to the browser.
