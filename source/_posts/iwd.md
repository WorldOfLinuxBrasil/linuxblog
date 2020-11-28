---
title: Uso e Instalação do iwd
date: 2020/11/28
author: Redson
---
* * *

O iwd é um daemon sem fio para Linux escrito pela Intel. O objetivo principal do projeto é otimizar a utilização de recursos, não dependendo de nenhuma biblioteca externa e, em vez disso, utilizando os recursos fornecidos pelo Kernel Linux na máxima extensão possível.

* * *

### **Instalando o iwd**

Para instalar o utilitário de wi-fi iwd no Arch e derivados, execute:

    # pacman -S iwd
    

Debian, Ubuntu e derivados:

    sudo apt-get install iwd
    

Fedora e derivados:

    sudo dnf install iwd
    

##### Vale ressaltar que se você está no meio da instalação do Arch Linux, não precisa seguir este passo.

* * *

Você também deve habilitar o iwd com o comando:

    # systemctl enable iwd.service
    

* * *

Como usar o iwd
---------------

O iwd na verdade usa o comando iwctl, execute:

    iwctl
    

* * *

Caso queira listar todos os comandos disponíveis, execute o comando:

    [iwd]#help
    

* * *

**Conectando a uma rede wireless**

primeiro, se você não souber como seu dispositivo wi-fi é reconhecido pelo sistema, execute:

    [iwd]# device list
    

Em seguida, busque por redes. Supondo que seu dispositivo seja wlan0, execute

    [iwd]# station wlan0 scan
    

Você pode listar todas as redes Wi-Fi. Mais uma vez supondo que seu dispositivo seja wlan0:

    [iwd]# station wlan0 get-networks
    

Você deve receber alguma coisa nesse estilo:

  
![demonstração do comando get-networks](https://media.discordapp.net/attachments/776201664902201346/776201725416833064/unknown.png)

* * *

Por fim, você deve apenas conectar ao wi-fi

    station wlan0 connect NOME_DO_WIFI
    

Você deve ver algo desse tipo:

  
![conectando a rede](https://media.discordapp.net/attachments/776201664902201346/776202258030395422/unknown.png)  
  

Agora é só digitar a senha da sua rede, e continuar com a instalação, ou com a navegação.

**Artigo por: Redson**