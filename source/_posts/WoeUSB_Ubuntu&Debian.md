# Pen Drive Bootável De Windows 10

## Avisos!

- Essa dica só funciona em distros baseadas em Debian e em Ubuntu.
- É necessario pelo menos um Pen Drive de 8GB para realizar o processo.
- Se certifique de ter o **GDEBI** instalado em seu computador e o **unzip**.

# Informações

O **Woeusb** é um programa feito para realizar pen drives bootáveis de Windows no Linux. Sua instalação e seu uso é simples porem ao decorrer do tempo bugs foram surgindo fazendo com que o programa fosse inutilizavel.

Mas tem uma versão em especifica que ainda possui suporte para distros baseadas em Debian 10 e Ubuntu 20.10

## Encontrando o Pen Drive

Com o terminal aberto primeiro precisamos identificar nosso Pen Drive

  Para isso digite: 
  
 ``` 
$ sudo fdisk --list (Comando para listar todos os dispositivos de armazenamento conectados em seu computador) 
 ```

![Screenshot](https://i.imgur.com/0JJ3Rci.png?raw=true"ffff")

Nesse print podemos ver que o meu Pen Drive é o **/dev/sdb**. Com essa informação já podemos formatar ele.

**--> TENHA UM BACKUP DE SEUS ARQUIVOS ANTES DE FORMATAR**

Primeiro vamos retirar as partições montadas

![Screenshot](https://i.imgur.com/iSapAia.png?raw=true)

```
$ sudo umount /dev/sdb1 
```

Com a partição desmontada agora vamos formatar em tipo FAT32

```
$ sudo mkfs.vfat -I /dev/sdb
```

Realize de novo o comando **sudo fdisk --list** e para saber se seu procedimento deu certo tenha esse resultado

![Screenshot](https://i.imgur.com/sPQDxs2.png?raw=true)

## Baixando o Woeusb
Com a informação do Pen Drive ja podemos agora baixar o **Woeusb**.

https://www.mediafire.com/file/e5pzmvqbdtynskv/woeusb.zip/file (Clique no link para baixar o Woeusb)

Clique em woeusb.zip e quando terminar de baixar extraia o arquivo ou entre no terminal e na sua pasta atual digite.

```
$ unzip woeusb.zip
```

Você vai ver um pacote deb chamado: **woeusb_3.3.1_amd64.deb**

Instale-o via interface gráfica com o **Gdeb** ou pelo terminal (que é mais recomendado):

```
$ sudo apt install ./woeusb_3.3.1_amd64.deb
```
O apt deverá resolver as dependências para você e instalar o pacote.

## Instalando o Windows 10

Com a ISO de Windows 10 baixada, siga os passos que estão descritos em baixo para realizar a instalação com sucesso.

![](https://img.vivaolinux.com.br/imagens/dicas/comunidade/woeusb.png?raw=true)

## Guia:
1. Selecione a opção **From a Disk Image** e selecione sua ISO de Windows 
2. Depois disso selecione a opção **File System** para **NTFS**
3. Em **Target Device** selecione seu Pen Drive e então clique em Install
4. Aguarde o processo e pronto, Pen Drive bootável de Windows feito.
