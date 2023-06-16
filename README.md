# Introdução

Essa wiki documenta as etapas de implementação de um servidor Windows (windows Server), realizado na disciplina de Redes de Computadores II do curso de Ciência da Computação do Instituto Federal de Educação, Ciência e Tecnologia do Maranhão - Campus Imperatriz (IFMA), ministrada pelo professor [Paulo Henrique Sousa Barbosa](https://github.com/agenteph). Projeto por [Pedro Fernades Bahury](https://github.com/pfbahury).

Para realizar as atividades será necessario a utilização de uma maquina virtual, ou [VirtualBox](https://www.virtualbox.org), e uma imagem `.iso` do sistema operacional que iremos utilizar, neste caso, o [Windows Server](https://www.microsoft.com/pt-br/evalcenter/download-windows-server-2016), e instalar a versão em inglês de 64 bits.

> ⚠️ esta é uma versão de teste, tendo acesso gratuito de apenas 180 dias, caso queira implementar como servidor de produção recomenda-se comprar uma licença oficial.

# Configurando a Maquina Virtual

Logo de começo, recomendo um guia de criação de uma maquina virtual, para os que não possuem o costume de utilizar uma, recomendo o seguinte [guia](https://tecnoblog.net/responde/como-criar-uma-maquina-virtual-virtualbox/)

> ⚠️ Recomendo colocar no mínimo 30GB na maquina virtual

## Configurando a rede

Após criar a sua maquina virtual, clique na engrenagem amarela para acessar as configuração gerais da maquina, dentro das configurações, clique nas aba de **rede**. As configurações estarão como padrão em modo NAT, mude para modo bridge, e dentro das configurações avançadas, mude o **Modo Promícuo**, para **Tudo Permitido**, deixando do mesmo jeito que a imagem.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/8c760376-c4c1-4bfc-a119-cd6cdfed3465)

Após essa configuração, iniciaremos a maquina. Dentro da instalação, nas primeiras 2 telas, selecione **next**, e logo em seguida, **Install now**. Na terceira tela de setup, selecionaremos a versão do Windows, neste caso a **2016 Standard Evaluation (Desktop Experience)**, que é a versão que utilizaremos.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/f6bc7d17-5ade-4e3d-ae3c-38eeddfa8db5)

Após aceitar os termos faremos uma instalação customizada

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6327db8a-395c-40c8-8f29-e578142ec0df)

Selecionaremos o Disco, e aguardaremos o fim da instalação

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/a05840d0-34fd-42ba-82f2-21d8edce6bfe)

Com o fim da instalação, faremos as configurações iniciais para o usuario e a senha, para um servidor real, é EXTREMAMENTE recomendado uma senha **forte** para o seu servidor em produção, com letras maiusculas, minusculas e números.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/497f60b7-dc3d-4360-8d84-ecc19bb2185e)

Na tela inicial do sistema, teremos que utilizar o comando **Ctrl + Alt + Delete** , você irá perceber que utilizar o teclado não funcionará na maquina virtual, neste caso, va na barra de ferramentas na parte de cima da maquina e clique em `Entrada -> Teclado -> Inserir Ctrl + Alt + Del` 

# Primeiros Passos

Assim que você acessar seu sistema operacional, o programa **Server Management** que é a ferramenta de gerenciamento do servidor irá abrir automaticamente, caso contrario, utilize a barra de pesquisa para abrir o programa.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/1573f6e1-d0f6-4e02-a11b-f56830cf5879)

## Configurando IP

Recomendo que a primeira configuração feita na maquina virtual seja definir um ip estatico/fixo no sistema operacional, caso não saiba como fazer essa configuração, recomendo este [guia](https://ajuda.programaconsumer.com.br/como-configurar-um-ip-fixo-no-computador-servidor/).

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/54672279-d61b-4256-a6b1-5325575a5dc3)

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


![image](https://github.com/pfbahury/WindowsServer/assets/90939515/e7174113-abec-48c5-ac16-63cc37d67d69)

Caso escolha prosseguir com a atualização, recomendo que separe um dia dia apenas para a atualização.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/f8886e35-d550-4a82-afbb-0fbcd3ea20ca)

Reinicie o servidor depois de atualizar.

## Configurando Nome do Servidor

Agora vamos finalmente configurar o servidor em si, dentro do Server Manager, faremos nossas primerias configurações, começando pelo nome. Para fazer isso, selecionamos o nome do servidor em `Local Server`

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/32b9093a-1619-40ec-ba55-bd40c1fa968a)

Clique em **Computer name** e logo em seguida **Change**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/33d041d2-cb43-427a-9095-639f26b8d22a)

A escolha de um bom nome para o servidor é importante, pois ajuda na identificação do servidor na rede. Ao nomear um servidor Windows, é importante seguir diretrizes essenciais. O nome deve ser descritivo, conciso e relevante para sua função. Mantenha uma convenção de nomenclatura consistente e evite caracteres especiais ou nomes genéricos. Essas diretrizes garantem uma identificação clara, facilidade de gerenciamento e organização da infraestrutura de servidores.

Aqui os exemplos de como configurei o nome no meu servidor:

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6c8cd9e9-1a43-4f0e-8396-7e684b988767)

Após configurar, clique em OK, e logo em seguida reinicie o seu servidor.

# IIS e FTP

O ISS, ou Internet Information Services, é um serviço de servidor web desenvolvido pela Microsoft. Ele permite hospedar e fornecer páginas da web na internet. Basicamente, quando você digita um endereço de site em seu navegador, o ISS é responsável por entregar as páginas desse site para você visualizar. Ele processa solicitações de clientes e envia as informações necessárias para exibir o conteúdo da página no navegador.

O FTP, ou File Transfer Protocol, é um protocolo de transferência de arquivos utilizado para enviar e receber arquivos entre um cliente e um servidor. Ele facilita a transferência de arquivos de um local para outro pela rede. No contexto do FTP, um cliente FTP é usado para se conectar a um servidor FTP. Através dessa conexão, é possível enviar arquivos do cliente para o servidor ou baixar arquivos do servidor para o cliente.

## Instalação

Para iniciar a instalação, clicamos em **Manage** na barra superior do Server Manager, e em seguida **Add Roles and Features**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/764694d5-f7b9-41d8-9173-22b7cfa36531)

Assim que você abrir a janela de serviços, estará em uma pagina padrão de instalação, vamos marcar **skip this page by default** para não aparecer novamente e apertar em **Next**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/e10c4556-3ce7-4905-99d9-659a906e44c6)

Em seguida, apertamos em **Next** na próxima tela, e na seleção de Servidor apertamos denovo **Next** ja que só estamos utilizando um servidor local.

Isso é um padrão que faremos para TODOS OS SERVIÇOS, de agora em diante, podemos pular direto para a sessão **Server Roles** e procure pelo **Web Service (ISS)**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/92302e33-9b27-402a-9493-b9ad305baa0e)

Em seguida o instalador irá demonstrar que *features* serão necessárias para a instalação completa. Selecione `Add Features` para prosseguir.

> Em todos os serviços que demonstrarem esta tela, iremos repetir esse processo, ja que as *features* são necessarias para o funcionamento adequado.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/5615bae7-4ee9-4953-b3da-4ba2a03723af)

Próxima tela questiona se alguma feature EXTRA, neste caso, que não são explicitamente necessárias pra execução do serviço, assim, não iremos mudar nada, e passaremos para a próxima tela apertando em **Next**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/e545f26e-7f27-4f50-87c6-34f3f81ee145)

A próxima tela é uma descrição sobre o serviço, podemos pular para a próxima, onde iremos selecionar funções que utilizaremos, selecione as que estão presentes nas printes e logo em seguida, pressione **Next**

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/2ade097c-764a-4ab0-9578-fb456c7ab050)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/c558c806-ec21-4ffd-a0d5-6d4514a6965d)

Agora, vamos exportar a configuração para gerar um relatório completo de tudo o que foi instalado. Essa exportação é essencial para fins de auditoria do sistema, fornecendo informações valiosas sobre a instalação. Para fazer isso, basta clicar em "Exportar Configurações de Configuração" e aguardar a geração do relatório.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/25873ee2-3db4-41fb-8994-62918826e001)

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/6daac65b-8f48-4b21-a126-58674c3351de)

Selecione uma pasta, e clique em salve

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/b6eac349-9e96-4931-b62d-19f58cf37743)

Agora, vamos apenas apertar em Install e aguardar o final da instalação.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/3dd07d1d-2ded-44f4-ba7b-cb5580f5fa9d)

Para checar se esta tudo funcionando acesse o ip da maquina virtual pelo navegador e verá uma tela assim.

![image](https://github.com/pfbahury/WindowsServer/assets/90939515/19c03c0b-4c85-49bd-a858-ced1ba88c5d9)

