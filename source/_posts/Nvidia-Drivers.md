# Drivers Nvidia no FreeBSD

Se você estiver seguindo o manual de configuração do Xorg, ignore o que o manual diz sobre a execução do Xorg -configure.

Não execute o Xorg -configure

Se você já seguiu o manual e criou um xorg.conf, certifique-se de remover /etc/X11/xorg.conf ou /usr/local/etc/X11/xorg.conf antes de prosseguir:
```
$ rm -f /etc/X11/xorg.conf /usr/local/etc/X11/xorg.conf
```

## Instalando os drivers nvidia:

1 - Instale  x11/nvidia-driver
```
$ pkg install nvidia-driver
```
Para algumas placas mais antigas, você precisa usar x11/nvidia-driver-340 ou x11/nvidia-driver-304.

Consulte a página de download da NVIDIA para ver qual versão do driver você precisa. Observe que não há necessidade (e é até contraproducente) baixar o driver dessa página.

2 - Execute
```
$  sysrc kld_list+="nvidia-modeset"
```
 Para adicionar uma entrada a /etc/rc.conf para carregar os módulos do kernel na inicialização.

nvidia-modeset está disponível apenas para versões de driver >= 358.009, se você usar uma versão mais antiga, use ``` sysrc kld_list+="nvidia"```.

3 - Reinicialize com ```shutdown -r now``` ou carregue os módulos de kernel necessários agora com ```kldload nvidia-modeset``` ou ```kldload nvidia```

4 - Crie o diretório:
```
$ mkdir -p /usr/local/etc/X11/xorg.conf.d
```

5 - Use seu editor de texto no /usr/local/etc/X11/xorg.conf.d/driver-nvidia.conf com o script abaixo:

```
Section "Device"
        Identifier "NVIDIA Card"
        VendorName "NVIDIA Corporation"
        Driver "nvidia"
EndSection
```

6 - Reinicialize
