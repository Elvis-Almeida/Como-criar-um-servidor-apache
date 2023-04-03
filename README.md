![intro](https://user-images.githubusercontent.com/70353348/226114161-a56a0475-c383-4d3d-9add-b48a8a57287e.gif)

# Introdução

Essa wiki documenta todas as etapas de implementação de um servidor apache proposto pelo professor [Paulo Henrique Sousa Barbosa](https://github.com/agenteph) na disciplina de Redes II do curso de Ciência da Computação do Instituto Federal de Educação, Ciência e Tecnologia do Maranhão - Campus Imperatriz (IFMA). Projeto implementado por [Elvis Rodrigues Almeida](https://github.com/Elvis-Almeida)

Em toda nossa jornada iremos utilizar uma máquina virtual, mas após a criação da máquina virtual e execução do `.iso` todo o resto será igual a um computador real após a execução do pen-drive bootável. Irei considerar que você saiba criar e executar um pen-drive bootável *(caso queira instalar em seu computador físico)* e também instalar o [VitualBox](https://www.virtualbox.org/) em seu PC, mas se você não tem esse conhecimento de como fazer, aqui estão alguns links que te ajudaram nisso:

>  [VirtualBox: Saiba o que é, como funciona e como instalar!](https://blog.b2bstack.com.br/virtualbox/)

> [Como criar um pendrive bootável com uma distro do Linux](https://tecnoblog.net/responde/como-criar-um-pendrive-bootavel-com-uma-distro-do-linux/)

> [Como dar boot no computador pelo pendrive](https://tecnoblog.net/responde/boot-pen-drive-windows-mac/). 

---

## Especificação do computador utilizado

Processador: Intel® Core™ i5-9300H CPU @ 2.40GHz × 8<br>
Memória ram: 8GB<br>
Placa de vídeo: GTX 1650<br>
Sistema operacioal: Linux Pop!_OS 22.04 LTS<br>
Disco: SSD NVMe m.2 512GB<br>
Placa de rede: Gigabit<br>

# Instalando servidor :rocket:

## Baixando `.iso` do ubunto server

Para baixar o `.iso` é muito simples, basta acessar o site oficial de download https://ubuntu.com/download/server e clicar em "Download Ubuntu Server". A versão que irei utilizar é a *Ubuntu Server 22.04.2 LTS*

![Captura de tela de 2023-03-18 14-47-23](https://user-images.githubusercontent.com/70353348/226124335-96c47bf8-fcf7-40c1-994e-fe983738a3cb.png)

---
Após clicar no botão seu download será iniciado automaticamente.

![Captura de tela de 2023-03-18 14-51-15](https://user-images.githubusercontent.com/70353348/226125864-17f81e97-f82c-439d-ae95-8bb678c0df0d.png)

---

## Criando máquina virtual 

Agora que já temos o `.iso` vamos criar nossa maquina virtual, basta abrir o **VirtualBox** e clicar em **Novo** 
![Captura de tela de 2023-03-18 15-03-38](https://user-images.githubusercontent.com/70353348/226125907-5a4ffd38-3f7c-4573-9467-1d90298dc66f.png)

Irá abrir uma janela como essa, e nela você colocará o nome da sua maquina vitual e selecionará a `.iso`. Após isso é só clicar em **Próximo**

![Captura de tela de 2023-03-21 21-44-12](https://user-images.githubusercontent.com/70353348/226775943-9eca2208-b0d8-41d8-8c8f-8330f963113d.png)

Nessa outra parte você vai apenas colocar um *nome do servidor* compatível e apertar em **Próximo** 

![Captura de tela de 2023-03-21 21-44-36](https://user-images.githubusercontent.com/70353348/226776355-4afe5481-f0c2-430e-be4d-b67a0df72eca.png)

Agora vamos configurar o hardware da nossa maquina virtual, essa parte é muito relativa ao hardware que você tem, o recomendado é que se utilize menos da metade da capacidade do seu computador, tanto em **CPU** quanto em menmória **RAM**. Depois é só clicar em  **Próximo**

![Captura de tela de 2023-03-21 21-44-59](https://user-images.githubusercontent.com/70353348/226776829-9e70487f-ced0-45e1-b607-23ef8be47666.png)

Essa parte irei colocar **25GB** de disco para ser usado pela maquina vitual, e conforme o espaço que você tiver disponível pode colocar mais ou menos, porém não deixe menos que **10GB** pois pode não ser sufuciente. Após isso é só clicar em  **Próximo**

![Captura de tela de 2023-03-21 21-45-19](https://user-images.githubusercontent.com/70353348/226777358-eff9fa2e-029b-4876-bc55-5375dd4718d7.png)

Nesse momento aparecerá um resumo das configurações, aperte em **Finalizar**

![Captura de tela de 2023-03-21 21-45-33](https://user-images.githubusercontent.com/70353348/226777840-fcbd6a80-9ce6-44a5-aa82-13c991c81f44.png)

## Instalando sistema operacional

Antes de iniciamos vamos em desativar a rede durante a instalação para que a instalação seja mais rápida, pois caso contrario iria ser feito varios downloads durante a instalação.

Para isso vamos em **Configurações**.

![Captura de tela de 2023-03-21 22-27-36](https://user-images.githubusercontent.com/70353348/226778223-c8cae63f-ea78-4bcf-9bee-0013e31c2b6b.png)

Depois selecione **Rede**, na janela de rede em **Conectado a**, selecione a opção **Placa em modo bridge** (*isso fará o computador virtual pegar o ip da sua rede real, dessa forma tornando possivel conectarmos ao servidor mais tarde*) e na opção avançado desmarque a caixinha de **Cabo conectado**. 

![Captura de tela de 2023-03-21 21-55-47](https://user-images.githubusercontent.com/70353348/226780008-fd604953-2cc2-45fa-b1c3-73e1ba0fdd1c.png)

Nesse momento é só apertar na setinha verde **Iniciar** para ligar a maquina virtual.

![Captura de tela de 2023-03-21 22-27-36](https://user-images.githubusercontent.com/70353348/226778223-c8cae63f-ea78-4bcf-9bee-0013e31c2b6b.png)

Quando iniciar aparecerá essa tela, nesse momento é só selecionar a primeira opção e apertar **Enter**

![Captura de tela de 2023-03-21 21-50-23](https://user-images.githubusercontent.com/70353348/226779184-242633d8-35f2-478b-b347-05095118a295.png)

Aqui você pode escolher o idioma. Aperte **Enter** para continuar

![Captura de tela de 2023-03-21 21-51-16](https://user-images.githubusercontent.com/70353348/226779458-0e9d69d4-9da4-4ab1-9d44-170b90260fd0.png)

Aqui você pode selecionar o idioma do teclado. Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-52-14](https://user-images.githubusercontent.com/70353348/226782227-3b948dd9-05a1-4e6e-be20-61c9eb552fe2.png)

Nessa parte mostra qual tipo de instalação você quer fazer. Selecione *Ubuntu server (minimized)* pois vamos instalar a versão minimizada do sistema e aperte em **Concluído**

![Captura de tela de 2023-03-21 21-52-25](https://user-images.githubusercontent.com/70353348/226782229-af819237-d418-4c3e-9317-f921c1c4518b.png)

Nessa parte mostra as entradas de rede. Como desativamos a rede aperte em **Contunuar sem rede**

![Captura de tela de 2023-03-21 21-56-36](https://user-images.githubusercontent.com/70353348/226782232-c4eb8acd-eee3-46fd-9db7-bd9aaf16d4d0.png)

Nessa parte é a configuração de proxy mas como não iremos utilizar agora aperte em **Concluído**

![Captura de tela de 2023-03-21 21-56-44](https://user-images.githubusercontent.com/70353348/226782234-3a6a2723-e0b3-4c06-b54e-a79a4fe4354d.png)

Aqui você pode apertar em **Concluído**

![Captura de tela de 2023-03-21 21-56-51](https://user-images.githubusercontent.com/70353348/226782237-99dce6ef-fb71-4c89-81fd-fb5c5a1f40ca.png)

Nessa parte também você aperte em **Concluído**

![Captura de tela de 2023-03-21 21-57-03](https://user-images.githubusercontent.com/70353348/226782238-1277eb33-506f-4808-982f-06269c203261.png)

Aqui mostra um resumo das configurações, aperte em **Concluído**

![Captura de tela de 2023-03-21 21-57-08](https://user-images.githubusercontent.com/70353348/226782240-2d2119f2-eaec-4e59-8906-b19c9c870912.png)

Aqui é só uma caixa de confirmação pois após continuar não será mais possível retornar as configurações anteriores, aperte em **Continue**

![Captura de tela de 2023-03-21 21-57-16](https://user-images.githubusercontent.com/70353348/226782244-4ac03b71-f1a5-4abe-a32c-a20118a47c14.png)

Nessa tela você colocará os nomes de servidor de usuario e de utilizador e a senha do seu servidor (*Não esqueça do nome do utilizador e nem da senha, pois você fará o login com eles*), aperte em **Concluído**

![Captura de tela de 2023-03-21 21-58-51](https://user-images.githubusercontent.com/70353348/226782247-d649147a-db61-45ab-8e13-13287108565f.png)

Aqui pergunta se você quer fazer o upgrade para ubunto pro, mas você pode pular apertando em **Continue**

![Captura de tela de 2023-03-21 21-59-00](https://user-images.githubusercontent.com/70353348/226782249-867ea921-e5af-43ec-923a-dbb010803fd5.png)

Aqui pergunta se você quer instalar SSH, você pode continuar sem instalar pois instalaremos esse serviço mais tarde. Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-59-11](https://user-images.githubusercontent.com/70353348/226782250-22c7610b-2ef2-4ecd-9704-273ef835f22d.png)

Nessa parte o sistema operacional será instalado e caso a instalação ocorra com sucesso é só apertar em **Reboot Now** para reiniar o servidor.

![Captura de tela de 2023-03-21 21-59-18](https://user-images.githubusercontent.com/70353348/226782252-a94d98c6-83bd-4ac2-97a1-8c25671c0654.png)

Após reiniciar o servidor será apresentado essa tela no qual você colocará seu usuário e senha (*agora você pode fazer o login no sistema com o usuario e a senha que criou anteriormente*).

![Captura de tela de 2023-03-21 22-05-36](https://user-images.githubusercontent.com/70353348/226784035-06cb94e8-c170-43da-8dfd-c308b32a6aca.png)

Se tudo estiver Ok você estará logado em seu servidor.

![Captura de tela de 2023-03-21 22-05-59](https://user-images.githubusercontent.com/70353348/226784037-b891ecf8-2ff4-434c-9f8d-6be9eab83dd6.png)

# Utilitários e configurações 

## Atualizando bibliotecas

Agora podemos voltar na configuração de rede da maquina vitual e selecionar a caixa *Cabo conectado* para podermos usar internet no computador virtual.

![Captura de tela de 2023-03-21 22-33-43](https://user-images.githubusercontent.com/70353348/226785748-b9e5d00b-20e4-4c9c-885d-3518c1e7031b.png)

> :warning: Vamos sempre está em modo **root** apartir de agora 

Para entrar nesse modo basta digitar o comando `sudo su` e depois digitar a senha.

![Captura de tela de 2023-03-21 22-32-31](https://user-images.githubusercontent.com/70353348/226785746-ad0f279b-c072-4cdf-a693-0a2e24d41efd.png)

Para atualizarmos as bibliotecas é só digitar o comando `apt update && apt upgrade` para baixar e atualizar.

![Captura de tela de 2023-03-21 22-34-51](https://user-images.githubusercontent.com/70353348/226785751-9128581c-1c1b-4c64-b6cf-75dc98750a24.png)

Ele irá perguntar se deseja continuar, é só digitar **y** e apetar **Enter**. É só aguardar atualizar que estará tudo pronto

![Captura de tela de 2023-03-21 22-39-54](https://user-images.githubusercontent.com/70353348/226785755-9d7718e8-20a1-4520-81f6-26e2f16c0749.png)

## Instalando utilitários 

Nessa parte vamos instalar algums utilitários que usaremos durante a instalação do apache, para isso utilizaremos o código `apt install nano inetutils-ping net-tools ip-tables iptraf-ng man-db openssh-server zip` que intalará todo o que precisamos por enguanto.

nesse comando instalaremos as seguites bibliotecas:

**Nano**: é um editor de texto simples e fácil de usar, com recursos básicos como edição, busca e substituição de texto.

**Inetutils-ping**: é uma ferramenta que permite testar a conectividade da rede, enviando pacotes de dados para um endereço IP e esperando por uma resposta.

**Net-tools**: é um conjunto de ferramentas de rede que inclui comandos como ifconfig, route e netstat, que permitem visualizar informações de rede, como endereços IP, rotas e conexões abertas.

**Ip-tables**: é um utilitário de linha de comando para gerenciamento de firewall, que permite bloquear ou permitir o tráfego de rede com base em regras definidas pelo usuário.

**Iptarf-ng**: é uma ferramenta de monitoramento de rede que exibe informações em tempo real sobre o tráfego de rede em uma interface gráfica do usuário.

**Man-db**: é um sistema de gerenciamento de manuais de usuário do Linux, que permite visualizar informações detalhadas sobre comandos e programas do sistema.

**OpenSSH-server**: é um servidor de protocolo SSH que permite o acesso remoto seguro a um computador ou servidor Linux.

**Zip**: é uma ferramenta de compactação de arquivos que permite criar, extrair e manipular arquivos ZIP.

![Captura de tela de 2023-03-22 16-35-47](https://user-images.githubusercontent.com/70353348/228021137-698c62b3-6d4a-4763-9b43-52bd0c1228de.png)

## Configurando SSH

> :warning: Todas as configurações no linux são arquivos 

Para configurarmos o SSH vamos nesse arquivo de configuração digitando o código `nano /etc/ssh/sshd_config`

![Captura de tela de 2023-03-23 14-52-59](https://user-images.githubusercontent.com/70353348/228023358-573c8db9-ec0b-45d1-aee8-722cf1342d04.png)

Após entrar no arquivo irá ter uma linha escrita `#Port 22` você irá apenas apagar a `#` e colocar a porta em que deseje utilizar o serviço, lembre-se de não utilizar 2 serviços na mesma porta, no meu caso coloquei na porta 222 como está na imagem.

![Captura de tela de 2023-03-23 14-55-08](https://user-images.githubusercontent.com/70353348/228025851-3093e86c-132e-42dd-beac-1079746ab00e.png)

![Captura de tela de 2023-03-23 14-53-42](https://user-images.githubusercontent.com/70353348/228024113-04fec54f-67f1-4933-8746-96e5a3990cac.png)

Aperte **Ctrl+O** e depois **Enter** para salvar o aquivo e depois de salvo **Ctrl+X** para sair do arquivo 

> :warning: Nunca esqueça de salvar o arquivo após editar, caso contrario será perdido toda modificação.

Vamos reiniciar o serviço SSH para aplicar as configurações corretamente, para isso digitaremos o comando `/etc/init.d/ssh restart`

![Captura de tela de 2023-03-23 14-56-31](https://user-images.githubusercontent.com/70353348/228026781-b818e2c0-d85a-48ce-8697-e3584a8259c3.png)

Para sabermos se tudo está correndo de forma certa após reiniciarmos vamos digitar o comando `/etc/init.d/ssh status`

![Captura de tela de 2023-03-23 14-56-43](https://user-images.githubusercontent.com/70353348/228027455-f67dc8f7-7e6e-4709-a162-04ae47a1709b.png)

Vemos que está funcionando corretamente 

## Acessando servidor via SSH

Para conectar precisamos saber o IP do servidor, para isso vamos digitar o comando `ifconfig`

![Captura de tela de 2023-03-23 15-07-02](https://user-images.githubusercontent.com/70353348/228029266-e3ae6465-2972-4a07-8902-4a83fb982555.png)

Vemos aqui que o IP do servidor é *192.168.43.227*

Após configurarmos o serviço SSH e pegarmos o IP podemos agora acessar nosso servidor apartir de outro computador, agora irei utilizar somente o terminal do meu computador real. Para acessar o SSH vamos digitar o seguinte comando na maquina que vai se conectar com o servidor `ssh nome_do_servidor@ip_do_servidor -p porta`, no meu caso ficou `ssh servidorifma@192.168.43.227 -p 222`

![Captura de tela de 2023-03-23 15-08-41](https://user-images.githubusercontent.com/70353348/228029921-7866777b-7d34-4793-8535-70ac17377281.png)

Digite `yes` e aperte `Enter`

![Captura de tela de 2023-03-23 15-08-51](https://user-images.githubusercontent.com/70353348/228029929-31287ce8-9a30-49a8-b4ba-96886d2273f6.png)

Digite a senha do seu servidor 

![Captura de tela de 2023-03-23 15-08-57](https://user-images.githubusercontent.com/70353348/228029931-f93fbe15-6e33-471c-a4a3-03b5a6c49814.png)

Agora vocẽ está conectado via SSH ao terminal do seu servidor

![Captura de tela de 2023-03-23 15-09-04](https://user-images.githubusercontent.com/70353348/228031335-5fc47ff5-bd6c-44be-a2e9-701c5bd2e8b1.png)

# Apache 

## Sobre o apache

O Apache é um software de servidor web que é utilizado para hospedar sites, aplicativos e serviços na Internet, ele oferece uma ampla variedade de recursos avançados, como suporte a múltiplos domínios e endereços IP, balanceamento de carga, segurança e controle de acesso e é altamente configurável e extensível, permitindo que você personalize a configuração para atender às necessidades específicas do seu projeto

## Baixando e instalando 

Vamos instalar o apache 
> :warning: Lembrando que todos os comandos seram feitos em usuário root

Para isso vamos digitar o comando `apt install apache2 apache2-doc` que baixará e instalará o apache e a documentação do mesmo

![Captura de tela de 2023-03-23 15-11-38](https://user-images.githubusercontent.com/70353348/228032706-9ddf0e75-84ad-41b9-8816-db7064b75094.png)

Após a instalação se ocorrer tudo certo você poderá escrever o ip do seu servidor no navegador que será apresentado uma página como esta.

![Captura de tela de 2023-03-23 15-12-49](https://user-images.githubusercontent.com/70353348/229310284-d0a6d24d-7039-441a-8a39-fbf7b0b9c30a.png)

## Arquivos e pastas

Antes de configurar vamos na pasta onde está as configurações do apache digitando `cd /etc/apache2` e depois `ls` para listar.

![Captura de tela de 2023-03-23 15-14-37](https://user-images.githubusercontent.com/70353348/229371040-a067301c-da8d-4008-bc05-441de0efb074.png)

São nesses arquivos e pastas que vamos configurar o apache. Esses arquivos e pastas são:

**apache2.conf**: Este é o arquivo de configuração principal do Apache. Ele define as configurações globais do servidor, como o diretório raiz do servidor, os módulos carregados e as opções de log.

**ports.conf**: Este arquivo define as portas nas quais o servidor web Apache escuta as conexões.

**sites-available** e **sites-enabled**: Essas pastas contêm arquivos de configuração que definem os sites virtuais que o Apache pode servir. O diretório sites-available contém os arquivos de configuração para todos os sites virtuais disponíveis, enquanto o diretório sites-enabled contém links simbólicos para os arquivos de configuração que estão ativos.

**mods-available** e **mods-enabled**: Essas pastas contêm arquivos de configuração que definem os módulos do Apache que estão disponíveis e habilitados. O diretório mods-available contém os arquivos de configuração para todos os módulos disponíveis, enquanto o diretório mods-enabled contém links simbólicos para os arquivos de configuração dos módulos habilitados.

**envvars**: Este arquivo define as variáveis de ambiente usadas pelo Apache, como o usuário e o grupo sob os quais o servidor é executado.

**conf-available** e **conf-enabled**: Essas pastas contêm arquivos de configuração que são usados para definir opções globais do servidor ou módulos que não têm um arquivo de configuração dedicado. O diretório conf-available contém os arquivos de configuração para todas as opções globais ou módulos disponíveis, enquanto o diretório conf-enabled contém links simbólicos para os arquivos de configuração que estão ativos.

**magic**: é um arquivo de especificações de formato de arquivo usado pelo Apache e outros utilitários para determinar o tipo de conteúdo de um arquivo com base em seu conteúdo.

---

O arquivo de log do apache fica em **/var/log/apache2**

![Captura de tela de 2023-03-23 15-45-20](https://user-images.githubusercontent.com/70353348/229380650-ab4fcc78-5b30-4ca0-b510-639fbcef1599.png)


## Configurando

### Gerais

> :warning: Sempre que modificarmos um arquivo vamos reiniciar o serviço e ver o status de funcionamento do mesmo, pois se deixar isso para o final será mais difícil descobrir o erro caso tenha ocorrido algum.

> :warning: Para evitar muita repetição de código, toda vez que eu voltar nas pastas estarei utulizando o código `cd ..`, para entrar em uma pasta estarei usando `cd nome_da_pasta`, para abrir um arquivo `nano nome_do_arquivo`, para salvar o arquivo `Ctrl + O` e para sair do arquivo `Ctrl + X`.

Para começarmos a configurar vamos entrar na pasta **conf-enabled** e abrir o arquivo **charset.conf**

![Captura de tela de 2023-03-23 15-15-59](https://user-images.githubusercontent.com/70353348/229372061-0cfa4932-9863-466d-a0e2-49e2f00d3c8b.png)

Dentro desse arquivo é só apagar a `#` do **AddDefultCharset UTF-8**. Essa configuração faz com que o servidor reconheça caracteres especiais como letras com acento por padrão.

![Captura de tela de 2023-03-23 15-16-06](https://user-images.githubusercontent.com/70353348/229372064-636844ba-e7d7-48a5-9dd1-c5105d93f535.png)

Agora voltando na pasta do apache vamos modificar o arquivo **apache2.conf**. Em **Timeout**, que é o tempo que uma conexão do cliente permaneçe aberta, *onde deixar o tempo muito alto pode consumir recursos do servidor e afetar o desempenho*, nessa configuração irei colocar em 60 (*esse numero é o tempo em segundos*). 

![Captura de tela de 2023-04-02 16-14-03](https://user-images.githubusercontent.com/70353348/229374158-917afa88-335c-48ab-9b40-ee8ba613acc5.png)

![Captura de tela de 2023-04-02 16-14-14](https://user-images.githubusercontent.com/70353348/229374159-d066ac05-c880-4c5a-ad3c-165e103fca3c.png)

Agora em **MaxKeepAliveRequests** que é quantidade de solicitações que podem ser enviadas por uma única conexão mantida ativa, que ajuda a equilibrar o desempenho e o uso de recursos do servidor, deixei no meu o valor de 50

![Captura de tela de 2023-04-02 16-22-15](https://user-images.githubusercontent.com/70353348/229375793-f7216a7c-7835-4f14-8edb-f41d8b4e67aa.png)

Descendo mais um pouco no arquivo temos o **<Directory /usr/share>** onde nele tem o **Require all granted** iremos modificar para **Require all denied** ele define as configurações para o diretório */usr/share* no sistema de arquivos e nesse caso estamos negando o acesso de todas as requisições.

![Captura de tela de 2023-04-02 16-15-46](https://user-images.githubusercontent.com/70353348/229374161-7774b070-b21e-4719-94fe-d91b01fcb699.png)

Agora você pode salvar e fechar esse arquivo.

---

Para aplicar e certificar que está tudo certo em nossa configuração vamos digitar o seguinte comando `/etc/init.d/apache2 restart` para reiniciar e o comando `/etc/init.d/apache2 status` para conferirmos se tudo ocorre como o esperado.

![image](https://user-images.githubusercontent.com/70353348/229376991-47d1dc3b-9b07-4225-b912-091761eb19eb.png)

Como podemos ver está tudo Ok.

---

Agora vamos para a pasta **sites-available** que é onde fica os sites disponíveis, vemos na imagem que dentro dessa pasta tem dois arquivos, o **000-defult.conf** e o **default-ssl.conf**, iremos fazer uma cópia do **000-defult.conf** com o nome de **010-elvis.conf** com o código `cp 000-defult.conf 010-elvis.conf`.

![Captura de tela de 2023-03-23 15-25-44](https://user-images.githubusercontent.com/70353348/229377142-bdde0fb5-0707-4618-b430-ab26d0f2f668.png)

Vamos habilitar nossa configuração de site **010-elvis.conf** com o comando `a2ensite 010-elvis.conf`, e já reiniciamos e conferimos se está tudo ok. 

![Captura de tela de 2023-03-23 15-31-04](https://user-images.githubusercontent.com/70353348/229377826-150c587d-3658-4a65-983a-e78a289ae01e.png)

A configuração **000-defult.conf** vem habilitada por padrão por isso vamos desabilitar ela com o comando `a2dissite 000-defult.conf`, e já reiniciamos e conferimos se está tudo ok. 

![Captura de tela de 2023-03-23 15-31-59](https://user-images.githubusercontent.com/70353348/229377827-c6dc4117-7658-4456-973d-0e519415a019.png)

Como agora temos somente a nossa configuração ativa vamos modifica-la entrando no arquivo **010-elvis.conf**. A primeira coisa que vamos fazer é apagar a `#` de **ServerName www.exemple.com** e modificar a url para a ulr que iremos usar futuramente com DNS que será **www.elvis.com** e em **ServerAdmin webmaster@localhost** vou trocar pelo meu email **elvis.r@acad.ifma.edu.br**

![Captura de tela de 2023-03-23 15-32-33](https://user-images.githubusercontent.com/70353348/229377919-805d807c-e587-4079-9857-50ef53c66729.png)
![Captura de tela de 2023-03-23 15-33-43](https://user-images.githubusercontent.com/70353348/229377920-6b5a0bd0-8486-4380-8621-21b9bb45d6de.png)

Após essas modificações iremos reiniciar e testar se está tudo Ok.

![Captura de tela de 2023-03-23 15-34-02](https://user-images.githubusercontent.com/70353348/229377922-61bb9f34-ded9-443a-b7df-85b6f1d61c05.png)

### Baixando e instalando site

Agora vamos trocar o site padrão que veio no apache para poder deixar nosso ambiente mais bonito, para isso vamos acessar o site https://html5up.net/ onde temos varios sites html para baixar.

![Captura de tela de 2023-03-21 21-27-56](https://user-images.githubusercontent.com/70353348/229378350-4621c116-fabd-4c5d-b7dd-485136e7f7b6.png)

Antes de baixarmos vamos primeiro deletar o site padrão, vamos para a pasta onde o site está o arquivo do site que é em `/var/www/html` e digitar o comando `rm index.html` que deletará o arquivo **index.html**

![image](https://user-images.githubusercontent.com/70353348/229379095-6dc2dbcf-9be9-41e6-8690-f1f2950048ab.png)

Vemos que não tem nada na pasta agora 

![image](https://user-images.githubusercontent.com/70353348/229379218-556da6b6-4dfa-4d25-96e6-b936863f0349.png)

Para baixarmos basta copiar o link de download do site e colar ele nesse comando (*você precisa está dentro da pasta /var/www/html para baixar dentro da pasta correta*) `wget --no-check-certificate link_de_download` no meu caso ficou `wget --no-check-certificate https://html5up.net/aerial/download`.

![image](https://user-images.githubusercontent.com/70353348/229379423-77e04ab7-bb22-4972-b8b9-79c0fcbf4d45.png)

Vemos que baixou um arquivo download, esse arquivo está compactado, para descompactar usaremos o código `unzip download`.

![image](https://user-images.githubusercontent.com/70353348/229379498-463cdf40-9c8f-4b68-b312-b28ef183fdeb.png)

![image](https://user-images.githubusercontent.com/70353348/229379591-b8ba611b-cbec-427c-b345-5eaac1ab1311.png)

Agora podemos ver os arquivos descompactados, observe que o arquivo download permaneceu vamos apaga-lo, já que não precisamos mais dele, usando `rm nome_do_arquivo`

![image](https://user-images.githubusercontent.com/70353348/229379705-bcab633f-c0fd-4a9f-b275-6374aa7ef60f.png)

Agora acessando nosso servidor pelo navegador vemos nossa nova página funcionando.

![image](https://user-images.githubusercontent.com/70353348/229379940-a399042d-b7b8-45fe-b855-7f8342a56bdc.png)

Caso queira modificar o site, é só mexer nos arquivos que baixou, eu fiz umas pequenas mudanças.

![image](https://user-images.githubusercontent.com/70353348/229380095-bbc326b8-7238-45f1-b6b2-da441a13b5bf.png)

Pronto agora finalizamos nossa configuração do apache.

# DNS 

## sobre 

DNS significa Domain Name System (Sistema de Nomes de Domínio, em português) e é um serviço essencial para a comunicação na internet ele é responsável por converter nomes de domínio em endereços IP, permitindo que os dispositivos se comuniquem uns com os outros.

## arquivos 

Os arquivos de configuração ficam na pasta **/etc/bind**


![Captura de tela de 2023-03-23 15-49-49](https://user-images.githubusercontent.com/70353348/229380749-b0b8ac3e-d33b-4803-926e-9edd68484cfa.png)

**db.0, db.255, db.empty, db.local, db.root**: São arquivos de zona que contêm informações básicas sobre os endereços IP e nomes de domínio, e são usados como modelos para a criação de novas zonas de DNS.

**named.conf.default-zones**: É um arquivo de configuração que define as zonas de DNS padrão que devem ser criadas automaticamente pelo BIND9.

**named.conf.options**: É um arquivo de configuração que contém opções de configuração gerais para o servidor BIND9, incluindo configurações de cache, limites de consultas, segurança e muito mais.

**named.conf.local**: É um arquivo de configuração que contém as informações específicas sobre as zonas de DNS que o servidor BIND9 deve hospedar, incluindo nomes de domínio, endereços IP e servidores de nomes autoritativos.

**named.conf**: É o arquivo de configuração principal do servidor BIND9, que inclui outros arquivos de configuração e define as configurações globais do servidor.

**named.rfc1912.zones**: É um arquivo de configuração que define as zonas de DNS que são sugeridas pela RFC 1912 para uso em redes locais.

**named.conf.local.dpkg-dist**: É um arquivo de configuração de backup que é criado durante a instalação do BIND9.

**bind.keys**: Este arquivo contém as chaves de assinatura de zona usadas para validar as respostas DNSSEC (DNS Security Extensions) que são recebidas pelo servidor

---

E o arquivo de log pode ser acessado por esse comando `journalctl -u named.service`

![image](https://user-images.githubusercontent.com/70353348/229381043-ec5644e2-27e6-436c-a3e3-8d7ed224954d.png)

## configurando 

Vamos começar copiando o arquivo **db.local** com o nome de **db.elvis.com** com o comando `cp nome_do_arquivo nome_do_novo_arquivo`


![Captura de tela de 2023-03-23 15-52-37](https://user-images.githubusercontent.com/70353348/229384521-7f2b6780-2710-452a-9308-a119cc2871c0.png)

Agora vamos entrar no arquivo db.elvis.com para configura-lo

![image](https://user-images.githubusercontent.com/70353348/229384637-3f46ffdf-927a-453c-9072-be9609ad82ed.png)

O TTL (Time-to-Live) define o tempo que o servidor leva para atualizar a cache dos dominios evitando que fiquem desatualizado*) não vamos modificar

Na linha abaixo do TTL vamos modificar o registro SOA (Start of Authority) para a zona. Ele contém informações de autoridade para a zona, incluindo o nome do servidor primário que é o **localhost.** e o endereço de e-mail do administrador que é **root.localhost** que vamos modificar respectivamente para **servidor.elvis.com** e **root.elvis.com** as configurações de serial refresh retry expire e negative cache TTL não iremos modificar

Nas proximas linhas iremos fazer a sequinte modificação 

```
@               IN      NS      elvis.com.
                IN      A       192.168.43.227
servidor        IN      A       192.168.43.227
www             IN      A       192.168.43.227
```

"**@ IN NS elvis.com.**", define o nome do servidor DNS como "elvis.com" para o domínio raiz, representado pelo "@".

"**IN A 192.168.43.227**", define o endereço IPv4 do servidor DNS como "192.168.43.227".

"**servidor IN A 192.168.43.227**", define um registro A para um host com o nome "servidor" e o endereço IPv4 correspondente "192.168.43.227".

"**www IN A 192.168.43.227**", define um registro A para um host com o nome "www" e o endereço IPv4 correspondente "192.168.43.227".

> :warning: O IP que você colocará no dns deve ser o do seu servidor

![image](https://user-images.githubusercontent.com/70353348/229384702-b0065ef0-e985-477d-b9ce-111b4a90a50f.png)

> :warning: Salve, reinicie e verifique o status

Agora vamos criar a zona DNS, basta irmos no arquivo `named.conf.local` e iremos adicionar a seguinte configuração.

```
zone "elvis.com" {
        type master;
        file "/etc/bind/db.elvis.com";
};
```

Em zone você adiciona o seu dominio igual ao do arquivo que acabamos de configurar, dentro das chaves coloque type master e em file você passe o local certinho do seu arquivo que configuramos anteriormente, certifique de que está tudo escrito de forma correta, qual quer detalhe pode acarretar em um erro

![image](https://user-images.githubusercontent.com/70353348/229389002-d3c552b1-67d7-461a-ad0b-e5441930675f.png)

> :warning: Salve, reinicie e verifique o status

Agora vamos criar a zona reversa do nosso dominio, para isso vamos copiar o arquivo **db.127** com o nome **db.seu_ip_ao_contrario.in-addr.arpa** que no meu caso ficou **db.43.168.192.in-addr.arpa**

![Captura de tela de 2023-03-23 16-21-40](https://user-images.githubusercontent.com/70353348/229389864-5531752a-6ce3-4efb-a388-e93ee50059bc.png)

Agora vamos modificar nosso arquivo, faremos o mesmo processo do nosso arquivo **db.elvis.com** porém agora vamos aplicar de forma inversa, que ficará dessa maneira

```
@       IN      NS      servidor.elvis.com.
        IN      PTR     servidor.elvis.com.
227     IN      PTR     servidor.elvis.com.
227     IN      PTR     www.
```

"**@ IN NS servidor.elvis.com.**" define que o servidor de nomes autoritativo para essa zona é servidor.elvis.com.

**IN PTR servidor.elvis.com.**: define um registro PTR (Pointer) que associa o endereço IP 192.168.43.227 ao nome de domínio servidor.elvis.com.

**227 IN PTR servidor.elvis.com.**: define um registro PTR que associa o endereço IP 192.168.43.227 ao nome de domínio servidor.elvis.com.

**227 IN PTR www.**: define um registro PTR que associa o endereço IP 192.168.43.227 ao nome de domínio www.

![image](https://user-images.githubusercontent.com/70353348/229390341-bedb67c9-98c2-43da-b7dc-7a9124045ae1.png)

> :warning: Salve, reinicie e verifique o status


Agora voltamos ao arquivo `named.conf.local` e iremos adicionar a seguinte configuração para a zona reversa.

```
zone "43.168.192.in-addr.arpa"{
        type master;
        file "/etc/bind/db.43.168.192.in-addr.arpa";
};
```
É a mesma logica do anterior só que para outro arquivo o 

> :warning: o nome da zona tem que ser o mesmo do arquivo sem o db. do inicio

![image](https://user-images.githubusercontent.com/70353348/229391253-424d62b7-5472-47c7-958e-52d33f7ce31f.png)

> :warning: Salve, reinicie e verifique o status

Agora vamos no arquivo **named.conf.opition** para adicionarmos um servidor de DNS no qual nosso servidor pode perguntar quando ele não souber as respostas.

Para isso é só descomentar a região **forwarders** e adicionar o ip do servidor de DNS que você quiser.

![Captura de tela de 2023-03-23 17-04-49](https://user-images.githubusercontent.com/70353348/229391999-3d666902-24f9-4194-8778-cdcf76695ec4.png)

> :warning: Salve, reinicie e verifique o status

Agora vamos mudar o dns do nosso computador indo em `/etc/resolv.conf` e colocando o ip do nosso servidor.

![Captura de tela de 2023-04-02 22-37-49](https://user-images.githubusercontent.com/70353348/229393156-cd02ecdd-1c2e-40e8-af07-4cb4324c063c.png)

Podemos testar usando o `nslookup ip_ou_dominio` e abrindo pelo navegador.

![image](https://user-images.githubusercontent.com/70353348/229393429-5e22e826-a13c-4c9a-a68f-bce77eedfe35.png)

![image](https://user-images.githubusercontent.com/70353348/229393477-05a9180f-00e4-4547-a7fd-12f806afb75e.png)

Como podemos ver, está tudo funcionando de acordo

# FTP