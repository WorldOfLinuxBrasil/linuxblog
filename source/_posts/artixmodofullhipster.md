---
title: Instalação Artix Linux no Modo full hipster (Zfs na raiz)
date: 2020/11/28
author: Lin Diniz
---
O Artix Linux é uma distribuição baseada em Arch Linux que visa rodar o sistema sem o famoso systemd, os sistemas de
arquvos suportados são:

## Openrc
 
 - O OpenRC é um sistema init baseado em dependência. Foi criado por Roy Marples, um desenvolvedor do NetBSD que também estava ativo no projeto Gentoo. 

## Runit  

- Criado por Gerrit Pape, usado no open bsd e mais notoramente no Void Linux, ele visa iniciar o sistema e desligar o mesmo com apenas 3 fases 

## s6

- Esse é o menos utilizado pois nada passa de uma modificação do runit feito para facilitar o uso do mesmo

