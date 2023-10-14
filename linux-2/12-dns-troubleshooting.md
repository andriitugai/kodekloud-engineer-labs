## DNS Troubleshooting

The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . <span style='color:cyan'>**App Server 3**</span> in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.



As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

### Solution
1. SSH to the server
2. Add the line  
```nameserver 8.8.8.8```  
to the  
```/etc/resolv.conf```.
```
search stratos.xfusioncorp.com
nameserver 127.0.0.11
nameserver 8.8.8.8
options ndots:0
```