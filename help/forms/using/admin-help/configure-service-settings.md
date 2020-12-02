---
title: Definir configurações de serviço
seo-title: Definir configurações de serviço
description: Saiba como configurar as configurações do serviço.
seo-description: Saiba como configurar as configurações do serviço.
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '10710'
ht-degree: 0%

---


# Definir configurações de serviço {#configure-service-settings}

Você pode usar a página Gerenciamento de serviços para definir as configurações de cada um dos serviços que fazem parte dos formulários AEM. As configurações disponíveis variam dependendo do serviço que está sendo configurado.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Pare o serviço antes de alterá-lo. (Consulte [Iniciar e parar serviços](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Clique no nome do serviço que deseja configurar.
1. Se o serviço tiver uma guia Configuração, use-a para alterar as configurações do serviço. Consulte a lista de links abaixo para obter detalhes.

   >[!NOTE]
   >
   >Nem todos os serviços listados na página Gerenciamento de serviços têm uma guia Configuração. Para os processos criados, a guia Configuração será exibida somente se você tiver adicionado um parâmetro de configuração ao processo no Workbench. (Consulte &quot;Parâmetros de configuração&quot; na [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Clique na guia Segurança e defina as configurações de segurança do serviço. Consulte [Modificando configurações de segurança para um serviço](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Se o serviço tiver uma guia Pontos de extremidade, use-a para alterar as configurações do ponto de extremidade. Consulte [Gerenciando Endpoints](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Clique na guia Pooling e defina as configurações de pooling. Consulte [Configuração de pooling para um serviço](configure-service-settings.md#configuring-pooling-for-a-service).
1. Clique em Salvar para salvar as alterações ou clique em Cancelar para descartá-las.
1. Marque a caixa de seleção ao lado do nome do serviço e clique em Start para reiniciar o serviço.

## Configurações do serviço de Fluxo de Trabalho de Auditoria {#audit-workflow-service-settings}

O Workbench fornece a capacidade de registrar instâncias de processo conforme elas são executadas no tempo de execução e, em seguida, reproduzi-las para observar o comportamento do processo. (Consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Para conservar espaço no sistema de arquivos do servidor de formulários, é possível limitar a quantidade de dados de gravação do processo armazenados. Você pode configurar as seguintes propriedades do serviço Serviço de Fluxo de Trabalho de Auditoria ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** o número máximo de gravações que são armazenadas. Quando o número máximo é armazenado, a gravação mais antiga é removida do sistema de arquivos quando uma nova gravação é criada. Essa propriedade é útil se você tende a criar muitas gravações e deseja remover gravações antigas automaticamente. O valor padrão é 50.

**MaxNumberOfRecordingEntries:** O número máximo de entradas de dados que podem ser armazenadas para cada gravação. As entradas de dados são informações sobre operações no processo. Várias entradas são armazenadas para cada execução de uma operação, como se a operação foi iniciada, se a operação foi concluída e se a rota que leva à operação foi concluída. Essa propriedade é útil quando os processos podem incluir muitas execuções de operações, por exemplo, quando um loop sem fim é encontrado. O valor padrão é 50.

## configurações de serviço de formulários com códigos de barras {#barcoded-forms-service-settings}

O serviço de formulários com códigos de barras `(BarcodedFormsService)` extrai dados de códigos de barras de imagens digitalizadas. O serviço aceita um formulário com código de barras (TIFF ou PDF) como entrada e extrai a representação da máquina dos dados codificados pelo código de barras.

As configurações a seguir estão disponíveis para o serviço de formulários com códigos de barras.

**Ler à esquerda:** quando selecionadas, as imagens de códigos de barras são digitalizadas horizontalmente da direita para a esquerda.

**Ler à direita:** quando selecionadas, as imagens de códigos de barras são digitalizadas horizontalmente da esquerda para a direita.

**Leitura para cima:** quando selecionadas, as imagens de códigos de barras são digitalizadas verticalmente de baixo para cima.

**Ler para baixo:** quando selecionadas, as imagens de códigos de barras são digitalizadas verticalmente de cima para baixo.

>[!NOTE]
>
>Por padrão, todas as opções são selecionadas. Desmarque uma opção somente se tiver certeza de que nenhum código de barras aparecerá dessa forma em seus formulários.

**Caminho do arquivo básico:** o caminho do arquivo relativo ao qual os parâmetros de entrada e saída do lote para as operações Executar trabalho de arquivo XML e Executar trabalho de arquivo simples são resolvidos. Nas configurações clusterizadas, o caminho do arquivo base deve ser um local do sistema de arquivos compartilhado no qual todos os nós do cluster têm acesso de leitura/gravação.

**Nome da Fonte de Dados:** O nome da fonte de dados usada para manter informações de estado e histórico sobre trabalhos de processamento em lote. A fonte de dados especificada deve suportar transações globais (XA).

## Configurações do serviço Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

O serviço Central Migration Bridge ( `CentralMigrationBridge`) chama um subconjunto da funcionalidade Adobe Central Pro Output Server (Central), que inclui os comandos JFMERGE, JFTRANS e XMLIMPORT. As operações do serviço Central Migration Bridge permitem que você reutilize os seguintes ativos centrais em formulários AEM:

* design de modelo (&amp;ast;.ifd)
* modelos de saída (&amp;ast;.mdf)
* arquivos de dados (&amp;ast;.dat files)
* arquivos preâmbulo (&amp;ast;.pre files)
* arquivos de definição de dados (&amp;ast;.tdf)

A configuração a seguir está disponível para o serviço Central Migration Bridge.

**Diretório de instalação central:** o diretório onde o Adobe Central 5.7 está instalado.

## Configurações do serviço Content Repository Connector for EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

O Content Repository Connector for EMC Documentum Service ( `EMCDocumentumContentRepositoryConnector`) permite criar processos que interagem com o conteúdo armazenado em um repositório Documentum.

A configuração a seguir está disponível para o Content Repository Connector for EMC Documentum Service.

**Caminho padrão do objeto de link de ativo:** a parte padrão do caminho no repositório Documentum para armazenar o objeto de link de ativo. O caminho real consiste no caminho padrão e no local do modelo de formulário no repositório de formulários AEM.

Por exemplo, se o caminho padrão estiver definido como `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` e o modelo de formulário estiver armazenado em uma pasta `/Docbase/forms/`, o objeto Link de ativo será armazenado no seguinte local:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

O valor padrão dessa configuração é `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Configurações do serviço Content Repository Connector for IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

O Content Repository Connector for IBM FileNet permite que você crie processos que interagem com o conteúdo armazenado em um repositório IBM FileNet.

A seguinte configuração está disponível para o Content Repository Connector para o serviço IBM FileNet.

**Caminho padrão do objeto de link de ativo:** a parte padrão do caminho no repositório IBM FileNet para armazenar o objeto Asset Link. O caminho real consiste no caminho padrão e no local do modelo de formulário no repositório de formulários AEM.

Por exemplo, se o caminho padrão estiver definido como `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` e o modelo de formulário estiver armazenado em uma pasta `/Docbase/forms/`, o objeto Link de ativo será armazenado no seguinte local:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

O valor padrão dessa configuração é `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Converter configurações do serviço PDF {#convert-pdf-service-settings}

O serviço Convert PDF ( `ConvertPdfService`) converte documentos PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para a impressão automática baseada em servidor em qualquer impressora PostScript. A conversão de um documento PDF em um arquivo TIFF de várias páginas é prática ao arquivar documentos em sistemas de gestão de conteúdo que não suportam documentos PDF.

As configurações a seguir estão disponíveis para o serviço Converter PDF.

**Tipo de Transação:** Especifica como um contexto de transação deve ser propagado para uma operação.

**Obrigatório:** Suporta um contexto de transação se existir; caso contrário, um novo contexto de transação será criado. Esse é o valor padrão.

**Requer Novo:** sempre cria um novo contexto de transação. Se houver um contexto de transação ativo, ele será suspenso.

**Tempo Limite da Transação (em segundos):** O número de segundos que o provedor de transação subjacente deve aguardar antes de reverter uma transação que está vinculando esta operação. Esse valor será ignorado se um contexto de transação existente for propagado. O valor padrão é 180.

**Resolução de limite para suavização (em dpi):** A resolução de imagem abaixo da qual a suavização (ou suavização de borda) é aplicada ao texto, arte de linha e imagens, se você selecionou as opções &quot;Aplicar suavização a&quot; para esses elementos.

**Aplicar suavização ao texto:** Controla a suavização de borda do texto. Para desativar a suavização do texto e tornar o texto mais nítido e mais fácil de ler com um ampliador de tela, desmarque essa caixa de seleção.

**Aplicar suavização a LineArt:** Aplica suavização para remover ângulos abruptos em linhas.

**Aplicar suavização a imagens:** Aplica suavização para minimizar alterações abruptas em imagens.

## Configurações do serviço Distiller {#distiller-service-settings}

O serviço Distiller ( `DistillerService`) converte arquivos PostScript, Encapsulated PostScript (EPS) e PRN em arquivos PDF em uma rede.

As configurações a seguir estão disponíveis para o serviço Distiller.

**Configurações do Adobe PDF:** as seguintes configurações predefinidas são aplicadas ao PDF gerado:

* Impressão de alta qualidade
* Páginas superdimensionadas
* CMYK do PDFA1b 2005
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* Qualidade da imprensa
* Menor tamanho de arquivo
* Padrão

Novas configurações podem ser criadas pela interface do usuário do Gerador de PDF.

**Configurações de segurança:configurações de segurança** pré-definidas aplicadas a documentos PDF gerados. O valor padrão é Sem segurança. Você deve criar configurações de segurança usando o Gerador de PDF e inserir a configuração aqui.

**Tamanho do pool:** o tamanho inicial do pool. Quando o serviço Distiller é implantado, esse número é usado para determinar o número de instâncias de implementação do serviço que são criadas e alocadas ao pool gratuito aguardando solicitações de invocação. O container de serviço pode responder imediatamente às solicitações de invocação sem precisar primeiro inicializar uma instância de serviço.

## Configurações do serviço Gerenciamento de documentos {#document-management-service-settings}

>[!NOTE]
>
>O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gestão de conteúdo instalado com o LiveCycle. Ela permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto do Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Para saber mais sobre como configurar o Content Services (obsoleto), consulte [Administração do Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

O serviço de Gerenciamento de Documentos ( `DocumentManagementService`) permite que os processos usem a funcionalidade de gestão de conteúdo fornecida pelo Content Services (obsoleto). As operações de Gerenciamento de documentos fornecem tarefas básicas necessárias para manter espaços e conteúdo no sistema de gestões de conteúdo. Exemplos dessas tarefas são copiar, excluir, mover, recuperar e armazenar conteúdo, criar espaços e associações e obter e definir atributos de conteúdo.

As configurações a seguir estão disponíveis para o serviço Gerenciamento de Documentos.

**Esquema de armazenamento:** O esquema da loja na qual o conteúdo está localizado. O valor padrão é espaço de trabalho.

**Porta HTTP:** a porta usada para acessar o Content Services (obsoleto). O valor padrão é 8080.

## Configurações do serviço de email {#email-service-settings}

O e-mail normalmente é usado para distribuir conteúdo ou fornecer informações de status como parte de um processo automatizado. O serviço de E-mail ( `EmailService`) permite que os processos recebam mensagens de e-mail de um servidor POP3 ou IMAP e enviem mensagens de e-mail para um servidor SMTP.

Por exemplo, um processo usa o serviço Email para enviar uma mensagem de email com um anexo de formulário PDF. O serviço Email se conecta a um servidor SMTP para enviar a mensagem de email com o anexo. O formulário PDF foi projetado para permitir que o recipient clique em Enviar depois de preencher o formulário. A ação faz com que o formulário seja retornado como um anexo para o servidor de email designado. O serviço Email recupera a mensagem de email retornada e armazena o formulário preenchido em uma variável de formulário de dados de processo.

As configurações a seguir estão disponíveis para o serviço Email.

**Host SMTP:** o endereço IP ou URL do servidor SMTP a ser usado para enviar e-mail.

**Número da porta SMTP:** a porta usada para conexão com o servidor SMTP.

**Autenticação SMTP:** selecione se a autenticação do usuário é necessária para se conectar ao servidor SMTP.

**Usuário SMTP:** o nome de usuário da conta de usuário a ser usada para fazer logon no servidor SMTP.

**Senha SMTP:** a senha associada à conta de usuário SMTP.

**Segurança de Transporte SMTP:** O protocolo de segurança a ser usado para conexão com o servidor SMTP:

* Selecione Nenhum se nenhum protocolo for usado (os dados são enviados em texto claro)
* Selecione SSL se o protocolo Secure Sockets Layer for usado.
* Selecione TLS se Transport Layer Security for usado.

**Host POP3/IMAP:** o endereço IP ou URL do servidor POP3 ou IMAP a ser usado para enviar emails.

**Nome de usuário POP3/IMAP:** O nome de usuário da conta de usuário a ser usada para fazer logon no servidor POP3 ou IMAP.

**Senha POP3/IMAP:** A senha associada à conta de usuário POP3 ou IMAP.

**Número da porta POP3/IMAP:** a porta usada para conexão com o servidor POP3 ou IMAP.

**POP3/IMAP:** o protocolo a ser usado para enviar e receber e-mails.

**Segurança de Transporte de Recebimento:** O protocolo de segurança a ser usado para conexão com o servidor SMTP:

* Selecione Nenhum se nenhum protocolo for usado (os dados são enviados em texto limpo).
* Selecione SSL se o protocolo Secure Sockets Layer for usado.
* Selecione TLS se Transport Layer Security for usado.

## Configurações do serviço de criptografia {#encryption-service-settings}

O serviço de criptografia ( `EncryptionService`) permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificá-la antes que o documento possa ser visualizado no Adobe Reader ou Adobe Acrobat. Da mesma forma, se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com a chave pública que corresponde ao certificado (chave privada) que foi usado para criptografar o documento PDF.

As configurações a seguir estão disponíveis para o serviço de Criptografia.

**Servidor LDAP padrão ao qual se conectar:Nome do** host do servidor LDAP usado para recuperar certificados de criptografia de documento.

**Porta LDAP padrão para conexão:número da** porta do servidor LDAP.

**Nome de usuário LDAP padrão:** se o servidor LDAP exigir autenticação, especifique o nome de usuário a ser usado para conexão com o servidor LDAP.

**Senha LDAP padrão:** se o servidor LDAP exigir autenticação, especifique a senha que corresponde ao nome de usuário a ser usado para conexão com o servidor LDAP.

>[!NOTE]
>
>Use autenticação simples (nome de usuário e senha) somente quando a conexão estiver protegida via SSL (usando LDAPS).

**Modo de compatibilidade:**

## Configurações do serviço FTP {#ftp-service-settings}

O serviço FTP ( `FTP`) permite que os processos interajam com um servidor FTP. As operações do serviço FTP podem recuperar arquivos do servidor FTP, colocar arquivos no servidor FTP e excluir arquivos do servidor FTP. Por exemplo, documentos como relatórios gerados a partir de um processo podem ser armazenados em um servidor FTP para distribuição. Ou um sistema externo pode gerar alguns arquivos com base em etapas anteriores em um processo. Em uma etapa subsequente do processo, os arquivos podem ser transferidos para um local remoto.

As configurações a seguir estão disponíveis para o serviço FTP.

**Host padrão:** o endereço IP ou URL do servidor FTP.

**Porta padrão:** a porta usada para se conectar ao servidor FTP. O valor padrão é 21.

**Nome de usuário padrão:** o nome da conta de usuário que você pode usar para acessar o servidor FTP. A conta de usuário deve ter privilégios suficientes para executar as operações FTP necessárias para esse serviço.

**Senha padrão:** A senha a ser usada com o nome de usuário especificado para autenticação no servidor FTP.

## Gerar configurações do serviço PDF {#generate-pdf-service-settings}

O serviço Gerar PDF ( `GeneratePDFService`) converte arquivos em vários formatos nativos em documentos PDF e converte documentos PDF em vários formatos de arquivo.

As configurações a seguir estão disponíveis para o serviço Gerar PDF.

**Configurações do Adobe PDF:** o nome das configurações pré-definidas do Adobe PDF a serem aplicadas a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações do Adobe PDF são definidas no console de administração, clicando em Serviços > Gerador de PDF > Configurações do Adobe PDF. Essas configurações são aplicáveis somente às conversões baseadas no PDFMaker.

**Configurações de segurança:** o nome das configurações de segurança pré-definidas a serem aplicadas a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações de segurança são definidas no console de administração, clicando em Serviços > Gerador de PDF> Configurações de segurança.

**Configurações de tipo de arquivo:** O nome da Configuração de tipo de arquivo pré-configurada a ser aplicada a um trabalho de conversão, se essas configurações não forem especificadas como parte dos parâmetros de invocação da API. As configurações de tipo de arquivo são definidas no console de administração, clicando em Serviços > Gerador de PDF> Configurações de tipo de arquivo.

**Usar o Acrobat WebCapture (somente Windows):** quando essa configuração for verdadeira, o serviço Gerar PDF usará o Acrobat X Pro para todas as conversões de HTML em PDF. Isso pode melhorar a qualidade dos arquivos PDF produzidos a partir de HTML, embora o desempenho possa ser um pouco menor. O valor padrão é false.

**Usar a conversão de imagem do Acrobat (somente Windows):** quando essa configuração for verdadeira, o serviço Gerar PDF usará o Acrobat X Pro para todas as conversões de imagem em PDF. Essa configuração é útil somente se o mecanismo de conversão Java puro padrão não conseguir converter uma proporção significativa das imagens de entrada com êxito. O valor padrão é false.

**Ativar conversões do AutoCAD baseadas em Acrobat (somente Windows):** Quando essa configuração for verdadeira, o serviço Gerar PDF usará o Acrobat X Pro para todas as conversões do DWG em PDF. Essa configuração é útil somente se o AutoCAD não estiver instalado no servidor ou se o mecanismo de conversão do AutoCAD não conseguir converter arquivos com êxito.

**Expressões Regulares Para Descobrir Caracteres Especiais Proibidos Em Nome De Usuário (Somente Windows):** Especifica Caracteres que interferem nas operações de Export PDF e Optimize PDF quando os caracteres aparecem no nome de um usuário.

**Tamanho do pool ImageToPDF:** O tamanho do pool do conversor padrão (Java puro) Imagem para PDF no serviço Gerar PDF. Essa configuração controla o máximo de conversões simultâneas de Imagem para PDF que o serviço Gerar PDF pode executar. O valor padrão dessa configuração (recomendado para sistemas de processador único) é 3, que pode ser aumentado em sistemas de vários processadores.

**Tamanho do pool de HTML para PDF:** O tamanho do pool do conversor de HTML para PDF no serviço Gerar PDF. Essa configuração controla o máximo de conversões simultâneas de HTML para PDF que o serviço Gerar PDF pode executar. O valor padrão dessa configuração (recomendado para sistemas de processador único) é 3, que pode ser aumentado em sistemas de vários processadores.

**Tamanho do pool de OCR:** O tamanho do pool do PaperCaptureService que o Gerador de PDF usa para OCR. O valor padrão dessa configuração (recomendado para sistemas de processador único) é 3, que pode ser aumentado em sistemas de vários processadores. Esta configuração é válida somente em sistemas Windows.

**Família de fontes de fallback para conversões de HTML em PDF:** o nome da família de fontes a ser usada em documentos PDF quando a fonte usada no HTML original não estiver disponível para o servidor de formulários AEM. Especifique uma família de fontes se você espera converter páginas HTML que usam fontes indisponíveis. Por exemplo, as páginas criadas em idiomas regionais podem usar fontes indisponíveis.

**A lógica de repetição para** conversões nativas governa as tentativas de geração de PDF se a primeira tentativa de conversão falhar:

**Nenhuma tentativa**

Não tente a conversão do PDF novamente se a primeira tentativa de conversão falhar

**Tentar novamente**

Repita a conversão do PDF independentemente de o limite de tempo limite ter sido atingido. A duração padrão do tempo limite para a primeira tentativa é 270s.

**Tentar novamente se o tempo permitir**

Tente novamente a conversão do PDF se o tempo consumido para a primeira tentativa de conversão for menor que a duração do tempo limite especificada. Por exemplo, se a duração do tempo limite for 270s e a primeira tentativa consumida 200s, o Gerador de PDF tentará novamente a conversão. Se a primeira tentativa consumiu 270, a conversão não será repetida.

## Guia as configurações do serviço Utilitários ES4 {#guides-es4-utilities-service-settings}

Quando você cria um Guia, alguns recursos, como a definição do Guia, são incorporados ao Guia. Os recursos também podem existir como referências aos ativos do aplicativo armazenados localmente ou no servidor de formulários AEM. O Guia não contém dados e os valores para o local de envio e as entradas não são adequados para todos os ambientes externos.

Na maioria dos casos, os serviços de renderização dos Guias padrão são suficientes para preparar um Guia para uso no Workspace ou em outros ambientes externos. (Na visualização Serviços, no Workbench, o serviço padrão é Guias (sistema)/Processos/Guia de Renderização - 1.0.) O serviço Utilitários do Guia ( `GuidesUtility`) permite que você crie um processo personalizado para renderizar um Guia, se necessário.

As operações de Utilitários do Guia permitem que você adicione as seguintes tarefas de renderização do Guia a um processo:

* Determine se os dados estão disponíveis para preencher o Guia com
* Incorporar os dados do Guia ou convertê-los em um link
* Converter o conteúdo referenciado em URLs acessíveis externamente
* Substitua os valores em um documento HTML ou em outro invólucro, ou converta-os em URLs acessíveis externamente
* Definir o local de envio
* Especificar valores de entrada
* Criar um parâmetro para representar o conteúdo referenciado
* Se houver variações disponíveis, defina uma variação

Os valores padrão para o serviço Utilitários do Guia suportam a maioria dos casos de uso. No entanto, se necessário, é possível alterar os seguintes valores.

**publicPaths:** Esta opção foi descontinuada. Não use essa opção com formulários AEM.

**pathInfoExpiryInSeconds:** O intervalo após o qual uma solicitação de informações de caminho de um cliente expira. O padrão é 1.

**collateralExpiryInSeconds:** O intervalo após o qual uma solicitação de garantia de um cliente expira. O padrão é 315576000.

**mismatchExpiryInSeconds:** O intervalo após o qual uma solicitação de garantia de um cliente expira, quando a eTag (tag de entidade) não corresponde. (Uma eTag é um cabeçalho de resposta HTTP.) O padrão é 1.

**guideContext:** A raiz de contexto do aplicativo da Web Guias. Corresponde ao valor definido usando o aplicativo da Web Guias. O padrão é /Guides/.

**secureRandomAlgorithm:** O algoritmo a ser usado ao gerar chaves e identificadores. Esse valor é passado para o método getInstance da classe Java SecureRandom. O padrão é SHA1PRNG.

**idBytes:** O número de bytes aleatórios a serem usados para um identificador de chave. O padrão é 6.

**macAlgorithm:** O algoritmo MAC (message authentication code) a ser usado para verificação de URL de garantia. Esse método é passado para o método getInstance da classe Mac. O padrão é HmacSHA1.

**macRefreshIntervalInMinutos:** A quantidade de tempo que uma chave está ativa. Quando uma chave está ativa para esse intervalo, uma nova chave é gerada. A nova chave se torna a chave ativa. A chave ativa anteriormente é mantida por 10% do intervalo de atualização. Esse comportamento permite que URLs gerados usando a chave antiga continuem funcionando no switch de chave. O padrão é 144000.

**macOverlapIntervalInMinutos:** Duração do tempo em que a chave anterior permanecerá válida depois que uma nova for gerada. O padrão é 1440 minutos (1 dia).

**macKeySeed:** Um valor semente para gerar o URL seguro. Quando essa é a opção, a chave nunca é atualizada. A configuração da mesma semente em diferentes servidores resultará na geração de URLs seguros compatíveis. Isso pode ser útil se vários servidores de formulários estiverem em uso atrás de um balanceador de carga. Insira uma sequência aleatória de caracteres e números como a semente.

### Usando guias em um cluster de servidor {#using-guides-in-a-server-cluster}

A renderização de um Guia em um cluster de servidor que não usa sessões adesivas falha com um NullPointerException. Uma solicitação de Guias aproveita URLs protegidos que, por padrão, são exclusivos ao servidor em que são gerados. Em um cluster que usa sessões aderentes, depois que uma solicitação atinge um nó no cluster, todas as solicitações subsequentes para essa sessão ou usuário são roteadas exclusivamente para esse servidor e tudo está bem. Em um cluster que não usa sessões aderentes, as solicitações subsequentes podem atingir qualquer servidor no cluster. Se o servidor que as solicitações acessaram não for o original, ele não conseguirá resolver o URL seguro.

Se você estiver usando Guias em um cluster de servidores que não usa sessões adesivas, defina o valor macKeySeed para o serviço GuidesUtility e pare e start o cluster.

O valor macKeySeed é a semente do gerador de números aleatórios usado para gerar os URLs seguros. Definir esse valor faz com que cada nó de cluster inicialize o gerador de números aleatórios da mesma maneira e tenha acesso aos mesmos URLs protegidos. Você pode usar qualquer string aleatória para esse valor semente.

Altere o valor macKeySeed quando precisar atualizar os URLs protegidos. Atualizar os URLs protegidos depende da sua política de segurança e é semelhante à política de atualização para alterar a senha raiz principal do servidor. O macSeedValue é análogo à senha principal para os URLs seguros, pois é usado para gerar um novo número aleatório exclusivo para uso na geração e recuperação seguras de URLs.

É necessário reiniciar o cluster porque macSeedValue é somente leitura na inicialização do sistema. Todos os nós precisam reiniciar para ler o valor, pois eles o usam independentemente para inicializar seus números aleatórios internos com o valor semente.

## Definições do serviço JDBC {#jdbc-service-settings}

O serviço JDBC ( `JdbcService`) permite que os processos interajam com bancos de dados.

A seguinte configuração está disponível para o serviço JDBC.

**datasourceName:** Um valor de string que representa o nome JNDI da fonte de dados a ser usada para conectar-se ao servidor de banco de dados. A fonte de dados deve ser definida no servidor de aplicativos que hospeda o servidor de formulários. O valor padrão é o nome JNDI da fonte de dados para o banco de dados de formulários AEM.

## Definições do serviço JMS {#jms-service-settings}

O serviço JMS ( `JMS`) permite a interação com provedores do Java Messaging System (JMS) que implementam mensagens ponto a ponto e publicam/assinam mensagens.

Configure o serviço JMS com as propriedades padrão para que as operações de serviço possam se conectar e interagir com um provedor JMS e um serviço JNDI associado. Os valores das propriedades do serviço são definidos como valores padrão com base no JBoss Application Server. Altere esses valores se estiver usando um servidor de aplicativos diferente para hospedar formulários AEM.

As configurações a seguir estão disponíveis para o serviço JMS.

**URL do provedor:** o URL do provedor de serviço JNDI. O valor padrão é baseado no JBoss Application Server. O URL a seguir são valores padrão para os servidores de aplicativos que AEM formulários oferecem suporte:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nome de usuário JNDI:** o nome de usuário da conta a ser usada para autenticação com o provedor de serviço JNDI usado para procurar nomes de fila e tópicos. O valor padrão é convidado.

**Senha JNDI:** a senha associada ao nome de usuário especificado para JNDI Username. O valor padrão é convidado.

**Fábrica de contexto inicial:** a classe Java a ser usada como a fábrica de contexto inicial. O serviço JMS usa essa classe para criar um contexto inicial, que é o ponto de partida para resolver nomes de tópicos e filas. O valor padrão é a fábrica de contexto inicial para o serviço JMS no JBoss. As seguintes classes são as fábricas de contexto iniciais para os servidores de aplicativos que AEM formulários oferecem suporte:

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.webphere.naming.WsnInitialContextFactory

**Nome de usuário da conexão:** a senha associada ao nome de usuário especificado para Nome de usuário da conexão. O valor padrão é convidado.

**Senha da conexão:** a senha associada ao nome de usuário especificado para o Nome de usuário da conexão. O valor padrão é convidado.

**Outras propriedades: nome da** propriedade e pares de valores que você pode passar para o provedor de serviço JNDI. Essas propriedades dependem da implementação e configuração do provedor que você está usando.

Os pares de nome e valor da propriedade são separados por ponto-e-vírgula **;**. Por exemplo, o texto a seguir mostra o valor que seria especificado para duas propriedades chamadas name1 e name2, com valores value1 e value2, respectivamente:

`name1=value1;name2=value2`

## Configurações do serviço LDAP {#ldap-service-settings}

O serviço LDAP ( `LDAPService`) fornece operações para consultar diretórios LDAP. Geralmente, os diretórios LDAP são usados para armazenar informações sobre pessoas, grupos e serviços em uma organização.

As configurações a seguir estão disponíveis para o serviço LDAP.

**Fábrica de contexto inicial:** a classe Java a ser usada como a fábrica de contexto. Essa classe é usada para criar uma conexão com o servidor LDAP. O valor padrão é com.sun.jndi.ldap.LdapCtxFactory, que é apropriado para a maioria dos servidores LDAP.

**URL do provedor:** o URL a ser usado para conexão com o serviço LDAP. O formato do valor é `ldap://server name:port`

*nome do servidor* é o nome do computador que hospeda o servidor LDAP

*porta* a porta de comunicação que o serviço LDAP usa. O valor padrão é 389, que é a porta padrão usada para conexões LDAP.

**Nome do usuário:** o nome de usuário da conta de usuário a ser usada para fazer logon no servidor LDAP. A conta de usuário precisa ter permissão para se conectar ao servidor e ler as informações no diretório LDAP.

Dependendo do servidor LDAP, o nome de usuário pode ser um nome de usuário simples, como `myname` ou um DN, como `cn=myname,cn=users,dc=myorg`.

**Senha:** A senha que corresponde ao nome de usuário fornecido para a configuração Nome de usuário.

**Outras propriedades:** Um valor de string que representa outras propriedades e seus valores correspondentes que você pode fornecer ao servidor LDAP. O valor está no seguinte formato:

`property=value;property=value;...`

## Definições do serviço de configuração do Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

O serviço de configuração do Microsoft SharePoint `(MSSharePointConfigService)`permite especificar credenciais para o usuário de formulários AEM que tem permissões de representação. Para obter informações sobre permissões de representação, consulte [Configuração do Conector para Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

As seguintes configurações estão disponíveis para o serviço de configuração do Microsoft SharePoint:

* Nome de usuário para um usuário com permissões de representação
* Senha do usuário acima

**Ativar SSL (HTTPS):**

**Tempo de ativação:** duração, em segundos, de validade e cache deste perfil de provisionamento no cliente. O padrão é 86400 (24 horas). Quando um aplicativo cliente sincroniza com o servidor e o tempo especificado passou, o aplicativo cliente solicita um novo perfil de provisionamento do servidor.

**Criptografia:** especifica se os dados armazenados no dispositivo móvel devem ser criptografados.

**Aplicativo Forms:** habilita o recurso Forms nos aplicativos clientes móveis. Quando essa opção é selecionada, os usuários podem abrir formulários e iniciar processos a partir de seus dispositivos móveis.

**Aplicativo Tarefa:** habilita o recurso Tarefa nos aplicativos clientes móveis. Quando essa opção é selecionada, os usuários podem acessar suas listas de tarefa e concluir tarefas de seus dispositivos móveis.

**Aplicativo Content Services:** habilita o recurso Content Services no aplicativo cliente móvel. Esse recurso está disponível somente para iOS. Quando essa opção é selecionada, os usuários do iPhone e do iPad podem acessar arquivos armazenados no servidor WebDAV de sua organização.

**Suporte offline:** permite que os usuários continuem usando os aplicativos clientes móveis mesmo quando não tiverem uma conexão com o servidor (por exemplo, quando estiverem fora do intervalo de células ou no modo de avião). Os usuários também devem ativar a configuração de suporte offline em seus dispositivos móveis. Esse recurso está disponível para dispositivos Android e iOS. Por padrão, esse recurso está desativado.

>[!NOTE]
>
>Se o suporte offline tiver sido ativado e você o desativar, os perfis de provisionamento dos usuários serão atualizados imediatamente ou assim que estiverem online. Se um usuário estiver trabalhando offline, todas as tarefas pendentes serão retornadas à lista do Tarefa e todos os itens em sua Fila, incluindo formulários pendentes, tarefas e formulários contendo erros de validação, serão excluídos da Fila.

**Android:** permite que dispositivos Android se conectem ao servidor.

**Apple iOS:** permite que iPhones e iPads se conectem ao servidor.

**AIR:** permite que dispositivos que executam aplicativos baseados na Adobe AIR® se conectem ao servidor.

**BlackBerry:** permite que dispositivos BlackBerry se conectem ao servidor.

**Android Microsoft Exchange AtiveSync Obrigatório:** Especifica se o Microsoft Exchange AtiveSync Policy Manager (EA) deve estar instalado e ativo em dispositivos Android. Quando essa opção é selecionada, EA deve ser imposta no dispositivo Android. Quando essa opção não está selecionada, nenhuma verificação é executada, embora outros requisitos ainda sejam aplicados.

**Comprimento mínimo do PIN no Android: os dispositivos** Android devem ter uma configuração global que imponha que o PIN ou a senha tenha pelo menos esse comprimento. Simplesmente ter um PIN com o comprimento especificado não é suficiente. A duração do PIN deve ser imposta pelo sistema para que os usuários não possam remover ou encurtar o PIN posteriormente. O valor padrão é 4.

**Tentativas máximas de senha do Android antes de limpar:dispositivos** Android têm uma configuração global que apaga o sistema após um número especificado de tentativas de senha inválida. Essa configuração global foi ativada e é igual ou inferior ao valor especificado aqui. O valor padrão é 5.

**Remoção de limpeza do Android:** especifica o que acontece quando uma violação de política ocorre em um dispositivo Android. Quando essa opção é selecionada, a conta é excluída. Quando essa opção não está selecionada, a senha da conta armazenada e os dados em cache são excluídos. Não são feitas mais tentativas de sincronização até que o usuário corrija a violação de política.

## Configurações do serviço de saída {#output-service-settings}

O serviço de Saída `(OutputService)`permite unir dados de formulário XML a um design de formulário criado AEM Designer de formulários para criar um fluxo de saída de documento em um dos seguintes formatos:

* Um fluxo de saída de documento PDF ou PDF/A.
* Um fluxo de saída do Adobe PostScript.
* Um fluxo de saída PCL (Printer Control Language).
* Um fluxo de saída ZPL (Zebra Programming Language).

O fluxo de saída pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo de disco. Quando você usa o serviço de Saída como parte de um processo, também pode enviar o fluxo de saída para um recipient de email como um anexo de arquivo.

As configurações a seguir estão disponíveis para o serviço de Saída.

**Tipo de Transação:** Especifica como um contexto de transação deve ser propagado para uma operação:

**Obrigatório:** suporta um contexto de transação se já existir; caso contrário, um novo contexto de transação será criado. Esse é o valor padrão.

**Requer Novo:** sempre cria um novo contexto de transação. Se houver um contexto de transação ativo, ele será suspenso.

**Tempo Limite da Transação (em segundos):** O número de segundos que o provedor de transação subjacente aguarda antes de reverter uma transação que está vinculando esta operação. Esse valor será ignorado se um contexto de transação existente for propagado.

Ao processar arquivos de dados grandes ou operar em um servidor ocupado, pode ser necessário aumentar o tempo limite do serviço de Saída. Para alterar o valor de tempo limite, verifique se os servidores de hardware têm memória adequada e se a memória está disponível para o heap do Java Application Server. O valor padrão é `180`.

## Configurações do serviço de configuração PDFG {#pdfg-config-service-settings}

As configurações a seguir estão disponíveis para o serviço de configuração PDFG ( `PDFGConfigService`).

**Diretório de opções de trabalho do usuário:** o caminho da pasta do sistema de arquivos onde o serviço c grava os arquivos de opções de trabalho acessíveis ao Acrobat Pro Extended. O valor padrão é [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**Diretório de inicialização do PS:** o caminho da pasta do sistema de arquivos onde os arquivos de inicialização exigidos pelo Adobe Acrobat Distiller são salvos. O valor padrão é [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**Arquivo de inicialização do PS:** o nome do arquivo de inicialização exigido pelo Adobe Acrobat Distiller. O valor padrão é example.ps.

**Tempo limite de conversão de servidor:** o tempo limite máximo de conversão de trabalho (em segundos) para o serviço Gerar PDF e o serviço Distiller. Essa configuração limita o tempo limite máximo de conversão que pode ser especificado no arquivo config.xml e nas páginas do console de administração do Gerador de PDF. O valor padrão é 270.

**Tempo limite global do servidor:** durante a execução de conversões de PDF, um servidor de formulários leva em conta o limite de tempo limite. Configure o valor de tempo limite para resolver o problema.

**Prefixo de opções de trabalho:** Um prefixo usado pelo serviço Gerar PDF para anexar uma sequência curta aos arquivos de opções de trabalho criados temporariamente para uso pela Acrobat Distiller. O valor padrão é pdfg.

**Aplicativos não Unicode:** uma lista separada por vírgulas de nomes de aplicativos que são conhecidos por serem incapazes de Unicode. Essa lista é pré-preenchida com os nomes de vários aplicativos, cujo suporte é pré-configurado no Gerador de PDF. Se você optar por adicionar suporte para conversões de PDF por meio de outros aplicativos de terceiros que não sejam compatíveis com o Unicode, será necessário adicioná-los a essa lista. O valor padrão é Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**Contagem de Threadpool de servidores:** controla o tamanho do pool de threads que o serviço Gerar PDF usa internamente para atender solicitações de conversão de HTML em PDF que envolvem spidering (conversão de páginas vinculadas acessíveis a partir da página principal). O valor padrão é 20.

**Segundos de verificação da limpeza do PDFG:** consulte a seção Segundos de expiração de trabalho para obter detalhes.

**Segundos de expiração de tarefa:** o serviço Gerar PDF exclui arquivos de entrada assim que eles são convertidos. Ele armazena arquivos de saída temporariamente, por um período determinado pelas configurações de Segundos de verificação da limpeza do PDFG e Segundos de expiração do trabalho.

A configuração Segundos de expiração de tarefa especifica a idade de um arquivo ou de uma pasta vazia antes de ser elegível para exclusão. A configuração Segundos de verificação da limpeza do PDFG especifica a frequência com que um thread de limpeza verifica as pastas temporárias em busca de arquivos que podem ser excluídos.

Por exemplo, se a opção Segundos de expiração do trabalho estiver definida como 100 e os Segundos de verificação da limpeza PDFG estiverem definidos como 200, o thread de limpeza será executado a cada 200 segundos e excluirá arquivos que tenham 100 segundos ou mais.

O valor padrão dos segundos de verificação da limpeza do PDFG é `43200` (12 horas). O valor padrão de Segundos de Expiração do Trabalho é `86400` (24 horas).

**Local padrão:** usado para substituir a localidade padrão (país + idioma) do servidor em que o serviço Gerar PDF é implantado. Se esse parâmetro não for especificado, a localidade padrão será determinada a partir do sistema operacional no qual o serviço é implantado. Esse parâmetro controla o idioma no qual as mensagens de erro são retornadas às APIs.

## configurações do serviço de Serviços de Dados do fluxo de trabalho de formulários {#forms-workflow-data-services-service-settings}

Os seguintes serviços estendem os Serviços de Dados e expõem os montadores que o Workspace usa para conversar com o servidor. Não altere as opções de configuração desses serviços, a menos que seja instruído a fazê-lo pelo Suporte ao Adobe. Estes serviços não se destinam ao acesso direto:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Remoção das configurações de serviço {#remoting-service-settings}

A maioria dos serviços é configurada para que você possa acessá-los por meio de (obsoleto para formulários AEM) AEM Remota de formulários. Para obter informações sobre (Obsoleto para formulários AEM) AEM Remoção de formulários, consulte [Programação com formulários AEM](https://adobe.com/go/learn_aemforms_programming_63).

As configurações a seguir estão disponíveis para o serviço Remoting.

**Método de Autenticação do Cliente Flex:** Determina o tipo de resposta que o servidor envia para o cliente quando o serviço chamado está habilitado para segurança, a operação invocada não suporta invocações anônimas e o cliente transmite nenhuma credenciais ou inválidas. Escolha entre Personalizado ou Básico. O valor padrão é Básico.

**Permitir serialização de classes não serializáveis:** A maioria dos pontos finais de formulários AEM permite que somente classes serializáveis sejam usadas para invocação. Em versões anteriores, o terminal Remoting permitia que classes não serializáveis fossem usadas para invocação de clientes baseados em Flex. Para evitar uma vulnerabilidade de segurança descrita em APS11-15, isso foi alterado. Se você quiser continuar usando classes não serializáveis com o ponto de extremidade Flex Remoting, marque essa caixa de seleção.

## Configurações do serviço de repositório {#repository-service-settings}

O serviço Repositório ( `RepositoryService`) fornece armazenamento de recursos e serviços de gerenciamento para AEM formulários. Quando os desenvolvedores criam um aplicativo, eles podem implantar os ativos no repositório em vez de em um sistema de arquivos. Os ativos podem incluir qualquer tipo de material de apoio, incluindo formulários XML, PDF forms (incluindo formulários Acrobat), fragmentos de formulário, imagens, perfis, políticas, arquivos SWF, arquivos DX, schemas XML, arquivos WSDL e dados de teste.

Você pode usar o repositório padrão incluído nos formulários AEM ou usar um repositório de terceiros (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager).

O serviço Provedor de Repositório é um delegado de serviço que atua como a interface para um serviço de provedor. Isso permite que você se conecte a uma API comum e não precisa estar ciente de qual serviço de provedor está implementando os recursos do armazenamento. O serviço Provedor de repositório fornece armazenamento de banco de dados para os recursos do serviço de Repositório.

A configuração a seguir está disponível para o serviço Repositório.

**Serviço de provedor:** o nome do serviço usado como provedor de armazenamentos. O valor padrão é RepositoryProviderService.

## Configurações do serviço de assinatura {#signature-service-settings}

O serviço de assinatura ( `SignatureService`) permite que sua organização proteja a segurança e a privacidade dos documentos Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que os documentos não sejam alterados. Alterar um documento quebra sua assinatura. Dado que os elementos de segurança são aplicados ao próprio documento, este permanece seguro e controlado durante todo o seu ciclo de vida; além do firewall, quando é baixado offline e quando é enviado de volta à sua organização.

As configurações a seguir estão disponíveis para o serviço de assinatura.

**Nome do serviço SPI HSM remoto:** esta opção é para uso quando o HSM está instalado em um computador remoto. Especifique essa opção quando AEM formulários estiverem instalados em um Windows de 64 bits e você estiver usando dispositivos HSM para assinatura.

**URL do serviço Web HSM Remoto:** Especifique essa opção quando os formulários AEM estiverem instalados no Windows de 64 bits e você estiver usando dispositivos HSM para assinatura.

**Certificação para incluir alterações no carregamento do formulário:** quando essa opção é selecionada, o Estado do formulário XFA é certificado além do modelo XFA. Observe que ativar essa opção pode ter um impacto negativo no desempenho. O valor padrão é true.

**Executar scripts JavaScript do Documento:** Especifica se os scripts JavaScript do Documento devem ser executados durante operações de assinatura. O valor padrão é false.

**Processar documentos com compatibilidade Acrobat 9:** Especifica se a compatibilidade com Acrobat 9 deve ser ativada. Por exemplo, quando essa opção é selecionada, a Certificação visível em PDFs dinâmicos é ativada. O valor padrão é false.

**Incorporar informações de revogação ao assinar:** especifica se as informações de revogação estão incorporadas ao assinar o documento PDF. O valor padrão é false.

**Incorporar informações de revogação ao certificar:** especifica se as informações de revogação estão incorporadas durante a certificação do documento PDF. O valor padrão é false.

**Impor incorporação de informações de revogação para todos os certificados durante a assinatura/certificação:** Especifica se uma operação de assinatura ou certificação falha se as informações de revogação válidas para todos os certificados não estão incorporadas. Observe que se um certificado não contém nenhuma informação CRL ou OCSP, ele é considerado válido, mesmo se nenhuma informação de revogação for recuperada. O valor padrão é false.

**Ordem de verificação de revogação:** especifica a ordem de verificação de revogação quando a verificação é possível por meio dos mecanismos CRL (Certificate Revocation Lista) e OCSP (Online Certificate Status Protocol). O valor padrão é OCSPFirst.

**Tamanho Máximo de Informações de Arquivamento de Revogação:** O tamanho máximo das informações de arquivamento de revogação em kilobytes. AEM formulários tentam armazenar o máximo possível de informações de revogação sem exceder o limite. O valor padrão é 10 KB.

**Assinaturas de suporte criadas a partir de compilações de pré-lançamento de produtos de Adobe:** Quando essa opção é selecionada, a assinatura criada usando a versão de pré-lançamento dos produtos de Adobe valida corretamente. O valor padrão é false.

**Opção Tempo de verificação:** especifica o tempo de verificação do certificado de um assinante. O valor padrão é Tempo seguro ou Hora atual.

**Usar informações de revogação arquivadas na assinatura durante a validação:** Especifica se as informações de revogação arquivadas com a assinatura são usadas para a verificação de revogação. O valor padrão é true.

**Usar informações de validação armazenadas no Documento para validação de assinaturas:** quando essa opção é selecionada, as informações de validação (incluindo informações de revogação e carimbo de data e hora) incorporadas no documento são usadas para validar assinaturas. O valor padrão é true.

**Máximo de sessões de verificação aninhadas permitidas:** o número máximo de sessões de verificação aninhadas permitidas. AEM formulários usam esse valor para impedir um loop infinito ao verificar os certificados do assinante OCSP ou CRL quando o certificado OCSP ou CRL não está configurado corretamente. O valor padrão é 10.

**Inclinação máxima do relógio para verificação:** o tempo máximo, em minutos, em que o tempo de assinatura pode ser após o tempo de validação. Se a inclinação do relógio for maior que esse valor, a assinatura não será válida. O valor padrão é 65 minutos.

**Cache de tempo de vida do certificado:** a duração de um certificado, recuperado online ou por outros meios, no cache. O valor padrão é 1 dia.

### Opções de transporte {#transport-options}

**Host proxy:** a URL do host proxy. Usado somente se algum valor válido for fornecido. Nenhum valor padrão.

**Porta de proxy:** a porta de proxy. Digite qualquer número de porta válido de 0 a 65535. O valor padrão é 80.

**Nome de usuário de logon de proxy:** o nome de usuário de logon de proxy. Usado somente se algum valor válido for fornecido para host proxy e porta proxy. Nenhum valor padrão.

**Senha de logon de proxy:** a senha de logon de proxy. Usado somente se algum valor válido for fornecido para o host proxy, porta proxy e nome de usuário de logon proxy. Nenhum valor padrão.

**Limite máximo de download:** a quantidade máxima de dados, em MBs, que podem ser recebidos por conexão. O valor mínimo é 1 MB e o valor máximo é 1024 MB. O valor padrão é 16 MB.

**Tempo limite da conexão:** o tempo máximo de espera, em segundos, para estabelecer uma nova conexão. O valor mínimo é 1 e o valor máximo é 300. O valor padrão é 5.

**Tempo limite do soquete:** o tempo máximo de espera, em segundos, antes de um tempo limite do soquete (enquanto espera pela transferência de dados) ocorrer. O valor mínimo é 1 e o valor máximo é 3600. O valor padrão é 30.

### Opções de validação de caminho {#path-validation-options}

**Exigir política explícita:** especifica se o caminho deve ser válido para pelo menos uma das políticas de certificado associadas à âncora de confiança do certificado do assinante. O valor padrão é false.

**Inibir QUALQUER Política:** Especifica se o identificador de objeto de política (OID) deve ser processado se estiver incluído em um certificado. O valor padrão é false.

**Inibir mapeamento de política:** especifica se o mapeamento de política é permitido no caminho de certificação. O valor padrão é false.

**Verificar todos os caminhos:** especifica se todos os caminhos devem ser validados ou se a validação deve parar após localizar o primeiro caminho válido. Selecione verdadeiro ou falso. O valor padrão é false.

**Servidor LDAP:** o servidor LDAP usado para procurar certificados para a validação de caminho. Nenhum valor padrão.

**Seguir URIs no Certificado AIA:** Especifica se os URIs (Uniform Resource Identifiers) no Certificado AIA são processados durante a descoberta do caminho. O valor padrão é false.

**Extensão de Restrições Básicas exigida em Certificados CA:** Especifica se a extensão de certificado de Restrições Básicas da autoridade de certificação (CA) deve estar presente para certificados CA. Alguns certificados originais de raiz certificados alemães (7 e anteriores) não são compatíveis com RFC 3280 e não contêm a extensão de restrição básica. Se for sabido que o certificado EE de um usuário está vinculado a uma raiz alemã, desmarque essa caixa de seleção. O valor padrão é true.

**Exigir assinatura de certificado válida durante o encadeamento:** especifica se o encadeador de cadeia exige assinaturas válidas em certificados usados para criar cadeias. Quando essa caixa de seleção é selecionada, o Construtor de cadeia não criará cadeias com assinaturas RSA inválidas em certificados. Considere a cadeia CA > ICA > EE, onde a assinatura da CA em uma ICA não é válida. Se essa configuração for verdadeira, o prédio da cadeia parará na ICA, e a CA não será incluída na cadeia. Se essa configuração for falsa, toda a cadeia de 3 certificados será gerada. Essa configuração não afeta as assinaturas DSA. O valor padrão é false.

### Opções do provedor de carimbo de data e hora {#timestamp-provider-options}

**URL do servidor TSP:** a URL do provedor de carimbo de data e hora padrão. Usado somente se algum valor válido for fornecido. Nenhum valor padrão.

**Nome de usuário do servidor TSP:** o nome de usuário, se exigido pelo provedor de carimbo de data e hora. Usado somente se algum valor válido for fornecido para o URL. Nenhum valor padrão.

**Senha do servidor TSP:** A senha do nome de usuário acima, se exigida pelo provedor de carimbo de data e hora. Usado somente se algum valor válido for fornecido para o URL e o nome do usuário. Nenhum valor padrão.

**Algoritmo de hash de solicitação:** especifica o algoritmo de hash a ser usado ao criar a solicitação para o provedor de carimbo de data e hora. O valor padrão é SHA1.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado para determinar o status de confiança do certificado do provedor de carimbo de data e hora a partir do status de revogação observado. O valor padrão é BestEffort.

**Enviar Nonce:** Especifica se um nonce é enviado com a solicitação do provedor de carimbo de data e hora. Um nonce pode ser um carimbo de data e hora, um contador de visitas em uma página da Web ou um marcador especial que se destina a limitar ou impedir a reprodução ou reprodução não autorizada de um arquivo. O valor padrão é true.

**Usar carimbos de data e hora expirados durante a validação:** quando essa opção é selecionada, os carimbos de data e hora expirados podem ser usados para recuperar os tempos de validação das assinaturas. O valor padrão é true.

**Tamanho da resposta TSP:tamanho** estimado, em bytes, da resposta TSP. Esse valor deve representar o tamanho máximo da resposta do carimbo de data e hora que o provedor configurado poderia retornar. Não altere isso a menos que tenha certeza absoluta. O valor mínimo é 60B e o valor máximo é 10240B. O valor padrão é 4096B.

**Ignorar extensão** do servidor TimeStamp: Selecione a opção  **Ignorar** extensão do servidor TimeStamp para impedir que o servidor AEM Forms entre em contato com o servidor de carimbo de data e hora especificado. A seleção da opção ajuda a evitar falhas no processo que ocorrem devido ao tempo limite de conexão entre a AEM Forms e os servidores de carimbo de data e hora.

### Opções de Lista de revogação de certificado {#certificate-revocation-list-options}

**Consultar URI local primeiro:** especifica se a localização da CRL fornecida na URI local ou na Pesquisa de CRL deve ter preferência sobre qualquer local especificado em um certificado para fins de verificação de revogação. O valor padrão é false.

**URI local para pesquisa de CRL:** URL do provedor de CRL local. Esse valor é consultado somente se a configuração Consultar URI local primeiro estiver definida como true. Nenhum valor padrão.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado para determinar o status de confiança do certificado do provedor CRL a partir do status de revogação observado. O valor padrão é BestEffort.

**Servidor LDAP para pesquisa CRL:** o servidor LDAP usado para obter as CRLs (como www.ldap.com). Todos os query baseados em DN para CRLs serão direcionados para este servidor. Nenhum valor padrão.

**Ficar online:** especifica se você deve estar online para buscar uma CRL. Se falso, somente CRLs em cache (no disco local ou aqueles incorporados com assinatura) serão consultados. O valor padrão é true.

**Ignorar datas de validade:** Especifica se deve ignorar os tempos thisUpdate e nextUpdate da resposta, o que impede que esses tempos tenham um efeito negativo na validade da resposta. O valor padrão é false.

**Exigir extensão do AKI em CRL:** Especifica se a extensão do Identificador da Chave da Autoridade deve ser incluída em uma CRL. O valor padrão é false.

### Opções de protocolo de status de certificado on-line {#online-certificate-status-protocol-options}

**URL do servidor OCSP:** URL do servidor OCSP padrão. Se o servidor OCSP especificado por meio desse URL é usado depende da configuração da opção URL para consulta. Nenhum valor padrão.

**Opção URL para consulta:** controla a lista e a ordem dos servidores OCSP usados para executar a verificação de status. O valor padrão é UseAIAInCert.

**Estilo de verificação de revogação:** Especifica o estilo de verificação de revogação usado ao verificar o certificado do servidor OCSP. O valor padrão é CheckIfAvailable.

**Enviar Nonce:** Especifica se um nonce é enviado com a solicitação OCSP. Um nonce pode ser um carimbo de data e hora, um contador de visitas em uma página da Web ou um marcador especial que se destina a limitar ou impedir a reprodução ou reprodução não autorizada de um arquivo. O valor padrão é true.

**Tempo máximo de inclinação do relógio:** máximo de inclinação permitido, em minutos, entre o tempo de resposta e o horário local. O valor mínimo é 0 e o valor máximo é 2147483647m. O valor padrão é 5m.

**Tempo de Frescura da Resposta:Tempo** máximo, em minutos, para o qual uma resposta OCSP pré-construída é considerada válida. O valor mínimo é 1 m e o valor máximo permitido é 2147483647. O valor padrão é 525600 (um ano).

**Assinar solicitação OCSP:** Especifica se a solicitação OCSP deve ser assinada. O valor padrão é false.

**Alias de Credencial do Assinante de Solicitação:** Especifica o alias de credencial a ser usado para assinar a solicitação OCSP se a assinatura estiver ativada. Usado somente se a assinatura da solicitação OCSP estiver ativada. Nenhum valor padrão.

**Estar online:** especifica se você deve estar online para fazer a verificação de revogação. O valor padrão é true.

**Ignorar os tempos thisUpdate e nextUpdate da resposta:** Especifica se deve ignorar os tempos thisUpdate e nextUpdate da resposta, o que impede que esses tempos tenham um efeito negativo na validade da resposta. O valor padrão é false.

**Permitir extensão OCSPNoCheck:** Especifica se a extensão OCSPNoCheck é permitida no certificado de assinatura de resposta. O valor padrão é true.

**Exigir extensão CertHash OCSP ISIS-MTT:** Especifica se uma extensão de hash de chave pública de certificado deve ser incluída nas respostas OCSP. O valor padrão é false.

### Opções de Tratamento de Erros para Depuração {#error-handling-options-for-debugging}

**Limpar cache de certificado na próxima chamada de API:** Especifica se a limpeza do cache de certificado deve ser feita quando a próxima operação do serviço de assinatura for chamada. Depois que a operação é chamada, essa opção é definida como false. O valor padrão é false.

**Limpar cache CRL na próxima chamada de API:** Especifica se o cache CRL deve ser expurgado quando a próxima operação do serviço de assinatura for chamada. Depois que a operação é chamada, essa opção é definida como false. O valor padrão é false.

**Expurgar Cache OCSP na próxima chamada de API:** Especifica se o cache OCSP deve ser expurgado quando a próxima Operação do serviço de assinatura for chamada. Depois que a operação é chamada, essa opção é definida como false. O valor padrão é false.

## Configurações do serviço de Pasta assistida {#watched-folder-service-settings}

O serviço de Pasta monitorada ( `WatchedFolder`) configura atributos que são comuns a todos os pontos de extremidade de pasta monitorados. Ele também fornece valores padrão para pontos de extremidade de pastas observados. (Consulte [Configuração de pontos finais de pastas observados](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Ela não é invocada por aplicativos clientes externos ou usada em processos criados no Workbench.

As configurações a seguir estão disponíveis para o serviço de Pasta assistida.

**Expressão Cron:** A expressão cron, como usada pelo quartzo para agendar a pesquisa do diretório de entrada.

**Contagem de repetição:** O número de vezes que o diretório de entrada é pesquisado. A contagem de repetição padrão a ser usada se esse valor não for especificado na configuração do ponto de extremidade. Um valor de -1 indica uma varredura indefinida do diretório. O valor padrão é -1.

**Intervalo de repetição:** O número padrão se houver segundos entre cada pesquisa. Esse valor é usado como o intervalo de repetição, a menos que um valor diferente seja especificado na configuração do ponto de extremidade da pasta monitorada. O valor padrão é 5. Consulte a descrição da configuração Tamanho do lote para obter mais informações.

**Assíncrono:** identifica o tipo de invocação como assíncrono ou síncrono. Processos transitórios e síncronos só podem ser chamados de forma síncrona. O valor padrão é assíncrono.

**Tempo de espera:** o valor padrão por tempo, em segundos, após o qual os arquivos são recuperados das pastas de entrada. Se o arquivo ou pasta for anterior ao tempo especificado no tempo de espera, ele será selecionado para processamento. O valor padrão é 0.

**Tamanho do lote:** o valor padrão para o número de arquivos ou pastas processados por verificação. O valor padrão é 2.

As configurações Repetir intervalo e Tamanho do lote determinam quantos arquivos a Pasta assistida seleciona em cada verificação. A Pasta assistida usa um pool de threads do Quartz para verificar a pasta de entrada. O pool de threads é compartilhado com outros serviços. Se o intervalo de digitalização for pequeno, os threads normalmente digitalizam a pasta de entrada. Se os arquivos forem descartados com frequência na pasta assistida, mantenha o intervalo de verificação pequeno. Se os arquivos forem descartados com pouca frequência, use um intervalo de verificação maior para que os outros serviços possam usar os threads.

Se houver um grande volume de arquivos sendo descartados, torne o tamanho do lote grande. Por exemplo, se o serviço chamado pelo ponto de extremidade da pasta assistida puder processar 700 arquivos por minuto, e os usuários soltarem arquivos na pasta de entrada à mesma taxa, então, definir o Tamanho do lote como 350 e o Intervalo de repetição como 30 segundos ajudará no desempenho da Pasta assistida sem incorrer no custo de digitalização da pasta assistida com muita frequência.

Quando os arquivos são descartados na pasta assistida, ele lista os arquivos na entrada, o que pode reduzir o desempenho se a varredura estiver ocorrendo a cada segundo. O aumento do intervalo de varredura pode melhorar o desempenho. Se o volume de arquivos que está sendo descartado for pequeno, ajuste o Tamanho do lote e o Intervalo de repetição de acordo. Por exemplo, se 10 arquivos forem descartados a cada segundo, tente definir o Intervalo de repetição como 1 segundo e o Tamanho do lote como 10.

Em uma configuração de cluster, o tamanho do lote de um ponto de extremidade de pasta monitorada não é dimensionado para vários nós de cluster. Por exemplo, se o tamanho do lote estiver definido como `2` para um cluster de dois nós e a opção Restringir estiver selecionada, os nós processarão arquivos coletivamente em lotes de dois em vez de cada nó processar dois arquivos de cada vez.

**Substituir nomes de arquivos de Duplicado:** Uma string booleana que especifica se a pasta assistida sobrescreve os nomes de arquivos de resultado do duplicado e se documentos preservados com o mesmo nome devem ser substituídos.

**Pasta de preservação:** o valor padrão para a pasta de preservação. Essa pasta é usada para copiar os arquivos de origem em caso de processamento bem-sucedido da entrada. Esse valor pode ser um caminho vazio, relativo ou absoluto com um padrão de arquivo, conforme descrito para a configuração Pasta de resultados.

**Pasta de falha:** o nome da pasta na qual os arquivos de falha são copiados. Esse valor pode ser um caminho vazio, relativo ou absoluto com um padrão de arquivo, conforme descrito para a configuração Pasta de resultados.

**Pasta de resultados:** o nome padrão para a pasta de resultados. Essa pasta é usada para copiar os arquivos de resultados. Esse valor pode ser um caminho vazio, relativo ou absoluto com o seguinte padrão de arquivo.

* %F = prefixo de nome de arquivo
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
* %l = milissegundos
* %R = número aleatório (de 0 a 9)
* %P = id de processo ou tarefa

Por exemplo, se forem 8 horas em 17 de julho de 2009 e você especificar `C:/Test/WF0/failure/%Y/%M/%D/%H/`, a pasta resultante será `C:/Test/WF0/failure/2009/07/17/20`.

Se o caminho não for absoluto, mas relativo, a pasta será criada dentro da pasta assistida. Para obter mais informações sobre padrões de arquivos, consulte [Sobre padrões de arquivos](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Quanto menor for o tamanho das pastas de resultados, melhor será o desempenho da Pasta assistida. Por exemplo, se a carga estimada para a pasta assistida for de 1.000 arquivos a cada hora, tente um padrão como `result/%Y%M%D%H` para que uma nova subpasta seja criada a cada hora. Se a carga for menor (por exemplo, 1000 arquivos por dia), você poderá usar um padrão como `result/%Y%M%D`.

**Pasta de palco:** o nome padrão da pasta de palco dentro da pasta assistida.

**Pasta de entrada:** o nome padrão da pasta de entrada dentro da pasta assistida.

**Preservar na falha:** se for verdadeiro, os arquivos originais serão preservados na pasta da falha na falha.

**Limitação:** quando essa opção é selecionada, ela limita o número de trabalhos de pasta observados que AEM processos de formulários em um determinado momento. O valor Tamanho do Lote determina o número máximo de trabalhos (Consulte Sobre a limitação).

## Configurações de serviço do serviço Web {#web-service-service-settings}

O serviço de serviço Web ( `WebService`) permite que os processos chamem operações de serviço Web.

O serviço Web permite que os processos chamem operações de serviço Web. Por exemplo, uma organização pode desejar integrar um processo para armazenar e recuperar informações, como detalhes de contato e conta, chamando os serviços da Web expostos de um provedor de serviço. O serviço Web chama um serviço Web especificado e transmite valores para cada um de seus parâmetros. Em seguida, salva os valores de retorno da operação em uma variável designada em um processo.

O serviço Web interage com os serviços da Web enviando e recebendo mensagens SOAP. O serviço também suporta o envio de anexos MIME, MTOM e SwaRef com mensagens SOAP usando o protocolo WS-Attachment. As interações do serviço Web são compatíveis com sistemas SAP e serviços Web .NET.

As configurações a seguir estão disponíveis para o serviço Web.

**Armazenamento de chaves:** o caminho completo do arquivo de armazenamento de chaves que contém a chave privada a ser usada para autenticação. O servidor de formulários deve poder acessar o arquivo.

**Senha do armazenamento de chaves:** a senha do arquivo do armazenamento de chaves.

**Tipo de armazenamento de chave:** o tipo de armazenamento de chave. Não forneça nenhum valor para usar o tipo de armazenamento de chaves padrão configurado para a JVM que executa o servidor de formulários. Caso contrário, forneça um dos seguintes valores:

* jatos
* pkcs12
* cms
* jceks

**Armazenamento de confiança:** o caminho completo do arquivo de repositório de confiança que contém a chave pública do servidor de serviço da Web.

**Senha do armazenamento de confiança:** a senha do arquivo do Truststore.

**Tipo de Armazenamento de Confiança:** o tipo de armazenamento de confiança. Não forneça nenhum valor para usar o tipo de armazenamento de chaves padrão configurado para a JVM que executa o servidor de formulários. Caso contrário, forneça um dos seguintes valores:

* jatos
* pkcs12
* cms
* jceks

## Configurações do serviço de Transformação XSLT {#xslt-transformation-service-settings}

O serviço de transformação XSLT ( `XSLTService`) permite que os processos apliquem Transformações de linguagem de folha de estilos extensível (XSLT) em documentos XML.

A seguinte configuração está disponível para o serviço de Transformação XSLT.

**Nome de fábrica:** o nome totalmente qualificado da classe Java a ser usado para executar transformações XSLT. Se nenhum valor for especificado, a fábrica padrão configurada na máquina virtual Java que executa o servidor de formulários será usada.

## Modificando configurações de segurança para um serviço {#modifying-security-settings-for-a-service}

o servidor de formulários permite que você defina as configurações de segurança para cada serviço, o que permite que você configure o controle de acesso refinado em um nível serviço por serviço.

São instalados perfis de segurança padrão, que podem ser configurados para atender às necessidades do seu sistema. Cada perfil de segurança tem um domínio associado e é criado no nível do usuário ou do grupo.

### Modificar configurações de segurança para um serviço {#modify-security-settings-for-a-service}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique no serviço a ser configurado.
1. Clique na guia Segurança.
1. Na lista Exigir que os chamadores autenticem, selecione Sim ou Não para especificar se o serviço pode ser chamado com ou sem credenciais.

   Se você selecionar Sim, o chamador do serviço deve ser autenticado e o principal do usuário desse chamador deve ser autorizado a invocar o serviço; caso contrário, a tentativa de invocação será recusada.

   Se você selecionar Não, o chamador do serviço pode ou não ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização.

1. Para serviços que contêm uma ou mais operações sinalizadas para acesso anônimo, selecione ou desmarque Acesso Anônimo Permitido. Quando o acesso anônimo está ativado, qualquer usuário no sistema pode chamar operações no serviço. Se o acesso anônimo estiver desativado, os usuários devem receber permissão para chamar o serviço e chamar as operações. Os usuários recebem essas permissões diretamente ou como parte de um grupo que tem essas permissões.
1. Para alguns serviços, a conta de usuário que executa a operação afeta os resultados. Por exemplo, nos Serviços de conteúdo (obsoleto), o usuário que armazena conteúdo se torna o proprietário do conteúdo, o que afeta quem pode acessar posteriormente o conteúdo. Se você estiver usando um processo para armazenar conteúdo, pense sobre qual usuário é usado para executar o serviço de Gerenciamento de Documentos, pois esse usuário será o proprietário do conteúdo armazenado.

   Para especificar a identidade de tempo de execução usada por um serviço para executar operações, selecione Especificar Executar como, selecione uma opção da lista associada e clique em Salvar. Escolha uma das seguintes opções:

   **Invocador:** Usa a mesma identidade do usuário que chamou o serviço.

   **Sistema:** usa o usuário do Sistema para executar o serviço com privilégios totais.

   **Usuário nomeado:** permite que você execute o serviço como um usuário específico. Ao selecionar essa opção, clique em Selecionar usuário para exibir a página Selecionar principal, na qual você pode pesquisar e selecionar o usuário.

   Se você não selecionar Especificar Executar como, o comportamento padrão será usado.

   >[!NOTE]
   >
   >Os serviços de renderização e envio usados com as variáveis xfaForm, Formulário de Documento e Formulário são sempre executados usando a conta de usuário do Sistema.

1. Clique em Adicionar Principal para especificar as permissões que os usuários e grupos têm para este serviço.
1. A tela Selecionar principal exibe os usuários e grupos configurados no Gerenciamento de usuários. Se o usuário ou grupo desejado não for exibido, use a função de pesquisa para encontrá-lo. Clique em um nome de usuário ou grupo.
1. Na tela Adicionar permissões, selecione as permissões a serem atribuídas ao usuário ou grupo para este serviço:

   * **INVOKE_PERM:** Para chamar todas as operações no serviço
   * **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço
   * **SUPERVISOR_PERM:** Para visualização dos dados da instância do processo para um serviço criado a partir de um processo
   * **START_STOP_PERM:** Para start e parar um serviço
   * **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar pontos de extremidade de um serviço
   * **CREATE_VERSION_PERM:** Para criar uma nova versão do serviço
   * **DELETE_VERSION_PERM:** Para excluir uma versão do serviço
   * **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço
   * **READ_PERM:** Para visualização do serviço
   * **PROCESS_OWNER_PERM:** Para uso em uma versão futura de formulários AEM. Não use esta permissão.
   * **SERVICE_MANAGER_PERM:** Para uso em uma versão futura de formulários AEM. Não use esta permissão.
   * **SERVICE_AGENT_PERM:** Para uso em uma versão futura de formulários AEM. Não use esta permissão.

1. Clique em Adicionar.

### Remova o principal de um perfil de segurança {#remove-the-principal-from-a-security-profile}

1. Na página Gerenciamento de serviços, selecione o serviço a ser configurado.
1. Clique na guia **Segurança**, selecione o perfil de segurança a ser removido e clique em **Remover**.

## Configuração de pooling para um serviço {#configuring-pooling-for-a-service}

Cada serviço pode aproveitar os recursos de pooling para lidar com solicitações de invocação recebidas. O uso de um pool de serviços garante que as instâncias de serviço sejam chamadas por um único thread por vez e sejam reutilizadas em solicitações de invocação, o que pode resultar em um desempenho aprimorado. Você também pode usar o pooling para especificar a opção Máximo de instâncias de serviço assíncronas, que permite que os serviços limitem o número de solicitações tratadas em paralelo.

### Ativar pooling {#enable-pooling}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique no serviço a ser configurado.
1. Clique na guia Pooling.
1. Na lista de Estratégia de Processamento de Solicitação, selecione Instâncias em Pool para Todas as Solicitações.
1. Na caixa Tamanho inicial do pool de instâncias de serviço, digite o tamanho inicial do pool. Quando o serviço é implantado, esse número é usado para determinar o número de instâncias de implementação do serviço que são criadas e alocadas ao pool gratuito, aguardando solicitações de invocação. Isso permite que o container de serviço responda imediatamente às solicitações de invocação sem precisar primeiro inicializar uma instância de serviço.
1. Na caixa Tamanho máximo do pool de instâncias de serviço, digite o número máximo de instâncias no pool para um determinado serviço. Essa configuração controla o número de threads que podem executar um determinado serviço em um determinado momento. O valor padrão é 0, o que resulta em um tamanho de pool ilimitado.
1. Na caixa Máximo de instâncias de serviço assíncronas, digite o número máximo de instâncias do pool que podem ser usadas para atender solicitações assíncronas em um determinado momento. Essa configuração permite que o serviço limite o número de solicitações que ele pode manipular em paralelo.
1. Na caixa Tempo limite de espera da chamada, digite o número de milissegundos para aguardar que um serviço fique disponível para uma solicitação de invocação. Se você não especificar um valor para essa configuração, o padrão será 0, o que resultará em nenhum tempo de espera.
1. Clique em Salvar.

### Remover pooling {#remove-pooling}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique no serviço a ser configurado.
1. Clique na guia Pooling.
1. Na lista de estratégia de processamento de solicitação, selecione Nova instância para cada solicitação ou Instância única para todas as solicitações.

   **Instância única para todas as solicitações:** uma instância de serviço é criada e armazenada em cache quando a primeira solicitação entra no container. Cada solicitação após essa solicitação usa a mesma instância de serviço para lidar com a solicitação.

   **Nova instância para cada solicitação:** uma nova instância de serviço é criada para cada invocação recebida.

1. Clique em Salvar.

