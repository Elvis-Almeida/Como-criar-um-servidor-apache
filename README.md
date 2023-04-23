![intro](https://user-images.githubusercontent.com/70353348/226114161-a56a0475-c383-4d3d-9add-b48a8a57287e.gif)

# Introdução

Essa wiki documenta todas as etapas de implementação de um servidor apache proposto pelo professor [Paulo Henrique Sousa Barbosa](https://github.com/agenteph) na disciplina de Redes de Computadores II do curso de Ciência da Computação do Instituto Federal de Educação, Ciência e Tecnologia do Maranhão - Campus Imperatriz (IFMA). Projeto implementado por [Elvis Rodrigues Almeida](https://github.com/Elvis-Almeida)

Em toda nossa jornada iremos utilizar uma máquina virtual, mas após a criação da máquina virtual e execução do `.iso` todo o resto será igual a um computador real após a execução do pen-drive bootável. Irei considerar que você saiba criar e executar um pen-drive bootável *(caso queira instalar em seu computador físico)* e também instalar o [VitualBox](https://www.virtualbox.org/) em seu PC, mas se você não tem esse conhecimento de como fazer, aqui estão alguns links que te ajudaram nisso:

>  [VirtualBox: Saiba o que é, como funciona e como instalar!](https://blog.b2bstack.com.br/virtualbox/)

> [Como criar um pendrive bootável com uma distro do Linux](https://tecnoblog.net/responde/como-criar-um-pendrive-bootavel-com-uma-distro-do-linux/)

> [Como dar boot no computador pelo pendrive](https://tecnoblog.net/responde/boot-pen-drive-windows-mac/). 

---

## Especificação do computador

Processador: Intel® Core™ i5-9300H CPU @ 2.40GHz × 8<br>
Memória ram: 8GB<br>
Placa de vídeo: GTX 1650<br>
Sistema operacioal: Linux Pop!_OS 22.04 LTS<br>
Disco: SSD NVMe m.2 512GB<br>
Placa de rede: Gigabit<br>

# Instalando servidor

## Baixando `.iso`

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

Depois selecione **Rede**, na janela de rede em **Conectado a**, selecione a opção **Placa em modo bridge** (*isso fará o computador virtual pegar o ip da sua rede real, dessa forma tornando possivel conectarmos ao servidor mais tarde*) e na opção avançado desmarque a caixinha de **Cabo conectado** (*isso fará nossa instalação ser mais rápida, pois não irá baixar pacotes durante a instalação o que pode causar demora*). 

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

## Atualizando pacotes

Agora podemos voltar na configuração de rede da maquina vitual e selecionar a caixa *Cabo conectado* para podermos usar internet no computador virtual.

![Captura de tela de 2023-03-21 22-33-43](https://user-images.githubusercontent.com/70353348/226785748-b9e5d00b-20e4-4c9c-885d-3518c1e7031b.png)

> :warning: Vamos sempre está em modo **root** apartir de agora 

Para entrar nesse modo basta digitar o comando `sudo su` e depois digitar a senha.

![Captura de tela de 2023-03-21 22-32-31](https://user-images.githubusercontent.com/70353348/226785746-ad0f279b-c072-4cdf-a693-0a2e24d41efd.png)

Para atualizarmos as pacotes é só digitar o comando `apt update && apt upgrade` para baixar e atualizar.

![Captura de tela de 2023-03-21 22-34-51](https://user-images.githubusercontent.com/70353348/226785751-9128581c-1c1b-4c64-b6cf-75dc98750a24.png)

Ele irá perguntar se deseja continuar, é só digitar **y** e apetar **Enter**. É só aguardar atualizar que estará tudo pronto

![Captura de tela de 2023-03-21 22-39-54](https://user-images.githubusercontent.com/70353348/226785755-9d7718e8-20a1-4520-81f6-26e2f16c0749.png)

## Instalando utilitários 

Nessa parte vamos instalar algums utilitários que usaremos durante a instalação do apache, para isso utilizaremos o código `apt install nano inetutils-ping net-tools ip-tables iptraf-ng man-db openssh-server zip` que intalará todo o que precisamos por enguanto.

nesse comando instalaremos as seguites pacotes:

**Nano**: é um editor de texto simples e fácil de usar, com recursos básicos como edição, busca e substituição de texto.

**Inetutils-ping**: é uma ferramenta que permite testar a conectividade da rede, enviando pacotes de dados para um endereço IP e esperando por uma resposta.

**Net-tools**: é um conjunto de ferramentas de rede que inclui comandos como ifconfig, route e netstat, que permitem visualizar informações de rede, como endereços IP, rotas e conexões abertas.

**Ip-tables**: é um utilitário de linha de comando para gerenciamento de firewall, que permite bloquear ou permitir o tráfego de rede com base em regras definidas pelo usuário.

**Iptarf-ng**: é uma ferramenta de monitoramento de rede que exibe informações em tempo real sobre o tráfego de rede em uma interface gráfica do usuário.

**Man-db**: é um sistema de gerenciamento de manuais de usuário do Linux, que permite visualizar informações detalhadas sobre comandos e programas do sistema.

**OpenSSH-server**: é um servidor de protocolo SSH que permite o acesso remoto seguro a um computador ou servidor Linux.

**Zip**: é uma ferramenta de compactação de arquivos que permite criar, extrair e manipular arquivos ZIP.

![Captura de tela de 2023-03-22 16-35-47](https://user-images.githubusercontent.com/70353348/228021137-698c62b3-6d4a-4763-9b43-52bd0c1228de.png)

# Serviço SSH

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

## Acessando SSH

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

# Servidor Web (Apache) 

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

### Adicionando site

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

# MySQL e PHP

## Sobre

MySQL é um sistema gerenciador de banco de dados relacional (RDBMS) de código aberto, ele é amplamente utilizado para armazenar e gerenciar grandes volumes de dados em sites e aplicativos web ele oferece uma variedade de recursos, incluindo suporte a múltiplos usuários, segurança, integridade de dados e alta disponibilidade.

PHP é uma linguagem de programação de código aberto amplamente utilizada para desenvolvimento web ela é usada principalmente para a criação de aplicativos web dinâmicos que interagem com bancos de dados, como o MySQL. O PHP permite a criação de páginas dinâmicas e interativas, além de oferecer suporte a diversas bibliotecas e frameworks para desenvolvimento web.

Juntos, o MySQL e o PHP formam uma combinação popular para desenvolvimento web, o PHP é capaz de se comunicar com bancos de dados MySQL e executar operações CRUD (criar, ler, atualizar, excluir) em registros de bancos de dados, permitindo que os desenvolvedores criem aplicativos web altamente dinâmicos e interativos.

## Instalando

Para instalar o php basta digitar esse comando `apt-get install php libapache2-mod-php` aonde `php` é o pacote de instalação da linguagem php já o pacote `libapache2-mod-php` é um módulo do Apache que permite ao servidor Apache interpretar e executar scripts PHP.

Para instalar o MySQL basta digitar esse comando `apt install MySQL-server` que será baixado e instalado em seu servidor.

## Configurando

Após instalado o php vamos reiniciar os serviços do apache2
`/etc/init.d/apache2 restart`

![image](https://user-images.githubusercontent.com/70353348/233841343-86a48d92-b63a-4950-9f08-20402dcb173f.png)

Agora vamos na pasta `/var/www/html` com o comando `cd /var/www/html` e vamos criar uma pasta php com o `mkdir php` vamos entrar nela com `cd` e criar o arquivo **index.php** com `touch index.php` e nesse arquivo vamos adicionar o sequinte código com o comando `nano index.php`:

```
<?php
phpinfo();
?>
```

![image](https://user-images.githubusercontent.com/70353348/233841472-ba744447-4dc8-4ac1-9abb-411162d27046.png)

Salve com Ctrl + O e feche com Ctrl + X

![image](https://user-images.githubusercontent.com/70353348/233841581-526e136d-9d02-46cc-933e-4b33fa7043ca.png)

Agora podemos acessar nosso servidor no endereço 192.168.43.227/php e vemos que está tudo funcionando. 

![image](https://user-images.githubusercontent.com/70353348/233841696-d8bbc5b3-b6f6-4f1e-9e04-a7a5dbb1bee3.png)

Você pode também configurar o php no arquivo de configuração com o código `nano /etc/php/VERSÃO/apache2/php.ini`

![image](https://user-images.githubusercontent.com/70353348/233841915-0713bbfb-6ec0-4990-b622-9e6b4a8e7fe5.png)

![image](https://user-images.githubusercontent.com/70353348/233841940-d145bf69-97d7-4a1a-a107-de89047a2d92.png)

Após instalar o MySQL, use o comando `mysql_secure_installation` para fazer as configurações iniciais 

Para vermos o se o MySQL está funcionando vamos ver o status do serviço com `systemctl status mysql`

![image](https://user-images.githubusercontent.com/70353348/233845503-a3b8b58f-0527-4e28-b692-f19f736598c6.png)

Vamos instalar também o PhpMyAdmin com o comando `apt install phpmyadmin` após você terminar a instalação basta acessar seu o menu de configuração que no meu caso é **192.168.43.227/phpmyadmin** 

![image](https://user-images.githubusercontent.com/70353348/233863232-35d78a2c-1ed3-4105-819b-4c7c547fd005.png)

![image](https://user-images.githubusercontent.com/70353348/233862994-cc977b1d-fdc0-4364-884f-305b3c369031.png)

![image](https://user-images.githubusercontent.com/70353348/233863571-d5c43de8-7145-4eae-9964-53b1cf16c89e.png)

![image](https://user-images.githubusercontent.com/70353348/233863591-2928d5c6-a409-44f8-b7fb-672a0f70bc26.png)




# Serviço DNS 

## Sobre 

DNS significa Domain Name System (Sistema de Nomes de Domínio, em português) e é um serviço essencial para a comunicação na internet ele é responsável por converter nomes de domínio em endereços IP, permitindo que os dispositivos se comuniquem uns com os outros.

## Instalando

Para baixar e instalar basta digitar esse código `apt install bind9 bind9-utils bind9-doc`

Onde temos os pacotes:

**bind9** que contém os arquivos necessários para instalar e executar o servidor DNS BIND9. Isso inclui os arquivos de configuração, pacotes e executáveis necessários para executar o servidor.

**bind9-utils** que contém utilitários e ferramentas adicionais relacionados ao BIND9, como o utilitário "dig" para consultas DNS, o utilitário "nslookup" para resolução de nomes de domínio, entre outros.

**bind9-doc** que contém documentação e manuais relacionados ao BIND9, incluindo o manual do usuário, manual do administrador e documentação técnica.

## Arquivos 

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

## Configurando 

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

# Serviço FTP

## Sobre

O FTP (File Transfer Protocol) é um protocolo utilizado para transferir arquivos pela internet. Ele permite a transferência de arquivos de um computador para outro através da rede, seja ela local ou global.

## Instalando

Para baixar e instalar basta digitar esse código `apt install proftpd` que baixará o pacote proftpd

## Configurando

Para confirarmos vamos primeiro á esse arquivo `/etc/proftpd/proftpd.conf` nele vamos primeiro trocar o nome do servidor de **Debian** para **elvis**


![Captura de tela de 2023-04-02 23-09-47](https://user-images.githubusercontent.com/70353348/229396057-930dac83-e253-4355-9bf9-6b9a0f5eb329.png)
![Captura de tela de 2023-04-02 23-10-00](https://user-images.githubusercontent.com/70353348/229396065-6234024e-2072-452e-861f-c73a3cb18796.png)

Em **ShowSymLinks** vamos deixar off, essa configuração determina se os links do sistema aparecem ou não para o usuário, nesse caso queremos que não apareça

![image](https://user-images.githubusercontent.com/70353348/229396228-d81eb931-ddd9-404c-b29f-0f305073c05a.png)

Vamos descomentar as configurações **DefaultRoot~** e **RequireValidShell off**, sendo que o **DefaultRoot** define o diretório inicial padrão para o usuário FTP após o login, no nosso caso o **~** representa o diretório home do usuário, onde após o login, o usuário será direcionado para o seu diretório home no servidor que no nosso caso será o **/home/usuarioftp1** já o **RequireValidShell off** define se permite que usuários com um shell inválido façam login no servidor FTP, como o valor que colocamos é off isso permite que qualquer usuário faça login, mesmo que o shell listado em /etc/passwd seja inválido.

![Captura de tela de 2023-04-02 23-15-03](https://user-images.githubusercontent.com/70353348/229396472-fc333883-28d6-4707-96ad-335e2ba078ec.png)
![Captura de tela de 2023-04-02 23-15-24](https://user-images.githubusercontent.com/70353348/229396476-71330164-3359-44ba-afe0-0e773ce5130a.png)

E no final do arquivo vamos adicionar as configurações **TransferRate RETR 30:100** e **RootLogin Off** onde o **TransferRate RETR 30:100** define o limite de taxa de transferência de download para os arquivos, no nosso caso, o limite é definido como sendo de 30 a 100 KB/s. já o **RootLogin Off** desabilita o login de usuários com o usuário root, faremos isso para melhor segurança. 

![Captura de tela de 2023-04-02 23-19-58](https://user-images.githubusercontent.com/70353348/229397311-1a7ac3a8-95cb-458e-9bca-d03bf40db352.png)

> :warning: Salve, reinicie e verifique o status

Use o comando `/etc/init.d/proftpd restart` para reiniciar o serviço e `/etc/init.d/proftpd status` para ver o status do serviço.

![image](https://user-images.githubusercontent.com/70353348/229621655-5650497a-4a17-435d-83d4-2beec2101ecd.png)

Após configuramos essa parte vamos criar um usuário, para poder usar o ftp com ele, para criar um usuário é só digitar o comando `adduser nome_do_usuário` e logo após digitar e senha (*não esqueça a senha!*)

![image](https://user-images.githubusercontent.com/70353348/229397732-c022c62f-29a5-45a8-8402-55ae8446d374.png)

Após isso aparecerá um breve formulário para preencher, ele é opicional, eu não preenchi e pulei apenas apertando `Enter`

---

Agora vamos modificar o seguinte arquivo `/etc/passwd` (*Muito cuidado ao mexer nessa configuração pois você pode perder o acesso ao servidor permanentimente, modifique somente o usuário que criou*) vamos modificar a pasta do usuário que acabamos de criar para ficar assim `/home/usuarioftp1/ftp` e a pasta do shell para `/usr/sbin/nologin` por isso colocamos o **RequireValidShell** em **off**

![Captura de tela de 2023-04-02 23-28-39](https://user-images.githubusercontent.com/70353348/229398049-43ce8e89-11e6-4872-bbc2-c74e9ebc0f98.png)
![Captura de tela de 2023-04-02 23-28-29](https://user-images.githubusercontent.com/70353348/229398041-c5d8de58-2732-496c-89b2-e34664b4a810.png)

Agora vamos criar a pasta ftp já que definimos anteriormente a pasta do usuário como `/home/usuarioftp1/ftp`, para isso vamos na pasta `/home` e no usurario que é o **usuarioftp1** em `/home/usuarioftp1` e estando nela digitamos `mkdir ftp` para criar a pasta **ftp**

![Captura de tela de 2023-04-02 23-33-49](https://user-images.githubusercontent.com/70353348/229399004-a18c127c-dfed-46bd-a780-71bee6713a40.png)
![Captura de tela de 2023-04-02 23-33-55](https://user-images.githubusercontent.com/70353348/229399009-0455b001-3e0c-4b40-8cec-55c35551c4bc.png)

> :warning: Salve, reinicie e verifique o status

Agora vamos mudar as permissões da pasta com os comandos `chown usuarioftp1:usuarioftp1 ftp` que troca o usuário da pasta **ftp** para o **usuarioftp1** pois como criamos ela com usuário root ela estava com permição apenas para o nosso usuário, e o `chmod 770 ftp` esse comando  modifica permissões de acesso a um arquivo ou diretório onde os numeros significam:

No primeiro dígito **7** define as permissões do proprietário do arquivo. No nosso caso o **7** significa que esse usuário pode ler, gravar e executar.

No segundo dígito **7** define as permissões do grupo proprietário do arquivo. O numero siginifica o mesmo do anterior

No terceiro dígito **0** define as permissões para outros usuários, nesse caso, esses usuários não tem permissão de leitura, gravação ou execução.

![Captura de tela de 2023-04-02 23-34-38](https://user-images.githubusercontent.com/70353348/229399010-78525847-3ef5-4731-9153-70344988837c.png)
![Captura de tela de 2023-04-02 23-37-35](https://user-images.githubusercontent.com/70353348/229399011-5910f8f4-24f2-40aa-808c-b6810e4733a3.png)

> :warning: Salve, reinicie e verifique o status

Agora é só conectar, no meu caso irei usar o gerenciador de arquivos do Linux que tem essa possibilidade de conectar FTP 

Digitei essa url `ftp://ip_do_seu_servidor` na página outros dispositivos

![Captura de tela de 2023-04-02 23-42-41](https://user-images.githubusercontent.com/70353348/229400683-699702a8-fbe7-4a05-8585-1e9840174d28.png)

Fiz o login com o usuário e a senha que criei

![Captura de tela de 2023-04-02 23-43-02](https://user-images.githubusercontent.com/70353348/229400686-d574ae0c-f972-4938-bdc7-870e25530f68.png)

E aqui estamos acessando a pasta do servidor direto do meu computador

![image](https://user-images.githubusercontent.com/70353348/229400541-af490a7d-4f6c-4f7d-93e8-845b518a203a.png)

Enviei uma imagem para essa pasta

![image](https://user-images.githubusercontent.com/70353348/229400800-c1c1ae3e-30a0-48b6-a3fa-3056d865f089.png)

Aqui podemos ver a imagem pelo nosso servidor

![image](https://user-images.githubusercontent.com/70353348/229400888-b73fb892-3acd-4833-a3b9-2a90a2bdbb13.png)

Aqui é um teste de download do arquivo do servidor, e como podemos ver está de fato limitado de 30Kb/s a 100Kb/s

![image](https://user-images.githubusercontent.com/70353348/229629901-74051f14-ce28-44bb-b9d7-902a20a851c4.png)

# Serviço Samba

## Sobre 

O Samba é também uma solução de compartilhamento de arquivos e também de impressoras, ele amplamente utilizado em redes mistas com diferentes sistemas operacionais, oferecendo uma forma simples e segura de compartilhar recursos em uma rede local ou na internet.

## Instalando 

Para baixar e instalar o Samba basta digitar esse código `apt install samba samba-common` onde o pacote **samba** contém os arquivos binários e pacotes necessários para executar o serviço, já o pacote **samba-common** contém arquivos de configuração compartilhados entre os componentes do Samba, como os arquivos de configuração do daemon e os arquivos de configuração do cliente.

## Configurando

Antes de configurarmos vamos fazer o backup do arquivo de configuração **smb.conf** que está na pasta `/etc/samba`, com o comando `cp` 

![image](https://user-images.githubusercontent.com/70353348/229634138-0075af68-c8b4-4bb8-a61c-9469e53576b6.png)

Após isso vamos abrir o arquivo **smb.conf** para configura-lo. vamos selecionar e apagar toda essa configuração que veio nele.

Para selecionar você segura o `Shift + seta para baixo` e para apagar precione `ctrl + k`

![image](https://user-images.githubusercontent.com/70353348/229635359-2453f854-3a53-4b42-b04c-5c6a15f511fd.png)

![image](https://user-images.githubusercontent.com/70353348/229636218-9846ed44-42d3-498b-8231-48d32bdc1c82.png)

Agora vamos adicionar um exemplo de configuração (*existem várias formas de configurar essa é apenas uma delas*)

```
[global]
netbios name = usuarioftp1
workgroup = usuarioftp1
server string = Servidor dos Alunos
security = user

[public]
path = /home/samba
guest ok = yes
browseable = yes
writeable = yes
printable = no
create mask = 0777
force create mode = 0777

[printers]
comment = Compartilhando as Impressoras
print ok = yes
guest ok = yes
path = /var/spool/samba

[elvis]
Comment = Diretórios dos alunos
path = /etc/samba/elvis
valid users = usuarioftp1
create mask = 0777
force create mode = 0777
read only = no
```

Onde essas configurações significam:

**[global]** - significa que as configurações dentro dela afetam todo o servidor Samba

**[homes]** - significa que as configurações dentro dela afetam a pasta home para cada usuário

**[printers]** - significa que as configurações dentro dela controlam as impressoras na rede

**[nome_qualquer]** – significa que as configurações e informações são personalizadas

---

Configurações dentro das chaves:

**_-_** **netbios name**: define o nome do servidor.

**_-_** **workgroup**: define o nome do grupo de trabalho/domínio.

**_-_** **server string**: define a string de descrição do servidor.

**_-_** **security**: define o modo de segurança que no nosso caso é de usuário.

**_-_** **path**: define o caminho para o diretório compartilhado.

**_-_** **guest ok**: permite que usuários não-autenticados acessem o compartilhamento.

**_-_** **browseable**: permite que o compartilhamento seja listado pelos clientes.

**_-_** **writeable**: permite que os usuários possam escrever arquivos no compartilhamento.

**_-_** **printable**: permite a impressão de arquivos do compartilhamento.

**_-_** **create mask**: define as permissões dos arquivos criados pelos usuários no compartilhamento.

**-- O que cada numero significa, você pode fazer junção deles --** 

>**0000**: Nenhum acesso para o usuário proprietário, nenhum acesso para o grupo proprietário e nenhum acesso para outros usuários.

>**0001**: Execução para outros usuários.

>**0002**: Escrita para outros usuários.

>**0003**: Escrita e execução para outros usuários.

>**0004**: Leitura para outros usuários.

>**0005**: Leitura e execução para outros usuários.

>**0006**: Leitura e escrita para outros usuários.

>**0007**: Leitura, escrita e execução para outros usuários.

>**0010**: Execução para o grupo proprietário.

>**0020**: Escrita para o grupo proprietário.

>**0030**: Escrita e execução para o grupo proprietário.

>**0040**: Leitura para o grupo proprietário.

>**0050**: Leitura e execução para o grupo proprietário.

>**0060**: Leitura e escrita para o grupo proprietário.

>**0070**: Leitura, escrita e execução para o grupo proprietário.

>**0100**: Execução para o proprietário do arquivo.

>**0200**: Escrita para o proprietário do arquivo.

>**0300**: Escrita e execução para o proprietário do arquivo.

>**0400**: Leitura para o proprietário do arquivo.

>**0500**: Leitura e execução para o proprietário do arquivo.

>**0600**: Leitura e escrita para o proprietário do arquivo.

>**0700**: Leitura, escrita e execução para o proprietário do arquivo.

**_-_** **force create mode**: força as permissões dos arquivos criados pelos usuários no compartilhamento.

**_-_** **Comment**: define o comentário sobre o compartilhamento.

**_-_** **valid users**: lista de usuários autorizados a acessar o compartilhamento, %U para todos os usuários.

**_-_** **hosts allow**: define uma lista de hosts ou sub-redes que podem acessar o compartilhamento.

**_-_** **read only**: define se o compartilhamento é somente leitura.

**_-_** **directory mask**: define as permissões dos diretórios criados pelos usuários no compartilhamento.

**_-_** **print ok**: permite que as impressoras sejam compartilhadas.

> Cada configuração dessa pode ser colcada em qualquer chave, há muitas possibilidades de configurações aqui, mas a que irei utilizar será essa.

![image](https://user-images.githubusercontent.com/70353348/233784814-d2d81a75-f203-4874-8e88-07d6b5a11039.png)

> :warning: Salve, reinicie e verifique o status

Para reiniciar o serviço digite o comando `/etc/init.d/smbd restart` e para ver o status do serviço `/etc/init.d/smbd status`

![image](https://user-images.githubusercontent.com/70353348/229672654-873bad8b-154b-4f06-8a32-460d12d528f1.png)

Agora vamos criar as pastas que listamos nas configurações e das as permissões para que ela possa ser acessada.

Nesse primeira parte criei a pasta **elvis** usando o comando `mkdir nome_da_pasta`, listei as permissões da pasta com `ls -l` alterei o usuario da pasta para o usuarioftp1 com o omando `chown usuário:grupo_do_usuário pasta` e depois alterei as permissões com o comando `chmod 777 pasta` permitindo que a pasta seja totalmente aberta, cuidado ao fazer isso, pois pode deixar falhas de segurança. 

![image](https://user-images.githubusercontent.com/70353348/232339331-286636b6-150a-450f-b116-85e0fa53b05d.png)

Fiz o mesmo processo para a pasta publica. 

Agora para finalizar a configuração vamos adicionar o usuarioftp aos usuarios samba com o comando `smbpasswd -a usuário`.

![image](https://user-images.githubusercontent.com/70353348/232340591-b34116c6-e3cd-43bc-a731-b9ee6e70b7a8.png)

Agora já podemos enviar arquivos para nosso servidor, basta colocar logim e senha na pasta de usuario ou entrar como anônimo na pasta publica.

![image](https://user-images.githubusercontent.com/70353348/232341386-37b2a33f-f434-4035-9102-441a1d35ca2b.png)

![image](https://user-images.githubusercontent.com/70353348/232341520-5f7b24a3-37ac-4895-b3df-52e9488cdfa6.png)

![image](https://user-images.githubusercontent.com/70353348/232341555-8e6dfac1-f566-43cc-8fd1-4fff66c6c6a5.png)

![image](https://user-images.githubusercontent.com/70353348/232341633-d0d2ce7f-648b-4af4-a277-3d150bca6e24.png)

![image](https://user-images.githubusercontent.com/70353348/232341674-8f29e741-4e46-48a5-bcaa-c70f12db0a2d.png)

![image](https://user-images.githubusercontent.com/70353348/232341690-c63a5f84-ba4f-47fa-8ad7-15899fd720cb.png)

# Serviço DHCP

## Sobre

O DHCP (Dynamic Host Configuration Protocol) é um protocolo de rede que permite a atribuição dinâmica de endereços IP (Internet Protocol) a dispositivos em uma rede. É o serviço que configura os ips automaticamente nas máquinas conectadas.

## Instalando

Para baixar e instalar o serviço basta digitar esse código `apt install isc-dhcp-server` que baixará os pacotes

## Configurando 

Primeiramente vamos configurar o arquivo `nano /etc/default/isc-dhcp-server`, nesse arquivo é onde apontamos qual será o nosso arquivo de configuração e onde apontaremos também qual interface de rede nosso serviço atuará. Para fazermos isso vamos descomentar o `DHCPDv4_CONF=/etc/dhcp/dhcpd.conf` que é aonde nosso arquivo de configuração está, agora vamos definir nossa interface de rede a qual nosso serviço atuará, para saber qual interface de rede você vai usar é só usar o comando `ifconfig` e escolher a interface que está utilizando, para saber qual interface está utilizando basta ver qual delas tem o **IP** da rede em que você está conectado. no meu caso é a **enp0s3**

![image](https://user-images.githubusercontent.com/70353348/233788063-abe746db-8983-4640-9845-20e70a7c3f6a.png)

![image](https://user-images.githubusercontent.com/70353348/233787327-cf501de6-bd70-4a2e-b479-e9cfcc1171ba.png)

> :warning: Não esqueça de salvar!

![image](https://user-images.githubusercontent.com/70353348/233787927-8fe1d81a-4ef0-41e2-8ad1-78822b9b4cea.png)

Agora vamos para a pasta do serviço `cd /etc/dhcp/` e abrir o arquivo **dhcpd.conf** que é o que faz a configuração do servidor DHCP e define as configurações de rede que o servidor DHCP deve oferecer aos clientes. 

Abrindo ele faremos as seguintes configurações, em **domain-name** irei colocar o meu **elvis.com** que foi criado anteriormente e em **domain-name-servers** colocarei o ip do meu servidor de DNS que é o `192.168.43.227` e mais outro sendo ele o servidor de DNS da CloundFLare `1.1.1.1`. O **default lease time** que é o tempo em que o cliente pode usar o endereço IP atribuído antes que ele precise renovar com o servidor DHCP vamos deixar em `86400` que é o tempo em segundos que em horas da 24, já o **max lease time** é o tempo máximo que o endereço IP pode ser mantido pelo cliente antes de precisar ser renovado vamos colocar em `172800` esse tempo também está em segundos que em horas dá 48. e vamos adicionar o **ignore client-updates** que faz que o servidor não atualize o DNS do cliente automáticamente quando ele solicita um novo ip.

> :warning: Esse é apenas um exemplo de configuração, você pode alterar essas configurações conforme suas nessecidades.

![image](https://user-images.githubusercontent.com/70353348/233789532-aae63e59-d7a2-4753-bb8c-bf7fc334969a.png)

![image](https://user-images.githubusercontent.com/70353348/233791044-a5125e6e-8da9-47c4-8e90-0200d4ca56ae.png)

Você pode adicionar uma máquina para ter um ip fixo basta adicionar esse código no arquivo substituindo o mac do computador e colocar o ip que você quer que ele tenha.

```
host meupcfixo {
  hardware ethernet 08:00:07:26:c0:a5;
  fixed-address 192.168.0.12;
}
```

Agora vamos adionar esse exemplo de configuração, no meu caso eu configurei dessa forma.

```
subnet 192.168.43.0 netmask 255.255.255.0 {
  range 192.168.43.2 192.168.43.254;
  option domain-name-servers 192.168.43.227;
  option domain-name "elvis.com";
  option routers 192.168.43.1;
  option broadcast-address 192.168.43.255;
  default-lease-time 600;
  max-lease-time 7200;
}
```

> :warning: é muito provavel que você terá que adaptar o código para sua rede.

![image](https://user-images.githubusercontent.com/70353348/233796764-367fc6a1-99df-4aa3-ae72-605bac9edc88.png)

Onde cada opção faz o seguinte:

**Subnet 192.168.43.0 netmask 255.255.255.0** - Define o endereço IP e a máscara de sub-rede da rede. O endereço IP é 192.168.43.227 e a máscara de sub-rede é 255.255.255.0, o que significa que a rede pode ter até 256 hosts (*mas somente 253 endereços IP disponíveis para alocação devido ao endereço de rede e de broadcast*).

**Range 192.168.43.2 192.168.43.254** - Define o intervalo de endereços IP que podem ser alocados aos clientes. No nosso caso, o intervalo é de **192.168.43.2 a 192.168.43.254**.

**Option domain-name-servers 192.168.43.227** - Especifica o endereço do servidor DNS que será fornecido aos clientes.

**Option domain-name "elvis.com"** - Define o nome de domínio que será fornecido aos clientes.

**Option routers 192.168.43.1** - Especifica o endereço do roteador padrão para a rede. Neste caso, o roteador padrão é 192.168.43.1.

**Option broadcast-address 192.168.43.255** - Define o endereço de broadcast da rede.

**Default-lease-time 600** - Define o tempo de locação padrão para os endereços IP alocados aos clientes. Neste caso, o tempo de locação padrão é de 600 segundos (*10 minutos*).

**Max-lease-time 7200** - Define o tempo máximo de locação para os endereços IP alocados aos clientes. Neste caso, o tempo máximo de locação é de 7200 segundos (*2 horas*), isso diz que após 2 horas, o cliente deverá renovar a locação do endereço IP.

**ddns-update-style** - Especifica como os registros DNS dinâmicos são atualizados. Em **none** ele não atualiza registros DNS dinâmicos automaticamente.

> :warning: após configurar salve, reinicie o serviço e verifique o status

Agora vamos reiniciar e conferir o status com `/etc/init.d/isc-dhcp-server restart` e `/etc/init.d/isc-dhcp-server status`

![image](https://user-images.githubusercontent.com/70353348/233796853-50549cb1-1180-4d09-b525-4f6ce70b71ba.png)

Caso haja algum erro você pode verificar o log do serviço com esse comando `journalctl -u isc-dhcp-server`.

Aqui vemos no mesmo log mensionado acima que um computador se conectou e recebeu ip de nosso servidor

![image](https://user-images.githubusercontent.com/70353348/233797076-9bf3aecd-ccb7-4b66-8b2b-a2e41242b9ba.png)

Aqui vemos o ip que foi fornecido

![image](https://user-images.githubusercontent.com/70353348/233797145-72232fab-b5c1-4922-aa30-ad065c165835.png)

Aqui vemos o DNS que foi fornecido

![image](https://user-images.githubusercontent.com/70353348/233797181-c19e18eb-00f5-43a0-8795-16fbf6b98a33.png)

# Serviço proxy (Squid)

## Sobre

O Squid é um servidor de proxy de cache web que é utilizado para melhorar a velocidade da internet armazenando em cache os arquivos e páginas da web frequentemente acessados, reduzindo assim o tráfego de internet e melhorando o desempenho geral da rede, além disso ele serve também como um bloqueador de conteúdo passando regras de bloqueio de acesso.

## Instalando

Para instalar o serviço é só digitar esse comando `apt install squid` que será baixado e instalado em seu computador.

## Configurando

Para começarmos vamos entrar na pasta do serviço `cd /etc/squid` e abrir o arquivo `nano squid.conf` 

> :warning: É fortemente recomendável você ler todo esse arquivo pois o squid apresenta uma grande variedade de configurações e eu vou apresentar apenas uma parte dela.

![image](https://user-images.githubusercontent.com/70353348/233801279-8564b619-4d75-48a8-944c-96fe4b292166.png)

Após isso vamos limpar todo o arquivo com esse comando `echo "0" > squid.conf` esse comando escreverá 0 substituindo todos os dados do arquivo, assim o arquivo terá apenas um 0 dentro dele.

![image](https://user-images.githubusercontent.com/70353348/233805776-7610769a-1bc7-4dff-811b-c5e81ad24124.png)

Para configurar o squid temos esse exemplo de configuração.

```
http_port 3128 
error_directory /usr/share/squid/errors/Portuguese
cache_mem 1024 MB
cache_dir ufs /var/spool/squid 1000 16 256
maximum_object_size_in_memory 64 KB
maximum_object_size 50 MB
cache_swap_low 70
cache_swap_high 95

access_log daemon:/var/log/squid/access.log squid
cache_log /var/log/squid/cache.log

acl localnet src 192.168.43.0/24
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 # https
http_access deny !Safe_ports

acl sitesproibidos url_regex -i "/etc/squid/sitesproibidos"
http_access deny localnet sitesproibidos
http_access allow localnet
http_access allow all
```

> :warning: A ordem das configurações **importam**, primeiro você coloca as configurações especificas depois você pode permitir ou negar tudo, caso você permita ou nege logo no inicio do arquivo todas as configurações especificas abaixo seram **ignoradas**.

Onde essas configurações siginificam: 

**http_port 3128** - Configura a porta em que o Squid irá escutar conexões HTTP que no nosso caso é a 3128.

**error_directory /usr/share/squid/errors/Portuguese** - Define o diretório em que o Squid irá buscar as páginas de erro para apresentar aos usuários em caso de acesso negado ou outro erro, no nosso caso o diretório é definido como /usr/share/squid/errors/Portuguese, indicando que as mensagens serão exibidas em português.

**cache_mem 1024 MB** - Define a quantidade de memória RAM que o Squid irá usar para armazenar em cache as requisições feitas pelos clientes.

**cache_dir ufs /var/spool/squid 1000 16 256** - Configura o diretório onde o Squid irá armazenar as páginas em cache em disco, bem como algumas opções de tamanho do cache.

> ufs: é o tipo de sistema de arquivos usado para armazenar o cache. "ufs" significa "Unix File System" (Sistema de Arquivos Unix).

> /var/spool/squid: é o diretório onde o cache será armazenado. 

> 1000: é o tamanho máximo do cache em megabytes, nesse caso, o tamanho máximo é de 1000 MB.

> 16: é o número máximo de subdiretórios no diretório de cache. Essa opção ajuda a limitar o tamanho do diretório de cache e melhorar a velocidade de acesso aos arquivos de cache.

> 256: é o número máximo de objetos de cache em cada subdiretório e tem a mesma finalidade da anterior

Como as pastas iram ficar com essa configuração 

![image](https://user-images.githubusercontent.com/70353348/233805677-b3552ca8-26d4-4124-9e48-370482b59521.png)

**maximum_object_size_in_memory 64 KB** - Define o tamanho máximo de objetos que serão armazenados na memória RAM do servidor.

**maximum_object_size 50 MB** - Define o tamanho máximo de objetos que serão armazenados em disco.

**cache_swap_low 70** - Define a porcentagem de uso do disco em que o Squid começa a mover objetos menos utilizados para o disco.

**cache_swap_high 95** - Define a porcentagem de uso do disco em que o Squid começa a remover objetos menos utilizados para liberar espaço em disco.

**access_log daemon /var/log/squid/access.log squid** - Configura o arquivo de log do Squid.

**cache_log /var/log/squid/cache.log** - Configura o arquivo de log do cache do Squid.

**acl localnet src 192.168.43.0/24** - Define uma lista de acesso para a rede local, permitindo que somente clientes dessa rede possam acessar o Squid.

**acl Safe_ports port 80** - Define uma ACL para as portas seguras que serão acessadas pelo Squid nesse caso permite o acesso à porta 80.

**http_access deny !Safe_ports** Define uma regra para negar o acesso a todas as portas que não estão listadas na ACL Safe_ports.

**acl sitesproibidos url_regex -i "/etc/squid/sitesproibidos"** - Define uma lista de acesso para os sites proibidos, baseada em uma expressão regular definida no arquivo /etc/squid/sitesproibidos.

> acl sitesproibidos: Cria uma lista de controle de acesso chamada "sitesproibidos".

> url_regex: Especifica que a ACL deve usar uma expressão regular para comparar as URLs.

> -i: Indica que a comparação deve ser case-insensitive.

> "/etc/squid/sitesproibidos": Especifica o caminho do arquivo contendo a lista de sites proibidos que será usado como base para comparação na ACL "sitesproibidos".

**http_access deny localnet sitesproibidos** - Define uma regra para negar o acesso aos sites proibidos pela ACL sitesproibidos para clientes da rede local.

**http_access allow localnet** - Define uma regra para permitir o acesso total à rede local.

**http_access allow all** - Define uma regra para permitir o acesso a todos os clientes.

> :warning: Salve o arquivo!!

Agora vamos criar o arquivo **sitesproibidos** com o comando `touch nome_do_arquivo` e vamos adicionar nele os sites que queremos bloquear

![image](https://user-images.githubusercontent.com/70353348/233802854-7101dea1-c8c3-463b-9e98-0879057d100e.png)

Aqui podemos adicionar a lista de todos os sites que queremos bloquear

![image](https://user-images.githubusercontent.com/70353348/233806793-9e8af3b0-21dc-4efb-9bf9-d33035a88032.png)

Agora vamos consigurar o arquivo `/proc/sys/net/ipv4/ip_forward` que é usado para ativar ou desativar o encaminhamento de pacotes IP entre as interfaces de rede de um sistema Linux, fazemos isso apenas mudando seu valor de 0 para 1 com o comando `echo 1 > /proc/sys/net/ipv4/ip_forward`

> :warning: Após configurado **reinicie** o servidor para a configuração ser efetivada

![image](https://user-images.githubusercontent.com/70353348/233803126-1243dbd8-cad0-4bd6-8920-03cfc8cdf1b4.png)

Agora vamos rodar esse comando `iptables -t nat -A POSTROUTING -o enp0s3 -s 192.168.43.0/24 -j MASQUERADE` esse comando adiciona uma regra à tabela **nat** do iptables que permite o mascaramento de endereços de rede. 

> A opção **-t nat** indica que estamos trabalhando na tabela de tradução de endereços de rede.

> A opção **-A POSTROUTING** indica que estamos adicionando uma nova regra de pós roteamento.

> **-o** é a opção que indica a interface de saída, ou seja, a interface pela qual os pacotes serão encaminhados.

> **-s** é a opção que define a origem dos pacotes que serão mascarados.

> **-j MASQUERADE** é a opção que faz o mascaramento de endereço. Quando essa opção é usada, o endereço de origem do pacote é alterado para o endereço IP da interface de saída.

![image](https://user-images.githubusercontent.com/70353348/233803454-671b8b74-29cf-48b7-a7e9-575dc3e5c6d8.png)

Após essas configurações reinicie e verifique o status

![image](https://user-images.githubusercontent.com/70353348/233803758-469e9f7b-66e8-41c5-b6d5-b35d3fbc3671.png)

Agora é para está tudo funcionando.

---

Vamos configurar o nosso sistema operacional (*no meu caso o PopOS*, caso você queira testar no windowns veja esse link, [windows-10-como-configurar-um-proxy](https://canaltech.com.br/windows/windows-10-como-configurar-um-proxy/)) para adicionar nosso proxy. Para isso vamos nas configurações e depois em rede.

![image](https://user-images.githubusercontent.com/70353348/233807972-5a14b82b-ba21-4f6d-b4e4-c692ced47426.png)

Em proxy de rede vamos adicionar nosso proxy manualmente

![image](https://user-images.githubusercontent.com/70353348/233807978-ac1d83a7-0a6d-40d5-87d0-2cadb8b11106.png)

Aqui fiz o teste tentando acessar o site que marquei como proibido, podemos ver que o squid não permitiu, como esperado.

![image](https://user-images.githubusercontent.com/70353348/233804103-b317b662-6888-4400-b67b-0dbe3bdf6d8c.png)

Com esse comando podemos ver o log em tempo real do nosso servidor `tail -f /var/log/squid/access.log`, aqui podemos os acessos que estava fazendo e ele bloqueando os do **pao.com**

![image](https://user-images.githubusercontent.com/70353348/233804181-bd1f961f-1f80-4cca-95ae-e9ec68435e11.png)

Para você que chegou até aqui tem um bônus, vamos personalizar nossa página de acesso negado ou qual quer outra que desejar. Basta ir para essa pasta `cd /usr/share/squid/errors/Portuguese/` onde estão as páginas HTML que aparecem em caso de erro. 

![image](https://user-images.githubusercontent.com/70353348/233804666-22709fc0-28c2-4319-bd1c-1c9ecf76af20.png)


Faça um backup antes de modificar `cp ERR_ACCESS_DENIED ERR_ACCESS_DENIED.bkp`

Após isso é só modificar conforme queira o arquivo com `nano ERR_ACCESS_DENIED`

![image](https://user-images.githubusercontent.com/70353348/233804683-e2482478-45a3-4905-8084-96c18b7bff66.png)

Adicionei meu código

![image](https://user-images.githubusercontent.com/70353348/233805075-e78a7cfe-aefc-41a5-978e-c21424c0bc59.png)

> :warning: Salve, reinicie o serviço e veja funcionando 

![image](https://user-images.githubusercontent.com/70353348/233805374-9f172579-21be-44d9-bbff-50c664818f93.png)

---

Após um tempinho de uso 

![image](https://user-images.githubusercontent.com/70353348/233809164-753d753a-da83-4a1b-a27a-cb4525d7cd6f.png)


# Serviço IPSec

## Sobre

## Instalando

## configurando



