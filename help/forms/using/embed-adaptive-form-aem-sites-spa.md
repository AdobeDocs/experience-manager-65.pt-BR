---
title: Incorpore um formulário adaptável ou a Comunicação interativa no aplicativo de página única do AEM Sites
description: Incorpore formulários adaptáveis ou Comunicação interativa nas páginas do AEM Sites. Os usuários podem preencher e enviar formulários sem sair da página Sites.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 0%

---

# Incorpore um formulário adaptável ou a Comunicação interativa no aplicativo de página única do AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

O AEM Forms permite que desenvolvedores de formulários incorporem formulários adaptáveis e comunicações interativas em um aplicativo de página única (SPA) do AEM Sites. O formulário adaptável incorporado e a Comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário adaptável ou a Comunicação interativa.

No Aplicativo de página única do AEM Sites, é possível adicionar um formulário adaptável ou a Comunicação interativa usando o [Componente de container do AEM Forms SPA](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) [.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) É um componente do AEM Forms para AEM Sites SPA que pode ser adicionado à sua página Sites.

Para obter informações sobre como incorporar um formulário adaptável em um AEM Sites não SPA, consulte [Incorporar um formulário adaptável ou comunicação interativa na página do AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou a Comunicação interativa em um SPA de sites AEM usando o componente de Contêiner AEM Forms SPA, verifique se você instalou:

* Java SE Development Kit 8 ou mais recente
* Apache Maven 3.3.1 ou mais recente
* Instância de autor AEM
* [pacote complementar do AEM Forms 6.4.2](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) na instância do autor

## Instalar o componente de Contêiner do AEM Forms SPA {#install-aem-forms-spa-container-component}

Execute as seguintes etapas para instalar o componente de Contêiner SPA do AEM Forms:

1. [Clonar ou baixar o componente AEM Forms para SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Instale o componente AEM Forms para SPA. As instruções para instalar o componente estão disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   O componente inclui um [componente React de amostra](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) que pode ser usado para integrar o componente do contêiner SPA com um projeto SPA baseado no React.

1. [Clonar ou baixar um projeto do SPA baseado no React](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integre o componente de contêiner SPA a um projeto SPA baseado no React usando as instruções disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor).

   Depois de instalar o componente de Contêiner do AEM Forms SPA e integrar o componente com um projeto SPA baseado no React, você pode incorporar formulários adaptáveis e Comunicações interativas na página do AEM Sites.

## Incorpore um formulário adaptável ou a comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou a Comunicação interativa usando o AEM Forms para o componente de Contêiner SPA:

1. Abra a página de sites do AEM, no modo de edição, na qual você deseja incorporar um formulário adaptável ou a Comunicação interativa.
1. Insira o componente **Formulário AEM para SPA** na página usando uma das seguintes opções:

   * Selecione o contêiner de layout na página Sites, selecione **+** e selecione o componente **Formulário AEM para SPA**.

   * No painel Navegador de componentes, arraste e solte na página o componente **Formulário AEM para SPA**.
   * Procure um formulário adaptável ou Comunicação interativa no navegador Assets e arraste-o para a página Sites. Ele incorpora o formulário em um contêiner de componente AEM Forms for SPA.

   >[!NOTE]
   >
   >A renderização de vários componentes do Contêiner do AEM Forms SPA em uma página não é suportada. Você pode ter vários Containers AEM Forms SPA em uma página, mas apenas um componente é renderizado de cada vez. Para evitar discrepâncias, verifique se apenas um componente está visível em uma página.

1. Selecione o componente de Contêiner de SPA do AEM Forms inserido na página de sites e selecione ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **Editar Contêiner de SPA do AEM Forms** é aberta.
1. Na caixa de diálogo **Editar Contêiner de AEM Forms**, especifique o seguinte:

   * **Tipo de ativo:** selecione o tipo de ativo a ser incorporado. As opções são **Formulário adaptável** e **Comunicação interativa**

   * **Caminho do ativo**: procure e selecione o formulário adaptável ou a Comunicação interativa a ser incorporada. O campo é preenchido automaticamente se um formulário adaptável ou uma Comunicação interativa for inserida usando o navegador Assets.
   * **Canal** (Somente comunicação interativa): selecione o tipo de canal interativo a ser incorporado. As opções são **Canal da Web** e **Canal de Impressão**.

   * **Tema**: selecione um tema que defina o estilo dos componentes do seu formulário adaptável ou da Comunicação interativa. O estilo inclui propriedades de aparência, como estilo da fonte, cor do plano de fundo, dimensões e alinhamento.

1. Selecione ![done_icon](assets/done_icon.png) para salvar as configurações. O formulário adaptável ou a Comunicação interativa agora está incorporado na página.

## Formulário adaptável incorporado do Publish e comunicação interativa {#publish-embedded-adaptive-form-and-interactive-communication}

Considere os seguintes cenários para publicar um ativo incorporado (formulário adaptável ou Comunicação interativa) na página do AEM Sites:

* Se você estiver publicando a página do AEM Sites pela primeira vez e ela incluir um formulário adaptável incorporado ou a Comunicação interativa, publique a página Sites e o ativo incorporado.
* Se você modificou somente o formulário adaptável incorporado ou a Comunicação interativa em uma página do Sites publicada, publique o ativo original e as alterações refletirão na página do Sites publicada. A página Sites publicada inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página Sites e o formulário adaptável incorporado ou a Comunicação interativa, republique a página Sites e o ativo incorporado.

## Modificar o formulário adaptável incorporado e a comunicação interativa {#modify-embedded-adaptive-form-and-interactive-communication}

A página de sites do AEM mantém uma referência ao formulário adaptável e à Comunicação interativa no AEM Forms Container. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no formulário adaptável original e na Comunicação interativa são mantidas no formulário adaptável incorporado e na Comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptável incorporado e da Comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou Comunicação interativa nos respectivos editores e modifique-os.
* Selecione o formulário adaptável ou a Comunicação interativa na página Sites no modo de edição e selecione **Editar em uma nova janela**. O formulário original é aberto no modo de edição.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não estão incluídos no formulário incorporado.
* Os rascunhos e envios de formulários incorporados pelo usuário são suportados e ficam visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página Sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.
