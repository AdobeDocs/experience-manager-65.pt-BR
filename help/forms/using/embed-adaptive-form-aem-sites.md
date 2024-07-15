---
title: Incorpore um formulário adaptável ou comunicação interativa na página de sites AEM
description: É possível incorporar formulários adaptáveis em páginas de sites AEM. Os usuários podem preencher e enviar formulários sem sair das páginas do site.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
feature: Adaptive Forms,Foundation Components
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 1%

---

# Incorpore um formulário adaptável ou comunicação interativa na página de sites AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-aem-sites.html) |
| AEM 6.5 | Este artigo |


## Visão geral {#overview}

O AEM Forms permite que desenvolvedores de formulários incorporem formulários adaptáveis e comunicações interativas em uma página do AEM Sites ou página da Web hospedada fora do AEM. O formulário adaptável incorporado e a comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário ou a comunicação interativa.

Para obter informações sobre como incorporar um formulário adaptável em uma página da Web externa, consulte [Incorporar formulário adaptável na página da Web externa](/help/forms/using/embed-adaptive-form-external-web-page.md).

Na página AEM Sites, é possível adicionar um formulário adaptável ou comunicação interativa usando:

* **[Componente de Contêiner do AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
O AEM Forms fornece um componente que pode ser adicionado às páginas do site. O componente de Contêiner do AEM Forms permite incorporar um formulário adaptável e a comunicação interativa.

* **[Navegador de ativos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos os formulários e comunicações interativas criados estão disponíveis no Assets. Você pode arrastar e soltar o formulário como um ativo na página.

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou comunicação interativa em uma página de sites AEM que use um modelo editável, verifique se o componente de Formulário AEM está configurado como um componente permitido no modelo associado. Para obter mais informações, consulte a seção **Política e propriedades (Contêiner de layout)** em [Criando modelos de página](/help/sites-authoring/templates.md).

Se houver uma página do Sites usando um modelo estático, será necessário configurá-la no sistema de parágrafo da página do site. Consulte [Configurando Componentes no Modo de Design](/help/sites-authoring/default-components-designmode.md) para obter mais informações.

## Incorporação de um formulário adaptável ou comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou a comunicação interativa usando o componente de Contêiner do AEM Forms:

1. Abra a página de sites do AEM, no modo de edição, em que você deseja incorporar um formulário adaptável ou uma comunicação interativa.
1. No painel Navegador de componentes, arraste e solte o componente Contêiner do AEM Forms na página.

   Como alternativa, você pode pesquisar um formulário adaptável ou comunicação interativa no navegador Assets e arrastá-lo e soltá-lo na página Sites. Ele incorpora o formulário em um Contêiner do AEM Forms.

   >[!NOTE]
   >
   >Não há suporte para vários componentes do AEM Forms Container em uma página.

1. Selecione o componente de Contêiner do AEM Forms inserido na página de sites e selecione ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **[!UICONTROL Editar Contêiner do AEM Forms]** é aberta.
1. Na caixa de diálogo Editar contêiner do AEM Forms, especifique o seguinte.

   * **Tipo de ativo:** selecione o tipo de ativo a ser incorporado. As opções são o formulário adaptável e a comunicação interativa
   * **Caminho do ativo**: procure e selecione o formulário adaptável ou a comunicação interativa a ser incorporada. Ela será preenchida automaticamente se você soltá-la no navegador Assets.
   * (Somente formulário adaptável) **Envio de Post**: selecione a ação a ser acionada no envio do formulário. Você pode optar por mostrar uma mensagem de agradecimento ou uma página de agradecimento.

      * **Mensagem de agradecimento**: escreva uma mensagem usando o editor de rich text para mostrar no envio do formulário. Essa opção está disponível somente quando você opta por mostrar uma mensagem de agradecimento.
      * **Página de Agradecimento**: procure e selecione a página a ser exibida no envio do formulário. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.
      * **Atualizar Página no Envio**: habilite essa opção para que você possa atualizar a página que contém o formulário adaptável inserido para mostrar a página de agradecimento. Caso contrário, a página de agradecimento substituirá o formulário adaptável no container do AEM Forms, sem atualizar a página. Essa opção está disponível somente quando você escolhe mostrar uma página de agradecimento.

   * **Tema**: selecione um tema que defina o estilo dos componentes do formulário adaptável ou da comunicação interativa. O estilo inclui propriedades de aparência, como estilo da fonte, cor do plano de fundo, dimensões e alinhamento.
   * **Altura**: especifique a altura do container. Deixe em branco para redimensionar automaticamente o contêiner.
   * **Biblioteca do cliente CSS**: especifique o caminho para uma biblioteca do cliente CSS.

1. Salve as configurações. O formulário adaptável ou a comunicação interativa agora está incorporada na página.

## Publicação de formulários adaptáveis incorporados e comunicação interativa {#publishing-embedded-adaptive-form-and-interactive-communication}

Considere os seguintes cenários para publicar um ativo incorporado (formulário adaptável ou comunicação interativa) na página de sites AEM:

* Se você estiver publicando a página de sites do AEM pela primeira vez e ela incluir um formulário adaptável incorporado ou comunicação interativa, publique a página de sites e o ativo incorporado.
* Se você modificou somente o formulário adaptável incorporado ou a comunicação interativa em uma página do site publicada, publique o ativo original e as alterações refletirão na página do site publicada. A página do site publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página de sites e o formulário adaptável incorporado ou a comunicação interativa, publique novamente a página de sites e o ativo incorporado.

## Modificação de formulários adaptáveis incorporados e da comunicação interativa {#modifying-embedded-adaptive-form-and-interactive-communication}

A página de sites do AEM mantém uma referência ao formulário adaptável e à comunicação interativa no AEM Forms Container. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no formulário adaptável original e na comunicação interativa são mantidas no formulário adaptável incorporado e na comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptável incorporado e da comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou comunicação interativa nos respectivos editores e modifique-os.
* Selecione o formulário adaptável ou a comunicação interativa na página do site no modo de edição e selecione **[!UICONTROL Editar em uma nova janela]**. O formulário original é aberto no modo de edição que você pode modificar.

>[!NOTE]
>
>As mudanças feitas no formulário adaptável original ou na comunicação interativa refletem automaticamente no formulário incorporado. No entanto, publique novamente o formulário adaptável, a comunicação interativa ou a página do site para refletir as alterações na página publicada.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não estão incluídos no formulário incorporado.
* Os rascunhos e envios de formulários incorporados pelo usuário são suportados e ficam visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página de sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.
