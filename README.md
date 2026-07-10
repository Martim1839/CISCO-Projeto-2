# CISCO-Projeto-2

Projeto CCNAv7 SRWE Final Exam — ISEP Academy.

Documento de referência com o esquema de endereçamento IP (IPv4/IPv6) usado na topologia (Zagreb, Pula e Split), e os comandos de configuração inicial dos equipamentos.

## Índice
- [Blocos de partida](#blocos-de-partida)
- [Zagreb](#zagreb-17220008-2001a61)
- [Pula](#pula-172208022-2001b61)
- [Split](#split-1722012023-2001c61)
- [Ligações WAN entre routers](#ligações-wan-entre-routers-ipv4)
- [Endereçamento de Interfaces — Pula](#endereçamento-de-interfaces--pula)
- [Endereçamento de Interfaces — Split](#endereçamento-de-interfaces--split)
- [Part 2 — Clear Configs and Reload](#part-2--clear-configs-and-reload-the-equipment)
- [Part 3 — Initial Configuration](#part-3--perform-equipment-initial-configuration)

---

## Blocos de partida

| Localização | Subnet IPv4 | Prefixo |
|---|---|---|
| Zagreb | 172.20.0.0 | /21 |
| Pula | 172.20.8.0 | /22 |
| Split | 172.20.12.0 | /23 |

| Localização | Subnet IPv6 | Prefixo |
|---|---|---|
| Zagreb | 2001:A:: | /61 |
| Pula | 2001:B:: | /61 |
| Split | 2001:C:: | /61 |

Um bloco `/61` dá exatamente **8 sub-redes /64**, correspondendo às 8 redes locais (VLANs) que cada localização precisa endereçar em IPv6. Os links ponto-a-ponto usam apenas **link-local** em IPv6 (não gastam espaço do `/61`) e em IPv4 saem de dentro do próprio bloco de cada localização.

---

## ZAGREB (172.20.0.0/21 | 2001:A::/61)

| Rede | IPv4 (rede/prefixo) | Gama utilizável | IPv6 (rede/prefixo) |
|---|---|---|---|
| VoIP (500) | 172.20.0.0/23 | .0.1 – .1.254 | 2001:A::/64 |
| Wireless-Zg (500) | 172.20.2.0/23 | .2.1 – .3.254 | 2001:A:0:1::/64 |
| Administration (250) | 172.20.4.0/24 | .4.1 – .4.254 | 2001:A:0:2::/64 |
| Staff (250) | 172.20.5.0/24 | .5.1 – .5.254 | 2001:A:0:3::/64 |
| Guests-Zg (250) | 172.20.6.0/24 | .6.1 – .6.254 | 2001:A:0:4::/64 |
| Management (30) | 172.20.7.0/27 | .7.1 – .7.30 | 2001:A:0:5::/64 |
| Servers (30) | 172.20.7.32/27 | .7.33 – .7.62 | 2001:A:0:6::/64 |
| APs (30) | 172.20.7.64/27 | .7.65 – .7.94 | 2001:A:0:7::/64 |
| To MLS1 (P2P) | 172.20.7.96/30 | .7.97 – .7.98 | link-local (fe80::/10) |
| To MLS2 (P2P) | 172.20.7.100/30 | .7.101 – .7.102 | link-local (fe80::/10) |
| **Free Space** | 172.20.7.104 – 172.20.7.255 (152 endereços) | — | — |

---

## PULA (172.20.8.0/22 | 2001:B::/61)

| Rede | IPv4 (rede/prefixo) | Gama utilizável | IPv6 (rede/prefixo) |
|---|---|---|---|
| Engineering (250) | 172.20.8.0/24 | .8.1 – .8.254 | 2001:B::/64 |
| Wireless-Pl (250) | 172.20.9.0/24 | .9.1 – .9.254 | 2001:B:0:1::/64 |
| Communication (100) | 172.20.10.0/25 | .10.1 – .10.126 | 2001:B:0:2::/64 |
| Staff (100) | 172.20.10.128/25 | .10.129 – .10.254 | 2001:B:0:3::/64 |
| Guests-Pl (50) | 172.20.11.0/26 | .11.1 – .11.62 | 2001:B:0:4::/64 |
| Design (25) | 172.20.11.64/27 | .11.65 – .11.94 | 2001:B:0:5::/64 |
| APs (6) | 172.20.11.96/29 | .11.97 – .11.102 | 2001:B:0:6::/64 |
| Management (6) | 172.20.11.104/29 | .11.105 – .11.110 | 2001:B:0:7::/64 |
| **Free Space** | 172.20.11.112 – 172.20.11.255 | — | — |

---

## SPLIT (172.20.12.0/23 | 2001:C::/61)

| Rede | IPv4 (rede/prefixo) | Gama utilizável | IPv6 (rede/prefixo) |
|---|---|---|---|
| Staff (100) | 172.20.12.0/25 | .12.1 – .12.126 | 2001:C::/64 |
| Wireless-St (100) | 172.20.12.128/25 | .12.129 – .12.254 | 2001:C:0:1::/64 |
| Multimedia (50) | 172.20.13.0/26 | .13.1 – .13.62 | 2001:C:0:2::/64 |
| Design (50) | 172.20.13.64/26 | .13.65 – .13.126 | 2001:C:0:3::/64 |
| Communication (50) | 172.20.13.128/26 | .13.129 – .13.190 | 2001:C:0:4::/64 |
| Guests-St (30) | 172.20.13.192/27 | .13.193 – .13.222 | 2001:C:0:5::/64 |
| APs (6) | 172.20.13.224/29 | .13.225 – .13.230 | 2001:C:0:6::/64 |
| Management (6) | 172.20.13.232/29 | .13.233 – .13.238 | 2001:C:0:7::/64 |
| **Free Space** | 172.20.13.240 – 172.20.13.255 | — | — |

---

## Ligações WAN entre routers (IPv4)

| Ligação | Subnet | Prefixo | RT1-Zg | RT1-Pl | RT1-St |
|---|---|---|---|---|---|
| Zagreb–Pula | 10.0.0.0 | /30 | 10.0.0.1 | 10.0.0.2 | — |
| Zagreb–Split | 10.0.0.4 | /30 | 10.0.0.5 | — | 10.0.0.6 |
| Pula–Split | 10.0.0.8 | /30 | — | 10.0.0.9 | 10.0.0.10 |

Em IPv6, as ligações inter-router (`Gig0/2.102`, `Gig0/2.103`, `Gig0/2.203`) usam apenas **link-local** (`fe80::/10`), conforme pedido no enunciado (Parte 1, Passo 2b).

---

## Endereçamento de Interfaces — Pula

> **Nota de raciocínio:** o RT1-Pl só tem uma ligação física de LAN (`Gig0/1`, com sub-interfaces para as VLANs 5, 6, 30, 50 e 60 — as únicas VLANs efetivamente criadas no SW1-Pl na Parte 5). As redes **Engineering, Design e Communication** não correspondem a nenhuma VLAN configurada no switch, por isso são **simuladas com as interfaces `Lo0`, `Lo1` e `Lo2`** do RT1-Pl (técnica comum nestes labs para representar uma LAN sem hardware físico a mais). Usa-se sempre o **primeiro endereço utilizável** de cada sub-rede como gateway/IP da interface do router.

### IPv4

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-Pl | Gig0/1.5 | 172.20.11.97 | /29 | APs (Pula) | N/A |
| RT1-Pl | Gig0/1.6 | 172.20.11.105 | /29 | Management (Pula) | N/A |
| RT1-Pl | Gig0/1.30 | 172.20.10.129 | /25 | Staff (Pula) | N/A |
| RT1-Pl | Gig0/1.50 | 172.20.9.1 | /24 | Wireless-Pl | N/A |
| RT1-Pl | Gig0/1.60 | 172.20.11.1 | /26 | Guests-Pl | N/A |
| RT1-Pl | Gig0/2.102 | 10.0.0.2 | /30 | Connection to RT1-Zg | N/A |
| RT1-Pl | Gig0/2.203 | 10.0.0.9 | /30 | Connection to RT1-St | N/A |
| RT1-Pl | Lo0 | 172.20.8.1 | /24 | Engineering (LAN simulada) | N/A |
| RT1-Pl | Lo1 | 172.20.11.65 | /27 | Design (LAN simulada) | N/A |
| RT1-Pl | Lo2 | 172.20.10.1 | /25 | Communication (LAN simulada) | N/A |
| SW1-Pl | VLAN 6 | 172.20.11.106 | /29 | Management (SVI de gestão) | 172.20.11.105 |
| AP1-Pl | Fa1 | 172.20.11.98 | /29 | APs | 172.20.11.97 |
| PCC | — | (via DHCP) | /25 | Host com fios em Staff | 172.20.10.129 |

### IPv6

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-Pl | Gig0/1.5 | 2001:B:0:6::1 | /64 | APs (Pula) | N/A |
| RT1-Pl | Gig0/1.6 | 2001:B:0:7::1 | /64 | Management (Pula) | N/A |
| RT1-Pl | Gig0/1.30 | 2001:B:0:3::1 | /64 | Staff (Pula) | N/A |
| RT1-Pl | Gig0/1.50 | 2001:B:0:1::1 | /64 | Wireless-Pl | N/A |
| RT1-Pl | Gig0/1.60 | 2001:B:0:4::1 | /64 | Guests-Pl | N/A |
| RT1-Pl | Gig0/2.102 | link-local (ex: `FE80::102`) | /64 | Connection to RT1-Zg | N/A |
| RT1-Pl | Gig0/2.203 | link-local (ex: `FE80::203PL`) | /64 | Connection to RT1-St | N/A |
| RT1-Pl | Lo0 | 2001:B::1 | /64 | Engineering (LAN simulada) | N/A |
| RT1-Pl | Lo1 | 2001:B:0:5::1 | /64 | Design (LAN simulada) | N/A |
| RT1-Pl | Lo2 | 2001:B:0:2::1 | /64 | Communication (LAN simulada) | N/A |
| SW1-Pl | VLAN 6 | 2001:B:0:7::2 | /64 | Management (SVI de gestão) | 2001:B:0:7::1 |
| AP1-Pl | Fa1 | 2001:B:0:6::2 | /64 | APs | 2001:B:0:6::1 |
| PCC | — | (via SLAAC/DHCPv6) | /64 | Host com fios em Staff | 2001:B:0:3::1 |

> Todas as interfaces devem também ficar com um endereço **link-local** próprio (obrigatório pela Parte 6d), gerado automaticamente ou definido à mão — os exemplos de `FE80::` acima são apenas ilustrativos.

### Notas importantes
- Em cada sub-rede, o **primeiro endereço utilizável** é normalmente atribuído ao gateway (SVI da MLS ou interface/sub-interface do router).
- Nas VLANs de Zagreb com HSRP (VLANs 5, 6, 10, 20, 30, 40, 50, 60), são precisos **3 endereços por VLAN**: IP da MLS1-Zg, IP da MLS2-Zg e o **virtual IP (vIP)** do HSRP.
- As sub-redes "Free Space" ficam de reserva para expansão futura.
- Nos pontos-a-ponto (WAN entre routers), o IPv6 fica marcado como link-local por não haver requisito de endereço global nesses troços.

---

## Endereçamento de Interfaces — Split

> **Nota de raciocínio:** o RT1-St só tem uma ligação física de LAN (`Gig0/1`, com sub-interfaces para as VLANs 5, 6, 30, 50 e 60 — as únicas VLANs efetivamente criadas no SW1-St na Parte 5). As redes **Multimedia, Design e Communication** não correspondem a nenhuma VLAN configurada no switch, por isso são **simuladas com as interfaces `Lo0`, `Lo1` e `Lo2`** do RT1-St (técnica comum nestes labs para representar uma LAN sem hardware físico a mais). Usa-se sempre o **primeiro endereço utilizável** de cada sub-rede como gateway/IP da interface do router.

### IPv4

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-St | Gig0/1.5 | 172.20.13.225 | /29 | APs (Split) | N/A |
| RT1-St | Gig0/1.6 | 172.20.13.233 | /29 | Management (Split) | N/A |
| RT1-St | Gig0/1.30 | 172.20.12.1 | /25 | Staff (Split) | N/A |
| RT1-St | Gig0/1.50 | 172.20.12.129 | /25 | Wireless-St | N/A |
| RT1-St | Gig0/1.60 | 172.20.13.193 | /27 | Guests-St | N/A |
| RT1-St | Gig0/2.103 | 10.0.0.6 | /30 | Connection to RT1-Zg | N/A |
| RT1-St | Gig0/2.203 | 10.0.0.10 | /30 | Connection to RT1-Pl | N/A |
| RT1-St | Lo0 | 172.20.13.1 | /26 | Multimedia (LAN simulada) | N/A |
| RT1-St | Lo1 | 172.20.13.65 | /26 | Design (LAN simulada) | N/A |
| RT1-St | Lo2 | 172.20.13.129 | /26 | Communication (LAN simulada) | N/A |
| SW1-St | VLAN 6 | 172.20.13.234 | /29 | Management (SVI de gestão) | 172.20.13.233 |
| AP1-St | Fa1 | 172.20.13.226 | /29 | APs | 172.20.13.225 |
| PCD | — | (via DHCP) | /25 | Host com fios em Staff | 172.20.12.1 |

### IPv6

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-St | Gig0/1.5 | 2001:C:0:6::1 | /64 | APs (Split) | N/A |
| RT1-St | Gig0/1.6 | 2001:C:0:7::1 | /64 | Management (Split) | N/A |
| RT1-St | Gig0/1.30 | 2001:C::1 | /64 | Staff (Split) | N/A |
| RT1-St | Gig0/1.50 | 2001:C:0:1::1 | /64 | Wireless-St | N/A |
| RT1-St | Gig0/1.60 | 2001:C:0:5::1 | /64 | Guests-St | N/A |
| RT1-St | Gig0/2.103 | link-local (ex: `FE80::103`) | /64 | Connection to RT1-Zg | N/A |
| RT1-St | Gig0/2.203 | link-local (ex: `FE80::203ST`) | /64 | Connection to RT1-Pl | N/A |
| RT1-St | Lo0 | 2001:C:0:2::1 | /64 | Multimedia (LAN simulada) | N/A |
| RT1-St | Lo1 | 2001:C:0:3::1 | /64 | Design (LAN simulada) | N/A |
| RT1-St | Lo2 | 2001:C:0:4::1 | /64 | Communication (LAN simulada) | N/A |
| SW1-St | VLAN 6 | 2001:C:0:7::2 | /64 | Management (SVI de gestão) | 2001:C:0:7::1 |
| AP1-St | Fa1 | 2001:C:0:6::2 | /64 | APs | 2001:C:0:6::1 |
| PCD | — | (via SLAAC/DHCPv6) | /64 | Host com fios em Staff | 2001:C::1 |

> Todas as interfaces devem também ficar com um endereço **link-local** próprio (obrigatório pela Parte 6d), gerado automaticamente ou definido à mão — os exemplos de `FE80::` acima são apenas ilustrativos.

### Notas importantes
- Em cada sub-rede, o **primeiro endereço utilizável** é normalmente atribuído ao gateway (interface/sub-interface do router, já que Split não tem MLS).
- Split não tem HSRP (só existe em Zagreb), por isso cada rede leva apenas **1 endereço de gateway**, não 3 como em Zagreb.
- As sub-redes "Free Space" ficam de reserva para expansão futura.
- Nos pontos-a-ponto (WAN entre routers), o IPv6 fica marcado como link-local por não haver requisito de endereço global nesses troços.

---

## Endereçamento de Interfaces — Zagreb

> **Nota de raciocínio:** O bloco de Zagreb é gerido com duas Multilayer Switches (MLS1-Zg e MLS2-Zg) a fazerem encaminhamento e redundância através de HSRP. O gateway virtual (vIP) de cada VLAN será o `.3` em IPv4 e o `::3` em IPv6. Adicionalmente, os links P2P utilizam apenas endereços link-local (FE80::) em IPv6.

### IPv4

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-Zg | Gig0/0 | 172.20.7.97 | /30 | Connection to MLS1 | N/A |
| RT1-Zg | Gig0/1 | 172.20.7.101 | /30 | Connection to MLS2 | N/A |
| RT1-Zg | Gig0/2.102 | 10.0.0.1 | /30 | Connection to RT1-Pl | N/A |
| RT1-Zg | Gig0/2.103 | 10.0.0.5 | /30 | Connection to RT1-St | N/A |
| SW1-Zg | VLAN 6 | 172.20.7.4 | /27 | Management (SW1) | 172.20.7.3 |
| SW2-Zg | VLAN 6 | 172.20.7.5 | /27 | Management (SW2) | 172.20.7.3 |
| MLS1-Zg | Gig0/1 | 172.20.7.98 | /30 | Connection to RT1-Zg | N/A |
| MLS1-Zg | VLAN 5 | 172.20.7.65 | /27 | APs | N/A |
| MLS1-Zg | VLAN 6 | 172.20.7.1 | /27 | Management | N/A |
| MLS1-Zg | VLAN 10 | 172.20.7.33 | /27 | Servers | N/A |
| MLS1-Zg | VLAN 20 | 172.20.4.1 | /24 | Administration | N/A |
| MLS1-Zg | VLAN 30 | 172.20.5.1 | /24 | Staff | N/A |
| MLS1-Zg | VLAN 40 | 172.20.0.1 | /23 | VoIP | N/A |
| MLS1-Zg | VLAN 50 | 172.20.2.1 | /23 | Wireless | N/A |
| MLS1-Zg | VLAN 60 | 172.20.6.1 | /24 | Guests | N/A |
| MLS2-Zg | Gig0/1 | 172.20.7.102 | /30 | Connection to RT1-Zg | N/A |
| MLS2-Zg | VLAN 5 | 172.20.7.66 | /27 | APs | N/A |
| MLS2-Zg | VLAN 6 | 172.20.7.2 | /27 | Management | N/A |
| MLS2-Zg | VLAN 10 | 172.20.7.34 | /27 | Servers | N/A |
| MLS2-Zg | VLAN 20 | 172.20.4.2 | /24 | Administration | N/A |
| MLS2-Zg | VLAN 30 | 172.20.5.2 | /24 | Staff | N/A |
| MLS2-Zg | VLAN 40 | 172.20.0.2 | /23 | VoIP | N/A |
| MLS2-Zg | VLAN 50 | 172.20.2.2 | /23 | Wireless | N/A |
| MLS2-Zg | VLAN 60 | 172.20.6.2 | /24 | Guests | N/A |
| MLS1/MLS2-Zg | VLAN 5 VIP | 172.20.7.67 | /27 | VIP APs | N/A |
| MLS1/MLS2-Zg | VLAN 6 VIP | 172.20.7.3 | /27 | VIP Management | N/A |
| MLS1/MLS2-Zg | VLAN 10 VIP | 172.20.7.35 | /27 | VIP Servers | N/A |
| MLS1/MLS2-Zg | VLAN 20 VIP | 172.20.4.3 | /24 | VIP Administration | N/A |
| MLS1/MLS2-Zg | VLAN 30 VIP | 172.20.5.3 | /24 | VIP Staff | N/A |
| MLS1/MLS2-Zg | VLAN 40 VIP | 172.20.0.3 | /23 | VIP VoIP | N/A |
| MLS1/MLS2-Zg | VLAN 50 VIP | 172.20.2.3 | /23 | VIP Wireless | N/A |
| MLS1/MLS2-Zg | VLAN 60 VIP | 172.20.6.3 | /24 | VIP Guests | N/A |
| WLC1-Zg | Management | 172.20.7.6 | /27 | Management | 172.20.7.3 |
| WLC1-Zg | wireless-zg | 172.20.2.4 | /23 | Wireless | 172.20.2.3 |
| WLC1-Zg | guest-zg | 172.20.6.4 | /24 | Guests | 172.20.6.3 |
| AP1-Zg | Fa1 | 172.20.7.68 | /27 | APs | 172.20.7.67 |
| PCA | N/A | 172.20.4.4 | /24 | Host com fios em Admin | 172.20.4.3 |
| PCB | N/A | 172.20.5.4 | /24 | Host com fios em Staff | 172.20.5.3 |
| DHCP-SRV | N/A | 172.20.7.36 | /27 | DHCP Server | 172.20.7.35 |

### IPv6

| Device | Interface | IP address | Prefixo | Description | Gateway |
|---|---|---|---|---|---|
| RT1-Zg | Gig0/0 | FE80::1 | link-local | IPv6 link-local | N/A |
| RT1-Zg | Gig0/1 | FE80::2 | link-local | IPv6 link-local | N/A |
| RT1-Zg | Gig0/2.102 | FE80::102 | link-local | Connection to RT1-Pl | N/A |
| RT1-Zg | Gig0/2.103 | FE80::103 | link-local | Connection to RT1-St | N/A |
| SW1-Zg | VLAN 6 | 2001:A:0:5::4 | /64 | Management (SW1) | 2001:A:0:5::3 |
| SW2-Zg | VLAN 6 | 2001:A:0:5::5 | /64 | Management (SW2) | 2001:A:0:5::3 |
| MLS1-Zg | Gig0/1 | FE80::11 | link-local | IPv6 link-local | N/A |
| MLS1-Zg | VLAN 5 | 2001:A:0:7::1 | /64 | APs | N/A |
| MLS1-Zg | VLAN 6 | 2001:A:0:5::1 | /64 | Management | N/A |
| MLS1-Zg | VLAN 10 | 2001:A:0:6::1 | /64 | Servers | N/A |
| MLS1-Zg | VLAN 20 | 2001:A:0:2::1 | /64 | Administration | N/A |
| MLS1-Zg | VLAN 30 | 2001:A:0:3::1 | /64 | Staff | N/A |
| MLS1-Zg | VLAN 40 | 2001:A::1 | /64 | VoIP | N/A |
| MLS1-Zg | VLAN 50 | 2001:A:0:1::1 | /64 | Wireless | N/A |
| MLS1-Zg | VLAN 60 | 2001:A:0:4::1 | /64 | Guests | N/A |
| MLS2-Zg | Gig0/1 | FE80::22 | link-local | IPv6 link-local | N/A |
| MLS2-Zg | VLAN 5 | 2001:A:0:7::2 | /64 | APs | N/A |
| MLS2-Zg | VLAN 6 | 2001:A:0:5::2 | /64 | Management | N/A |
| MLS2-Zg | VLAN 10 | 2001:A:0:6::2 | /64 | Servers | N/A |
| MLS2-Zg | VLAN 20 | 2001:A:0:2::2 | /64 | Administration | N/A |
| MLS2-Zg | VLAN 30 | 2001:A:0:3::2 | /64 | Staff | N/A |
| MLS2-Zg | VLAN 40 | 2001:A::2 | /64 | VoIP | N/A |
| MLS2-Zg | VLAN 50 | 2001:A:0:1::2 | /64 | Wireless | N/A |
| MLS2-Zg | VLAN 60 | 2001:A:0:4::2 | /64 | Guests | N/A |
| MLS1/MLS2-Zg | VLAN 5 VIP | 2001:A:0:7::3 | /64 | VIP APs | N/A |
| MLS1/MLS2-Zg | VLAN 6 VIP | 2001:A:0:5::3 | /64 | VIP Management | N/A |
| MLS1/MLS2-Zg | VLAN 10 VIP | 2001:A:0:6::3 | /64 | VIP Servers | N/A |
| MLS1/MLS2-Zg | VLAN 20 VIP | 2001:A:0:2::3 | /64 | VIP Administration | N/A |
| MLS1/MLS2-Zg | VLAN 30 VIP | 2001:A:0:3::3 | /64 | VIP Staff | N/A |
| MLS1/MLS2-Zg | VLAN 40 VIP | 2001:A::3 | /64 | VIP VoIP | N/A |
| MLS1/MLS2-Zg | VLAN 50 VIP | 2001:A:0:1::3 | /64 | VIP Wireless | N/A |
| MLS1/MLS2-Zg | VLAN 60 VIP | 2001:A:0:4::3 | /64 | VIP Guests | N/A |
| WLC1-Zg | Management | 2001:A:0:5::6 | /64 | Management | 2001:A:0:5::3 |
| WLC1-Zg | wireless-zg | N/A | N/A | Apenas IPv4 | N/A |
| WLC1-Zg | guest-zg | N/A | N/A | Apenas IPv4 | N/A |
| AP1-Zg | Fa1 | 2001:A:0:7::4 | /64 | APs | 2001:A:0:7::3 |
| PCA | N/A | 2001:A:0:2::4 | /64 | Host com fios em Admin | 2001:A:0:2::3 |
| PCB | N/A | 2001:A:0:3::4 | /64 | Host com fios em Staff | 2001:A:0:3::3 |
| DHCP-SRV | N/A | 2001:A:0:6::5 | /64 | DHCP Server | 2001:A:0:6::3 |

## Part 2 — Clear Configs and Reload the Equipment

| Task | IOS Command |
|---|---|
| Erase the startup-config file on the Routers | `erase startup-config` |
| Reload the Routers | `reload` |
| Erase the startup-config file on the Switches | `erase startup-config` |
| Delete the vlan.dat file on the Switches | `delete vlan.dat` |
| Reload the Switches | `reload` |
| Verify the Switches SDM Template | `sdm prefer dual-ipv4-and-ipv6 default` (requer reload) |
| Clear the WLC Config | Menu de boot (ESC) → opção **5. Clear Configuration** |
| Clear the APs Config | Premir o botão **MODE** ~30s durante o arranque |

**Notas:**
- O `delete vlan.dat` é exclusivo dos switches — o `erase startup-config` não apaga a base de dados de VLANs, que fica guardada à parte na flash.
- O comando `sdm prefer dual-ipv4-and-ipv6 default` garante que a TCAM do switch reserva espaço suficiente para tabelas IPv6, necessário para a conectividade IPv6 pedida no Part 13. Exige **reload** para ter efeito.
- A WLC (AireOS) e os APs não usam comandos IOS — a limpeza é feita via menu de boot / botão físico.

---

## Part 3 — Perform Equipment Initial Configuration

Aplica-se a **todos os dispositivos intermediários** (routers, switches e MLS).

enable
configure terminal
no ip domain-lookup
hostname <nome>
ip domain-name isepacademy.ccna.itn.com
security passwords min-length 10
service password-encryption
enable secret classclass
username cisco secret classclass
crypto key generate rsa 
2048
ip ssh version 2
line console 0
password classclass
login
exit
line vty 0 15
transport input ssh
login local
exec-timeout 0 30
exit
login block-for 300 attempts 3 within 120
banner motd #
AVISO: Acesso restrito a utilizadores autorizados. Todas as ligacoes sao monitorizadas e registadas. Qualquer tentativa de acesso nao autorizado sera reportada as autoridades competentes. #
ip hosts <prencher conforme>

---

## Part 4 —  Enable EtherChannel Between MLSs

MLS1-Zg

enable
configure terminal
interface range gigabitEthernet 0/2 - 3
 channel-group 1 mode on
 no shutdown
exit

end 
write memory


MLS2-Zg

enable
configure terminal
interface range gigabitEthernet 0/2 - 3
 channel-group 1 mode on
 no shutdown
exit

end 
write memory

parte 6

Router

enable
configure terminal

ipv6 unicast-routing
interface GigabitEthernet0/1
 description Link to SW1-St (LAN VLANs)
 no ip address
 no shutdown
exit

interface GigabitEthernet0/1.5
 description APs (Split)
 encapsulation dot1Q 5
 ip address 172.20.13.225 255.255.255.248
 ipv6 address 2001:C:0:6::1/64
 ipv6 address FE80::1 link-local
 ipv6 enable
exit

interface GigabitEthernet0/1.6
 description Management (Split)
 encapsulation dot1Q 6
 ip address 172.20.13.233 255.255.255.248
 ipv6 address 2001:C:0:7::1/64
 ipv6 address FE80::1 link-local
 ipv6 enable
exit

interface GigabitEthernet0/1.30
 description Staff (Split)
 encapsulation dot1Q 30
 ip address 172.20.12.1 255.255.255.128
 ipv6 address 2001:C::1/64
 ipv6 address FE80::1 link-local
 ipv6 enable
exit

interface GigabitEthernet0/1.50
 description Wireless-St
 encapsulation dot1Q 50
 ip address 172.20.12.129 255.255.255.128
 ipv6 address 2001:C:0:1::1/64
 ipv6 address FE80::1 link-local
 ipv6 enable
exit

interface GigabitEthernet0/1.60
 description Guests-St
 encapsulation dot1Q 60
 ip address 172.20.13.193 255.255.255.224
 ipv6 address 2001:C:0:5::1/64
 ipv6 address FE80::1 link-local
 ipv6 enable
exit

interface GigabitEthernet0/2
 no ip address
 no shutdown
exit

interface GigabitEthernet0/2.103
 description Connection to RT1-Zg
 encapsulation dot1Q 103
 ip address 10.0.0.6 255.255.255.252
 ipv6 address FE80::103 link-local
 ipv6 enable
exit

interface GigabitEthernet0/2.203
 description Connection to RT1-Pl
 encapsulation dot1Q 203
 ip address 10.0.0.10 255.255.255.252
 ipv6 address FE80::203 link-local
 ipv6 enable
exit

interface Loopback0
 description Multimedia (LAN simulada)
 ip address 172.20.13.1 255.255.255.192
 ipv6 address 2001:C:0:2::1/64
exit

interface Loopback1
 description Design (LAN simulada)
 ip address 172.20.13.65 255.255.255.192
 ipv6 address 2001:C:0:3::1/64
exit

interface Loopback2
 description Communication (LAN simulada)
 ip address 172.20.13.129 255.255.255.192
 ipv6 address 2001:C:0:4::1/64
exit

Switch

enable
configure terminal

interface Vlan6
 description Management SVI
 ip address 172.20.13.234 255.255.255.248
 ipv6 address 2001:C:0:7::2/64
 ipv6 address FE80::2 link-local
 ipv6 enable
 no shutdown
exit
ip default-gateway 172.20.13.233
ipv6 route ::/0 FE80::1 Vlan6
end
copy running-config startup-config

---

Parte 10 - St
a. Parte 5 verificar com
show interfaces status | include disabled

b.
enable
configure terminal
interface range FastEthernet0/2 - 15
 switchport port-security
 switchport port-security maximum 5
 switchport port-security violation shutdown
 switchport port-security aging time 5
 switchport port-security aging type inactivity
exit

c.
ip dhcp snooping
ip dhcp snooping vlan 30,50,60
interface FastEthernet0/1
 ip dhcp snooping trust
exit
interface range FastEthernet0/2 - 15
 ip dhcp snooping limit rate 5
exit
interface range FastEthernet0/21 - 22
 ip dhcp snooping limit rate 5
exit

d.
ip arp inspection vlan 30
interface FastEthernet0/1
 ip arp inspection trust
exit
interface range FastEthernet0/2 - 15
 ip arp inspection limit rate 5
exit


e.
spanning-tree portfast default

f.
interface range FastEthernet0/2 - 15
 spanning-tree bpduguard enable
exit

---

## Autores
Grupo 134 — ISEP
