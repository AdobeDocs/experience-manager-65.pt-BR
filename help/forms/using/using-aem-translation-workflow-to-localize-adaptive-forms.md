---
title: Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro
seo-title: Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro
description: Saiba como usar fluxos de trabalho de tradução AEM para localizar formulários adaptáveis e documentos de registro.
seo-description: Saiba como usar fluxos de trabalho de tradução AEM para localizar formulários adaptáveis e documentos de registro.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Formulários localizados ajudam você a oferecer um público-alvo maior em várias regiões. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar formulários adaptáveis e seus documentos de registro . Você pode usar **tradução automática** ou **tradutores humanos** para localizar um formulário adaptável.

Este artigo explica o processo para usar AEM fluxo de trabalho de tradução com formulários adaptáveis e documentos de registro.

## Localização de um formulário adaptável e documento de registro usando tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática traduz imediatamente seu conteúdo em forma adaptável e documento de registro. O AEM Forms é pré-configurado para usar uma versão de avaliação do Microsoft Translator para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para os formulários adaptáveis e o documento de registro:

1. Na interface do usuário do AEM Forms, selecione um formulário e toque na opção **Adicionar dicionário** .
1. Na tela **Adicionar dicionário ao projeto de tradução**, selecione a opção **Criar um novo projeto de tradução** ou **Adicionar a um projeto de tradução existente**.
1. No campo **Título do projeto**, especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No campo **Idiomas de destino**, especifique uma localidade (Por exemplo, `German(de)`) e clique em **Concluído**. Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas no campo **Idiomas de destino**.
1. Na caixa de diálogo Dicionário adicionado, clique em **Abrir projetos**. Na tela Projetos , abra o projeto recém-criado.
1. Clique no **elipses** na parte inferior do bloco **Resumo da tradução**. A tela Resumo da tradução é aberta.
1. Clique no ícone **Editar** na parte superior da tela **Resumo da tradução**. Abra a guia **Translation** e selecione Machine Translation na tela **Translation Method**. Selecione o **Provedor de Tradução** apropriado e **Configuração da Nuvem**. Clique no ícone **Concluído** na parte superior da tela.
1. No bloco **Tarefa de Tradução**, clique no ícone ![aem62forms_downseta](assets/aem62forms_downarrow.png) e clique em **Iniciar**. O status do bloco é alterado para Rascunho. Após a conclusão da tradução, o status muda para **Ready for review**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Ready for review** no bloco **Translation Job**, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão(de), defina a localidade do navegador como alemão(de).
   >* Os componentes de formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.


   Juntamente com o formulário adaptável, o documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do Documento de registro, consulte:

   [Documento de configuração modelo de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Configurações do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalize as informações de marca do documento de ](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) registro e verifique se a localidade do navegador está definida com o mesmo idioma no qual você localizou o formulário adaptável usando o idioma da máquina. A localidade do navegador ajuda a localizar as informações de marca no documento de registro.
1. Para exibir o documento localizado de registro, toque em Gerar visualização. O documento de registrar PDF é gerado e aberto em uma nova guia no navegador.

## Localização de um formulário adaptável e seu documento de registro usando Tradução Humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Na tradução humana, o conteúdo é enviado a um provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.

Para tradução, um dicionário contendo arquivos no formato XLIFF é compartilhado com os tradutores profissionais. O dicionário inclui um arquivo XLIFF separado para cada localidade. Cada arquivo XLIFF contém texto que será exibido aos usuários finais e aos espaços reservados para o texto localizado correspondente.

Execute as seguintes etapas para localizar um formulário e seu documento de registro usando Tradutores humanos:

1. [Conecte AEM com seu ](/help/sites-administering/tc-tic.md) provedor de serviços de tradução e  [crie configurações](/help/sites-administering/tc-tic.md) de estrutura de integração de tradução.

1. [Associe as páginas do ](/help/sites-administering/tc-tic.md) domínio de idioma com o serviço de tradução e as configurações de estrutura.

1. [Identifique o tipo de ](/help/sites-administering/tc-rules.md) conteúdo a ser traduzido.

1. [Prepare o conteúdo para ](/help/sites-administering/tc-prep.md) tradução criando o idioma principal e criando as páginas raiz das cópias de idioma.

1. [Crie ](/help/sites-administering/tc-manage.md) projetos de tradução para coletar o conteúdo para traduzir e preparar o processo de tradução.

1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Os componentes de formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.

>



