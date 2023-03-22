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
