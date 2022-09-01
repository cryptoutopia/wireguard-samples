# wireguard-samples
sample configs for different wireguard scenarios



# easy setup

## server
<pre>
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = YOUR PK
</pre>


# Nat routing on the server part
<pre>
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o ens4 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o ens4 -j MASQUERADE
</pre>

# peers section: pk, ips
<pre>
[Peer]
PublicKey = Peer PK
AllowedIPs = 10.0.0.2
PersistentKeepalive=30
</pre>

## client
<pre>
[Interface]
Address = 10.0.0.2/24
PrivateKey = YOUR PK
DNS = 8.8.8.8

[Peer]
PublicKey = Server PK
AllowedIPs = 0.0.0.0/0
Endpoint = 34.78.102.70:51820
PersistentKeepalive = 30
</pre>



# Other sources

* https://github.com/pirate/wireguard-docs - best WG documentation
* 
