---
title: Usar o fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro
seo-title: Usar o fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro
description: Saiba como usar fluxos de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro.
seo-description: Saiba como usar fluxos de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Usar o fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documento de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Os formulários localizados ajudam você a oferecer um público maior em várias regiões geográficas. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar formulários adaptáveis e seus documentos de registro. Você pode usar tradução **** automática ou tradutores **** humanos para localizar um formulário adaptável.

Este artigo explica o processo para usar o fluxo de trabalho de tradução do AEM com formulários adaptáveis e documentos de registro.

## Localização de um formulário adaptável e de um documento de registro usando tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática imediatamente traduz seu conteúdo em forma adaptável e documento de registro. O AEM Forms está pré-configurado para usar uma versão de avaliação do Microsoft Translator para tradução automática. Execute as seguintes etapas para habilitar a tradução automática para seus formulários adaptativos e o documento de registro:

1. Na interface do usuário do AEM Forms, selecione um formulário e toque na opção **Adicionar dicionário** .
1. Na tela **Adicionar dicionário ao projeto** de tradução, selecione a opção **Criar um novo projeto** de tradução ou **Adicionar a um projeto** de tradução existente.
1. No campo Título **do** projeto, especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No campo Idiomas **de** destino, especifique uma localidade (por exemplo, `German(de)`) e clique em **Concluído**. É possível especificar várias localidades. O formulário é convertido em todas as localidades especificadas no campo Idiomas **de** destino.
1. Na caixa de diálogo Dicionário adicionado, clique em **Abrir projetos**. Na tela Projetos, abra o projeto recém-criado.
1. Clique nas **elipses** na parte inferior do bloco Resumo **da** tradução. A tela Resumo da tradução é aberta.
1. Clique no ícone **Editar** na parte superior da tela **Resumo** da tradução. Abra a guia **Tradução** e selecione Tradução automática na tela Método **de** tradução. Selecione o Provedor **de** tradução e a Configuração **da** nuvem apropriados. Click the **Done** icon at the top of the screen.
1. No bloco Trabalho **de** tradução, clique no ícone ![aem62forms_downseta](assets/aem62forms_downarrow.png) e clique em **Iniciar**. O status do bloco muda para Rascunho. Após a conclusão da tradução, o status é alterado para **Pronto para revisão**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Pronto para revisão** no bloco Trabalho **de** tradução, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão(de), defina a localidade do navegador como alemão(de).
   >* Os componentes de formulário adaptáveis não suportam os idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.


   Junto com o formulário Adaptive, o documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do Documento de Registro, consulte:

   [Documento de configuração modelo de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Configurações do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalize as informações de marca do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e verifique se a localidade do navegador está definida para o mesmo idioma no qual você localizou o Formulário adaptativo usando o idioma da máquina. A localidade do navegador ajuda a localizar as informações de marca no documento de registro.
1. Para exibir o documento localizado do registro, toque em Gerar visualização. O documento de registro PDF é gerado e aberto em uma nova guia no navegador.

## Localização de um formulário adaptável e de seu documento de registro usando a Tradução Humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Na tradução humana, o conteúdo é enviado a um provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo convertido é retornado e importado para o AEM. Quando seu provedor de tradução está integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.

Para tradução, um dicionário que contém arquivos no formato XLIFF é compartilhado com os tradutores profissionais. O dicionário inclui um arquivo XLIFF separado para cada localidade. Cada arquivo XLIFF contém texto que será exibido para os usuários finais e os espaços reservados para o texto localizado correspondente.

Execute as seguintes etapas para localizar um formulário e seu documento de registro usando o Human Translators:

1. [Conecte o AEM ao seu provedor](/help/sites-administering/tc-tic.md) de serviços de tradução e [crie configurações](/help/sites-administering/tc-tic.md)de estrutura de integração de tradução.

1. [Associe as páginas do seu idioma mestre](/help/sites-administering/tc-tic.md) ao serviço de tradução e às configurações de estrutura.

1. [Identifique o tipo de conteúdo](/help/sites-administering/tc-rules.md) a ser traduzido.

1. [Prepare o conteúdo para tradução](/help/sites-administering/tc-prep.md) criando o idioma mestre e as páginas raiz das cópias de idioma.

1. [Crie projetos](/help/sites-administering/tc-manage.md) de tradução para coletar o conteúdo para traduzir e preparar o processo de tradução.

1. Use os projetos de tradução para [gerenciar o processo](/help/sites-administering/tc-manage.md)de tradução de conteúdo.

>[!NOTE]
>
>* Os componentes de formulário adaptáveis não suportam os idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.
>



