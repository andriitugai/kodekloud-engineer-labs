## Haproxy LBR Troubleshooting

xFusionCorp Industries has an application running on Nautlitus infrastructure in Stratos Datacenter. The monitoring tool recognised that there is an issue with the <span style='color:cyan'>**haproxy**</span> service on <span style='color:cyan'>**LBR server**</span>. That needs to fixed to make the application work properly.



Troubleshoot and fix the issue, and make sure haproxy service is running on Nautilus LBR server. Once fixed, make sure you are able to access the website using StaticApp button on the top bar.

### Solution
1. SSH to LBR server
2. Check status of haproxy
```
sudo systemctl status haproxy
```
3. Try to start ```haproxy```
```
sudo systemctl start haproxy
```
4. Check ```haproxy``` configuration file:
```
sudo haproxy -c -f /etc/haproxy/haproxy.cfg
```
5. Fix it
6. Check ```haproxy``` configuration file again:
```
sudo haproxy -c -f /etc/haproxy/haproxy.cfg
```
7. Apply conf file:
```
sudo haproxy -f /etc/haproxy/haproxy.cfg
```
8. Enable and start ```haproxy```
```
sudo systemctl enable haproxy
sudo systemctl start haproxy
```
9. Should work
