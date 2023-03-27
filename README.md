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

Selecione o idioma e aperte **Enter**

![Captura de tela de 2023-03-21 21-51-16](https://user-images.githubusercontent.com/70353348/226779458-0e9d69d4-9da4-4ab1-9d44-170b90260fd0.png)

Selecione o idioma do teclado e aperte em **Concluído**

![Captura de tela de 2023-03-21 21-52-14](https://user-images.githubusercontent.com/70353348/226782227-3b948dd9-05a1-4e6e-be20-61c9eb552fe2.png)

Selecione *Ubuntu server (minimized)* pois vamos instalar a versão minimizada do sistema e aperte em **Concluído**

![Captura de tela de 2023-03-21 21-52-25](https://user-images.githubusercontent.com/70353348/226782229-af819237-d418-4c3e-9317-f921c1c4518b.png)

Aperte em **Contunuar sem rede**

![Captura de tela de 2023-03-21 21-56-36](https://user-images.githubusercontent.com/70353348/226782232-c4eb8acd-eee3-46fd-9db7-bd9aaf16d4d0.png)

Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-56-44](https://user-images.githubusercontent.com/70353348/226782234-3a6a2723-e0b3-4c06-b54e-a79a4fe4354d.png)

Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-56-51](https://user-images.githubusercontent.com/70353348/226782237-99dce6ef-fb71-4c89-81fd-fb5c5a1f40ca.png)

Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-57-03](https://user-images.githubusercontent.com/70353348/226782238-1277eb33-506f-4808-982f-06269c203261.png)

Aqui mostra um resumo das configurações, aperte em **Concluído**

![Captura de tela de 2023-03-21 21-57-08](https://user-images.githubusercontent.com/70353348/226782240-2d2119f2-eaec-4e59-8906-b19c9c870912.png)

Aqui é só apertar em **Continue**

![Captura de tela de 2023-03-21 21-57-16](https://user-images.githubusercontent.com/70353348/226782244-4ac03b71-f1a5-4abe-a32c-a20118a47c14.png)

Nessa tela você colocará os nomes e senha do seu servidor (*Não esqueça do usuário e nem da senha*), aperte em **Concluído**

![Captura de tela de 2023-03-21 21-58-51](https://user-images.githubusercontent.com/70353348/226782247-d649147a-db61-45ab-8e13-13287108565f.png)

Aperte em **Continue**

![Captura de tela de 2023-03-21 21-59-00](https://user-images.githubusercontent.com/70353348/226782249-867ea921-e5af-43ec-923a-dbb010803fd5.png)

Aperte em **Concluído**

![Captura de tela de 2023-03-21 21-59-11](https://user-images.githubusercontent.com/70353348/226782250-22c7610b-2ef2-4ecd-9704-273ef835f22d.png)

Nessa parte ele será instalado e caso a instalação ocorra com sucesso é só apertar em **Reboot Now** para reiniar o servidor.

![Captura de tela de 2023-03-21 21-59-18](https://user-images.githubusercontent.com/70353348/226782252-a94d98c6-83bd-4ac2-97a1-8c25671c0654.png)

Após reiniciar o servidor será apresentado essa tela no qual você colocará seu usuário e senha.

![Captura de tela de 2023-03-21 22-05-36](https://user-images.githubusercontent.com/70353348/226784035-06cb94e8-c170-43da-8dfd-c308b32a6aca.png)

Se tudo estiver Ok você estará logado em seu servidor.

![Captura de tela de 2023-03-21 22-05-59](https://user-images.githubusercontent.com/70353348/226784037-b891ecf8-2ff4-434c-9f8d-6be9eab83dd6.png)

# Utilitários e configurações 

## Atualizando bibliotecas

Agora podemos voltar na configuração de rede da maquina vitual e selecionar a caixa *Cabo conectado* para podermos usar internet no computador virtual.

![Captura de tela de 2023-03-21 22-33-43](https://user-images.githubusercontent.com/70353348/226785748-b9e5d00b-20e4-4c9c-885d-3518c1e7031b.png)

Vamos sempre está em modo **root** no servidor para fazer todas as configurações apartir de agora. para entrar nesse modo basta digitar o comando `sudo su` e depois digitar a senha.

![Captura de tela de 2023-03-21 22-32-31](https://user-images.githubusercontent.com/70353348/226785746-ad0f279b-c072-4cdf-a693-0a2e24d41efd.png)

Para atualizarmos as bibliotecas é só digitar o comando `apt update && apt upgrade` para baixar e atualizar.

![Captura de tela de 2023-03-21 22-34-51](https://user-images.githubusercontent.com/70353348/226785751-9128581c-1c1b-4c64-b6cf-75dc98750a24.png)

Ele irá perguntar se deseja continuar, é só digitar **y** e apetar **Enter**

![Captura de tela de 2023-03-21 22-39-54](https://user-images.githubusercontent.com/70353348/226785755-9d7718e8-20a1-4520-81f6-26e2f16c0749.png)

Após isso vamos reiniciar nosso servidor digitando o comando `reboot`

![Captura de tela de 2023-03-21 23-22-43](https://user-images.githubusercontent.com/70353348/226785757-d3cd3d7c-679e-4196-a2f3-bfecc5654f58.png)

## Instalando utilitários 

Nessa parte vamos instalar algums utilitários que usaremos durante a instalação do apache, para isso utilizaremos o código `apt install nano inetutils-ping net-tools ip-tables iptraf-ng man-db openssh-server zip` que intalará todo o que precisamos por enguanto.

![Captura de tela de 2023-03-22 16-35-47](https://user-images.githubusercontent.com/70353348/228021137-698c62b3-6d4a-4763-9b43-52bd0c1228de.png)

## Configurando SSH

Para configurarmos o SSH vamos nesse arquivo de configuração digitando o código `nano /etc/ssh/sshd_config`

![Captura de tela de 2023-03-23 14-52-59](https://user-images.githubusercontent.com/70353348/228023358-573c8db9-ec0b-45d1-aee8-722cf1342d04.png)

Após entrar no arquivo irá ter uma linha escrita `#Port 22` você irá escrever apenas apagar a `#` e colocar a porta em que deseje utilizar o serviço, lembre-se de não utilizar 2 serviços na mesma porta, no meu caso coloquei na porta 222 como está na imagem.

![Captura de tela de 2023-03-23 14-55-08](https://user-images.githubusercontent.com/70353348/228025851-3093e86c-132e-42dd-beac-1079746ab00e.png)

![Captura de tela de 2023-03-23 14-53-42](https://user-images.githubusercontent.com/70353348/228024113-04fec54f-67f1-4933-8746-96e5a3990cac.png)

Aperte **Ctrl+O** e depois **Enter** para salvar o aquivo e depois de salvo **Ctrl+X** para sair do arquivo 

Vamos reiniciar o serviço SSH para aplicar as configurações corretamente, para isso digitaremos o comando `/etc/init.d/ssh restart`

![Captura de tela de 2023-03-23 14-56-31](https://user-images.githubusercontent.com/70353348/228026781-b818e2c0-d85a-48ce-8697-e3584a8259c3.png)

Para sabermos se tudo está correndo de forma certa após reiniciarmos vamos digitar o comando `/etc/init.d/ssh status`

![Captura de tela de 2023-03-23 14-56-43](https://user-images.githubusercontent.com/70353348/228027455-f67dc8f7-7e6e-4709-a162-04ae47a1709b.png)

Vemos que está funcionando corretamente 

## Acessando servidor via SSH

Para conectar precisamos saber o IP do servidor, para isso vamos digitar o comando `ifconfig`

![Captura de tela de 2023-03-23 15-07-02](https://user-images.githubusercontent.com/70353348/228029266-e3ae6465-2972-4a07-8902-4a83fb982555.png)

Vemos aqui que o IP do servidor é *192.168.43.227*

Após configurarmos o serviço SSH e pegarmos o IP podemos agora acessar nosso servidor apartir de outro computador, agora irei utilizar somente o terminal do meu computador real. Para acessar o SSH vamos digitar o seguinte comando `ssh nome_do_servidor@ip_do_servidor -p porta`, no meu caso ficou `ssh servidorifma@192.168.43.227 -p 222`

![Captura de tela de 2023-03-23 15-08-41](https://user-images.githubusercontent.com/70353348/228029921-7866777b-7d34-4793-8535-70ac17377281.png)

Digite `y` e aperte `Enter`

![Captura de tela de 2023-03-23 15-08-51](https://user-images.githubusercontent.com/70353348/228029929-31287ce8-9a30-49a8-b4ba-96886d2273f6.png)

Digite a senha do seu servidor 

![Captura de tela de 2023-03-23 15-08-57](https://user-images.githubusercontent.com/70353348/228029931-f93fbe15-6e33-471c-a4a3-03b5a6c49814.png)

Agora vocẽ está conectado via SSH ao terminal do seu servidor

![Captura de tela de 2023-03-23 15-09-04](https://user-images.githubusercontent.com/70353348/228031335-5fc47ff5-bd6c-44be-a2e9-701c5bd2e8b1.png)

# Instalando Apache 

Agora podemos instalar o apache Lembrando que todo comando será feito em usuário root

![Captura de tela de 2023-03-23 15-11-38](https://user-images.githubusercontent.com/70353348/228032706-9ddf0e75-84ad-41b9-8816-db7064b75094.png)
