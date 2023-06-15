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

Na tela inicial do sistema, teremos que utilizar o comando **Ctrl + Alt + Delete** , você irá perceber que utilizar o teclado não funcionará na maquina virtual, neste caso, va na barra de ferramentas na parte de cima da maquina e clique em `Entrada -> Teclado -> Ctrl + Alt + Del` 
