---
title: Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: Saiba como usar fluxos de trabalho de tradução AEM para localizar formulários adaptáveis e documentos de registro.
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# Uso AEM fluxo de trabalho de tradução para localizar formulários adaptáveis e documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Formulários localizados ajudam você a oferecer um público-alvo maior em várias regiões. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar formulários adaptáveis e seus documentos de registro . Você pode usar **tradução automática** ou **tradutores humanos** para localizar um formulário adaptável.

Este artigo explica o processo para usar AEM fluxo de trabalho de tradução com formulários adaptáveis e documentos de registro.

## Localização de um formulário adaptável e documento de registro usando tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática traduz imediatamente seu conteúdo em forma adaptável e documento de registro. O AEM Forms é pré-configurado para usar uma versão de avaliação do Microsoft Translator para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para os formulários adaptáveis e o documento de registro:

1. Na interface do usuário do AEM Forms, selecione um formulário e toque no **Adicionar dicionário** opção.
1. Em **Adicionar dicionário ao projeto de tradução** selecione o **Criar um novo projeto de tradução** ou **Adicionar a um projeto de tradução existente** opção.
1. No **Título do projeto** , especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No **Idiomas de destino** , especifique uma localidade (por exemplo, `German(de)`) e clique em **Concluído**. Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas na variável **Idiomas de destino** campo.
1. Na caixa de diálogo Dicionário adicionado, clique em **Projetos abertos**. Na tela Projetos , abra o projeto recém-criado.
1. Clique no botão **elipses** na parte inferior do **Resumo da tradução** mosaico. A tela Resumo da tradução é aberta.
1. Clique no botão **Editar** na parte superior do **Resumo da tradução** tela. Abra o **Tradução** e selecione Tradução automática na guia **Método de tradução** tela. Selecione o **Provedor de Tradução** e **Configuração na nuvem**. Clique no botão **Concluído** na parte superior da tela.
1. No **Tarefa de tradução** bloco , clique no botão ![aem62forms_downseta](assets/aem62forms_downarrow.png) e clique em **Iniciar**. O status do bloco é alterado para Rascunho. Ao concluir a tradução, o status é alterado para **Pronto para revisão**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Pronto para revisão** no **Tarefa de tradução** em mosaico, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão(de), defina a localidade do navegador como alemão(de).
   >* Os componentes de formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.


   Juntamente com o formulário adaptável, o documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do Documento de registro, consulte:

[Documento de configuração modelo de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configurações do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizar as informações de marca do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e verifique se a localidade do navegador está definida com o mesmo idioma no qual você localizou o Formulário adaptável usando o idioma do computador. A localidade do navegador ajuda a localizar as informações de marca no documento de registro.
1. Para exibir o documento localizado de registro, toque em Gerar visualização. O documento do PDF de registro é gerado e aberto em uma nova guia no seu navegador.

## Localização de um formulário adaptável e seu documento de registro usando Tradução Humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Na tradução humana, o conteúdo é enviado a um provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.

Para tradução, um dicionário contendo arquivos no formato XLIFF é compartilhado com os tradutores profissionais. O dicionário inclui um arquivo XLIFF separado para cada localidade. Cada arquivo XLIFF contém texto que será exibido aos usuários finais e aos espaços reservados para o texto localizado correspondente.

Execute as seguintes etapas para localizar um formulário e seu documento de registro usando Tradutores humanos:

1. [Conecte o AEM com seu provedor de serviços de tradução](/help/sites-administering/tc-tic.md) e [crie configurações da estrutura de integração de tradução](/help/sites-administering/tc-tic.md).

1. [Associe as páginas do seu idioma principal](/help/sites-administering/tc-tic.md) com o serviço de tradução e as configurações da estrutura.

1. [Identifique o tipo de conteúdo](/help/sites-administering/tc-rules.md) para traduzir.

1. [Prepare o conteúdo para tradução](/help/sites-administering/tc-prep.md) criando o idioma principal e as páginas raiz das cópias de idioma.

1. [Crie projetos de tradução](/help/sites-administering/tc-manage.md) para coletar o conteúdo para traduzir e para preparar o processo de tradução.

1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Os componentes de formulário adaptável não suportam idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.
>

