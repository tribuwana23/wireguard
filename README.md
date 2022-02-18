## 1. Install wireguard server ubuntu
run `wireguard-install.sh` scrip for easy install wireguard server and follow all step
after install wireguard server you can add more client with run the sript again 

## 2. Install wireguard on client ubuntu
First we update our Ubuntu host machine then install WireGuard:

```sh
sudo apt update
sudo apt install wireguard
```

Create configuration file
```sh
sudo nano /etc/wireguard/wg0.conf
```
and add following client configuration that you have generated from server before, example :
```sh
[Interface]
PrivateKey = DESKTOP_CLIENT_PRIVATE_KEY
Address = 10.0.0.2/24

[Peer]
PublicKey = YOUR_SERVER_PUBLIC_KEY
Endpoint = YOUR_SERVER_IP_ADDRESS:51820
AllowedIPs = 0.0.0.0/0
```
## 3. Start WireGuard
3.0. wg up
When everything done above, bring the wg0 interface up using the attributes specified in the configuration file:
```sh
sudo wg-quick up wg0
```
Now you should be connected to your Ubuntu VPN server, and the traffic from your client machine should be routed through it. You can check the connection with:
```sh
sudo wg
```
and the output should be like:
`
interface: wg0
  public key: HFqTSN2SE6LvvEU/xV3eJ0KArQEkTx1mYZpAjRtAjwE=
  private key: (hidden)
  listening port: 22870
  fwmark: 0xca6c

peer: 8Mg3Vgw+QduVhJaLERXQbyrPL1/nUWa27Ly8ZVTGTHs=
  endpoint: XXX.XXX.XXX.XXX:51820
  allowed ips: 0.0.0.0/0
  latest handshake: 1 minute, 18 seconds ago
  transfer: 67.58 KiB received, 170.36 KiB sent
`
## 4. Start at Boot
If you want to to start your WireGuard after every system reboot just run:
```sh
sudo systemctl enable wg-quick@wg0
```
To remove this:
```sh
sudo systemctl disable wg-quick@wg0
```
4. Test WireGuard
You can now check you IP searching on the browser what is my ip or just use curl to achieve that from your cli:
```sh
curl ifconfig.me
```
