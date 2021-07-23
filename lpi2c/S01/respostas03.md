---
template: index
title: Laboratório 01
sitename: LPIC-II - Laboratório 01
---

## Roteadores

* [X] Configuração do serviço de DNS (bind)
* [X] Forwarder
* [X] Autoritativo
* [X] Master/Slave
* [X] Configuração da transferência de zonas entre os dois DNSs

### named.conf
* CentOS: [/etc/named/named.conf](rtr-ctos/named.conf)
* Ubuntu: [/etc/bind/named.conf](rtr-ubnt/named.conf)

### arquivos de zona

* CentOS: /var/named
* Ubuntu: /var/cache/bind

* Domínio 1: [theforce.local.db](rtr-ubnt/theforce.local.db)

```dns
$TTL 3D
@                  IN  SOA ns1.theforce.local. nsadmin.theforce.local. (
            2019101801  ; Serial
            28800       ; refresh (8h)
            7200        ; retry (2h)
            2592000     ; expire (30d)
            86400       ; minimum (1d)
    )
                   IN NS      c3po
                   IN MX  5   luke
luke               IN A       172.17.15.2
c3po               IN A       172.17.15.1
r2d2               IN CNAME   c3po

frederico-ubnt     IN A   172.17.15.2
frederico-rtr-02   IN A   172.17.15.1

saltmaster         IN A   172.31.7.54
```

* Domínio 2: [darkside.local.db](rtr-ctos/darkside.local.db)
* Reverso 1: [172.17.15.rev.db](rtr-ubnt/172.17.15.rev.db)
* Reverso 3: [172.18.2.rev.db](rtr-ctos/172.18.2.rev.db)

## Clientes

* [X] Configurar para utilizar o roteador como servidor de DNS primário

1. Alterar os nameservers nos arquivos de configuração de rede (netplan e network-scripts)
2. Alterar o arquivo `/etc/resolv.conf`

```
nameserver 10.9.8.X
domain <dominio>.local
search <dominio>.local
```

* [X] Testar acesso e funcionamento dos servidores de DNS

```
ping <nome_do_host>
host <nome_do_host>
host <endereco_ip>
```

* [X] Fazer consultas avançadas aos servidores de DNS

```
dig @10.9.8.X <ns|mx|cname|a> <dominio>.local
```