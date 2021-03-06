# Mini guia                 
  ## GATEWAY (G1)
    É necessária a criação de 3 interfaces na máquina Gateway.
    Configurações > Network/Rede > Adaptador 1 > Modo Bridge (DHCP)
                                   Adaptador 2 > Rede Interna > Defina um nome para esta rede. Ex: rede1
                                   Adaptador 3 > Rede Interna > Defina um nome para esta rede. Ex: rede2

  ### Configuração de interfaces:
  #### Ubuntu 18:  
    network:
        ethernets:
            enp0s3:
                addresses: []
                dhcp4: true
            enp0s8:
                addresses: [192.168.100.254/24]
                dhcp4: false
            enp0s9:
                addresses: [192.168.110.254/24]
                dhcp4: false
        version: 2
   netplan apply
   #### Ubuntu 14:
     auto eth0
     iface eth0 inet dhcp
     
     auto eth1
     iface eth1 inet static
     address 192.168.100.254
     netmask 255.255.255.0
     
     auto eth2
     iface eth2 inet static
     address 192.168.110.254
     netmask 255.255.255.0
   ifdown -a && ifup -a 
     
  ### Configurando Gateway
  #### Ubuntu 18:
      echo 1 > /proc/sys/net/ipv4/ip_forward
      iptables -t nat -o enp0s3 -A POSTROUTING -j MASQUERADE  
  #### Ubuntu 14:
      echo 1 > /proc/sys/net/ipv4/ip_forward
      iptables -t nat -o eth0 -j MASQUERADE -A POSTROUTING
      
      
      
      
      
      
      
      
      
  ## SERVIDOR (S2)
  ### Na Virtualbox
      Configurações > Rede/Network > Rede Interna/Internal Network 
      Entre com o nome da rede interna correspondente Ex: rede1
      
  ### Configurando IP Fixo e Gateway
  #### Ubuntu 18:
      network:
        ethernets:
            enp0s3:
                addresses: [192.168.100.11/24]
                dhcp4: false
                gateway4: 192.168.100.254
        version: 2     
   netplan apply
   
   #### Ubuntu 14:
      auto eth0
      iface eth0 inet static
      address 192.168.100.11
      netmask 255.255.255.0
      gateway 192.168.100.254
   ifdown -a && ifup -a
   
   ## CLIENTE (C1)
  ### Na Virtualbox
      Configurações > Rede/Network > Rede Interna/Internal Network 
      Entre com o nome da rede interna correspondente Ex: rede2
      
  ### Configurando IP Fixo e Gateway
  #### Ubuntu 18:
      network:
        ethernets:
            enp0s3:
                addresses: [192.168.110.11/24]
                dhcp4: false
                gateway4: 192.168.110.254
        version: 2     
   netplan apply
   
   #### Ubuntu 14:
      auto eth0
      iface eth0 inet static
      address 192.168.110.11
      netmask 255.255.255.0
      gateway 192.168.110.254
   ifdown -a && ifup -a
   
   ### Configurando DNS 
   #### Definir nameserver como 8.8.8.8
    cd /etc/
    nano resolv.conf
    nameserver 8.8.8.8
   
   
   # Vídeo explicativo
   [YouTube](https://youtu.be/AzYgLqNN0xg)
    
   ![](https://github.com/w1redl4in/.dotfiles/blob/master/finallymesatopo.jpg)
    
    
   # Referências:
      Fatec Osasco - Redes de Computadores - http://www.fatecosasco.edu.br
      Professor Leandro Palha - https://www.youtube.com/channel/UC1fek237kXqkmU_lQVk5OCw
    
