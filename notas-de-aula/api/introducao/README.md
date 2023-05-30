# API (Application Programming Interface)

## O que é uma API?

Trazendo a definição da RedHat, as interfaces de programação de 
aplicativos (APIs) são conjuntos de ferramentas, definições e protocolos 
para a criação de aplicações de software.

## Como funcionam?

Com as APIs, sua solução ou serviço podem se comunicar com outros 
produtos e serviços sem precisar saber como eles foram implementados. 
Isso simplifica o desenvolvimento de aplicações, gerando economia de 
tempo e dinheiro. Na hora de desenvolver suas novas ferramentas e 
soluções (ou ao gerenciar aquelas já existentes), as APIs oferecem a 
flexibilidade necessária para simplificar o **design**, a **administração** 
e o **uso**, além de trazer oportunidades de inovação.

Elas funcionam como se fossem contratos, com documentações que 
representam um acordo entre as partes interessadas. Se uma dessas partes 
enviar uma **solicitação** remota estruturada de uma forma específica, isso 
determinará como a aplicação da outra parte **responderá**.

## APIs remotas ou APIs Web

As APIs remotas foram projetadas para interagir por meio de uma rede de 
comunicações. Quando falamos remota, queremos dizer que os recursos 
utilizados pela API estão em algum **lugar fora do computador que realiza** 
**a solicitação**. Como a rede de comunicações mais usada é a Internet, 
a maioria das APIs são projetadas com base em padrões da web. Nem todas 
as APIs remotas são web, mas é justo afirmar que, em geral, as APIs web 
são remotas.

As APIs web normalmente usam o **protocolo HTTP** para mensagens de 
**solicitação** e fornecem uma definição da estrutura das mensagens de 
**resposta**. Essas mensagens de resposta geralmente têm o formato de 
arquivo **XML** ou **JSON**. Tanto XML quanto JSON são formatos de 
preferência porque apresentam os dados de forma simplificada, facilitando 
a manipulação por outras aplicações.

## API SOAP e API REST

Com a proliferação das APIs web, uma especificação de protocolo foi 
desenvolvida para ajudar a padronizar a troca de informações: o 
*Simple Object Access Protocol*, mais conhecido como **SOAP**. 

As APIs projetadas com SOAP usam o XML como formato de mensagem e recebem 
solicitações por HTTP ou **SMTP**. O SOAP facilita o compartilhamento 
de informações por aplicações executadas em ambientes diferentes ou 
escritos em linguagens diferentes.

Outra especificação é a *Representational State Transfer* (**REST**). 
APIs web que adotam as restrições de arquitetura da REST são chamadas de 
**APIs RESTful**. A REST é fundamentalmente diferente do SOAP: o **SOAP** 
**é um protocolo** e a **REST é um estilo de arquitetura**. Isso 
significa que não há um padrão oficial para APIs RESTful web. 

Conforme definido na dissertação de Roy Fielding 
*"Architectural Styles and the Design of Network-based Software Architectures"*, 
as APIs serão consideradas RESTful se estiverem em conformidade com 
seis restrições de arquitetura:

- **Arquitetura cliente-servidor:** a arquitetura REST é composta por 
clientes, servidores e recursos. Ela lida com as solicitações via HTTP.

- **Sem monitoração de estado (Stateless):** nenhum conteúdo do cliente 
é armazenado no servidor entre as solicitações. Em vez disso, as informações 
sobre o estado da sessão são mantidas com o cliente. Os clientes podem 
solicitar recursos em qualquer ordem, e cada solicitação é sem estado ou 
isolada de outras solicitações. Essa restrição de design da API REST 
implica que o servidor possa entender completamente e atender à solicitação 
todas as vezes. 

- **Capacidade de armazenamento:**  os serviços da Web RESTful permite 
o armazenamento em cache, que é o processo de armazenar algumas respostas 
no cliente ou em um intermediário para melhorar o tempo de resposta do 
servidor. Por exemplo, digamos que você visite um site que tenha imagens 
comuns de cabeçalho e rodapé em todas as páginas. Toda vez que você 
visita uma nova página do site, o servidor deve reenviar as mesmas 
imagens. Para evitar isso, o cliente armazena em cache ou armazena 
essas imagens após a primeira resposta e, em seguida, usa as imagens 
diretamente do cache. Os serviços da Web RESTful controlam o cache 
usando respostas de API que se definem como armazenáveis ou não em 
cache.

- **Sistema em camadas:** as interações entre cliente e servidor podem 
ser mediadas por camadas adicionais. Essas camadas podem oferecer recursos 
extras, como balanceamento de carga (**load balancing**), caches 
compartilhados ou segurança.

- **Código sob demanda (opcional):** os servidores podem ampliar a 
funcionalidade de um cliente por meio da transferência de códigos 
executáveis. Por exemplo, quando você preenche um formulário de registro 
em qualquer site, seu navegador imediatamente destaca os erros cometidos, 
como números de telefone incorretos. Ele pode fazer isso devido ao código 
enviado pelo servidor.

- **Interface uniforme:** essa restrição é essencial para o design de 
APIs RESTful e inclui quatro vertentes:

  - **Identificação de recursos nas solicitações:** os recursos são 
  identificados nas solicitações e separados das representações retornadas 
  para o cliente. Essas solicitações precisam conter os seguintes
  componentes: 
    - **identificador de recurso exclusivo:** URL que especifica o caminho 
    para o recurso;
    - **método HTTP:** informa o que o servidor precisa fazer com o recurso;
    - **cabeçalho HTTP:** são os metadados trocados entre o cliente e o 
    servidor. Por exemplo, o cabeçalho da solicitação indica o formato 
    da solicitação e da resposta, fornece informações sobre o status da 
    solicitação e assim por diante;

  - **Manipulação de recursos por meio de representações:** os clientes 
  recebem arquivos que representam recursos. Essas representações precisam 
  ter informações suficientes para permitir a modificação ou exclusão.
  O servidor atende a essa condição enviando metadados que descrevem 
  melhor o recurso.

  - **Mensagens autodescritivas:** cada mensagem retornada para um cliente 
  contém informações suficientes para descrever como ele deve processá-las.

  - **Hipermídia como plataforma do estado das aplicações:** depois de 
  acessar um recurso, o cliente REST pode descobrir todas as outras ações 
  disponíveis no momento por meio de hiperlinks.

Essas restrições podem parecer excessivas, mas são muito mais simples 
do que um protocolo prescrito. Por isso, as APIs RESTful estão se tornando 
mais comuns do que as APIs SOAP.

Nos últimos anos, as especificações da *OpenAPI* se tornaram o padrão na 
hora de definir APIs REST. A OpenAPI permite que desenvolvedores de todas 
as linguagens criem interfaces de API REST compreensíveis com o mínimo de 
suposições.

<hr>

Para mais informações, visite as fontes usadas para esse readme:

- [O que é API RESTful? AWS Amazon, 2023.](https://aws.amazon.com/pt/what-is/restful-api/)
- [O que é uma API? RedHat, 2023.](https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces)