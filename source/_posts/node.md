---
title: Como instalar nodejs no Ubuntu e derivados
date: 2020/11/28
author: Redson
---
Saudações! No artigo de hoje irei ensinar a instalar o Node.js no Ubuntu e distribuições derivadas. Bom… você já deve ter percebido que o Node dos repositórios do Ubuntu vem desatualizado, com a versão 10, quando a atual no momento é a 15.2.0, vamos lá!

Instalando o NVM
----------------

É recomendável desinstalar qualquer versão do Node.js presente em sua máquina antes de instalar o NVM, para evitar futuros problemas.

Para instalar o NVM basta usar o comando Curl. Execute no terminal:

    $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | bash
    

Este comando executa um script que clona o repositório do NVM e coloca em um diretório em sua home, sendo ele `~/.nvm`

A versão mais recente do NVM no momento em que escrevi este artigo era a 0.37.0. Para garantir que você irá instalar a versão mais recente do NVM, copie este mesmo comando da [página do repositório do NVM no github](https://github.com/nvm-sh/nvm#installing-and-updating).

* * *

**Perfeito! Node instalado, mas não configurado**

Se você tentasse executar o NVM agora, receberia um erro como `bash: nvm: comando não encontrado` ou `zsh: command not found: nvm.` Para contornar isso, você deve colocar essas linhas no final do seu arquivo `.bashrc` ou `.zshrc`:

export NVM\_DIR="$HOME/.nvm"

`

[ -s "$NVM_DIR/nvm.sh"] && \. "NVM_DIR/nvm.sh" # Isso carrega o nvm

[ -s $NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # Isso carrega o auto complete do nvm

`

* * *

Utilizando o NVM
----------------

Agora irei mostrar alguns comandos disponíveis no NVM

**Verificando a versão do NVM**

    nvm --version
    

**Lista completa de versões do Node**

    nvm ls-remote node
    

**Instalando versões do Node**  
O NVM permite ter várias versões do Node.js na mesma máquina, e trocar de uma para outra de uma forma bem ágil. Basta executar o comando de instalação seguido da versão desejada.

Para instalarmos o Node.js na versão 14.15.0, executamos o seguinte comando:

     nvm install 14.15.0
    

Se você quiser simplesmente a versão mais atual do Node, o comando é esse:

    nvm install node
    

**Listando versões já instaladas**

    nvm ls
    

Você deve ver algo como isso:

![Imagem de demonstração do comando nvm ls](https://miro.medium.com/max/860/1*w7MUztGg0JvsCIN2Rk9wkw.png)

**Alternando entre as versões**

Uma coisa admirável no NVM é que você é capaz de usar mais de uma versão do node, e escolher a melhor na situação. Para usar, por exemplo, a LTS do Node.js mais recente instalada em sua máquina, execute isto:

    nvm use lts
    

Espero que com isso você consiga usufruir muito bem do Node no seu Ubuntu, obrigado por acessar este blog ;).

  

Artigo por: Redson dos Santos Silva

Revisado por: Daki