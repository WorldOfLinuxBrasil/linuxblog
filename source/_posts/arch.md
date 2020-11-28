---
title: Instalação Arch Linux 
date: 2020/11/28
author: Redson
---
Arch Linux, é uma distribuição Linux para computadores com arquitetura 64 bits, desenvolvido inicialmente pelo canadense Judd Vinet. Esse sistema operacional se apresenta de maneira diferente de outros, como Windows e MacOS. Ele tem como objetivo dar ao usuário total controle sobre o seu computador, e é conhecido por ser “aquilo que o usuário quer que ele seja”. Sabendo disso podemos iniciar com o Guia de instalação.

Vale ressaltar que
-------------------

1.  É de alta recomendação que leia a **Wiki Oficial do Arch Linux, ela te ajudará muito**.
2.  Neste guia só irei apresentar o básico do Arch Linux, desde a instalação até um sistema com interface gráfica
3.  Este guia não é para dual-boot, e, se possível, teste em uma máquina virtual antes de tentar em seu computador.
4.  Não digite os `**#**` dos comandos, eles são apenas para informar que os comandos estão sendo executados como root.

Baixando a ISO de instalação
----------------------------

 Para poder prosseguir, você deve baixar a ISO de instalação do Arch Linux, que é levíssimo, possuindo apenas 700 MB de tamanho [Baixe a ISO clicando aqui](https://www.archlinux.org/download/).

 Após ter efetuado o Download, crie um pendrive bootável com seu programa favorito, eu particularmente recomendo o [Balena Etcher](https://www.balena.io/etcher/).

* * *

Iniciando o ambiente em modo live
---------------------------------

 A partir do seu menu de boot, selecione o dispositivo que você colocou a ISO de instalação do Arch Linux, quando isso acontecer, você será redirecionado para uma tela parecida com esta:

![Tela do Grub Arch Linux](https://miro.medium.com/max/2508/1*y0tS-2m4E7k92RBDuR__PA.png)

 Caso você esteja dando boot em UEFI, verá uma tela mais simplificada, mas será algo do mesmo estilo. Normalmente é só selecionar a primeira opção e dar enter ;)

* * *

Definindo o Layout do teclado:
------------------------------

 Este passo consiste em informar pro sistema qual o layout do seu teclado, caso seu teclado seja americano (US), você não precisa seguir esses passos.

* * *

 Todos os layouts de teclado disponíveis podem ser listados com o seguinte comando:

    # ls /usr/share/kbd/keymaps/**/*.map.gz
    

 Para modificar o layout para o padrão brasileiro (ABNT-2) utilize o comando:

    loadkeys br-abnt2
    

 Ou para definir para um layout de teclado de português de Portugal:

    loadkeys pt-latin1
    

* * *

Conectar à internet
-------------------

*   Se você usa internet cabeada, certifique-se de que ela foi configurada com sucesso utilizando o comando `# ip link`
*   Para conexões sem fio utilize o comando [iwctl](https://www.cafecomterminal.cf/2020/11/iwd-um-curioso-utilitario-de-wi-fi.html)
*   Certifique-se que está conectado a internet `# ping duck.com`

* * *

#### Atualizar o Relógio do sistema

 Use o comando `# timedatectl set-ntp true` para garantir que o relógio do sistema esteja configurado corretamente.

* * *

Particionamento
---------------

 Está na hora de particionar seu sistema, e montar todas as partições.

 Primeiro use o comando `# fdisk -l` para listar todos os discos e partições do sistema. Agora você é capaz de ver todos os seus discos e partições, no meu caso, estou em uma máquina virtual, onde o disco tem 10 GB e nenhuma partição.

* * *

 Eu particularmente prefiro o particionamento a partir do cfdisk, faça isso utilizando o comando `cfdisk`.

 As seguintes partições são exigidas para instalação do Arch Linux:

*   Uma partição para a raiz do sistema `/`.
*   Para iniciar a partir de um sistema Uefi: uma partição de sistema EFI

**Exemplos de particionamento:**

**Bios com MBR**

Ponto de montagem

Partição

Tamanho sugerido

\[SWAP\]

/dev/partição\_swap

O mesmo que sua RAM

/mnt

/dev/partição\_raiz

Restante do Disco

**Uefi com GPT**

Ponto de montagem

Partição

Tamanho sugerido

/mnt/efi

/dev/partição\_efi

pelo menos 256 Mb

\[SWAP\]

/dev/partição\_swap

O mesmo que sua RAM

/mnt

/dev/partição\_raiz

Restante do Disco

### Formatar as partições

 Assim que você tenha criado todas as partições, cada uma deve ser formatada com um sistema de arquivos adequado. Por exemplo, se a partição raiz está em /dev/sda1 e receberá o sistema de arquivos ext4. Sabendo disso, execute:

`# mkfs.ext4 /dev/partição_raiz`

 Se você criou uma partição para SWAP (por exemplo, /dev/sda3), inicialize-a com os comandos:

`# mkswap /dev/partição_swap`  
`# swapon /dev/partição_swap`

### Montando as partições

* * *

 Monte a partição raiz em /mnt. Por exemplo, se a partição raiz for `/dev/sda1`:

    # mount /dev/sda1 /mnt
    

 Crie os pontos de montagem restantes (como /mnt/efi) usando o comando `mkdir` e monte suas partições.

* * *

Instalação
----------

### Instalar os pacotes essenciais

 Use o `pacstrap` para instalar o pacote base, um kernel e um firmware para hardwares comuns:

    # pacstrap /mnt base linux linux-firmware
    

Configuração do sistema
-----------------------

**Fstab**  

 Gere o arquivo fstab executando o comando 

`# genfstab -U /mnt >> /mnt/etc/fstab`

**Chroot**  

 “Transfira a consciência” para o seu novo sistema. Tudo que você fizer a partir de agora resultará no sistema final.

    # arch-chroot /mnt
    

**Fuso horário**

 Defina o fuso horário de acordo com a sua localização, por exemplo, para definir o fuso horário para o Recife:

    # ln -sf /usr/share/zoneinfo/America/Recife /etc/localtime
    

 Execute o comando hwclock para gerar o arquivo /etc/adjtime

    # hwclock --systohc
    

**Localização**

 Edite o arquivo `/etc/locale.gen` e remova o `#` da linha `pt_BR.UTF-8 UTF-8`. após isso, gere os locales executando:

    # locale-gen
    

 Crie o arquivo locale.gen para informar ao sistema que você precisa dele em português com o seguinte comando:

    # echo LANG=pt_BR.UTF-8 >> /etc/locale.conf
    

 Se você quiser tornar a alteração do layout do teclado permanente, utilize o comando:

    echo KEYMAP=seu_layout >> /etc/vconsole.conf
    

##### obs: substitua seu\_layout pelo layout do seu teclado, por exemplo: `# echo KEYMAP=br-abnt2 >> /etc/vconsole.conf`

* * *

**Configuração de rede**

 Escolha o nome do seu computador na rede:

    # echo umnomelegalaqui >> /etc/hostname
    

 Adicione as entradas de rede ao arquivo /etc/hosts, para isso você irá precisar do nano `# pacman -S nano`, após a instalação do nano ser concluida, digite o comando `# nano /etc/hosts`.

 Agora adicione as entradas correspondentes no arquivo:

127.0.0.1      localhost.localdomain	 localhost

`

::1		localhost.localdomain	  localhost

127.0.1.1	meuhostname.localdomain	  meuhostname

`

* * *

**Senha do usuário root**

 Este passo é muito importante. Caso você ignore-o, não conseguirá fazer login no seu sistema. Você deve digitar o comando `# passwd`, e escolher uma senha para o superusuário, não esqueça esta senha, ela será de extrema importância.

* * *

**Gerenciador de boot**

 Existem vários gerenciadores de boot, tais como Clover, GRUB, Syslinux, systemd-boot, entre outros, mais iremos instalar o mais comum entre distros Linux, o **GRUB.**

* * *

### Grub em máquinas Bios Legacy

 Para Instalar o GRUB na sua máquina, digite os seguintes comandos:

    # pacman -S grub
    

 O comando acima instala o pacote do GRUB, mas para instalá-lo na MBR, utilize o seguinte comando, substituindo sdX pela partição raiz do seu sistema.

    # grub-install --target=i386-pc /dev/sdX
    

 Perfeito! O GRUB está instalado, porém não está configurado. Irei ensinar como configurar um pouco mais abaixo.

* * *

### GRUB em sistema UEFI

 Para instalar o Grub em sua máquina UEFI, você irá precisar de 2 pacotes, o `grub` e o `efibootmgr`, você pode instalá-los com o seguinte comando:

    # pacman -S grub efibootmgr
    

 Para instalar o grub num sistema UEFI, você deve ter montado a partição EFI. Sendo assim, use o seguinte comando, e substitua `esp` pelo seu ponto de montagem:

    # grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB
    

Configuração do Grub BIOS/EFI
-----------------------------

 Sem este arquivo de configuração você receberá uma tela como esta se reiniciar: 

![Imagem demonstrando a tela de Grub Rescue](https://www.blogdainformatica.com.br/wp-content/uploads/2015/10/Grub-Reinstalando-Corrigindo-Atualizando.jpg)

 Para que isso não aconteça, você deve gerar o arquivo de configuração, usando o comando:

    # grub-mkconfig -o /boot/grub/grub.cfg
    

Grub instalado, mas... e a internet ?
-------------------------------------

 Você instalou o Grub com sucesso, mais caso reiniciasse agora, não teria acesso a internet. Para contornar isso, execute:

    # pacman -S networkmanager network-manager-applet && systemctl enable NetworkManager
    

* * *

**Parabéns!**  
 Você acaba de concluir a instalação do Arch Linux! Agora, você pode sair do ambiente de chroot, pressionando `ctrl + D`, e digitando reboot. Você pode, e deve remover o pendrive do seu computador, e se necessário, configurar a BIOS/UEFI.

  

Artigo escrito por: Redson

Revisado por: Daki e Kyu