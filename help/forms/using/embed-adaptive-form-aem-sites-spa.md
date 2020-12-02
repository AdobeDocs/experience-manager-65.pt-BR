---
title: Incorporar um formulário adaptável ou Comunicação interativa no aplicativo de página única AEM Sites
seo-title: Incorporar formulários adaptativos ou Comunicações interativas em páginas do AEM Sites
description: Incorpore formulários adaptativos ou Comunicação interativa em páginas do AEM Sites. Os usuários podem preencher e enviar formulários sem sair da página Sites.
seo-description: É possível incorporar formulários adaptáveis ou Comunicação interativa em páginas do AEM Sites. Os usuários podem preencher e enviar formulários sem sair da página Sites.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Incorporar um formulário adaptável ou uma Comunicação interativa no aplicativo de página única da AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Visão geral {#overview}

A AEM Forms permite que desenvolvedores de formulários incorporem sem problemas formulários adaptativos e Comunicações interativas em um aplicativo de página única (SPA) da AEM Sites. O formulário adaptativo incorporado e a Comunicação interativa estão totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário adaptável ou com a Comunicação interativa.

No aplicativo de página única da AEM Sites, é possível adicionar um formulário adaptável ou uma Comunicação interativa usando o [componente de Container do AEM Forms SPA](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) É um componente AEM Forms para o AEM Sites SPA que você pode adicionar à página Sites.

Para obter informações sobre como incorporar um formulário adaptável em um AEM Sites não SPA, consulte [Incorporar um formulário adaptável ou comunicação interativa na página do AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou uma Comunicação interativa em AEM sites SPA usando o componente de Container do AEM Forms SPA, verifique se você instalou:

* Java SE Development Kit 8 ou mais recente
* Apache Maven 3.3.1 ou mais recente
* instância do autor AEM
* [Instância do autor do ](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) pacote suplementar AEM Forms 6.4.2

## Instalar o componente de Container do AEM Forms SPA {#install-aem-forms-spa-container-component}

Execute as seguintes etapas para instalar o componente do Container AEM Forms SPA:

1. [Clonar ou baixar o componente AEM Forms para SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Instale o componente AEM Forms para SPA. As instruções para instalar o componente estão disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   O componente inclui um [componente React de amostra](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) que pode ser usado para integrar SPA componente de container a um projeto SPA baseado em React.

1. [Clonar ou baixar um projeto](https://github.com/adobe/aem-sample-we-retail-journal) de SPA baseado em React.
1. Integre SPA componente de container a um projeto SPA baseado em React usando as instruções disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor).

   Depois de instalar o componente do Container AEM Forms SPA e integrar o componente a um projeto SPA baseado em React, você pode incorporar formulários adaptáveis e Comunicações interativas na página do AEM Sites.

## Incorporar um formulário adaptável ou Comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou uma Comunicação interativa usando o AEM Forms para SPA componente de Container:

1. Abra a página AEM sites, no modo de edição, na qual você deseja incorporar um formulário adaptável ou uma Comunicação interativa.
1. Insira o **AEM Formulário para SPA** componente na página usando qualquer uma das seguintes opções:

   * Toque no container de layout na página Sites, toque em **+** e selecione o **AEM Formulário para SPA** componente.

   * No painel Navegador de componentes, arraste e solte o **AEM Formulário para o componente SPA** na página.
   * Procure um formulário adaptável ou Comunicação interativa no navegador Ativos e arraste-o e solte-o na página Sites. Ele incorpora o formulário em um AEM Forms para SPA container de componente.

   >[!NOTE]
   >
   >Não há suporte para a renderização de vários componentes do Container AEM Forms SPA em uma página. Você pode ter vários Container SPA do AEM Forms em uma página, mas apenas um componente é renderizado de cada vez. Certifique-se de que apenas um componente esteja visível em uma página para evitar discrepâncias.

1. Toque no componente de Container AEM Forms SPA incorporado na página de sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **Editar Container SPA do AEM Forms** é aberta.
1. Na caixa de diálogo **Editar Container AEM Forms**, especifique o seguinte:

   * **Tipo de ativo:** selecione o tipo de ativo a ser incorporado. As opções são **Formulário adaptável** e **Comunicação interativa**

   * **Caminho** do ativo: Procure e selecione o formulário adaptável ou a Comunicação interativa a ser incorporada. O campo será preenchido automaticamente se um formulário adaptável ou Comunicação interativa for inserido usando o navegador Ativos.
   * **Canal**  (somente comunicação interativa): Selecione o tipo de canal interativo a ser incorporado. As opções são **Canal da Web** e **Canal de impressão**.

   * **Tema**: Selecione um tema que defina o estilo para os componentes do formulário adaptável ou da Comunicação interativa. O estilo inclui propriedades de aparência como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.

1. Toque em ![done_icon](assets/done_icon.png) para salvar as configurações. O formulário adaptável ou a Comunicação interativa agora está incorporado na página.

## Publicar formulário adaptável incorporado e Comunicação interativa {#publish-embedded-adaptive-form-and-interactive-communication}

Considere os seguintes cenários para publicar um ativo incorporado (formulário adaptável ou Comunicação interativa) na página do AEM Sites:

* Se você estiver publicando a página do AEM Sites pela primeira vez e ela incluir um formulário adaptável incorporado ou uma Comunicação interativa, publique a página Sites e o ativo incorporado.
* Se você modificou apenas o formulário adaptativo incorporado ou a Comunicação interativa em uma página de Sites publicada, publique o ativo original e as alterações refletirão na página de Sites publicados. A página Sites publicada inclui uma referência ao ativo e não exige a republicação da página.
* Se você modificou a página Sites e o formulário adaptativo incorporado ou a Comunicação interativa, publique novamente a página Sites e o ativo incorporado.

## Modificar formulário adaptável incorporado e Comunicação interativa {#modify-embedded-adaptive-form-and-interactive-communication}

AEM página de sites mantém uma referência ao formulário adaptável e Comunicação interativa no Container AEM Forms. Portanto, todas as configurações e propriedades, como o tema, os estilos e a ação de envio, configuradas no formulário adaptativo original e a Comunicação interativa são retidas no formulário adaptativo incorporado e na Comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptativo incorporado e da Comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou em Comunicação interativa nos respectivos editores e modifique-os.
* Toque no formulário adaptável ou em Comunicação interativa na página Sites no modo de edição e toque em **Editar em uma nova janela**. O formulário original é aberto no modo de edição.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptativos em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms Submetidos no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página Sites para apresentar diferentes formulários com base em perfis do usuário.
* Se a Adobe Analytics estiver configurada para o formulário original, os dados de análise do formulário incorporado serão capturados no Adobe Analytics. No entanto, ele não está disponível no relatório de análise de formulários.

