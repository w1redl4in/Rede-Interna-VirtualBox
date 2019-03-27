# Configurações VirtualBox
  ## GATEWAY (G1)
    É necessário a criação de 3 interfaces na máquina Gateway.
    1 - Configurações > Network/Rede > Adaptador 1 > Modo Bridge (DHCP)
                                       Adaptador 2 > Rede Interna > Defina um nome para esta rede. Ex: rede1
                                       Adaptador 3 > Rede Interna > Defina um nome para esta rede. Ex: rede2
                                       
  ### Configuração das interfaces e iptables
    O próximo passo é a configuração das interfaces previamente criadas.
    
    sudo su
    cd /etc/netplan (Ubuntu 18) ou cd /etc/network (Ubuntu 14)
    
  ### Configuração interfaces:
    
