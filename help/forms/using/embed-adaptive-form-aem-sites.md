---
title: Incorporar um formulário adaptável ou comunicação interativa AEM página de sites
seo-title: Incorporar um formulário adaptável ou comunicação interativa AEM página de sites
description: É possível incorporar formulários adaptáveis AEM páginas de sites. Os usuários podem preencher e enviar formulários sem sair das páginas do site.
seo-description: É possível incorporar formulários adaptáveis AEM páginas de sites. Os usuários podem preencher e enviar formulários sem sair das páginas do site.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---


# Incorporar um formulário adaptável ou comunicação interativa AEM página de sites {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Visão geral {#overview}

A AEM Forms permite que os desenvolvedores de formulários incorporem sem problemas formulários adaptativos e comunicações interativas em uma página do AEM Sites ou em uma página da Web hospedada fora do AEM. O formulário adaptativo incorporado e a comunicação interativa estão totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário ou a comunicação interativa.

Para obter informações sobre como incorporar um formulário adaptável em uma página da Web externa, consulte [Incorporar formulário adaptável em uma página](/help/forms/using/embed-adaptive-form-external-web-page.md)da Web externa.

Na página do AEM Sites, é possível adicionar um formulário adaptável ou uma comunicação interativa usando:

* **[Componente](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)** do Container AEM Forms A AEM Forms fornece um componente que você pode adicionar às páginas do site. O componente Container AEM Forms permite incorporar um formulário adaptável e uma comunicação interativa.

* **[Navegador](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)** de ativos Todos os formulários e comunicações interativas que você cria estão disponíveis em Ativos. Você pode arrastar e soltar o formulário como um ativo na sua página.

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou uma comunicação interativa em uma página de sites AEM que usa um modelo editável, verifique se o componente de Formulário AEM está configurado como um componente permitido no modelo associado. Para obter mais informações, consulte a seção **Política e propriedades (Container de layout)** em [Criação de modelos](/help/sites-authoring/templates.md)de página.

No caso de uma página Sites usando um modelo estático, é necessário configurá-la no sistema de parágrafo da página do site. Para obter mais informações, Consulte [Configuração dos componentes no modo de Design](/help/sites-authoring/default-components-designmode.md).

## Como incorporar um formulário adaptável ou comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou comunicação interativa usando o componente de Container AEM Forms:

1. Abra a página AEM sites, no modo de edição, na qual você deseja incorporar um formulário adaptável ou uma comunicação interativa.
1. No painel Navegador de componentes, arraste e solte o componente do Container AEM Forms na página.

   Como alternativa, você pode procurar um formulário adaptável ou uma comunicação interativa no navegador Ativos e arrastá-lo e soltá-lo na página Sites. Ele incorpora o formulário a um Container AEM Forms.

   >[!NOTE]
   >
   >Não há suporte para vários componentes de Container AEM Forms em uma página.

1. Toque no componente de Container AEM Forms incorporado na página de sites e, em seguida, toque em ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **[!UICONTROL Editar Container]** AEM Forms é aberta.
1. Na caixa de diálogo Editar Container AEM Forms, especifique o seguinte.

   * **Tipo de ativo:** Selecione o tipo de ativo a ser incorporado. As opções são forma adaptável e comunicação interativa
   * **Caminho** do ativo: Procure e selecione o formulário adaptável ou a comunicação interativa a ser incorporada. Ele é preenchido automaticamente se você soltou do navegador Ativos.
   * (Somente formulário adaptável) Envio **de publicação**: Selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.

      * **Mensagem** de agradecimento: Grave uma mensagem usando o editor de rich text para mostrar no envio do formulário. Esta opção está disponível somente quando você escolhe mostrar uma mensagem de agradecimento.
      * **Página** de agradecimento: Navegue e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
      * **Atualizar página no envio**: Ative para atualizar a página que contém o formulário adaptável incorporado para mostrar a página de agradecimentos. Caso contrário, a página de agradecimentos substituirá o formulário adaptável no container AEM Forms, sem atualizar a página. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
   * **Tema**: Selecione um tema que defina o estilo para os componentes do formulário adaptável ou da comunicação interativa. O estilo inclui propriedades de aparência como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.
   * **Altura**: Especifique a altura do container. Deixe em branco para redimensionar automaticamente o container.
   * **Biblioteca** do cliente CSS: Especifique o caminho para uma biblioteca de cliente CSS.


1. Salve as configurações. O formulário adaptável ou a comunicação interativa agora está incorporado na página.

## Publicação de formulários adaptativos incorporados e comunicação interativa {#publishing-embedded-adaptive-form-and-interactive-communication}

Considere os seguintes cenários para a publicação de um ativo incorporado (formulário adaptável ou comunicação interativa) AEM página de sites:

* Se você estiver publicando a página de sites AEM pela primeira vez e ela incluir um formulário adaptável incorporado ou uma comunicação interativa, publique a página de sites e o ativo incorporado.
* Se você modificou apenas o formulário adaptativo incorporado ou a comunicação interativa em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicado. A página do site publicada inclui uma referência ao ativo e não exige a republicação da página.
* Se você modificou a página de sites e o formulário adaptativo incorporado ou a comunicação interativa, publique novamente a página de sites e o ativo incorporado.

## Modificação de formulários adaptativos incorporados e comunicação interativa {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM página de sites mantém uma referência ao formulário adaptável e à comunicação interativa no Container AEM Forms. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no formulário adaptativo original e a comunicação interativa são retidas no formulário adaptativo incorporado e na comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptável incorporado e da comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou comunicação interativa nos respectivos editores e modifique-os.
* Toque no formulário adaptável ou na comunicação interativa na página do site no modo de edição e toque em **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que você pode modificar.

>[!NOTE]
>
>As alterações feitas na forma adaptativa original ou na comunicação interativa refletem automaticamente no formulário incorporado. Entretanto, publique novamente o formulário adaptável, a comunicação interativa ou a página do site para refletir as alterações na página publicada.

## Considerations and best practices {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptativos em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms Submetidos no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página de sites para apresentar formulários diferentes com base em perfis do usuário.
* Se a Adobe Analytics estiver configurada para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, ele não está disponível no relatório de análise de formulários.

