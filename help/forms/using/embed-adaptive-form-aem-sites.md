---
title: Incorporar um formulário adaptável ou comunicação interativa AEM página de sites
seo-title: Embed an adaptive form or interactive communication in AEM sites page
description: Você pode incorporar formulários adaptáveis em páginas de sites AEM. Os usuários podem preencher e enviar formulários sem sair das páginas do site.
seo-description: You can embed adaptive forms in AEM sites pages. Users can fill and submit forms without leaving the site pages.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
feature: Adaptive Forms
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Incorporar um formulário adaptável ou comunicação interativa AEM página de sites {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Visão geral {#overview}

O AEM Forms permite que desenvolvedores de formulários incorporem, sem interrupções, formulários adaptáveis e comunicações interativas em uma página do AEM Sites ou em uma página da Web hospedada fora do AEM. O formulário adaptável incorporado e a comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário ou a comunicação interativa.

Para obter informações sobre como incorporar um formulário adaptável em uma página da Web externa, consulte [Incorporar formulários adaptáveis à página da Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).

Na página AEM Sites, é possível adicionar um formulário adaptável ou uma comunicação interativa usando:

* **[Componente Contêiner do AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
O AEM Forms fornece um componente que pode ser adicionado às páginas do site. O componente Contêiner do AEM Forms permite que você incorpore um formulário adaptável e uma comunicação interativa.

* **[Navegador de ativos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos os formulários e comunicações interativas criados estão disponíveis em Ativos. Você pode arrastar e soltar o formulário como um ativo na página.

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou uma comunicação interativa em uma página de sites de AEM que use um modelo editável, verifique se o componente Formulário de AEM está configurado como um componente permitido no modelo associado. Para obter mais informações, consulte **Política e propriedades (contêiner de layout)** seção em [Criação de modelos de página](/help/sites-authoring/templates.md).

No caso de uma página Sites usando um modelo estático, é necessário configurá-la no sistema de parágrafo da página do site. Para obter mais informações, Consulte [Configuração dos componentes no modo de Design](/help/sites-authoring/default-components-designmode.md).

## Como incorporar um formulário adaptável ou comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou uma comunicação interativa usando o componente Contêiner do AEM Forms:

1. Abra a página AEM sites, no modo de edição, na qual deseja incorporar um formulário adaptável ou uma comunicação interativa.
1. No painel Navegador de componentes , arraste e solte o componente Contêiner do AEM Forms na página.

   Como alternativa, você pode pesquisar um formulário adaptável ou uma comunicação interativa no navegador Ativos e arrastar e soltar na página Sites . Ele incorpora o formulário em um Contêiner do AEM Forms.

   >[!NOTE]
   >
   >Vários componentes do contêiner do AEM Forms em uma página não são compatíveis.

1. Toque no componente AEM Forms Container incorporado na página Sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. O **[!UICONTROL Editar contêiner do AEM Forms]** será aberta.
1. Na caixa de diálogo Editar contêiner do AEM Forms , especifique o seguinte.

   * **Tipo de ativo:** Selecione o tipo de ativo a ser incorporado. As opções são forma adaptável e comunicação interativa
   * **Caminho do ativo**: Navegue e selecione o formulário adaptável ou a comunicação interativa a ser incorporada. Ele é preenchido automaticamente se você soltou no navegador Ativos.
   * (Somente formulário adaptável) **Pós-envio**: Selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.

      * **Mensagem de agradecimento**: Escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
      * **Página de agradecimento**: Navegue e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
      * **Atualizar página no envio**: Permita atualizar a página que contém o formulário adaptável incorporado para mostrar a página de agradecimento. Caso contrário, a página de agradecimento substituirá o formulário adaptável no contêiner do AEM Forms, sem atualizar a página. Essa opção está disponível somente quando você opta por mostrar uma página de agradecimento.
   * **Tema**: Selecione um tema que defina o estilo de componentes do formulário adaptável ou da comunicação interativa. O estilo inclui propriedades de aparência, como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.
   * **Altura**: Especifique a altura do contêiner. Deixe em branco para redimensionar automaticamente o contêiner.
   * **Biblioteca de clientes CSS**: Especifique o caminho para uma biblioteca de cliente CSS.


1. Salve as configurações. O formulário adaptável ou a comunicação interativa agora está incorporado na página.

## Publicação de formulário adaptável incorporado e comunicação interativa {#publishing-embedded-adaptive-form-and-interactive-communication}

Vamos considerar os seguintes cenários para a publicação de um ativo incorporado (formulário adaptável ou comunicação interativa) AEM página de sites:

* Se você estiver publicando a página AEM sites pela primeira vez e ela incluir um formulário adaptável incorporado ou uma comunicação interativa, publique a página sites e o ativo incorporado.
* Se você modificou apenas o formulário adaptável incorporado ou a comunicação interativa em uma página de site publicada, publique o ativo original e as alterações refletirão na página de site publicada. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o formulário adaptável incorporado ou a comunicação interativa, republique a página de sites e o ativo incorporado.

## Modificação de formulários adaptáveis incorporados e comunicação interativa {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM página de sites mantém uma referência ao formulário adaptável e à comunicação interativa no Contêiner do AEM Forms. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no formulário adaptável original e a comunicação interativa são retidas no formulário adaptável incorporado e na comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptável incorporado e da comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou comunicação interativa em seus respectivos editores e modifique-o.
* Toque no formulário adaptável ou na comunicação interativa na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que pode ser modificado.

>[!NOTE]
>
>As alterações feitas no formulário adaptável original ou na comunicação interativa refletem automaticamente no formulário incorporado. No entanto, republique o formulário adaptável, a comunicação interativa ou a página do site para refletir as alterações na página publicada.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página de sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados analíticos do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.
