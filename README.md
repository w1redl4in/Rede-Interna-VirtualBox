# Configurações VirtualBox                  
   ========= HASHTAG (#) SIGNIFICA COMENTÁRIO ==========

  ## GATEWAY (G1)
    É necessária a criação de 3 interfaces na máquina Gateway.
    1 - Configurações > Network/Rede > Adaptador 1 > Modo Bridge (DHCP)
                                       Adaptador 2 > Rede Interna > Defina um nome para esta rede. Ex: rede1
                                       Adaptador 3 > Rede Interna > Defina um nome para esta rede. Ex: rede2

  ### Configuração interfaces:
  #### Ubuntu 18:
    sudo su # Virando root
    cd /etc/netplan # Entrando no diretório do 50-cloud-init.yaml 
    
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
    
    
    
