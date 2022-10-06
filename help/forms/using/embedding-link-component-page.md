---
title: Como incorporar o componente de link em uma página
seo-title: Embedding link component in a page
description: Você pode usar o componente de link para vincular um documento adaptável ou um formulário adaptável de qualquer página.
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Como incorporar o componente de link em uma página{#embedding-link-component-in-a-page}

## Pré-requisitos {#prerequisites}

O componente de link é um membro da categoria Serviços de documento . Certifique-se de que a categoria Serviços de documento esteja visível no navegador de componentes do AEM. Se a categoria não estiver listada, siga as etapas listadas em [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md).

## Componente de link {#link-component}

O componente Link permite que os autores do portal de formulários criem um link para um formulário adaptável de qualquer lugar em uma página. O componente Link está disponível na seção Serviços de documento no navegador de componentes.

Execute as seguintes etapas para adicionar um componente Link à página:

1. Arraste o **Link** na página. Selecione o componente e toque em ![cmppr](assets/cmppr.png). A caixa de diálogo Editar componente de link é aberta.

   ![editar-link-componente](assets/edit-link-component.png)

1. No **Exibir** , especifique o seguinte:

   * **Legenda do link**: Texto ou legenda do link.
   * **Dica de ferramenta do link**: Dica de ferramenta do link.
   * **Modelo de layout**: Modelo para o layout do componente Link.

1. Abra o **Informações do ativo** e especifique o tipo do ativo. Um ativo pode ser um **formulário**. Dependendo do tipo de ativo selecionado, as opções listadas abaixo são exibidas:

   * **Caminho do ativo**: Caminho do repositório no qual o ativo é armazenado.

   * **Tipo de renderização**: O formato de renderização — PDF, HTML ou Auto. O tipo de renderização automática detecta o ambiente do usuário e, de acordo, renderiza o formulário como HTML ou PDF. Por exemplo, se o formulário for acessado de um dispositivo móvel, o tipo de renderização automática renderizará o formulário no HTML.
   * **Enviar URL:**  URL para o servlet onde os dados do formulário são enviados.
   * **Perfil de HTML**: Perfil para renderizar o formulário como HTML.
   * **Perfil de PDF**: Perfil para renderizar o formulário como documento PDF.

1. Abra a guia **Avançado.** Você pode especificar os parâmetros adicionais no formato do par de valores chave. Quando o link é clicado, esses parâmetros adicionais e são transmitidos com o formulário.

   Toque **Concluído** para salvar a configuração.

## Práticas recomendadas para usar o componente Link {#best-practices-for-using-link-component-br}

* Certifique-se de selecionar PDF como o tipo de renderização se o caminho especificado no Caminho do formulário apontar para um documento que tenha PDF como o formato de renderização permitido.
* O URL de envio para um formulário pode ser especificado em vários locais e sua ordem de precedência é a seguinte:

   1. O URL de envio incorporado no formulário (no botão Enviar) tem a prioridade mais alta.
   1. O URL de envio mencionado no Forms Manager tem a prioridade média.
   1. O URL de envio mencionado no portal de formulários tem a prioridade mais baixa.
