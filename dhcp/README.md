# SV43 ネットワークを超えたDHCP

## cisco設定

### コンソール接続してから

### 1. 特権モードに入る

```
Router> enable
```

### 2. グローバルコンフィギュレーションモードに入る

```
Router# configure terminal
```

### 3. interface設定モード

```
Router(config)# interface fastethernet 0
``` 

### 4. ip address設定

```
Router(config-if)# ip address <IP Address> 255.255.255.0
Router(config-if)# no shutdown
// 自動取得側の場合
Router(config-if)# ip helper-address <DHCPサーバーのIP Address>
```

### 5. 確認

```
Router(config-if)# exit
Router(config)# exit
Router# show interfaces fastEthernet 0
```

## DHCP設定

/etc/dhcp/dhcpd.conf

```
subnet 192.168.111.0 netmask 255.255.255.0 {
    range dynamic-bootp 192.168.111.10 192.168.111.20;
    option rooters 192.168.111.254;
    option domain-name "sv4309.jp";
}
```

ネットワーク周り, DHCP周り再起動

```
# service network restart
# service dhcpd restart
```

