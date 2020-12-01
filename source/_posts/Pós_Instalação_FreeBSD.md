---
title: Pós Instalação Do FreeBSD
date: 2020/12/01
author: Drack
---

# Pos Install Free-BSD

Esse arquivo tem como intuito ser um pequeno ajudante na pós instalação do Free-BSD, mas como sempre, é **altamente recomendado** você ler a wiki oficial do Free-BSD.

## O que é o Free-BSD? 

Não é atoa que o **Free-BSD** é um dos segundos sistemas operacionais **Unix** mais populares, ficando apenas atras do **Linux** o **Free-BSD** se destaca pelo seu padrão **Unix-Like** e pelo seu alto valor de conteúdos e historia.

O sistema em si **BSD** é utilizado em plataformas muito populares e que hoje são as mais consumidas no mercado, isso acontece pela sua licença que permite você usar o código e privar ele ou manter livre, sempre ira depender das escolhas do usuário.

O **BSD** pode ser tanto utilizado para servidores em geral quanto em desktops normais, um exemplo disso é o tão grande (e caro) **MacOS**, sim o grande computador que custa um rim, e atualmente pertence a  Apple é feito a partir do sistema Free-BSD, como dito antes, a licença permite você privar o código.

Não está convencido? Sabia que até mesmo consoles como o **Playstation 3 e 4** são feitos a base do Free-BSD? Tanto que os usuários mais **hackerman** acharam jeitos de usar o Free-BSD no própio console, incrível não?

## Pós instalação do Free-BSD

Depois que você instalar o **Free-BSD** é necessário atualizar ele para podermos pegar a versão mais recente do sistema, para isso é necessário entrar como root e digitar o comando:
```bash
$ freebsd-update fetch && freebsd-update install
```
Esse comando ira pegar o update e atualizar direto.

## Atualizar a lista de ports

Para atualizar a lista de ports do Free-BSD precisamos importar o patch recente:
```
$ portsnap fetch
```
Extraimos os patchs:
```
$ portsnap extract
```
Agora atualizamos ele:
```
$ portsnap update
```

### Alterar o Shell

Uma coisa que iremos fazer agora séra instalar o Shell Bash, se você usa linux você sabe então o que o Bash. No Free-BSD por padrão o bash não vem configurando então teremos que configurar ele, para isso iremos dar o comando:
```bash
$ pkg install bash bash-completion
```
Aqui vai um pequeno resumo:
 - **Bash** --> Shell que normalmente é usado no **Linux**
 - **Bash Completion** --> Quando pressionar a tecla TAB, o comando se auto completa no Bash.
 
 Para alterar o Shell e agora podemos iniciar ele com o Bash definido como padrão nós damos o comando:
 ```bash
$ chsh -s /usr/local/bin/bash
```

Agora reinicie a maquina e pronto! Você tem o Bash como padrão.

## Configurar o sudo

Para configurar o sudo primeiro precisamos instalar ele, no caso iremos baixar duas coisas, o sudo e o editor de textos via terminal nano:
```bash
$ pkg install nano sudo
```

Depois de instalar esses dois pacotes agora precisamos condicionar nosso usurário como root, para isso iremos utilizar o nano justamente para editar essas configurações. Iremos então dar o comando:
```bash
$ nano /usr/local/etc/sudoers
```

Para isso precisamos procurar a linha com o ```root ALL=(ALL) ALL``` e então iremos adicionar em baixo dele o nosso usuário, ira ficar assim: 
```bash
root ALL=(ALL) ALL
seunomedeusuario ALL=(ALL) ALL
```

Depois descomem te a linha:
```bash
%wheel	ALL=(ALL=ALL)	ALL
```

## Corrigindo seu TimeZone

Se quiser ajustar seu timezoen basta digitar:
```bash
$ sudo tzsetup
```

## Configurando um firewall simples

Para podermos criar um firewall nós precisamos editar o arquivo rc.conf, então daremos o comando:
```bash
$ sudo nano /etc/rc.conf
```
Agora adicionamos nas ultimas linhas:
```bash
firewall_enable="YES"
firewall_quiet="YES" 
firewall_type="workstation"  
firewall_myservices="22 80 443 10000"  
firewall_allowservices="any"  
firewall_logdeny="YES"
```

Agora iremos iniciar esse serviço:

```bash
$ sudo service ipfw onestart
```

## Instalar uma Interface Gráfica

Aqui você pode escolher qual interface gráfica ira querer, no meu caso eu irei usar a interface **MATE**, então para isso iremos configurar o mate e uma tela de login para podermos iniciar.

Primeiro precisamos instalar o Xorg, então para isso iremos instalar através do comando:
```bash
$ pkg install xorg mate mate-desktop slim
```
Agora para configuramos a tela de login iremos editar o arquivo /etc/rc.conf, para isso digite:
```bash
$ sudo /etc/rc.conf
```
E iremos adicionar no arquivo:
```bash
hald_enable="YES"
dbus_enable="YES"
slim_enable="YES"
```

Agora iremos criar o arquivo **xinitrc**:
```bash
$ nano ~/.xinitrc
```

E nesse arquivo iremos adicionar as linhas:
```bash
export LC_ALL=pt_BR.UTF-8
export LANGUAGE=pt_BR.UTF-8
export LANG=pt_BR.UTF-8
exec mate-session
```
Depois é só dar reboot e então iniciar, e prontinho! Agora você tem o Free-BSD instalado e configurado na sua maquina!

## Bônus

Instale o projeto Homura para instalar steam, discord e drivers para jogar no Free-BSD

https://github.com/pehsa/Homura
