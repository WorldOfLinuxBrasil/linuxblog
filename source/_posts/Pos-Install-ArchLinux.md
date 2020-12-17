---
title: Pós instalação Arch Linux
date: 2020/11/29
author: Drack
---
## Configurar o sudo para seu usuário

Por padrão o Arch linux não vem com o sudo instalado, para podermos instalar e configurar ele nós entramos como root e escrevemos no terminal:
``` 
$ pacman -S sudo
```
Quando ele terminar a instalação nós vamos adicionar nosso usuário ao grupo root, com isso a gente escreve:
```
$ nano /etc/sudoers
``` 
Iremos descer até encontrar uma linha onde está escrito **"root ALL=(ALL) ALL"**, quando encontrarmos ele nós colocamos em baixo uma linha com nosso usuário, no meu caso ira ficar:

```
drack ALL=(ALL) ALL
```

Salve o arquivo e tente executar o comando:
```
$ sudo pacman -Syu
```

## Instalando o yay

O yay é um pacote onde permite baixar os pacotes e já ter eles compilados em nosso sistema, com ele a gente não precisa ir no git, clonar e dar makepkg.

Para baixarmos ele precisamos primeiramente do **git** e do **base-devel**, o git é o que permite clonarmos repositórios do github, o base-devel é o que permite a gente compilar ele.
```
$ sudo pacman -S git go base-devel
```
Depois de termos baixado vamos agora clonar o repositório do yay:
``` 
$ git clone https://aur.archlinux.org/yay.git
```
Entramos no diretório do yay:
``` 
$ cd yay/
``` 
E então compilamos ele:
``` 
$ makepkg -si
```
E pronto! Agora podemos uilizar o yay sem problemas, por exemplo instalar o discord, podemos instalar ele usando o yay dessa forma:

```
$ yay -S discord
```
## Instalar codecs de mídia

``` 
$ sudo pacman -S a52dec faac faad2 flac jasper lame libdca libdv libmad libmpeg2 libtheora libvorbis libxv wavpack x264 xvidcore gstreamer0.10-plugins
``` 
Codecs extras:
``` 
$ sudo pacman -S exfat-utils fuse-exfat a52dec faac faad2 flac jasper lame libdca libdv gst-libav libmad libmpeg2 libtheora libvorbis libxv wavpack x264 xvidcore gstreamer0.10-plugins flashplugin libdvdcss libdvdread libdvdnav gecko-mediaplayer dvd+rw-tools dvdauthor dvgrab
```
## Descompactadores
```
 $ sudo pacman -S p7zip p7zip-plugins unrar tar rsync
```
## Firewall

Nós iremos instalar um firewall, habilitar ele e habilitar durante a inicialização

Instalar:
``` 
$ sudo pacman -S ufw
```
Ativar ele:
``` 
$ sudo ufw enable
``` 
Conferir seus status:
``` 
$ sudo ufw status verbos
``` 
Ativar durante a inicialização
``` 
$ sudo systemctl enable ufw.service
``` 
