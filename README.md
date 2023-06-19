# Introdução

Essa wiki documenta as etapas de implementação de um servidor Windows (windows Server), realizado na disciplina de Redes de Computadores II do curso de Ciência da Computação do Instituto Federal de Educação, Ciência e Tecnologia do Maranhão - Campus Imperatriz (IFMA), ministrada pelo professor [Paulo Henrique Sousa Barbosa](https://github.com/agenteph). Projeto por [Pedro Fernades Bahury](https://github.com/pfbahury).

Para realizar as atividades será necessario a utilização de uma maquina virtual, ou [VirtualBox](https://www.virtualbox.org), e uma imagem `.iso` do sistema operacional que iremos utilizar, neste caso, o [Windows Server](https://www.microsoft.com/pt-br/evalcenter/download-windows-server-2016), e instalar a versão em inglês de 64 bits.

> ⚠️ esta é uma versão de teste, tendo acesso gratuito de apenas 180 dias, caso queira implementar como servidor de produção recomenda-se comprar uma licença oficial.

# Configurando a Maquina Virtual

Logo de começo, recomendo um guia de criação de uma maquina virtual, para os que não possuem o costume de utilizar uma, recomendo o seguinte [guia](https://tecnoblog.net/responde/como-criar-uma-maquina-virtual-virtualbox/)

> ⚠️ Recomendo colocar no mínimo 30GB na maquina virtual

## Configurando a rede

Após criar a sua maquina virtual, clique na engrenagem amarela para acessar as configuração gerais da maquina, dentro das configurações, clique nas aba de **rede**. As configurações estarão como padrão em modo NAT, mude para modo bridge, e dentro das configurações avançadas, mude o **Modo Promícuo**, para **Tudo Permitido**, deixando do mesmo jeito que a imagem.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/73dc8de2-e7be-4595-9e82-7651347d2ea3)

Após essa configuração, iniciaremos a maquina. Dentro da instalação, nas primeiras 2 telas, selecione **next**, e logo em seguida, **Install now**. Na terceira tela de setup, selecionaremos a versão do Windows, neste caso a **2016 Standard Evaluation (Desktop Experience)**, que é a versão que utilizaremos.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/059dfa5a-bf9d-421a-9168-be59033921d6)

Após aceitar os termos faremos uma instalação customizada

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/c723ec2e-69fa-4e8d-aba9-de40956f2bfa)

Selecionaremos o Disco, e aguardaremos o fim da instalação

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/54fa6fd2-21eb-4d1e-b007-d123855b879d)

Com o fim da instalação, faremos as configurações iniciais para o usuario e a senha, para um servidor real, é EXTREMAMENTE recomendado uma senha **forte** para o seu servidor em produção, com letras maiusculas, minusculas e números.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9acf8b7b-a65d-4f34-8ff1-97a6c639c088)

Na tela inicial do sistema, teremos que utilizar o comando **Ctrl + Alt + Delete** , você irá perceber que utilizar o teclado não funcionará na maquina virtual, neste caso, va na barra de ferramentas na parte de cima da maquina e clique em `Entrada -> Teclado -> Inserir Ctrl + Alt + Del` 

# Primeiros Passos

Assim que você acessar seu sistema operacional, o programa **Server Management** que é a ferramenta de gerenciamento do servidor irá abrir automaticamente, caso contrario, utilize a barra de pesquisa para abrir o programa.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b92f06dd-f39c-4583-a555-747f73dd5bcb)

## Configurando IP

Recomendo que a primeira configuração feita na maquina virtual seja definir um ip estatico/fixo no sistema operacional, caso não saiba como fazer essa configuração, recomendo este [guia](https://ajuda.programaconsumer.com.br/como-configurar-um-ip-fixo-no-computador-servidor/).

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/c0503521-37cc-4d28-b0c5-fd782f0b683a)

Minha configuração ficou assim:

```

IP address: 10.0.0.27
Subnet mask: 255.255.255.0
Default Geteway: 10.0.0.1

Preferred DNS server: 127.0.0.1
Alternate DNS server: 1.1.1.1

```

## Atualizando Servidor

Logo em seguida, vamos atualizar o servidor, atualizações regulares fornecem correções para vulnerabilidades de segurança conhecidas. Hackers e indivíduos mal-intencionados estão constantemente buscando maneiras de explorar brechas em sistemas desatualizados. Ao manter seu servidor atualizado, você protege seus dados, aplicativos e usuários contra ameaças cibernéticas, mantendo-se à frente dos ataques mais recentes.

Dentro da barra de pesquisa do windows, pesquise `Windows Update` e selecione `Check for updates`.

> ⚠️ Recomendo que faça essa atualização em uma maquina virtual APENAS se tiver alocado muito espaço no disco da maquina, a atualização do servidor é demorada, pode encher a memória e possivelmente corromper a memória


![image](https://github.com/pfbahury/WindowsServer/assets/90939515/fc9bd1a6-ab3d-465f-9d42-42e3472a8987)

Caso escolha prosseguir com a atualização, recomendo que separe um dia dia apenas para a atualização.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6c83b6c8-aea3-4cc2-b237-7adb2179f5c4)

Reinicie o servidor depois de atualizar.

## Configurando Nome do Servidor

Agora vamos finalmente configurar o servidor em si, dentro do Server Manager, faremos nossas primerias configurações, começando pelo nome. Para fazer isso, selecionamos o nome do servidor em `Local Server`

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/86a4d8b7-603a-4909-820c-6605e6144ee4)

Clique em **Computer name** e logo em seguida **Change**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d6e1dc36-34b4-4edd-8cbe-d93334ebcf9a)

A escolha de um bom nome para o servidor é importante, pois ajuda na identificação do servidor na rede. Ao nomear um servidor Windows, é importante seguir diretrizes essenciais. O nome deve ser descritivo, conciso e relevante para sua função. Mantenha uma convenção de nomenclatura consistente e evite caracteres especiais ou nomes genéricos. Essas diretrizes garantem uma identificação clara, facilidade de gerenciamento e organização da infraestrutura de servidores.

Aqui os exemplos de como configurei o nome no meu servidor:

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a0b6a555-296e-4713-b9ab-70e8f1a59bf3)

Após configurar, clique em OK, e logo em seguida reinicie o seu servidor.

# IIS e FTP

O ISS, ou Internet Information Services, é um serviço de servidor web desenvolvido pela Microsoft. Ele permite hospedar e fornecer páginas da web na internet. Basicamente, quando você digita um endereço de site em seu navegador, o ISS é responsável por entregar as páginas desse site para você visualizar. Ele processa solicitações de clientes e envia as informações necessárias para exibir o conteúdo da página no navegador.

O FTP, ou File Transfer Protocol, é um protocolo de transferência de arquivos utilizado para enviar e receber arquivos entre um cliente e um servidor. Ele facilita a transferência de arquivos de um local para outro pela rede. No contexto do FTP, um cliente FTP é usado para se conectar a um servidor FTP. Através dessa conexão, é possível enviar arquivos do cliente para o servidor ou baixar arquivos do servidor para o cliente.

## Instalação

Para iniciar a instalação, clicamos em **Manage** na barra superior do Server Manager, e em seguida **Add Roles and Features**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/68928328-b619-47f5-bad9-3a37275435d9)

Assim que você abrir a janela de serviços, estará em uma pagina padrão de instalação, vamos marcar **skip this page by default** para não aparecer novamente e apertar em **Next**

Em seguida, apertamos em **Next** na próxima tela, e na seleção de Servidor apertamos denovo **Next** ja que só estamos utilizando um servidor local.

Isso é um padrão que faremos para TODOS OS SERVIÇOS, de agora em diante, podemos pular direto para a sessão **Server Roles** e procure pelo **Web Service (ISS)**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/199645cf-19d0-4fc9-979c-55dc0791be48)

Em seguida o instalador irá demonstrar que *features* serão necessárias para a instalação completa. Selecione `Add Features` para prosseguir.

> Em todos os serviços que demonstrarem esta tela, iremos repetir esse processo, ja que as *features* são necessarias para o funcionamento adequado.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b527c5e7-31b0-48e8-b889-939c69aa4489)

Próxima tela questiona se alguma feature EXTRA, neste caso, que não são explicitamente necessárias pra execução do serviço, assim, não iremos mudar nada, e passaremos para a próxima tela apertando em **Next**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6fa9f570-df15-4a44-9592-2764afdccba8)

A próxima tela é uma descrição sobre o serviço, podemos pular para a próxima, onde iremos selecionar funções que utilizaremos, selecione as que estão presentes nas printes e logo em seguida, pressione **Next**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/1e723333-3338-4417-8a47-fa9c2131349b)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/41712370-279e-4bbb-b75e-d94089716dde)

Agora, vamos exportar a configuração para gerar um relatório completo de tudo o que foi instalado. Essa exportação é essencial para fins de auditoria do sistema, fornecendo informações valiosas sobre a instalação. Para fazer isso, basta clicar em "Exportar Configurações de Configuração" e aguardar a geração do relatório.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/ca500611-e49a-48c4-8cbd-1ceeba9389be)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/01666d35-3bca-425e-b05c-bfa0608ea187)

Selecione uma pasta, e clique em salve

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d7a4f4bc-2d85-41ab-9ab9-d89e17e34272)

Agora, vamos apenas apertar em Install e aguardar o final da instalação.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/5e60874e-bd14-4d55-8a72-3de99aef8d83)

Para checar se esta tudo funcionando acesse o ip da maquina virtual pelo navegador e verá uma tela assim.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/0b75e907-d3bb-47dc-9659-f09f301e34ea)

## Configuração

Você pode acessar as configurações do serviço indo em Tools e depois procurar por Internet Information Services (IIS) Manager

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/4d09e5c5-4761-45ef-9656-88d58ce0068c)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/31466f1f-d63b-4991-8ef6-aa320f96bfc6)

Veremos as configurações do servidor ao clicar no seu nome.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/da03ac0e-622f-4574-a0fa-dfd8ae721c7e)

Podemos ver mais opções clicando com o botão direito no nome do seu servidor. poderá ver mais opções de gerenciamento do serviço

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/12069532-f323-43eb-888b-a115539fca94)

Na categoria ISS clicando em Default Document podemos ver os documentos padrão do site

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9ad1d820-68d3-4fd7-a377-e625df6c9b61)

Podemos ver que a pasta do arquivo que do site que é entregue pelo servidor fica na pasta `C:/inetpub/wwwroot`

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b044dc07-6f13-49bd-b9f9-a10d3b14e844)

Na categoria ISS, clicando em Authentication podemos ver as configurações de autenticação, que podem ser habilitadas ou desabilitadas clicando com o botão direito.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/5ae0080a-ee10-4249-a2bb-de9c4d4f80ff)

Podemos também criar um site novo, clicando com o botão direito na pasta **Sites** e clicando em **Add Website**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/25d76ab5-de32-41eb-b443-52325546fd01)

VocÊ pode criar uma nova pasta para salvar os arquivos do seu site.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/cf1957c1-1104-4631-9e6c-d4364cdb0c32)

Salve os arquivos e selecione uma porta diferente da default (80), no meu caso eu coloquei 8080

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/915fd223-d02e-4b6d-8d2d-7267c1b8c024)

Dentro dessa pagina podemos criar um certificado SSL

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/04ab7089-27b6-4960-83d2-2c75fb75a6a6)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a898e175-d8b1-460e-8715-4ce6e6232dee)

E adicionar no site que criamos indo em Edit bidings depois de clicar com o botão direito no site criado

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/f5565052-1126-43d2-9ebe-bac75a7b9f8d)

Indo no endereço do site, será possivel verificar o certificado.

# Samba

O serviço Samba no Windows Server é uma implementação do protocolo SMB/CIFS que permite a interoperabilidade entre sistemas Windows e sistemas baseados em Linux/Unix. Ele permite compartilhar arquivos e recursos de rede entre servidores Windows e clientes Linux/Unix, além de oferecer recursos de autenticação, integração com o Active Directory, compartilhamento de impressoras em rede e promover a interoperabilidade entre diferentes plataformas. 

## Instalação

Para instalar o serviço, seguimos os mesmos passos realizados no serviço anterior, indo em **Manage**, **Add Roles and Features** e depois procurar por File Server Resource Manager, adicionando as features necessarias.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/f6e95080-d077-4515-a852-7bd16a6f200d)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3a2f1122-2b14-4c67-8d89-48404d65c7cf)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/304245fa-3997-4c88-a844-366e1b153367)

Indo para Tools e acessando o **File Server Resource Manager** encontramos a tela de gerenciamento do Serviço

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9e9a875b-5392-4fa5-9bab-d7071327e3a9)

Na tela de Quotas Management e em Quotas, é possivel condigurar a quantidade de MB que a pasta deve conter, ou você pode acessar diretamente em Templates configurações de espaço prontas.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b3c0b8da-37e4-4206-a94a-d66e288e7c3e)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d79c9a00-7838-40fa-b483-bf0fa4d39741)

Dentro das opções de **File Screens Templates**, você pode escolher uma das configurações pré-existentes. Caso prefira criar sua própria configuração, basta clicar com o botão direito do mouse e selecionar **Create File Screen Template** para personalizar suas preferências.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/4869a6b7-8e3b-4764-bf32-7f61f9a64466)

Dentro das opções de **Reports Storage Management**, é onde realizamos a configuração dos relatórios que o servidor irá gerar, fornecendo informações sobre todas as atividades ocorridas. Esses relatórios são extremamente importantes para fins de auditoria, ajudando a identificar e resolver problemas caso eles ocorram.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/df4ad4dd-c33f-433e-8c9f-687b37a74bb6)

Dentre as configurações disponiveis, pode-se comentar:

- Local de Armazenamento: Você pode definir o local onde os relatórios serão armazenados no servidor. Isso pode ser um diretório local ou uma pasta de rede compartilhada.
- Retenção de Relatórios: É possível configurar a quantidade de tempo que os relatórios serão mantidos no armazenamento. Isso pode ser definido em dias, semanas, meses ou com base em um período específico.
- Agenda de Geração de Relatórios: Você pode agendar a frequência com que os relatórios serão gerados. Isso pode ser diário, semanal, mensal ou em um intervalo personalizado.
- Formato do Relatório: É possível especificar o formato dos relatórios gerados, como HTML, CSV (Comma-Separated Values) ou XML (eXtensible Markup Language).
- Configurações de Notificação: Você pode definir opções de notificação para ser informado sobre a geração dos relatórios ou em caso de falhas na geração.

E por fim em **File Management Task** é possivel ver as atividades que ocorrem no servidor. Ja que não estão conectado ao meu servidor, ele está vazio.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/44b3b43d-05bd-4af1-8b39-383a652209e3)

Voltando para o gerenciamento do servidor, e acessando **File and Storage Service -> Shares**, criamos nossa pasta compartilhada, iniciando o assitente, clicando com o botão direito e clicando em **New Share**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9d46166a-489c-4bd9-9969-89dfc1e87ba4)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/23000160-7c3c-4f17-8adb-635edff6f074)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3d08afd3-c85a-4956-9a48-af7d7eadbf03)

As configurações aqui envolvem customizar os detalhes da pasta como nome ou descrição.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b09f3a04-367a-4cb7-9f76-e23284e235f4)

Aqui temos as seguintes configurações:

- Enable Access-based Enumeration: Controla a visibilidade de arquivos e pastas compartilhados com base nas permissões de acesso dos usuários.
- Allow caching of share: Permite que os arquivos do compartilhamento sejam armazenados em cache nos clientes que acessam o compartilhamento.
- Encrypt Data Access: Aplica criptografia aos dados que estão sendo acessados no compartilhamento de pasta.

Deixaremos todas ativadas.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9df10225-7f27-4c15-82b9-946c3377a680)

Na próxima janela, vamos configurar as permissões na pasta, no caso recomendo que apague todas as permissões predefinidas, clicando em  **Disable Inheritance** e depois em **Remove all inherited permissions from this object** 

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6a64ac29-bbd3-49c7-9ddd-3e00eb4e5488)

Customize as permissões pesquisando em Find Now recomendo que permita o Administrador e os usuarios, e de as permissões que achar mais apropiado. 

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/04ab24a1-087c-4cfa-b94c-b1c671f0e490)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/68b6a2af-c819-42a2-bbc9-da2e904d7cb5)

Em seguida aperte Next na próxima tela e selecione um espaço customizado.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/7fc6597e-c72e-478c-8992-e034d1684e89)

Em seguida você confirmará suas configurações, e concluir a criação clicando em **Create**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/c724b7b7-e6e7-4a60-9aed-976cc451234b)

Você podera ver aqui sua pasta feita, e clicando com o botão direito e em seguida **properties** poderá ver suas configurações.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/cb5beaa6-94e0-49a2-8e65-f11c9cb111fc)

# DHCP

O DHCP (Dynamic Host Configuration Protocol) é um serviço utilizado em redes de computadores para atribuir automaticamente configurações de rede a dispositivos, como endereços IP, máscaras de sub-rede, gateways padrão, servidores DNS e outros parâmetros de rede. Ele simplifica a administração e configuração de dispositivos em uma rede, evitando a necessidade de configurar manualmente cada dispositivo individualmente.

## Instalação e Configuração

O processo de instalação envolve o mesmo processo, indo em Manage, add roles and features e em seguida procurando o serviço DHCP para a instalação, e no fim da instalação, selecionaremos **Complete DHCP Configuration**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/bf2fe15b-bc3b-4bc9-9143-263fdd3eec42)

No caso apenas daremos Next nas próximas telas, ja que não mudaremos necessariamente as configurações default, e iremos apenas focar em terminar com o processo completo de instalação

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/fd2bd665-5344-4717-aeed-b227368ee177)

Agora que o processo foi finalizado, indo para o ambiente de gerenciamento do DHCP, indo para **Tools -> DHCP** faremos todas as nossas configurações

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d760ba20-fd26-476f-8f14-f28dd786f156)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/8c80e4cb-6e5b-4d38-acdc-3929c2188edd)

Clicando com o botão direito do mouse em IPV4 vamos clicar na opção New Scope para configurarmos nosso serviço.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/60102a9b-0bba-404b-ab88-cf8d7c1908a8)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/519edbe3-a6ed-4d6b-83fd-740f2cd4c733)

Definiremos o nome da nossa configuração e uma descrição

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3452c434-ffa6-42f1-bebf-d45cfe6f369e)

Dividiremos a faixa de ip que o DHCP irá entregar para as maquinas.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/ebbd63e6-a347-4a5a-ad72-41908b56acc1)

Podemos selecionar também uma faixa de ip a ser excluida

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/5450a24a-07a5-4332-a92a-07fb3ae44c67)

Nessa configuração, podemos definir o tempo em que um dispositivo pode manter o mesmo endereço IP atribuído pelo servidor DHCP antes de renovar a solicitação. Esse aspecto é muito importante, principalmente em ambientes com alta rotatividade de dispositivos, como shoppings. Se o tempo for configurado de forma muito longa, os endereços IP disponíveis podem se esgotar rapidamente, impedindo que novos dispositivos se conectem à rede. Talvez você já tenha se deparado com a mensagem "Não foi possível obter endereço IP" ao tentar se conectar a uma rede desse tipo. Para evitar esse problema, é essencial ajustar adequadamente o tempo de renovação, levando em consideração as características do ambiente em que o servidor DHCP estará operando.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/cd53691f-f4ae-4200-a3fb-0a6371db02d7)

Depois apertamos em next e podemos definir o nosso gateway

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d6d1a6cd-6207-40cd-8a18-bf5c5b076122)

E na próxima tela podemos definir nosso DNS

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/647e88f2-1ce9-4147-a54a-0bc1920e4743)

Em seguida podemos apertar next até chegar no final da instalação

Podemos também ir na pasta **Reservation** e clicando com o botão direito para criar criar IP reservados para maquinas especificas, tal como uma impressora.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/4f24d29d-ae88-408a-9c39-b19bde7b7c77)

Clicando com o botão direito em IPV4, iremos clicar na opção **Reconcile All Scope** depois em **Verify** e verificamos nossa configuração.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/d5d862df-a0f4-4819-b1b2-a041ce823ef8)

Ainda nas opções em IPV4 podemos clicar em **Properties** e ativamos a opção de atualizar as estatisticas para atualizar a cada 8 horas. 

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6d76544f-2be6-4213-b1e2-6c749bef19f7)

E em **Display Statistics** poderemos ver as estatisticas do DHCP.

# Serviço de Impressão

O serviço Print and Document Services no Windows Server é um conjunto de recursos e funcionalidades que permitem gerenciar e controlar as impressoras e os documentos em uma rede. Ele oferece um ambiente centralizado para configurar e monitorar dispositivos de impressão, bem como gerenciar os fluxos de trabalho relacionados a documentos.

## Instalação e Configuração

A instalação segue o mesmo processo dos serviços anteriores, desta vez iremos procurar pelo serviço **Print and Document Services** 

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/594a0e27-f32f-4e23-9789-e848876cd3d2)

Daremos **Next** nas janelas até chegar em **Roles Service** onde selecionaremos as funções que instalaremos no serviço.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/4b44e8b9-a401-49db-b144-d6fbfb6332e9)

Logo em seguida iremos prosseguir a terminar a instalação assim como nos outros serviços, dentro da pagina principal do gerenciador do servidor, o serviço estará salvo como print services

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/833e7d1a-7d35-403f-8d06-ec4aa21bfa4e)

Nessa janela vemos todos os detalhes do serviço

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3d926921-37fa-49bb-8705-ea156119aeb4)

Dentro da seção **Print Servers** estão armazenados todos os servidores de impressão. Nessa seção, existem algumas pastas específicas para organizar diferentes elementos relacionados às impressoras. A pasta **Drivers** contém todos os drivers necessários para o funcionamento das impressoras. A pasta **Forms** guarda os formatos de papel disponíveis para impressão. A pasta **Ports** armazena as configurações das portas de cada impressora. E a pasta **Prints** contém as informações e configurações de todas as impressoras disponíveis na rede.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a095d8cd-6950-4072-ab63-b6e2015897de)

Podemos adicionar uma porta padrão para as impressoras, clicando com o botão direito  no servidor e logo em seguida em **Properties**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/793ba98b-2b93-41a1-a783-b52054484b75)

Logo em seguida clicando em **Add Port** e selecionando um IP para a impressora e a porta.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b571df32-484f-4c8d-afa2-a0fc1136fcb9)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/428cc97a-4a68-4601-a318-7767a6ee3943)

Em seguida apertamos em **Next** e **Finish**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/97bd3436-35bf-4f0c-b357-9ac85821a9c6)

Aqui podemos ver nosso dispositivo adicionado.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b107b731-da6c-4123-8469-9255f196aaa3)

Para adicionar um driver para uma nova impressora, podemos ir na aba **Drivers** e deposi em **Add**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/7827bd99-fc61-4b7f-a9a6-ce5a055c2fbe)

Podemos escolher entre 64 ou 86 bits

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/218f5f0f-3cc8-490e-9a2a-d9229895f49f)

O Serviço oferece diversos Drivers ja presentes para que você instale, recomendo algum que ja venha com um servidor para instalar

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/31daff0c-a514-4cef-93fc-fea8f838c57b)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/ddf5316a-dabe-4904-93d8-8a10608ed95e)

Aqui poderemos ver os Drivers instalados

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/acafb8e3-32b9-48c0-859d-ac8f7e1615da)

O serviço ainda permite que você verifique as impressoras na pagina web acessando `127.0.0.1/printers` no seu navegador.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b16028bb-1239-4946-a085-12295668e4fc)

# Active Directory

O Active Directory é um serviço de diretório desenvolvido pela Microsoft que é amplamente utilizado em ambientes empresariais que utilizam o Windows Server. Ele fornece recursos de gerenciamento centralizado de usuários, grupos, computadores e recursos de rede. O Active Directory é projetado para facilitar a administração e o gerenciamento de uma rede, oferecendo recursos como autenticação, autorização e gerenciamento de políticas de segurança.

O Active Directory possui algumas caracteristicas em serviço:

- Autenticação de usuários: O Active Directory permite autenticar os usuários em uma rede, fornecendo um nome de usuário e uma senha. Isso garante que apenas usuários autorizados possam acessar recursos e informações na rede.
- Gerenciamento centralizado de usuários e grupos: O Active Directory permite que os administradores criem e gerenciem contas de usuário, atribuam permissões e grupos de segurança, definam políticas de senha e personalizem configurações específicas para cada usuário. Isso simplifica a administração de usuários em uma rede.
- Organização hierárquica de objetos: O Active Directory organiza objetos, como usuários, grupos e computadores, em uma estrutura hierárquica chamada de árvore de diretórios. Essa estrutura permite que os administradores organizem e gerenciem eficientemente os objetos com base em departamentos, locais geográficos ou outros critérios.
- Políticas de segurança: O Active Directory permite que os administradores apliquem políticas de segurança em toda a rede, como exigir senhas fortes, definir políticas de bloqueio de contas e configurar restrições de acesso aos recursos. Isso ajuda a manter a segurança da rede e proteger informações confidenciais.
- Serviços adicionais: O Active Directory suporta outros serviços, como o Domain Name System (DNS) para resolução de nomes na rede, o Group Policy para aplicação de configurações e políticas em vários computadores e o Lightweight Directory Access Protocol (LDAP) para acesso e consulta dos dados do diretório.

## Instalação e Configuração

Nesse ponto eu presumo que ja saiba qual o processo de instalação, para prosseguir, iremos procurar dentro de Add Features and Roles por Active Directory Domain Server.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a33f6b2b-3b32-42d2-bc6c-824ac5c87ba3)

Teremos uma pagina que descreve o serviço, mas podemos apenas clicar em Next.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3e5a893c-854e-41ca-a345-7b9a320cbea8)

No final da instalação teremos a opção de transformar o servidor em uma maquina de dominio clicando no link azul escrito **Promote this server to a domain controller**.


Aqui possuimos diversas opções de configuração, mas selecionaremos **Create a New Forest** para criar um dominio novo.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/7b4f763b-c157-4d83-bb48-1884317c6b20)

Colocaremos um nome para o dominio

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b6ae2008-6233-4fba-b7e6-6c53a1c24221)

Aqui poderemos colocar a senha para o Directory Services Restore Mode (DSRM) que é um modo especial de inicialização do sistema operacional Windows Server, que permite a recuperação e a restauração do serviço de diretório Active Directory em um controlador de domínio. É utilizado quando ocorre uma falha grave no Active Directory ou quando há a necessidade de restaurar um backup do banco de dados do Active Directory.

> ⚠️ esta senha é de extrema importancia, então crie uma senha robusta, mas que o usuario não possa esquecer.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/1168124b-43cd-427d-8b29-9a8d74e67e51)

Clique next na proxima tela e logo depois configure o endereço para o NetBIOS, que é um conjunto de protocolos de comunicação usado principalmente em redes locais (LANs) para permitir a comunicação entre dispositivos. 

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/f4333d28-5643-4541-b86e-361b8361b584)

Clique em **Next** na próxima pagina e logo em seguida, veja o resumo de suas configurações

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/34f2456c-51dd-4542-84e2-648833bd7b4f)

O serviço farar uma checagem de pre-requisitos, quando terminar clique em **Install**.

> Logo em depois deste processo o computador irá reiniciar para configurar o serviço.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/2998b3d4-9288-4c1b-a7d7-86de827bceda)

Espere a reinicialização, e quando a maquina se iniciar novamente, poderá checar o seu processo ja funcionando. Para fazer login, use sua senha padrão, ou a senha configurada durante a instalação do serviço.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/4c2984a2-94ff-40a5-84d0-1042b93c3515)

Em DNS manager dentro de tools, podemos adicionar um host novo clicando em **New Host**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/cb423ee6-7189-41c8-a9bb-58c47b83d037)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a3dffa45-4418-4b56-98f4-01e3f89727ec)

Qualquer usuario novo que for adicionado podera ser visualizado na pasta **Users** do gerenciador do **Active Directory Users and Computers**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/82714ed4-0ff2-4fa3-90c1-7365307aba9a)

Aqui você pode configurar diretórios para usuarios diferentes de diferentes niveis de acesso. Vamos pegar como exemplo uma escola, para uma rede escolar, os acessos podem ser divididos em 3 grupos: Administração, Professores e Alunos. Clicando com o botão direito nos grupos criados, você pode criar um usuario novo, seu nome, iniciais e endereço de acesso.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/e605ca81-ad58-4aa3-bd7b-78788c3c4e19)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/bf860376-9afe-488b-b357-87c84ecdc7d0)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/70a36c7e-304a-4b9d-a48d-bc171d499695)

Podemos também acessar o **Group Policy Management Editor**, com ele, os administradores podem criar, editar e aplicar políticas de grupo para controlar e gerenciar as configurações dos sistemas na rede. A ferramenta oferece uma interface gráfica que facilita a definição de configurações específicas para grupos de usuários ou computadores, permitindo a aplicação consistente dessas configurações em toda a rede.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/ffaf6e90-bbc4-43f9-b3ce-bc769f6aeccb)

Clicando em **Edit** no **Default Domain Policy**, podemos mudar nas configurações da política do serviço, como configurações de segurança, políticas de senha, configurações de auditoria, entre outras.

Um dos exemplos de edição que podemos fazer, é o requisito minimo na criação de senhas:

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/9e3fd867-fb6d-42b5-9335-5611bad320ae)

Outro exemplo é dentro das opções de segurança que mostra varias opções de customizações dentro de login, como por exemplo, uma mensagem de logon.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/e0996d7a-e611-40ee-8a23-bf7e48894cd5)

Esses são apenas alguns dos varios exemplos de configurações, utilizando o Active Directory, possuimos uma ampla capacidade de customização para criar um dominio completamente unico, e com um sistema de usuario completo de facil acesso. Com isso concluo essa documentação, agradeço por ler até aqui.
