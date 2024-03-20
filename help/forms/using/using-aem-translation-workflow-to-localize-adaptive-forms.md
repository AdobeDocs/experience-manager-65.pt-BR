---
title: Uso do fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documentos de registro
description: Saiba como usar fluxos de trabalho de tradução do AEM para localizar formulários adaptáveis e documentos de registro.
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms, Foundation Components
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 14%

---

# Uso do fluxo de trabalho de tradução do AEM para localizar formulários adaptáveis e documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Os formulários localizados ajudam você a atender um público-alvo maior em todas as regiões geográficas. O fluxo de trabalho de tradução do Adobe Experience Manager ajuda a localizar formulários adaptáveis e seus documentos de registro. Você pode usar **tradução automática** ou **tradutores humanos** para localizar um formulário adaptável.

Este artigo explica o processo de uso do fluxo de trabalho de tradução do AEM com formulários adaptáveis e documentos de registro.

## Localizar um formulário adaptável e um documento de registro usando a tradução automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

O serviço de tradução automática traduz imediatamente seu conteúdo em forma adaptável e documento de registro. O AEM Forms é pré-configurado para usar uma versão de avaliação do Microsoft Translator para tradução automática. Execute as seguintes etapas para habilitar a tradução automática dos formulários adaptáveis e do documento de registro:

1. Na interface do usuário do AEM Forms, selecione um formulário e selecione a **Adicionar dicionário** opção.
1. Entrada **Adicionar dicionário ao projeto de tradução** , selecione a **Criar um novo projeto de tradução** ou **Adicionar a um projeto de tradução existente** opção.
1. No **Título do projeto** especifique o título. Por exemplo, `Government Reference Site - German locale.`
1. No **Idiomas de destino** especifique um local (Por exemplo, `German(de)`) e clique em **Concluído**. Você pode especificar várias localidades. O formulário é traduzido para todas as localidades especificadas no **Idiomas de destino** campo.
1. Na caixa de diálogo Dicionário adicionado, clique em **Abrir Projetos**. Na tela Projetos, abra o projeto recém-criado.
1. Clique em **reticências** na parte inferior do **Resumo da tradução** bloco. A tela Resumo da tradução é aberta.
1. Clique em **Editar** ícone na parte superior do **Resumo da tradução** tela. Abra o **Tradução** e selecione Tradução automática na guia **Método de tradução** tela. Selecione o apropriado **Provedor de tradução** e **Configuração na nuvem**. Clique em **Concluído** no topo da tela.
1. No **Tarefa de tradução** lado a lado, clique no link ![aem62forms_downarrow](assets/aem62forms_downarrow.png) e clique em **Início**. O status do bloco muda para Rascunho. Na conclusão da tradução, o status muda para **Pronto para revisão**. Atualize a página após alguns minutos e verifique o status.
1. Depois que o status for alterado para **Pronto para revisão** no **Tarefa de tradução** bloco, abra o formulário em uma janela do navegador. Uma versão localizada do formulário é exibida.

   >[!NOTE]
   >
   >* Antes de abrir a versão localizada do formulário na janela do navegador, verifique se a localidade do navegador está definida para corresponder à localidade do formulário. Por exemplo, se o formulário for traduzido para o idioma alemão (de), defina o local do navegador como alemão (de).
   >* Os componentes do formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.

   Juntamente com o formulário adaptável, o documento de registro gerado automaticamente também é localizado.

   Para obter mais informações sobre configurações e configurações do documento de registro, consulte:

[Documento de configuração modelo de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configurações do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalizar as informações de marca do documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) e certifique-se de que a localidade do navegador esteja definida com o mesmo idioma para o qual você localizou o Formulário adaptável usando o idioma do computador. A localidade do navegador ajuda a localizar as informações de marca no documento de registro.
1. Para exibir o documento de registro localizado, selecione Gerar visualização. O documento do PDF de registro é gerado e aberto em uma nova guia no navegador.

## Localizar um formulário adaptável e seu documento de registro usando a Tradução humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

Na Tradução humana, o conteúdo é enviado a um provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.

Para tradução, um dicionário contendo arquivos no formato XLIFF é compartilhado com os tradutores profissionais. O dicionário inclui um arquivo XLIFF separado para cada localidade. Cada arquivo XLIFF contém texto que será exibido aos usuários finais e espaços reservados para o texto localizado correspondente.

Execute as seguintes etapas para localizar um formulário e seu documento de registro usando Tradutores Humanos:

1. [Conecte o AEM com seu provedor de serviços de tradução](/help/sites-administering/tc-tic.md) e [crie configurações da estrutura de integração de tradução](/help/sites-administering/tc-tic.md).

1. [Associe as páginas do seu idioma principal](/help/sites-administering/tc-tic.md) com o serviço de tradução e as configurações da estrutura.

1. [Identifique o tipo de conteúdo](/help/sites-administering/tc-rules.md) para traduzir.

1. [Prepare o conteúdo para tradução](/help/sites-administering/tc-prep.md) criando o idioma principal e as páginas raiz das cópias de idioma.

1. [Crie projetos de tradução](/help/sites-administering/tc-manage.md) para coletar o conteúdo para traduzir e para preparar o processo de tradução.

1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Os componentes do formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.
>
