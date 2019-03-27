# Configurações VirtualBox                  
   // = Comentários 

  ## GATEWAY (G1)
    É necessária a criação de 3 interfaces na máquina Gateway.
    1 - Configurações > Network/Rede > Adaptador 1 > Modo Bridge (DHCP)
                                       Adaptador 2 > Rede Interna > Defina um nome para esta rede. Ex: rede1
                                       Adaptador 3 > Rede Interna > Defina um nome para esta rede. Ex: rede2

  ### Configuração de interfaces:
  #### Ubuntu 18:
  sudo su    // Virando root  
  cd /etc/netplan   // Entrando no diretório do 50-cloud-init.yaml   
  cp 50-cloud-init.yaml 50-cloud-init.yaml.bkp      // Criando backup  
    
    network:
        ethernets:
            enp0s3:
                addresses: []
                dhcp4: true
            enp0s8:
                addresses: [192.168.110.254/24]
                dhcp4: false
            enp0s9:
                addresses: [192.168.100.254/24]
                dhcp4: false
        version: 2
   #### Ubuntu 14:
   
  sudo su      // Virando root  
  cd /etc/network     // Entrando no diretório do interfaces  
  cp interfaces interfaces.bkp    // Criando backup  
     
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
   
   ifdown -a && ifup -a   // Aplicando novas configurações
     
  ### Configurando Gateway
      ufw enable
      echo 1 > /proc/sys/net/ipv4/ip_forward
      iptables -t nat -o enp0s3 -A POSTROUTING -j MASQUERADE 
      
  ### Gateway finalizado!
  
  ## CLIENTE 1 (S2)
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
   netplan apply   // Aplicando novas configurações
   
   #### Ubuntu 14:
      auto eth0
      iface eth0 inet static
      address 192.168.110.11
      netmask 255.255.255.0
      gateway 192.168.110.254
   ifdown -a && ifup -a
   
      
     
    
    
    
