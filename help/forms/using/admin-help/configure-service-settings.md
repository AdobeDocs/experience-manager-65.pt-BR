---
title: Definir configurações de serviço
description: Saiba como definir configurações de serviço. Você pode usar a página Gerenciamento de serviços para definir as configurações de cada um dos serviços que fazem parte dos formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '10692'
ht-degree: 0%

---

# Definir configurações de serviço {#configure-service-settings}

Você pode usar a página Gerenciamento de Serviços para definir configurações para cada um dos serviços que fazem parte dos formulários AEM. As configurações disponíveis variam dependendo do serviço que está sendo configurado.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Interrompa o serviço antes de alterá-lo. (Consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Clique no nome do serviço que deseja configurar.
1. Se o serviço tiver uma guia Configuração, use-a para alterar as definições do serviço. Consulte a lista de links abaixo para obter detalhes.

   >[!NOTE]
   >
   >Nem todos os serviços listados na página Gerenciamento de Serviços têm uma guia Configuração. Para processos criados, a guia Configuração só será exibida se você tiver adicionado um parâmetro de configuração ao processo no Workbench. (Consulte &quot;Parâmetros de configuração&quot; no [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Clique na guia Segurança e defina as configurações de segurança do serviço. Consulte [Modificando configurações de segurança para um serviço](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Se o serviço tiver uma guia Endpoints, use-a para alterar as configurações do endpoint. Consulte [Gerenciamento de pontos de extremidade](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Clique na guia Pooling e defina as configurações de pooling. Consulte [Configurando o pool de um serviço](configure-service-settings.md#configuring-pooling-for-a-service).
1. Clique em Salvar para salvar as alterações ou clique em Cancelar para descartá-las.
1. Marque a caixa de seleção ao lado do nome do serviço e clique em Iniciar para reiniciar o serviço.

## Configurações do serviço de Fluxo de Trabalho de Auditoria {#audit-workflow-service-settings}

O Workbench oferece a capacidade de registrar instâncias de processos como são executadas em tempo de execução e, em seguida, reproduzi-las para observar o comportamento do processo. (Consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Para conservar espaço no sistema de arquivos do Forms Server, você pode limitar a quantidade de dados de gravação de processo armazenados. Você pode configurar as seguintes propriedades do serviço de Fluxo de trabalho de auditoria ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** O número máximo de gravações armazenadas. Quando o número máximo é armazenado, a gravação mais antiga é removida do sistema de arquivos quando uma nova gravação é criada. Essa propriedade é útil se você tende a criar muitas gravações e deseja remover gravações antigas automaticamente. O valor padrão é 50.

**MaxNumberOfRecordingEntries:** O número máximo de entradas de dados que podem ser armazenadas para cada gravação. As entradas de dados são informações sobre operações no processo. Várias entradas são armazenadas para cada execução de uma operação, como se a operação foi iniciada, se a operação foi concluída e se a rota que leva à operação foi concluída. Essa propriedade é útil quando os processos podem incluir muitas execuções de operação, por exemplo, quando um loop infinito é encontrado. O valor padrão é 50.

## configurações do serviço de formulários com código de barras {#barcoded-forms-service-settings}

O serviço de formulários com código de barras `(BarcodedFormsService)` O extrai dados de código de barras de imagens digitalizadas. O serviço aceita um formulário com código de barras (TIFF ou PDF) como entrada e extrai a representação da máquina dos dados codificados pelo código de barras.

As configurações a seguir estão disponíveis para o serviço de formulários com código de barras.

**Ler à esquerda:** Quando selecionadas, as imagens de código de barras são digitalizadas horizontalmente, da direita para a esquerda.

**Ler à direita:** Quando selecionadas, as imagens de código de barras são digitalizadas horizontalmente, da esquerda para a direita.

**Leitura:** Quando selecionadas, as imagens de código de barras são digitalizadas verticalmente, de baixo para cima.

**Leia abaixo:** Quando selecionadas, as imagens de código de barras são digitalizadas verticalmente, de cima para baixo.

>[!NOTE]
>
>Por padrão, todas as opções são selecionadas. Desmarque uma opção somente se tiver certeza de que nenhum código de barras será exibido dessa maneira em seus formulários.

**Caminho do arquivo base:** O caminho do arquivo relativo ao qual os parâmetros do arquivo de entrada e saída em lote para as operações Executar Trabalho de Arquivo XML e Executar Trabalho de Arquivo Simples são resolvidos. Em configurações em cluster, o caminho do arquivo base deve ser um local de sistema de arquivos compartilhado ao qual todos os nós de cluster têm acesso de leitura/gravação.

**Nome da fonte de dados:** O nome da fonte de dados usada para manter informações de estado e histórico sobre trabalhos de processamento em lote. A fonte de dados especificada deve suportar transações globais (XA).

## Configurações do serviço Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

O serviço Central Migration Bridge ( `CentralMigrationBridge`) chama um subconjunto da funcionalidade Adobe Central Pro Output Server (Central), que inclui os comandos JFMERGE, JFTRANS e XMLIMPORT. As operações de serviço do Central Migration Bridge permitem reutilizar os seguintes ativos centrais em formulários AEM:

* design do modelo (&amp;ast;.ifd)
* modelos de saída (&amp;ast;.mdf)
* arquivos de dados (&amp;ast;.dat)
* arquivos preâmbulo (&amp;ast;.pre)
* arquivos de definição de dados (&amp;ast;.tdf)

A configuração a seguir está disponível para o serviço Central Migration Bridge.

**Diretório de Instalação Central:** O diretório onde o Adobe Central 5.7 está instalado.

## Configurações de serviço do Conector de repositório de conteúdo do EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

O serviço Content Repository Connector for EMC Documentum ( `EMCDocumentumContentRepositoryConnector`) permite criar processos que interagem com o conteúdo armazenado em um repositório do Documentum.

A configuração a seguir está disponível para o serviço Conector de repositório de conteúdo do EMC Documentum.

**Caminho padrão do objeto do link do ativo:** A parte padrão do caminho no repositório do Documentum para armazenar o objeto Asset Link. O caminho real consiste no caminho padrão e no local do modelo de formulário no repositório de formulários AEM.

Por exemplo, se o caminho padrão estiver definido como `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`, e o modelo de formulário for armazenado em uma pasta `/Docbase/forms/`, o objeto Asset Link é armazenado no seguinte local:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

O valor padrão dessa configuração é `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Configurações do serviço Conector de repositório de conteúdo para IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

O Conector do repositório de conteúdo do IBM FileNet permite criar processos que interagem com o conteúdo armazenado em um repositório do IBM FileNet.

A configuração a seguir está disponível para o Conector de repositório de conteúdo do serviço IBM FileNet.

**Caminho padrão do objeto do link do ativo:** A parte padrão do caminho no repositório FileNet do IBM para armazenar o objeto Asset Link. O caminho real consiste no caminho padrão e no local do modelo de formulário no repositório de formulários AEM.

Por exemplo, se o caminho padrão estiver definido como `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`, e o modelo de formulário for armazenado em uma pasta `/Docbase/forms/`, o objeto Asset Link é armazenado no seguinte local:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

O valor padrão dessa configuração é `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Converter configurações do serviço PDF {#convert-pdf-service-settings}

O serviço de conversão de PDF ( `ConvertPdfService`) converte documentos PDF para PostScript e para vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para impressão autônoma baseada em servidor em qualquer impressora PostScript. A conversão de um documento de PDF em um arquivo de TIFF de várias páginas é prática ao arquivar documentos em sistemas de gerenciamento de conteúdo que não aceitam documentos de PDF.

As configurações a seguir estão disponíveis para o serviço Converter PDF.

**Tipo de transação:** Especifica como um contexto de transação deve ser propagado para uma operação.

**Obrigatório:** Suporta um contexto de transação, se existir; caso contrário, um novo contexto de transação é criado. Este é o valor padrão.

**Exige novo:** Sempre cria um novo contexto de transação. Se existir um contexto de transação ativo, ele será suspenso.

**Tempo limite da transação (em segundos):** O número de segundos que o provedor de transação subjacente deve aguardar antes de reverter uma transação que está quebrando esta operação. Esse valor será ignorado se um contexto de transação existente for propagado. O valor padrão é 180.

**Resolução limite para suavização (em dpi):** A resolução de imagem abaixo da qual a suavização (ou suavização de serrilhado) é aplicada ao texto, ao traçado e às imagens, se você tiver selecionado as opções &quot;Aplicar suavização a&quot; para esses elementos.

**Aplicar suavização ao texto:** Controla a suavização de texto. Para desativar a suavização de texto e tornar o texto mais nítido e fácil de ler com uma lente de aumento de tela, desmarque esta caixa de seleção.

**Aplicar suavização a LineArt:** Aplica suavização para remover ângulos abruptos em linhas.

**Aplicar suavização a imagens:** Aplica suavização para minimizar alterações abruptas em imagens.

## Configurações de serviço do Distiller {#distiller-service-settings}

O serviço Distiller ( `DistillerService`) converte arquivos PostScript, Encapsulated PostScript (EPS) e PRN em arquivos PDF em uma rede.

As configurações a seguir estão disponíveis para o serviço Distiller.

**Configurações do Adobe PDF:** As seguintes configurações pré-configuradas são aplicadas ao PDF gerado:

* Impressão de alta qualidade
* Páginas superdimensionadas
* PDFA1b 2005 CMYK
* PDFA1b RGB 2005
* PDFX1a 2001
* PDFX3 2002
* Qualidade da imprensa
* Menor tamanho de arquivo
* Padrão

É possível criar novas configurações por meio da interface do usuário do PDF Generator.

**Configurações de segurança:** Configurações de segurança pré-configuradas que são aplicadas a documentos de PDF gerados. O valor padrão é Sem segurança. Você deve criar as configurações de segurança usando o PDF Generator e depois inserir a configuração aqui.

**Tamanho do Pool:** O tamanho inicial do pool. Quando o serviço Distiller é implantado, esse número é usado para determinar o número de instâncias de implementação de serviço criadas e alocadas para o pool livre aguardando solicitações de chamada. O contêiner de serviço pode então responder imediatamente às solicitações de chamada sem ter que primeiro inicializar uma instância de serviço.

## Configurações do serviço de Gerenciamento de Documentos {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (Obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários projetem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Content Services (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

O serviço de Gestão de Documentos ( `DocumentManagementService`) permite que os processos usem a funcionalidade de gerenciamento de conteúdo fornecida pelos Serviços de conteúdo (obsoleto). As operações de gerenciamento de documentos fornecem tarefas básicas necessárias para manter espaços e conteúdo no sistema de gerenciamento de conteúdo. Exemplos dessas tarefas são copiar, excluir, mover, recuperar e armazenar conteúdo, criar espaços e associações e obter e definir atributos de conteúdo.

As configurações a seguir estão disponíveis para o serviço de Gerenciamento de Documentos.

**Esquema de armazenamento:** O esquema do armazenamento no qual o conteúdo está localizado. O valor padrão é espaço de trabalho.

**Porta HTTP:** A porta usada para acessar os Serviços de conteúdo (obsoleto). O valor padrão é 8080.

## Configurações do serviço de email {#email-service-settings}

O email é usado para distribuir conteúdo ou fornecer informações de status como parte de um processo automatizado. O serviço de e-mail ( `EmailService`) permite que os processos recebam mensagens de e-mail de um servidor POP3 ou IMAP e enviem mensagens de e-mail para um servidor SMTP.

Por exemplo, um processo usa o serviço de email para enviar uma mensagem de email com um anexo de formulário PDF. O serviço de email se conecta a um servidor SMTP para enviar a mensagem de email com o anexo. O formulário PDF foi projetado para permitir que o recipient clique em Enviar depois de preencher o formulário. A ação faz com que o formulário seja retornado como um anexo ao servidor de email designado. O serviço de email recupera a mensagem de email retornada e armazena o formulário preenchido em uma variável de formulário de dados de processo.

As configurações a seguir estão disponíveis para o serviço de email.

**Host SMTP:** O endereço IP ou URL do servidor SMTP a ser usado para enviar email.

**Número da Porta SMTP:** A porta usada para se conectar ao servidor SMTP.

**Autenticação SMTP:** Selecione se a autenticação de usuário é necessária para se conectar ao servidor SMTP.

**Usuário SMTP:** O nome de usuário da conta a ser usada para fazer login no servidor SMTP.

**Senha SMTP:** A senha associada à conta de usuário SMTP.

**Segurança de Transporte SMTP:** O protocolo de segurança a ser usado para conexão com o servidor SMTP:

* Selecione Nenhum se nenhum protocolo for usado (os dados são enviados em texto não criptografado)
* Selecione SSL se o protocolo Secure Sockets Layer for usado.
* Selecione TLS se a Segurança da camada de transporte for usada.

**Host POP3/IMAP:** O endereço IP ou URL do servidor POP3 ou IMAP a ser usado para enviar email.

**Usuário POP3/IMAP:** O nome de usuário da conta de usuário a ser usada para efetuar login no servidor POP3 ou IMAP.

**Senha POP3/IMAP:** A senha associada à conta de usuário POP3 ou IMAP.

**Número da Porta POP3/IMAP:** A porta usada para conectar ao servidor POP3 ou IMAP.

**POP3/IMAP:** O protocolo a ser usado para enviar e receber email.

**Receber Segurança de Transporte:** O protocolo de segurança a ser usado para conexão com o servidor SMTP:

* Selecione Nenhum se nenhum protocolo for usado (os dados são enviados em texto não criptografado).
* Selecione SSL se o protocolo Secure Sockets Layer for usado.
* Selecione TLS se a Segurança da camada de transporte for usada.

## Configurações do serviço de criptografia {#encryption-service-settings}

O Serviço de criptografia ( `EncryptionService`) permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificar a senha aberta para que o documento possa ser visualizado no Adobe Reader ou no Adobe Acrobat. Da mesma forma, se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com a chave pública que corresponde ao certificado (chave privada) usado para criptografar o documento PDF.

As configurações a seguir estão disponíveis para o serviço de Criptografia.

**Servidor LDAP padrão ao qual se conectar:** Nome do host do servidor LDAP usado para recuperar certificados para criptografia de documentos.

**Porta LDAP padrão para conexão:** Número da porta do servidor LDAP.

**Nome de usuário LDAP padrão:** Se o servidor LDAP exigir autenticação, especifique o nome de usuário a ser usado para conexão com o servidor LDAP.

**Senha LDAP padrão:** Se o servidor LDAP exigir autenticação, especifique a senha que corresponde ao nome de usuário a ser usado para conexão com o servidor LDAP.

>[!NOTE]
>
Usar autenticação simples (nome de usuário e senha) somente quando a conexão estiver protegida por SSL (usando LDAPS).

**Modo de compatibilidade:**

## Configurações do serviço FTP {#ftp-service-settings}

O serviço FTP ( `FTP`) permite que os processos interajam com um servidor FTP. As operações de serviço de FTP podem recuperar arquivos do servidor FTP, colocar arquivos no servidor FTP e excluir arquivos do servidor FTP. Por exemplo, documentos como relatórios gerados de um processo podem ser armazenados em um servidor FTP para distribuição. Ou um sistema externo pode gerar alguns arquivos com base nas etapas anteriores de um processo. Em uma etapa subsequente do processo, os arquivos podem ser transferidos para um local remoto.

As configurações a seguir estão disponíveis para o serviço FTP.

**Host padrão:** O endereço IP ou o URL do servidor FTP.

**Porta padrão:** A porta usada para se conectar ao servidor FTP. O valor padrão é 21.

**Nome de usuário padrão:** O nome da conta de usuário que pode ser usada para acessar o servidor FTP. A conta de usuário deve ter privilégios suficientes para executar as operações de FTP exigidas por esse serviço.

**Senha padrão:** A senha a ser usada com o nome de usuário especificado para autenticação com o servidor FTP.

## Gerar configurações do serviço PDF {#generate-pdf-service-settings}

O serviço Gerar PDF ( `GeneratePDFService`) converte arquivos em vários formatos nativos para documentos PDF e converte documentos PDF para vários formatos de arquivo.

As seguintes configurações estão disponíveis para o serviço Gerar PDF.

**Configurações do Adobe PDF:** O nome das configurações pré-configuradas do Adobe PDF a serem aplicadas a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações do Adobe PDF são definidas no console de administração, clicando em Serviços > PDF Generator > Configurações do Adobe PDF. Essas configurações são aplicáveis somente às conversões baseadas no PDFMaker.

**Configurações de segurança:** O nome das configurações de segurança predefinidas a serem aplicadas a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações de segurança são definidas no console de administração, clicando em Serviços > PDF Generator > Configurações de segurança.

**Configurações de tipo de arquivo:** O nome da Configuração de Tipo de Arquivo pré-configurada a ser aplicada a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações de tipo de arquivo são definidas no console de administração, clicando em Serviços > PDF Generator > Configurações de tipo de arquivo.

**Usar o Acrobat WebCapture (somente Windows):** Quando esta configuração é verdadeira, o serviço Gerar PDF usa o Acrobat X Pro para todas as conversões de HTML para PDF. Isso pode melhorar a qualidade dos arquivos PDF produzidos a partir do HTML, embora o desempenho possa ser um pouco menor. O valor padrão é false.

**Usar a Conversão de imagem do Acrobat (somente Windows):** Quando esta configuração é verdadeira, o serviço Gerar PDF usa o Acrobat X Pro para todas as conversões de Imagem para PDF. Essa configuração é útil somente se o mecanismo de conversão Java puro padrão não puder converter uma proporção significativa das imagens de entrada com êxito. O valor padrão é false.

**Ativar conversões do AutoCAD com base em Acrobat (somente Windows):** Quando esta configuração é verdadeira, o serviço Gerar PDF usa o Acrobat X Pro para todas as conversões DWG para PDF. Essa configuração é útil somente se o AutoCAD não estiver instalado no servidor ou se o mecanismo de conversão do AutoCAD não puder converter arquivos com êxito.

**Expressões Regulares Para Descobrir Caracteres Especiais Proibidos No Nome De Usuário (Somente Windows):** Especifica caracteres que interferem nas operações Export PDF e Optimize PDF quando os caracteres são exibidos no nome de um usuário.

**Tamanho do pool ImageToPDF:** O tamanho do pool do conversor de imagem para PDF padrão (Java puro) no serviço Gerar PDF. Esta configuração controla o número máximo de conversões simultâneas Imagem-para-PDF que o serviço Gerar PDF pode executar. O valor padrão dessa configuração (recomendada para sistemas com um único processador) é 3, que pode ser aumentado em sistemas com vários processadores.

**Tamanho do pool de HTML para PDF:** O tamanho do pool do conversor HTML para PDF no serviço Gerar PDF. Essa configuração controla o máximo de conversões HTML para PDF simultâneas que o serviço Gerar PDF pode executar. O valor padrão dessa configuração (recomendada para sistemas com um único processador) é 3, que pode ser aumentado em sistemas com vários processadores.

**Tamanho do Pool de OCR:** O tamanho do pool do PaperCaptureService que o PDF Generator usa para OCR. O valor padrão dessa configuração (recomendada para sistemas com um único processador) é 3, que pode ser aumentado em sistemas com vários processadores. Esta configuração é válida somente em sistemas Windows.

**Família De Fontes De Fallback Para Conversões De HTML Para PDF:** O nome da família de fontes a ser usada nos documentos do PDF quando a fonte usada no HTML original não estiver disponível para o AEM Forms Server. Especifique uma família de fontes se você espera converter páginas de HTML que usam fontes indisponíveis. Por exemplo, as páginas criadas em idiomas regionais podem usar fontes indisponíveis.

**Tentar novamente lógica para conversões nativas** Controla as tentativas de geração de PDF se a primeira tentativa de conversão falhar:

**Nenhuma tentativa**

Não repita a conversão de PDF se a primeira tentativa de conversão falhar

**Tentar novamente**

Repita a conversão de PDF independentemente de o limite de tempo ter sido atingido. A duração de tempo limite padrão para a primeira tentativa é de 270s.

**Tentar novamente se o tempo permitir**

Repita a conversão de PDF se o tempo consumido para a primeira tentativa de conversão for menor que a duração de tempo limite especificada. Por exemplo, se a duração do tempo limite for 270s e a primeira tentativa tiver consumido 200s, o PDF Generator tentará novamente a conversão. Se a primeira tentativa consumiu 270s, a conversão não será repetida.

## Configurações de serviço dos Utilitários ES4 {#guides-es4-utilities-service-settings}

Quando você cria um Guia, alguns recursos, como a definição do Guia, são incorporados ao Guia. Os recursos também podem existir como referências aos ativos de aplicativos armazenados localmente ou no servidor do AEM Forms. O Guia não contém dados, e os valores para o local de envio e as entradas não são adequados para todos os ambientes externos.

Na maioria dos casos, os serviços de renderização de Guias padrão são suficientes para preparar um Guia para uso no Workspace ou em outros ambientes externos. (Na visualização Serviços, no Workbench, o serviço padrão é Guias (sistema)/Processos/Guia de renderização - 1.0.) O serviço do Guia de utilitários ( `GuidesUtility`) permite criar um processo personalizado para renderizar um Guia, se necessário.

As operações do Guia de utilitários permitem adicionar as seguintes tarefas de renderização do Guia a um processo:

* Determine se os dados estão disponíveis para preencher o Guia com
* Incorporar os dados do Guia ou convertê-los em um link
* Converter conteúdo referenciado em URLs acessíveis externamente
* Substitua valores em um documento HTML ou outro invólucro, ou converta-os em URLs acessíveis externamente
* Definir a localização de envio
* Especificar valores de entrada
* Criar um parâmetro para representar o conteúdo referenciado
* Se houver variações disponíveis, defina uma variação

Os valores padrão para o serviço Utilitários guia suportam a maioria dos casos de uso. No entanto, se necessário, é possível alterar os valores a seguir.

**publicPaths:** Essa opção foi substituída. Não use essa opção com formulários AEM.

**pathInfoExpiryInSeconds:** O intervalo após o qual uma solicitação de informações de caminho de um cliente expira. O padrão é 1.

**collateralExpiryInSeconds:** O intervalo após o qual uma solicitação de garantias de um cliente expira. O padrão é 315576000.

**mismatchExpiryInSeconds:** O intervalo após o qual uma solicitação de material de apoio de um cliente expira, quando o eTag (marca de entidade) não corresponde. (Uma eTag é um cabeçalho de resposta HTTP.) O padrão é 1.

**guideContext:** A raiz de contexto do aplicativo web Guides. Corresponde ao valor definido usando o aplicativo web Guides. O padrão é /Guides/.

**secureRandomAlgorithm:** O algoritmo a ser usado ao gerar chaves e identificadores. Esse valor é passado para o método getInstance da classe Java SecureRandom. O padrão é SHA1PRNG.

**idBytes:** O número de bytes aleatórios a serem usados para um identificador de chave. O padrão é 6.

**macAlgorithm:** O algoritmo MAC (código de autenticação de mensagem) a ser usado para verificação de URL adicional. Este método é passado para o método getInstance da classe Mac. O padrão é HmacSHA1.

**macRefreshIntervalInMinutes:** O tempo em que uma chave está ativa. Quando uma chave está ativa nesse intervalo, uma nova chave é gerada. A nova chave se torna a chave ativa. A chave anteriormente ativa é mantida por 10% do intervalo de atualização. Esse comportamento permite que os URLs gerados com o uso da chave antiga continuem a funcionar no switch de chave. O padrão é 144000.

**macOverlapIntervalInMinutes:** Tempo em que a chave anterior permanecerá válida após a geração de uma nova. O padrão é 1440 minutos (1 dia).

**macKeySeed:** Um valor de seed para gerar o URL seguro. Quando essa é a opção, a chave nunca é atualizada. Definir a mesma seed em servidores diferentes resultará na geração de URLs seguros compatíveis. Isso pode ser útil se vários servidores de formulários estiverem em uso atrás de um balanceador de carga. Insira uma sequência aleatória de caracteres e números como a seed.

### Usando Guias em um cluster de servidores {#using-guides-in-a-server-cluster}

A renderização de um Guia em um cluster de servidores que não usa sessões aderentes falha com uma exceção de ponteiro nulo. Uma solicitação do Guides usa URLs seguros que, por padrão, são exclusivos do servidor em que são gerados. Em um cluster que usa sessões aderentes, depois que uma solicitação atinge um nó no cluster, todas as solicitações subsequentes dessa sessão ou usuário são roteadas exclusivamente para esse servidor e tudo está OK. Em um cluster que não usa sessões aderentes, as solicitações subsequentes podem atingir qualquer servidor no cluster. Se o servidor que as solicitações atingiram não for o servidor original, eles não resolverão o URL seguro.

Se você estiver usando Guides em um cluster de servidores que não usa sessões adesivas, defina o valor macKeySeed para o serviço GuidesUtility e, em seguida, pare e inicie o cluster.

O valor macKeySeed é a semente do gerador de números aleatórios usado para gerar os URLs seguros. A definição desse valor faz com que cada nó do cluster inicialize o gerador de números aleatórios da mesma maneira e tenha acesso aos mesmos URLs seguros. Você pode usar qualquer string aleatória para esse valor de seed.

Altere o valor macKeySeed quando precisar atualizar os URLs seguros. Atualizar os URLs seguros depende da sua política de segurança e é semelhante à política de atualização para alterar a senha raiz mestre do servidor. O macSeedValue é análogo à senha mestre para os URLs seguros, porque é usado para gerar um novo número aleatório exclusivo para uso na geração e recuperação de URL seguros.

Você deve reiniciar o cluster porque o macSeedValue é somente leitura na inicialização do sistema. Todos os nós precisam reiniciar para ler o valor, porque eles o usam independentemente para inicializar seus números aleatórios internos com o valor de seed.

## Configurações do serviço JDBC {#jdbc-service-settings}

O serviço JDBC ( `JdbcService`) permite que os processos interajam com bancos de dados.

A configuração a seguir está disponível para o serviço JDBC.

**datasourceName:** Um valor de string que representa o nome JNDI da origem de dados a ser usada para conexão com o servidor de banco de dados. A fonte de dados deve ser definida no servidor de aplicativos que hospeda o Forms Server. O valor padrão é o nome JNDI da fonte de dados para o banco de dados de formulários AEM.

## Configurações do serviço JMS {#jms-service-settings}

O serviço JMS ( `JMS`) permite a interação com provedores Java Messaging System (JMS) que implementam mensagens ponto a ponto e publicam/assinam mensagens.

Configure o serviço JMS com propriedades default para que as operações do serviço possam se conectar e interagir com um provedor JMS e um serviço JNDI associado. Os valores das propriedades do serviço são definidos como valores padrão com base no JBoss Application Server. Altere esses valores se estiver usando um servidor de aplicativos diferente para hospedar formulários AEM.

As seguintes configurações estão disponíveis para o serviço JMS.

**URL do provedor:** O URL do provedor de serviços JNDI. O valor padrão é baseado no JBoss Application Server. Os seguintes URL são valores padrão para os servidores de aplicativos compatíveis com os formulários AEM:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nome de usuário JNDI:** O nome de usuário da conta a ser usada para autenticação com o provedor de serviços JNDI que é usado para procurar nomes de filas e tópicos. O valor padrão é convidado.

**Senha JNDI:** A senha associada ao nome de usuário especificado para o Nome de Usuário JNDI. O valor padrão é convidado.

**Fábrica de contexto inicial:** A classe Java a ser usada como a fábrica de contexto inicial. O serviço JMS usa essa classe para criar um contexto inicial, que é o ponto de partida para resolver nomes de tópicos e filas. O valor padrão é o fatory de contexto inicial do serviço JMS no JBoss. As classes a seguir são as fábricas de contexto inicial para os servidores de aplicativos compatíveis com os formulários AEM:

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**Nome de usuário da conexão:** A senha associada ao nome de usuário especificado para o Nome de Usuário da Conexão. O valor padrão é convidado.

**Senha da conexão:** A senha associada ao nome de usuário especificado para o Nome de Usuário da Conexão. O valor padrão é convidado.

**Outras propriedades:** Pares de nome e valor de propriedade que você pode passar para o provedor de serviços JNDI. Essas propriedades dependem da implementação e da configuração do provedor que você está usando.

Os pares de nome e valor da propriedade são separados por ponto e vírgula **;**. Por exemplo, o texto a seguir mostra o valor que seria especificado para duas propriedades chamadas name1 e name2, com valores value1 e value2, respectivamente:

`name1=value1;name2=value2`

## Configurações do serviço LDAP {#ldap-service-settings}

O serviço LDAP ( `LDAPService`) fornece operações para consultar diretórios LDAP. Diretórios LDAP são geralmente usados para armazenar informações sobre as pessoas, grupos e serviços em uma organização.

As configurações a seguir estão disponíveis para o serviço LDAP.

**Fábrica de contexto inicial:** A classe Java a ser usada como a fábrica de contexto. Essa classe é usada para criar uma conexão com o servidor LDAP. O valor padrão é com.sun.jndi.ldap.LdapCtxFactory, que é apropriado para a maioria dos servidores LDAP.

**URL do provedor:** O URL a ser usado para conexão com o serviço LDAP. O formato do valor é `ldap://server name:port`

*nome do servidor* é o nome do computador que hospeda o servidor LDAP

*porta* é a porta de comunicação que o serviço LDAP usa. O valor padrão é 389, que é a porta padrão usada para conexões LDAP.

**Nome de usuário:** O nome de usuário da conta de usuário a ser usada para fazer login no servidor LDAP. A conta de usuário precisa ter permissão para se conectar ao servidor e ler as informações no diretório LDAP.

Dependendo do servidor LDAP, o nome de usuário pode ser um nome de usuário simples, como `myname` ou um DN, como `cn=myname,cn=users,dc=myorg`.

**Senha:** A senha que corresponde ao nome de usuário fornecido para a configuração Nome de usuário.

**Outras propriedades:** Um valor de string que representa outras propriedades e seus valores correspondentes que você pode fornecer ao servidor LDAP. O valor está no seguinte formato:

`property=value;property=value;...`

## Definições do serviço de configuração do Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

O serviço de configuração do Microsoft SharePoint `(MSSharePointConfigService)`permite especificar credenciais para o usuário do AEM Forms que tem permissões de representação. Para obter informações sobre permissões de representação, consulte [Configuração do conector para o Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

As seguintes configurações estão disponíveis para o serviço de configuração do Microsoft SharePoint:

* Nome de usuário para um usuário com permissões de representação
* Senha do usuário acima

**Habilitar SSL (HTTPS):**

**Tempo de vida:** Tempo, em segundos, que este perfil de provisionamento é válido e armazenado em cache no cliente. O padrão é 86400 (24 horas). Quando um aplicativo cliente é sincronizado com o servidor e o tempo especificado passa, o aplicativo cliente solicita um novo perfil de provisionamento do servidor.

**Criptografia:** Especifica se os dados armazenados no dispositivo móvel devem ser criptografados.

**Aplicativo Forms:** Ativa o recurso Forms nos aplicativos de cliente móvel. Quando essa opção é selecionada, os usuários podem abrir formulários e iniciar processos em seus dispositivos móveis.

**Aplicativo de tarefas:** Habilita o recurso Tarefas nos aplicativos de cliente móvel. Quando essa opção é selecionada, os usuários podem acessar suas listas de tarefas e concluir tarefas de seus dispositivos móveis.

**Aplicativo Content Services:** Habilita o recurso Serviços de conteúdo no aplicativo cliente móvel. Esse recurso está disponível somente para o iOS. Quando essa opção é selecionada, os usuários do iPhone e do iPad podem acessar arquivos armazenados no servidor WebDAV de suas organizações.

**Suporte offline:** Permite que os usuários continuem usando os aplicativos cliente móveis mesmo quando não têm uma conexão com o servidor (por exemplo, quando estão fora do intervalo de células ou no modo avião). Os usuários também devem ativar a configuração Suporte offline em seus dispositivos móveis. Esse recurso está disponível para dispositivos Android e iOS. Por padrão, esse recurso está desativado.

>[!NOTE]
>
Se o suporte Offline tiver sido habilitado e você desabilitá-lo, os perfis de provisionamento dos usuários serão atualizados imediatamente ou assim que estiverem online. Se um usuário estiver trabalhando offline, todas as tarefas pendentes serão retornadas à lista Tarefas e todos os itens em sua Fila, incluindo formulários, tarefas e formulários pendentes com erros de validação, serão excluídos da Fila.

**Android:** Permite que dispositivos Android se conectem ao servidor.

**Apple iOS:** Permite que iPhones e iPads se conectem ao servidor.

**AIR:** Permite que dispositivos que executam aplicativos baseados em Adobe AIR® se conectem ao servidor.

**BlackBerry:** Permite que dispositivos BlackBerry se conectem ao servidor.

**Android Microsoft Exchange AtiveSync Necessário:** Especifica se o gerenciador de políticas do Microsoft Exchange AtiveSync (EA) deve estar instalado e ativo em dispositivos Android. Quando essa opção é selecionada, o EA deve ser aplicado no dispositivo Android. Quando essa opção não está selecionada, nenhuma verificação é executada, embora outros requisitos ainda sejam aplicados.

**Comprimento mínimo do PIN do Android:** Os dispositivos Android devem ter uma configuração global que imponha que o PIN ou a senha tenha pelo menos esse comprimento. Simplesmente ter um PIN do comprimento especificado não é suficiente. O comprimento do PIN deve ser aplicado pelo sistema para que os usuários não possam remover ou encurtar o PIN posteriormente. O valor padrão é 4.

**Máximo de tentativas de senha do Android antes de apagar:** Os dispositivos Android têm uma configuração global que apaga o sistema após um número especificado de tentativas de senha inválidas. Essa configuração global está ativada e é igual ou inferior ao valor especificado aqui. O valor padrão é 5.

**Apagamento Do Android Na Remoção:** Especifica o que acontece quando uma violação de política ocorre em um dispositivo Android. Quando essa opção é selecionada, a conta é excluída. Quando essa opção não está selecionada, a senha da conta armazenada e os dados em cache são excluídos. Não são feitas mais tentativas de sincronização até que o usuário corrija a violação de política.

## Configurações do serviço de saída {#output-service-settings}

O Serviço de saída `(OutputService)`O permite mesclar dados de formulário XML com um design de formulário criado no AEM Forms Designer para criar um fluxo de saída de documento em um dos seguintes formatos:

* Um fluxo de saída de documento PDF ou PDF/A.
* Um fluxo de saída do Adobe PostScript.
* Um fluxo de saída PCL (Printer Control Language).
* Um fluxo de saída da Linguagem de programação de zebra (ZPL).

O fluxo de saída pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo de disco. Ao usar o Serviço de saída como parte de um processo, também é possível enviar o fluxo de saída para um destinatário de email como um anexo de arquivo.

As configurações a seguir estão disponíveis para o serviço de Saída.

**Tipo de transação:** Especifica como um contexto de transação deve ser propagado para uma operação:

**Obrigatório:** suporta um contexto de transação se já existir um; caso contrário, um novo contexto de transação é criado. Este é o valor padrão.

**Exige novo:** Sempre cria um novo contexto de transação. Se existir um contexto de transação ativo, ele será suspenso.

**Tempo limite da transação (em segundos):** O número de segundos que o provedor de transação subjacente aguarda antes de reverter uma transação que está quebrando esta operação. Esse valor será ignorado se um contexto de transação existente for propagado.

Ao processar arquivos de dados grandes ou operar em um servidor ocupado, pode ser necessário aumentar o tempo limite do serviço de Saída. Para alterar o valor de tempo limite, verifique se os servidores de hardware têm memória adequada e se a memória está disponível para o heap do Java Application Server. O valor padrão é `180`.

## Configurações do serviço de configuração do PDFG {#pdfg-config-service-settings}

As seguintes configurações estão disponíveis para o serviço de configuração PDFG ( `PDFGConfigService`).

**Diretório de Opções de Trabalho do Usuário:** O caminho da pasta do sistema de arquivos onde o serviço c grava os arquivos de opções de trabalho acessíveis ao Acrobat Pro Extended. O valor padrão é [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**Diretório de inicialização PS:** O caminho da pasta do sistema de arquivos onde os arquivos de inicialização exigidos pelo Adobe Acrobat Distiller são salvos. O valor padrão é [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**Arquivo de inicialização PS:** O nome do arquivo de inicialização exigido pelo Adobe Acrobat Distiller. O valor padrão é example.ps.

**Tempo limite de conversão do servidor:** O tempo limite máximo de conversão de trabalho (em segundos) para o serviço Generate PDF e o serviço Distiller. Essa configuração limita o tempo limite máximo de conversão que pode ser especificado no arquivo config.xml e nas páginas de console de administração para o PDF Generator. O valor padrão é 270.

**Tempo limite global do servidor:** Ao executar conversões de PDF, um servidor Forms considera o tempo limite. Configure o valor de tempo limite para resolver o problema.

**Prefixo das opções de trabalho:** Um prefixo usado pelo serviço Gerar PDF para anexar uma pequena string aos arquivos de opções de trabalho criados temporariamente para uso pelo Acrobat Distiller. O valor padrão é pdfg.

**Aplicativos não Unicode:** Uma lista separada por vírgulas de nomes de aplicativos que são conhecidos por serem incompatíveis com Unicode. Essa lista é pré-preenchida com os nomes de vários aplicativos, suporte para o qual é pré-configurado no PDF Generator. Se você optar por adicionar suporte para conversões de PDF por meio de outros aplicativos de terceiros incompatíveis com Unicode, será necessário adicioná-los a esta lista. O valor padrão é Autocad, Excel, PowerPoint, Projeto, Editor, Visio, Word, WordPerfect.

**Contagem de Threadpool do Servidor:** Controla o tamanho do pool de threads que o serviço Gerar PDF usa internamente para atender às solicitações de conversão HTML para PDF que envolvem spidering (convertendo páginas vinculadas acessíveis a partir da página principal). O valor padrão é 20.

**Segundos para varredura de limpeza do PDFG:** Consulte a seção Segundos para expiração da tarefa para obter detalhes.

**Segundos para expiração da tarefa:** O serviço Generate PDF exclui os arquivos de entrada assim que são convertidos. Ele armazena arquivos de saída temporariamente, por um período determinado pelas configurações Segundos de verificação de limpeza do PDFG e Segundos de expiração da tarefa.

A configuração Segundos para expiração da tarefa especifica a idade de um arquivo ou pasta vazia antes de ser elegível para exclusão. A configuração Segundos para varredura de limpeza do PDFG especifica com que frequência um thread de limpeza examina as pastas temporárias em busca de arquivos que podem ser excluídos.

Por exemplo, se a opção Segundos para expiração da tarefa estiver definida como 100 e a opção Segundos para verificação de limpeza do PDFG estiver definida como 200, o thread de limpeza será executado a cada 200 segundos e excluirá os arquivos com 100 segundos ou mais.

O valor padrão de Segundos para varredura de limpeza do PDFG é `43200` (12 horas). O valor padrão de Segundos para expiração da tarefa é `86400` (24 horas).

**Localidade padrão:** Usado para substituir a localidade padrão (país + idioma) do servidor onde o serviço Gerar PDF está implantado. Se esse parâmetro não for especificado, a localidade padrão será determinada a partir do sistema operacional no qual o serviço é implantado. Esse parâmetro controla o idioma em que as mensagens de erro são retornadas às APIs.

## configurações do serviço Data Services do fluxo de trabalho de formulários {#forms-workflow-data-services-service-settings}

Os serviços a seguir estendem o Data Services e expõem os assemblers que o Espaço de trabalho usa para se comunicar com o servidor. Não altere as opções de configuração desses serviços, a menos que seja instruído a fazê-lo pelo Suporte Adobe. Estes serviços não se destinam ao acesso direto:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Configurações do serviço de comunicação remota {#remoting-service-settings}

A maioria dos serviços é configurada para que você possa acessá-los por meio do AEM forms Remoting (Obsoleto para o AEM forms). Para obter informações sobre a comunicação remota de formulários AEM (obsoleto para o AEM), consulte [Programação com formulários AEM](https://adobe.com/go/learn_aemforms_programming_63).

As configurações a seguir estão disponíveis para o serviço de Comunicação Remota.

**Método de autenticação de cliente Flex:** Determina o tipo de resposta que o servidor envia de volta ao cliente quando o serviço chamado está habilitado para segurança, a operação chamada não dá suporte a invocações anônimas e o cliente passa credenciais inválidas ou nenhuma. Escolha Personalizado ou Básico. O valor padrão é Básico.

**Permitir Serialização De Classes Não Serializáveis:** A maioria dos pontos de extremidade de formulários AEM permite que somente classes Serializáveis sejam usadas para invocação. Em versões mais antigas, o endpoint de Comunicação Remota permitia que classes não serializáveis fossem usadas para invocação de clientes baseados em Flex. Para evitar uma vulnerabilidade de segurança descrita no APS11-15, isso foi alterado. Se quiser continuar a usar classes não serializáveis com o ponto de extremidade do Flex Remoting, marque esta caixa de seleção.

## Configurações do serviço de repositório {#repository-service-settings}

O serviço de Repositório ( `RepositoryService`) fornece serviços de armazenamento e gerenciamento de recursos para formulários AEM. Quando desenvolvedores criam um aplicativo, eles podem implantar os ativos no repositório em vez de em um sistema de arquivos. Os ativos podem incluir qualquer tipo de material adicional, incluindo formulários XML, PDF forms (incluindo formulários Acrobat), fragmentos de formulário, imagens, perfis, políticas, arquivos SWF, arquivos DDX, esquemas XML, arquivos WSDL e dados de teste.

Você pode usar o repositório padrão incluído com formulários AEM ou usar um repositório de terceiros (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager).

O Serviço do Provedor do Repositório é um delegado de serviço que atua como a interface para um serviço do provedor. Isso permite que você se conecte a uma API comum e não precise saber qual provedor de serviço está implementando os recursos de armazenamento. O serviço do Provedor do Repositório fornece armazenamento de banco de dados para os recursos do serviço do Repositório.

A configuração a seguir está disponível para o serviço de Repositório.

**Serviço do provedor:** O nome do serviço usado como provedor de armazenamento. O valor padrão é RepositoryProviderService.

## Configurações do serviço de assinatura {#signature-service-settings}

O serviço de assinatura ( `SignatureService`) permite que sua organização proteja a segurança e a privacidade de documentos do Adobe PDF que ela distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que os documentos não sejam alterados. Alterar um documento quebra sua assinatura. Como os recursos de segurança são aplicados ao próprio documento, ele permanece seguro e controlado durante todo o ciclo de vida; além do firewall, quando é baixado offline e quando é enviado de volta à sua organização.

As configurações a seguir estão disponíveis para o serviço de Assinatura.

**Nome do serviço SPI do HSM remoto:** Essa opção é para uso quando o HSM é instalado em um computador remoto. Especifique esta opção quando o AEM Forms estiver instalado em um Windows de 64 bits e você estiver usando dispositivos HSM para assinatura.

**URL Do Serviço Web HSM Remoto:** Especifique esta opção quando o AEM Forms estiver instalado no Windows de 64 bits e você estiver usando dispositivos HSM para assinatura.

**Certificação Para Incluir Alterações De Carregamento De Formulário:** Quando essa opção é selecionada, o Estado do formulário XFA é certificado, além do modelo XFA. Observe que ativar essa opção pode ter um impacto negativo no desempenho. O valor padrão é true.

**Executar scripts de JavaScript de documentos:** Especifica se scripts JavaScript de documentos devem ser executados durante operações de assinatura. O valor padrão é false.

**Processar documentos com compatibilidade com o Acrobat 9:** Especifica se a compatibilidade com o Acrobat 9 deve ser habilitada. Por exemplo, quando essa opção é selecionada, a opção Certificação visível em PDF dinâmico é ativada. O valor padrão é false.

**Incorporar Informações De Revogação Ao Assinar:** Especifica se as informações de revogação são inseridas durante a assinatura do documento PDF. O valor padrão é false.

**Incorporar Informações De Revogação Ao Certificar:** Especifica se as informações de revogação são inseridas durante a certificação do documento PDF. O valor padrão é false.

**Forçar a incorporação de informações de revogação para todos os certificados durante a assinatura/certificação:** Especifica se uma operação de assinatura ou certificação falhará se as informações de revogação válidas para todos os certificados não estiverem incorporadas. Observe que, se um certificado não contiver informações de CRL ou OCSP, ele será considerado válido, mesmo se nenhuma informação de revogação for recuperada. O valor padrão é false.

**Ordem de verificação de revogação:** Especifica a ordem de verificação de revogação quando a verificação é possível por meio dos mecanismos CRL (Lista de Revogação de Certificados) e OCSP (Protocolo de Status de Certificados Online). O valor padrão é OCSPFirst.

**Tamanho Máximo Das Informações De Arquivamento De Revogação:** O tamanho máximo das informações de arquivamento de revogação, em quilobytes. Os formulários AEM tentam armazenar o máximo possível de informações de revogação sem exceder o limite. O valor padrão é 10 KB.

**Assinaturas De Suporte Criadas De Builds De Pré-Lançamento De Produtos Adobe:** Quando essa opção estiver selecionada, a assinatura criada usando a versão de pré-lançamento dos produtos Adobe será validada corretamente. O valor padrão é false.

**Opção de Tempo de Verificação:** Especifica a hora de verificação do certificado de um signatário. O valor default é Horário de Segurança Mais Horário Atual.

**Usar informações de revogação arquivadas na assinatura durante a validação:** Especifica se as informações de revogação arquivadas com a assinatura são usadas para verificação de revogação. O valor padrão é true.

**Usar Informações De Validação Armazenadas No Documento Para Validação De Assinaturas:** Quando essa opção é selecionada, as informações de validação (incluindo informações de revogação e carimbo de data e hora) incorporadas ao documento são usadas para validar assinaturas. O valor padrão é true.

**Máximo de Sessões de Verificação Aninhadas Permitidas:** O número máximo de sessões de verificação aninhadas permitidas. Os formulários AEM usam esse valor para impedir um loop infinito ao verificar os certificados do assinante do OCSP ou da CRL quando o certificado do OCSP ou da CRL não está configurado corretamente. O valor padrão é 10.

**Desvio máximo do relógio para verificação:** O tempo máximo, em minutos, que o tempo de assinatura pode ser posterior ao tempo de validação. Se a inclinação do relógio for maior que esse valor, a assinatura não será válida. O valor padrão é 65 minutos.

**Cache vitalício do certificado:** A duração de um certificado, recuperado online ou por outros meios, no cache. O valor padrão é 1 dia.

### Opções de transporte {#transport-options}

**Host do proxy:** O URL do host proxy. Usado somente se algum valor válido for fornecido. Nenhum valor padrão.

**Porta do proxy:** A porta do proxy. Digite qualquer número de porta válido de 0 a 65535. O valor padrão é 80.

**Nome de usuário de logon de proxy:** O nome de usuário de logon do proxy. Usado somente se algum valor válido for fornecido para host de proxy e porta de proxy. Nenhum valor padrão.

**Senha de logon de proxy:** A senha de login do proxy. Usado somente se algum valor válido for fornecido para o host do proxy, porta do proxy e nome de usuário de logon do proxy. Nenhum valor padrão.

**Limite máximo de download:** A quantidade máxima de dados, em MBs, que pode ser recebida por conexão. O valor mínimo é 1 MB e o máximo é 1024 MB. O valor padrão é 16 MB.

**Tempo limite da conexão:** O tempo máximo de espera, em segundos, para estabelecer uma nova conexão. O valor mínimo é 1 e o máximo é 300. O valor padrão é 5.

**Tempo limite do soquete:** O tempo máximo de espera, em segundos, antes que ocorra um tempo limite do soquete (durante a espera pela transferência de dados). O valor mínimo é 1 e o máximo é 3600. O valor padrão é 30.

### Opções de validação de caminho {#path-validation-options}

**Exigir Política Explícita:** Especifica se o caminho deve ser válido para pelo menos uma das políticas de certificado associadas à âncora de confiança do certificado do signatário. O valor padrão é false.

**Política de inibição de QUALQUER tipo:** Especifica se o OID (identificador de objeto de política) deverá ser processado se estiver incluído em um certificado. O valor padrão é false.

**Impedir mapeamento de política:** Especifica se o mapeamento de política é permitido no caminho de certificação. O valor padrão é false.

**Verificar todos os caminhos:** Especifica se todos os caminhos devem ser validados ou se a validação deve parar após localizar o primeiro caminho válido. Selecione verdadeiro ou falso. O valor padrão é false.

**Servidor LDAP:** O servidor LDAP usado para procurar certificados para validação de caminho. Nenhum valor padrão.

**Seguir URIs na AIA do certificado:** Especifica se os URIs (Uniform Resource Identifiers) no AIA do certificado são processados durante a descoberta de caminhos. O valor padrão é false.

**Extensão de Restrições Básicas necessária nos Certificados CA:** Especifica se a extensão de certificado de Restrições Básicas da autoridade de certificação (CA) deve estar presente para certificados de CA. Alguns certificados de raiz certificados alemães mais antigos (7 e anteriores) não estão em conformidade com a RFC 3280 e não contêm a extensão de restrição básica. Se souber que o certificado EE de um usuário está vinculado a essa raiz alemã, desmarque essa caixa de seleção. O valor padrão é true.

**Exigir Assinatura De Certificado Válida Durante A Construção Da Cadeia:** Especifica se o criador de cadeias requer assinaturas válidas em certificados usados para criar cadeias. Quando essa caixa de seleção estiver marcada, o criador de cadeias não criará cadeias com assinaturas RSA inválidas nos certificados. Considere cadeia CA > ICA > EE onde a assinatura da CA em um ICA não é válida. Se esta configuração for verdadeira, a construção da cadeia parará no ICA e o CA não será incluído na cadeia. Se essa configuração for falsa, a cadeia completa de três certificados será produzida. Essa configuração não afeta assinaturas DSA. O valor padrão é false.

### Opções do provedor de carimbo de data e hora {#timestamp-provider-options}

**URL do servidor TSP:** O URL do provedor de carimbo de data e hora padrão. Usado somente se algum valor válido for fornecido. Nenhum valor padrão.

**Nome de usuário do servidor TSP:** O nome do usuário, se necessário, pelo provedor de carimbo de data e hora. Usado somente se algum valor válido for fornecido para o URL. Nenhum valor padrão.

**Senha do servidor TSP:** A senha do nome de usuário acima, se necessário, pelo provedor de carimbo de data e hora. Usado somente se algum valor válido for fornecido para o URL e o nome de usuário. Nenhum valor padrão.

**Algoritmo de hash de solicitação:** Especifica o algoritmo de hash a ser usado ao criar a solicitação para o provedor de carimbo de data/hora. O valor padrão é SHA1.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado para determinar o status de confiança do certificado do provedor de carimbo de data/hora a partir do status de revogação observado. O valor padrão é BestEffort.

**Enviar nonce:** Especifica se um nonce é enviado com a solicitação de provedor de carimbo de data/hora. Um nonce pode ser um carimbo de data e hora, um contador de visitas em uma página da Web ou um marcador especial destinado a limitar ou impedir a reprodução ou reprodução não autorizada de um arquivo. O valor padrão é true.

**Usar carimbos de data/hora expirados durante a validação:** Quando essa opção é selecionada, os carimbos de data e hora expirados podem ser usados para recuperar tempos de validação de assinaturas. O valor padrão é true.

**Tamanho da resposta de TSP:** Tamanho estimado, em bytes, da resposta do TSP. Esse valor deve representar o tamanho máximo da resposta do carimbo de data e hora que o provedor de carimbo de data e hora configurado pode retornar. Não altere a menos que tenha certeza. O valor mínimo é de 60B e o máximo é de 10240B. O valor padrão é 4096B.

**Ignorar extensão de servidor de carimbo de data/hora**: selecione a variável **Ignorar extensão de servidor de carimbo de data/hora** opção para impedir que o servidor do AEM Forms entre em contato com o servidor de carimbo de data e hora especificado. Selecionar a opção ajuda a evitar falhas de processo que ocorrem devido ao tempo limite da conexão entre o AEM Forms e os servidores de carimbo de data e hora.

### Opções de Lista de Revogação de Certificado {#certificate-revocation-list-options}

**Consultar URI local primeiro:** Especifica se a localização da CRL fornecida na URI Local ou na Pesquisa da CRL deve ter preferência sobre qualquer localização especificada em um certificado para fins de verificação de revogação. O valor padrão é false.

**URI local para pesquisa de CRL:** URL do provedor local de CRL. Este valor é consultado somente se a configuração Consultar URI local primeiro estiver definida como verdadeiro. Nenhum valor padrão.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado para determinar o status de confiança do certificado do provedor da CRL a partir do status de revogação observado. O valor padrão é BestEffort.

**Servidor LDAP para Pesquisa de CRL:** O Servidor LDAP usado para obter as CRLs (como www.ldap.com). Todas as consultas baseadas em DN para CRLs serão direcionadas a este servidor. Nenhum valor padrão.

**Ficar online:** Especifica se é necessário entrar online para buscar uma CRL. Se for falso, somente as CRLs em cache (no disco local ou aquelas incorporadas com assinatura) serão consultadas. O valor padrão é true.

**Ignorar datas de validade:** Especifica se deve ignorar os tempos thisUpdate e nextUpdate da resposta, o que impede que esses tempos tenham um efeito negativo na validade da resposta. O valor padrão é false.

**Exigir extensão AKI na CRL:** Especifica se a extensão Identificador de Chave da Autoridade deve ser incluída em uma CRL. O valor padrão é false.

### Opções de Protocolo de Status de Certificado Online {#online-certificate-status-protocol-options}

**URL do servidor OCSP:** URL do servidor OCSP padrão. Se o servidor OCSP especificado por meio desse URL for usado, isso dependerá da configuração da opção URL para consulta. Nenhum valor padrão.

**Opção de URL para consulta:** Controla a lista e a ordem dos servidores OCSP usados para executar a verificação de status. O valor padrão é UseAIAInCert.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado ao verificar o certificado do servidor OCSP. O valor padrão é CheckIfAvailable.

**Enviar nonce:** Especifica se um nonce é enviado com a solicitação OCSP. Um nonce pode ser um carimbo de data e hora, um contador de visitas em uma página da Web ou um marcador especial destinado a limitar ou impedir a reprodução ou reprodução não autorizada de um arquivo. O valor padrão é true.

**Tempo máximo de desvio do relógio:** Extensão máxima permitida, em minutos, entre o tempo de resposta e o horário local. O valor mínimo é 0 e o máximo é 2147483647m. O valor padrão é 5m.

**Tempo de atualização da resposta:** Tempo máximo, em minutos, durante o qual uma resposta de OCSP pré-construída é considerada válida. O valor mínimo é 1m e o máximo permitido é 2147483647. O valor padrão é 525600 (um ano).

**Solicitação do Sign OCSP:** Especifica se a solicitação OCSP deve ser assinada. O valor padrão é false.

**Alias da credencial do assinante da solicitação:** Especifica o alias de credencial a ser usado para assinar a solicitação OCSP se a assinatura estiver habilitada. Usado somente se a assinatura da solicitação OCSP estiver habilitada. Nenhum valor padrão.

**Ficar online:** Especifica se deve ficar online para fazer a verificação de revogação. O valor padrão é true.

**Ignore as respostas thisUpdate e nextUpdate vezes:** Especifica se deve ignorar os tempos thisUpdate e nextUpdate da resposta, o que impede que esses tempos tenham um efeito negativo na validade da resposta. O valor padrão é false.

**Permitir extensão OCSPNoCheck:** Especifica se a extensão OCSPNoCheck é permitida no certificado de assinatura de resposta. O valor padrão é true.

**Exigir extensão CertHash ISIS-MTT do OCSP:** Especifica se uma extensão de hash de chave pública de certificado deve ser incluída nas respostas OCSP. O valor padrão é false.

### Opções de tratamento de erros para depuração {#error-handling-options-for-debugging}

**Limpar cache de certificado na próxima chamada de API:** Especifica se o Cache de Certificado deve ser limpo quando a próxima Operação do Serviço de Assinatura for chamada. Depois que a operação é chamada, essa opção é definida novamente como false. O valor padrão é false.

**Limpar cache da CRL na próxima chamada da API:** Especifica se o Cache de CRL deve ser limpo quando a próxima Operação do Serviço de Assinatura for chamada. Depois que a operação é chamada, essa opção é definida novamente como false. O valor padrão é false.

**Limpar cache OCSP na próxima chamada de API:** Especifica se o cache OCSP deve ser limpo quando a próxima operação de serviço de assinatura for chamada. Depois que a operação é chamada, essa opção é definida novamente como false. O valor padrão é false.

## Configurações do serviço de pasta monitorada {#watched-folder-service-settings}

O serviço Pasta monitorada ( `WatchedFolder`) configura atributos que são comuns para todos os endpoints de pasta monitorados. Também fornece valores padrão para endpoints de pastas monitoradas. (Consulte [Configurando pontos de extremidade de pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Ele não é chamado por aplicativos clientes externos nem usado em processos criados no Workbench.

As configurações a seguir estão disponíveis para o serviço Pasta monitorada.

**Expressão Cron:** A expressão cron foi usada pelo quartzo para agendar a pesquisa do diretório de entrada.

**Contagem de repetição:** O número de vezes que o diretório de entrada é sondado. A contagem de repetição padrão a ser usada se esse valor não for especificado na configuração do endpoint. Um valor -1 indica uma varredura indefinida do diretório. O valor padrão é -1.

**Intervalo de Repetição:** O número padrão em segundos entre cada enquete. Esse valor é usado como o intervalo de repetição, a menos que um valor diferente seja especificado na configuração de ponto de extremidade da pasta monitorada. O valor padrão é 5. Consulte a descrição da configuração de Tamanho de lote para obter mais informações.

**Assíncrono:** Identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é assíncrono.

**Tempo de espera:** O valor padrão para o tempo, em segundos, após o qual os arquivos são recuperados das pastas de entrada. Se o arquivo ou pasta for anterior ao tempo especificado no tempo de espera, ele será selecionado para processamento. O valor padrão é 0.

**Tamanho do lote:** O valor padrão para o número de arquivos ou pastas processados por varredura. O valor padrão é 2.

As configurações Intervalo de repetição e Tamanho do lote determinam quantos arquivos a Pasta monitorada coleta em cada verificação. A pasta monitorada usa um pool de threads do Quartz para verificar a pasta de entrada. O pool de threads é compartilhado com outros serviços. Se o intervalo de verificação for pequeno, as threads examinam a pasta de entrada com frequência. Se os arquivos forem soltos com frequência na pasta monitorada, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar as threads.

Se houver um grande volume de arquivos sendo descartados, aumente o tamanho do lote. Por exemplo, se o serviço chamado pelo endpoint da pasta monitorada puder processar 700 arquivos por minuto e os usuários soltarem arquivos na pasta de entrada na mesma taxa, definir o Tamanho do lote como 350 e o Intervalo de repetição como 30 segundos ajudará no desempenho da Pasta monitorada sem incorrer no custo de verificar a pasta monitorada com muita frequência.

Quando os arquivos são colocados na pasta monitorada, ela lista os arquivos na entrada, o que pode reduzir o desempenho se a varredura estiver ocorrendo a cada segundo. O aumento do intervalo de verificação pode melhorar o desempenho. Se o volume de arquivos que está sendo descartado for pequeno, ajuste o Tamanho do lote e o Intervalo de repetição de acordo. Por exemplo, se 10 arquivos forem descartados a cada segundo, tente definir o Intervalo de repetição como 1 segundo e o Tamanho do lote como 10.

Em uma configuração de cluster, o tamanho do lote de um endpoint de pasta monitorada não é dimensionado para vários nós de cluster. Por exemplo, se o tamanho do lote estiver definido como `2` para um cluster de dois nós e a opção Acelerar estiver selecionada, os nós processarão arquivos coletivamente em lotes de dois, em vez de cada nó processar dois arquivos de cada vez.

**Substituir nomes de arquivo duplicados:** Uma string booleana que especifica se a pasta monitorada substitui nomes de arquivo de resultados duplicados e se os documentos preservados com o mesmo nome devem ser substituídos.

**Preservar pasta:** O valor padrão para a pasta de preservação. Esta pasta é usada para copiar os arquivos de origem em se houver um processamento bem-sucedido da entrada. Esse valor pode ser um caminho vazio, relativo ou absoluto com um padrão de arquivo, conforme descrito na configuração Pasta de resultados.

**Pasta com falha:** O nome da pasta onde os arquivos com falha são copiados. Esse valor pode ser um caminho vazio, relativo ou absoluto com um padrão de arquivo, conforme descrito na configuração Pasta de resultados.

**Pasta de resultado:** O nome padrão da pasta de resultados. Esta pasta é usada para copiar os arquivos de resultados para o. Esse valor pode ser um caminho vazio, relativo ou absoluto com o seguinte padrão de arquivo.

* %F = prefixo do nome do arquivo
* %E = extensão de nome de arquivo
* %Y = ano (completo)
* %y = ano (últimos dois dígitos)
* %M = mês
* %D = dia do mês
* %d = dia do ano
* %H = hora (relógio de 24 horas)
* %h = hora (relógio de 12 horas)
* %m = minuto
* %s = segundo
* %l = milissegundo
* %R = número aleatório (de 0 a 9)
* %P = id do processo ou da tarefa

Por exemplo, se forem 20h em 17 de julho de 2009 e você especificar `C:/Test/WF0/failure/%Y/%M/%D/%H/`, a pasta de resultados é `C:/Test/WF0/failure/2009/07/17/20`.

Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta monitorada. Para obter mais informações sobre padrões de arquivo, consulte [Sobre padrões de arquivo](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
Quanto menor o tamanho das pastas de resultados, melhor será o desempenho das Pastas monitoradas. Por exemplo, se a carga estimada para a pasta monitorada for de 1000 arquivos a cada hora, tente um padrão como `result/%Y%M%D%H` para que uma nova subpasta seja criada a cada hora. Se a carga for menor (por exemplo, 1000 arquivos por dia), você poderá usar um padrão como `result/%Y%M%D`.

**Pasta de Preparo:** O nome padrão da pasta de preparo dentro da pasta monitorada.

**Pasta de entrada:** O nome padrão da pasta de entrada dentro da pasta monitorada.

**Preservar na Falha:** Se verdadeiro, os arquivos originais são preservados na pasta de falha em caso de falha.

**Acelerador:** Quando essa opção é selecionada, ela limita o número de trabalhos de pastas monitoradas que o AEM forma processados a qualquer momento. O valor Tamanho do Lote determina o número máximo de trabalhos (Consulte Sobre limitação).

## Configurações do serviço de Web {#web-service-service-settings}

O serviço Web ( `WebService`) permite que os processos chamem operações de serviço da web.

O serviço Web permite que processos chamem operações de serviço Web. Por exemplo, uma organização pode querer integrar um processo para armazenar e recuperar informações como contato e detalhes da conta, chamando os serviços da Web expostos de um provedor de serviços. O serviço da Web chama um serviço da Web especificado e transmite valores para cada um de seus parâmetros. Em seguida, salva os valores de retorno da operação em uma variável designada em um processo.

O serviço Web interage com os serviços Web enviando e recebendo mensagens SOAP. O serviço também oferece suporte ao envio de anexos MIME, MTOM e SwaRef com mensagens SOAP usando o protocolo WS-Attachment. As interações do serviço Web são compatíveis com os sistemas SAP e os serviços Web .NET.

As configurações a seguir estão disponíveis para o serviço Web.

**Armazenamento de chaves:** O caminho completo do arquivo de armazenamento de chaves que contém a chave privada a ser usada para autenticação. O Forms Server deve ser capaz de acessar o arquivo.

**Senha da chave de armazenamento:** A senha do arquivo de armazenamento de chaves.

**Tipo de armazenamento de chave:** O tipo de armazenamento de chaves. Não forneça nenhum valor para usar o tipo de armazenamento de chaves padrão configurado para a JVM que executa o Forms Server. Caso contrário, forneça um dos seguintes valores:

* jks
* pkcs12
* cms
* jceks

**Armazenamento de confiança:** O caminho completo do arquivo de armazenamento de confiança que contém a chave pública do servidor do serviço Web.

**Senha do armazenamento de confiança:** A senha do arquivo truststore.

**Tipo de armazenamento de confiança:** O tipo de truststore. Não forneça nenhum valor para usar o tipo de armazenamento de chaves padrão configurado para a JVM que executa o Forms Server. Caso contrário, forneça um dos seguintes valores:

* jks
* pkcs12
* cms
* jceks

## Configurações do serviço de transformação XSLT {#xslt-transformation-service-settings}

O serviço de transformação XSLT ( `XSLTService`) permite que os processos apliquem XSLT (Extensible Stylesheet Language Transformations, transformações de linguagem de folha de estilos extensível) em documentos XML.

A configuração a seguir está disponível para o serviço de transformação XSLT.

**Nome da fábrica:** O nome totalmente qualificado da classe Java a ser usada para executar transformações XSLT. Se nenhum valor for especificado, a fábrica padrão configurada na Java Virtual Machine que executa o Forms Server será usada.

## Modificando configurações de segurança para um serviço {#modifying-security-settings-for-a-service}

O Forms Server permite definir configurações de segurança para cada serviço, o que permite configurar o controle de acesso refinado em um nível de serviço por serviço.

Os perfis de segurança padrão são instalados, que podem ser configurados para atender às necessidades do sistema. Cada perfil de segurança tem um domínio associado e é criado no nível do usuário ou no nível do grupo.

### Modificar as configurações de segurança de um serviço {#modify-security-settings-for-a-service}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de Serviços, clique no serviço a ser configurado.
1. Clique na guia Segurança.
1. Na lista Exigir Chamadores para Autenticação, selecione Sim ou Não para especificar se o serviço pode ser chamado com ou sem credenciais.

   Se você selecionar Sim, o chamador do serviço deverá ser autenticado e o usuário principal desse chamador deverá estar autorizado a chamar o serviço; caso contrário, a tentativa de invocação será recusada.

   Se você selecionar Não, o chamador do serviço poderá ou não ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização.

1. Para serviços que contêm uma ou mais operações sinalizadas para acesso anônimo, selecione ou desmarque Acesso Anônimo Permitido. Quando o acesso anônimo está ativado, qualquer usuário no sistema pode chamar operações no serviço. Se o acesso anônimo estiver desativado, os usuários deverão receber permissão para chamar o serviço e chamar as operações. Os usuários recebem essas permissões diretamente ou como parte de um grupo que as tem.
1. Para alguns serviços, a conta de usuário que executa a operação afeta os resultados. Por exemplo, nos Serviços de conteúdo (Obsoleto), o usuário que armazena conteúdo se torna o proprietário do conteúdo, o que afeta quem poderá acessá-lo posteriormente. Se você estiver usando um processo para armazenar conteúdo, pense em qual usuário será usado para executar o serviço de Gerenciamento de Documentos, pois esse usuário será o proprietário do conteúdo armazenado.

   Para especificar a identidade de runtime usada por um serviço para executar operações, selecione Especificar Executar Como, selecione uma opção na lista associada e, em seguida, clique em Salvar. Escolha entre as seguintes opções:

   **Chamador:** Usa a mesma identidade do usuário que chamou o serviço.

   **Sistema:** Usa o usuário Sistema para executar o serviço com privilégios totais.

   **Usuário nomeado:** Permite executar o serviço como um usuário específico. Ao selecionar essa opção, clique em Selecionar Usuário para exibir a página Selecionar Principal, onde você pode pesquisar e selecionar o usuário.

   Se você não selecionar Especificar executar como, o comportamento padrão será usado.

   >[!NOTE]
   >
   Os serviços de renderização e envio usados com as variáveis xfaForm, Document Form e Form são sempre executados usando a conta de usuário Sistema.

1. Clique em Adicionar Principal para especificar as permissões que os usuários e grupos têm para este serviço.
1. A tela Selecionar principal exibe os usuários e grupos configurados no Gerenciamento de usuários. Se o usuário ou grupo desejado não for exibido, use a função de pesquisa para localizá-lo. Clique em um nome de usuário ou de grupo.
1. Na tela Adicionar permissões, selecione as permissões a serem atribuídas ao usuário ou grupo para este serviço:

   * **INVOKE_PERM:** Para chamar todas as operações no serviço
   * **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço
   * **SUPERVISOR_PERM:** Para exibir dados da instância do processo para um serviço criado a partir de um processo
   * **START_STOP_PERM:** Para iniciar e parar um serviço
   * **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar endpoints de um serviço
   * **CREATE_VERSION_PERM:** Para criar uma versão do serviço
   * **DELETE_VERSION_PERM:** Para excluir uma versão do serviço
   * **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço
   * **READ_PERM:** Para exibir o serviço
   * **PROCESS_OWNER_PERM:** Para uso em uma versão futura de formulários AEM. Não use essa permissão.
   * **SERVICE_MANAGER_PERM:** Para uso em uma versão futura de formulários AEM. Não use essa permissão.
   * **SERVICE_AGENT_PERM:** Para uso em uma versão futura de formulários AEM. Não use essa permissão.

1. Clique em Adicionar.

### Remover o principal de um perfil de segurança {#remove-the-principal-from-a-security-profile}

1. Na página Gerenciamento de Serviços, selecione o serviço a ser configurado.
1. Clique em **Segurança** selecione o perfil de segurança a ser removido e clique em **Remover**.

## Configurando o pool de um serviço {#configuring-pooling-for-a-service}

Cada serviço pode aproveitar os recursos de pool para lidar com as solicitações de chamada recebidas. O uso de um pool de serviços garante que as instâncias de serviço sejam chamadas por um único thread por vez e reutilizadas em solicitações de chamada, o que pode resultar em melhor desempenho. Você também pode usar o pool para especificar a opção Máximo de Instâncias de Serviço Assíncronas, que permite que os serviços limitem o número de solicitações tratadas em paralelo.

### Ativar pooling {#enable-pooling}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de Serviços, clique no serviço a ser configurado.
1. Clique na guia Pooling (Pool).
1. Na lista Estratégia de processamento de solicitações, selecione Instâncias em pool para todas as solicitações.
1. Na caixa Tamanho do Pool da Instância do Serviço Inicial, informe o tamanho inicial do pool. Quando o serviço é disponibilizado, esse número é usado para determinar o número de instâncias de implementação de serviço criadas e alocadas para o pool livre, aguardando solicitações de chamada. Isso permite que o contêiner de serviço responda imediatamente às solicitações de invocação sem ter que primeiro inicializar uma instância de serviço.
1. Na caixa Tamanho Máximo do Pool de Instâncias do Serviço, informe o número máximo de instâncias no pool para um determinado serviço. Esta configuração controla o número de threads que podem executar um determinado serviço em um determinado momento. O valor padrão é 0, o que resulta no tamanho ilimitado do pool.
1. Na caixa Máximo de Instâncias de Serviço Assíncronas, informe o número máximo de instâncias do pool que podem ser usadas para atender a solicitações assíncronas a qualquer momento. Essa configuração permite que o serviço limite o número de solicitações que ele pode lidar em paralelo.
1. Na caixa Timeout de Espera de Chamada, informe o número de milissegundos para esperar que um serviço fique disponível para uma solicitação de chamada. Se você não especificar um valor para essa configuração, o padrão será 0, o que não resultará em tempo de espera.
1. Clique em Salvar.

### Remover pool {#remove-pooling}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de Serviços, clique no serviço a ser configurado.
1. Clique na guia Pooling (Pool).
1. Na lista Estratégia de processamento de solicitações, selecione Nova instância para cada solicitação ou Instância única para todas as solicitações.

   **Instância única para todas as solicitações:** Uma instância de serviço é criada e armazenada em cache quando a primeira solicitação entra no container. Cada solicitação após essa solicitação usa a mesma instância de serviço para lidar com a solicitação.

   **Nova instância para cada solicitação:** Uma nova instância de serviço é criada para cada chamada recebida.

1. Clique em Salvar.
