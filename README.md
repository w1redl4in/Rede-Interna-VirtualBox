# Configurações VirtualBox                  
   ========= HASHTAG (#) SIGNIFICA COMENTÁRIO ==========

  ## GATEWAY (G1)
    É necessária a criação de 3 interfaces na máquina Gateway.
    1 - Configurações > Network/Rede > Adaptador 1 > Modo Bridge (DHCP)
                                       Adaptador 2 > Rede Interna > Defina um nome para esta rede. Ex: rede1
                                       Adaptador 3 > Rede Interna > Defina um nome para esta rede. Ex: rede2

  ### Configuração interfaces:
  #### Ubuntu 18:
  sudo su    #Virando root  
  cd /etc/netplan   #Entrando no diretório do 50-cloud-init.yaml   
  cp 50-cloud-init.yaml 50-cloud-init.yaml.bkp      #Criando backup  
    
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
   
  sudo su      #Virando root  
  cd /etc/network     #Entrando no diretório do interfaces  
  cp interfaces interfaces.bkp    #Criando backup  
     
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
     
    
    
    
