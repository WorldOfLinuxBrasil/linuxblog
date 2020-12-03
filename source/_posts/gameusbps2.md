---
title: Como rodar jogos via usb no PS2
date: 2020/12/02
author: Androwinbr
---

--------------------------------------------------------------------------------------------------------

# Você vai precisar de:

-Um PC ou Notebook
-Um Pen Drive
-OPL instalado no seu PS2

# Atenção:

O windows é um sistema que colabora muito com instalação de jogos, já que existem varios apps que fazem isso, mas a ferramenta que sera usada esta disponivel para as duas plataformas de forma nativa.

# Instalando a ferramenta no Windows e no Linux

Voce devera baixar a ferramenta de acordo com seu sistema, as duas versões estão disponiveis no link no final do post.

# Windows:

Para usar a ferramenta no Windows basta você procurar o execultavel do programa.

# Linux:

Para execultar o programa no linux você devera abrir o terminal dentro da pasta que esta o arquivo e colocar o seguinte comando:

    ./oplpctools.sh

caso queira criar um arquivo desktop para colocar na area de trabalho execulte o comando:

    ./make-desktop-file.sh

# Escolhendo as pastas de destinos e instalando os jogos:

Quando o programa estiver aberto, você tera uma opção escrita open(abrir), que te levara para escolher o diretorio onde você ira colocar os jogos (Recomendo que instale no HD para depois copia para o Pen Drive), logo apos você ter escolhido, o diretorio, você devera escolher a opção install (Instalar), que te redirecionara para uma tela que tera duas opções: add image e add disc

# Adicionando jogos baixados:

Caso você tenha jogos baixados da internet, você devera escolher a opção add image que vai levar a uma tela para escolher onde esta a iso.
Com a iso selecionada você tera as opções no app:

    Media type: por padrão vem em auto, deixe inalterado

Por limitações de partições de FAT32, que não tem suporte a arquivos maiores que 4Gb, ele tambem das a opção:

    Split up ISO files into parts

Caso o jogo não tenha mais que 4Gb, você pode marcar a opção:

    Do not split up

O resto você podera deixar inalterado

# OBS.:

Caso você vá instalar mais de uma iso de uma vez lembre-se de fazer as escolhas de split up uma por uma, pois o app não aplica em todas de uma vez

--------------------------------------------------------------------------------------------------------
Site de download da ferramenta:
(https://github.com/brainstream/OPL-PC-Tools/releases)
---------------------------------------------------------------------
* * *
**artigo feito por: Vinicius Cavati Gobbi**
* * *