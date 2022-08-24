---
title: Atualizando certificados de serviço de extensão do Reader expirados
description: Reader estendido documentos não funcionando, atualizar certificados
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# Atualizando certificados de serviço de extensão do Reader expirados {#Updating-expired-Reader-Extension-service-certificates}

Os clientes da Adobe Experience Manager Forms (AEM Forms) com o Adobe Managed Services ou licenças no local da Enterprise Base têm direito de usar o serviço de Extensão do Reader. O serviço permite que uma organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço adiciona direitos de uso a um documento do PDF e ativa recursos que normalmente não estão disponíveis quando um documento do PDF é aberto usando o Adobe Acrobat Reader DC, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com documentos ativados por direitos. Os documentos do PDF com direitos de uso adicionados são chamados de documentos ativados por direitos. Um usuário que abre um documento do PDF habilitado para direitos no Adobe Reader pode executar as operações ativadas para esse documento.

O Adobe aproveita um PKI (infraestrutura de chave pública) para emitir certificados digitais para uso em licenciamento e ativação de recursos. A Adobe está emitindo certificados sob a autoridade de certificação &quot;Adobe Root CA&quot;, está agendado para expirar em 7 de janeiro de 2023. Causará a expiração de todos os certificados emitidos ao abrigo desta autoridade de certificação. Depois que o certificado expirar, todos os recursos dependentes dos certificados não funcionarão mais. Por exemplo, um documento PDF estendido pelo leitor que permite a adição de comentários usando o Adobe Acrobat Reader para de funcionar para os clientes após 7 de janeiro de 2023. Para resolver o problema, o administrador do serviço Reader Extension, usando certificados antigos, deve obter e reaplicar novos certificados emitidos pela nova Adobe Root CA G2 a seus documentos PDF (o leitor estende os documentos PDF com novos certificados).

A expiração dos certificados afeta a AEM Forms no JEE e a AEM Forms nas pilhas OSGi. Ambas as pilhas têm um conjunto de instruções diferente. Após a reunião do [pré-requisitos](#Pre-requisites) e [obtenção de novos certificados](#obtain-the-certificates), dependendo da pilha, escolha um dos seguintes caminhos:

* [Atualização de certificados para um ambiente AEM Forms em JEE](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [Atualização de certificados para uma AEM Forms no ambiente OSGi](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>O documento utiliza o termo certificados e credenciais alternadamente.

## Pré-requisitos {#Pre-requisites}

A atualização dos certificados requer o uso de ações disponíveis no console do administrador do AEM Forms e nas APIs de extensão do Reader fornecidas pela AEM Forms. O documento destina-se a usuários e administradores com conhecimento em usar APIs do Adobe Experience Manager Forms. Antes de começar, verifique se:

* o usuário tem direitos de administrador no ambiente subjacente do AEM Forms.
* o usuário configurou a variável [ambiente de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) e tem acesso a ela.
* obter os certificados.

### Obter os certificados {#obtain-the-certificates}

A credencial de direitos é entregue como um certificado digital que contém a chave pública, a chave privada e a senha usada para acessar a credencial.

Se sua organização comprar uma versão de produção das Extensões do Reader, a credencial de Direitos de produção será entregue pelo Site de Licenciamento de Adobe (LWS). Uma credencial de Direitos de produção é exclusiva de sua organização e pode habilitar os direitos de uso específicos que você precisa.

Se você obteve Extensões do Reader por meio de um parceiro ou provedor de software que integrou as Extensões do Reader ao software, a credencial de Direitos é fornecida a você pelo parceiro que, por sua vez, recebe essa credencial do Adobe.

>[!NOTE]
>
>A credencial de direitos não pode ser usada para a assinatura típica do documento ou asserção de identidade. Para esses aplicativos, você pode usar um certificado de autoassinatura ou adquirir um certificado de identidade de uma autoridade de certificação (CA).

Os seguintes tipos de credenciais de Direitos estão disponíveis:

**Avaliação do cliente**: Uma credencial com um curto período de validade fornecido aos clientes que desejam avaliar as extensões do Reader. Os direitos de uso aplicados a documentos que usam essa credencial expiram quando a credencial expira. Esse tipo de credencial é válido apenas por dois a três meses.

**Produção**: Uma credencial com um período de validade longo, fornecida aos clientes que compraram o produto completo. As credenciais de produção são exclusivas para cada cliente, mas podem ser instaladas em vários sistemas.

Se você já tiver usado certificados para estender arquivos PDF do leitor, baixe um certificado de produção de [Site de Licenciamento de Adobe (LWS)](https://licensing.adobe.com/).

## Atualização e aplicação de certificados para um ambiente AEM Forms em JEE {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

A atualização e aplicação de novos certificados na AEM Forms na pilha JEE requer a importação de novas credenciais, a remoção de direitos de uso de documentos PDF existentes e a aplicação de direitos de uso. Você pode usar o Admin Console para importar credenciais e APIs de extensão do AEM Forms Reader para remover e aplicar direitos de uso.

### Importar e configurar credenciais

Você pode usar as páginas de Gerenciamento de armazenamento de confiança para importar uma credencial nova ou de substituição. O Armazenamento de Confiança pode conter mais de uma credencial de Extensões do Reader. Você deve designar uma dessas credenciais como a credencial de extensões Reader padrão. A credencial padrão é usada quando um usuário do Workbench não consegue determinar qual credencial usar durante a criação do processo. Essas regras se aplicam às credenciais padrão:

* Se você importar uma credencial de extensões do Reader e a Loja de Confiança não contiver outras credenciais de Extensões do Reader, ela será definida como padrão.
* Se você importar uma credencial de extensões Reader com a opção Padrão selecionada, o tipo padrão será removido de uma credencial padrão existente. A credencial importada se torna o padrão.
* Não é possível excluir uma credencial de extensões Reader padrão. Para excluir a credencial padrão, primeiro defina outra credencial como padrão. Uma exceção a essa regra é que, se houver apenas uma credencial, você poderá excluí-la mesmo que seja o padrão.
* Não é possível atualizar uma credencial de extensões Reader padrão.

Para importar as credenciais:

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar e, em Tipo de armazenamento de confiança, selecione Credencial de extensões do Acrobat Reader DC.
1. (Opcional) Para indicar que essa credencial é a credencial padrão a ser usada com as extensões do Acrobat Reader DC, selecione Padrão.
1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição para a credencial nas extensões do Acrobat Reader DC. Esse alias também é usado para acessar a credencial de forma programática usando o SDK dos formulários AEM.
1. Clique em Escolher arquivo para localizar a credencial, digite a senha da credencial e clique em OK.

Se a mensagem de erro &quot;Falha ao importar credencial devido a um formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

Também é possível importar e excluir credenciais de forma programática. (Consulte [Programação com formulários AEM](../../developing/credentials.md).)

### Remover direitos de uso de documentos de PDF habilitados por direitos existentes

Remova direitos de uso de documentos do PDF habilitados por direitos existentes antes de aplicar direitos de uso com credenciais mais recentes. O AEM Forms no JEE fornece APIs para remover direitos de uso. Para obter instruções detalhadas, consulte [Removendo direitos de uso de documentos do PDF](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Para remover direitos de uso do AEM Forms em processos JEE desenvolvidos no Workbench, consulte [Ajuda do Workbench](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Aplicar direitos de uso a documentos do PDF

Depois de importar novas credenciais e remover direitos de uso de documentos do PDF ativados por direitos existentes, aplique direitos de uso a documentos do PDF usando as novas credenciais. Você pode aplicar direitos de uso a documentos do PDF usando a API do cliente Java do Acrobat Reader DC Extensions e o serviço da Web.  Para obter detalhes, consulte [Aplicação de direitos de uso a documentos do PDF](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Atualização e aplicação de certificados para uma AEM Forms em um ambiente OSGi {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

A atualização e aplicação de novos certificados na AEM Forms na pilha OSGi requer a importação de novas credenciais, a remoção de direitos de uso de documentos PDF existentes e a aplicação de direitos de uso. Você pode usar o Admin Console para importar credenciais e APIs de extensão do AEM Forms Reader para remover e aplicar direitos de uso.

### Importar credenciais {#Import-credentials}

Em um AEM Forms em um ambiente OSGi, uma credencial de Extensão do Reader é associada ao usuário do serviço fd. Antes de adicionar credenciais para o armazenamento de chave fd-user, execute as seguintes etapas para criar um armazenamento de chave:

1. Faça logon na instância do autor do AEM como um administrador.
1. Ir para **[!UICONTROL Ferramentas]**> **[!UICONTROL Segurança]**>**[!UICONTROL Usuários]**.
1. Role para baixo na lista de usuários até encontrar a conta de usuário do fd-service.
1. Clique em **[!UICONTROL fd-service]** usuário.
1. Clique na guia keystore .
1. Clique em **[!UICONTROL Criar KeyStore]**.
1. Defina a Senha de Acesso do KeyStore e salve as configurações para criar a senha do KeyStore.

Depois de criar o armazenamento de chaves, adicione credenciais ao usuário do fd-service. O vídeo a seguir explica as etapas:

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

Os comandos a seguir listam os detalhes do arquivo pfx. Antes de executar o comando, navegue até o diretório que contém o arquivo .pfx.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Por exemplo keytool -v -list -storetype pkcs12 -keystore 1005566.pfx onde 1005566.pfx é o nome do meu arquivo pfx

### Remover direitos de uso de documentos de PDF habilitados por direitos existentes

Remova direitos de uso de documentos do PDF habilitados por direitos existentes antes de aplicar direitos de uso com credenciais mais recentes. Você pode remover os direitos de uso de um documento, chamando a API removeUsageRights de dentro da docAssuranceServiceAPI. Para obter informações detalhadas, consulte [Remover direitos de uso](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) documento.

### Aplicar direitos de uso a documentos do PDF

Para aplicar direitos de uso em um ambiente AEM Forms em OSGi, crie um serviço OSGi personalizado para usar direitos de uso nos documentos. Você também pode criar um servlet com um método POST para retornar o PDF estendido do leitor ao usuário. Para obter instruções detalhadas, consulte [Aplicação de extensões Reader](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## Perguntas frequentes

**Com quem devo entrar em contato se tiver perguntas adicionais?**

Você pode entrar em contato [Suporte a Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) ou crie um tíquete de suporte.

**O que acontece se eu não atualizar meu certificado antes de 7 de janeiro de 2023?**

Ao tentar abrir um Reader de documentos PDF Extended com certificados antigos, os usuários recebem uma mensagem de erro e não podem mais acessar os recursos estendidos do leitor. Um exemplo de erro é .

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**Há alguma alteração no nome da nova descrição?**

Os novos certificados de Extensão do Reader mencionam G3-P24 como nome do programa na descrição. Nos certificados mais antigos, o nome de programa P24 foi mencionado na descrição.
