---
title: Incorpore um formulário adaptável ou uma Comunicação interativa no aplicativo de página única do AEM Sites
seo-title: Incorporar formulários adaptáveis ou Comunicações interativas nas páginas do AEM Sites
description: Incorporar formulários adaptáveis ou Comunicação interativa em páginas do AEM Sites. Os usuários podem preencher e enviar formulários sem sair da página Sites .
seo-description: É possível incorporar formulários adaptáveis ou Comunicação interativa em páginas do AEM Sites. Os usuários podem preencher e enviar formulários sem sair da página Sites .
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Incorpore um formulário adaptável ou uma Comunicação interativa no aplicativo de página única do AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Visão geral {#overview}

O AEM Forms permite que desenvolvedores de formulários incorporem, sem interrupções, formulários adaptáveis e Comunicações interativas em um aplicativo de página única (SPA) da AEM Sites. O formulário adaptável incorporado e a Comunicação interativa são totalmente funcionais e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário adaptável ou a Comunicação interativa.

No Aplicativo de página única do AEM Sites, é possível adicionar um formulário adaptável ou uma Comunicação interativa usando o [Componente de contêiner de SPA do AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) É um componente do AEM Forms para o AEM Sites SPA que pode ser adicionado à página Sites.

Para obter informações sobre como incorporar um formulário adaptável em um AEM Sites não SPA, consulte [Incorporar um formulário adaptável ou comunicação interativa na página do AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Pré-requisitos {#prerequisites}

Para incorporar um formulário adaptável ou uma Comunicação interativa em um AEM sites SPA usando o componente AEM Forms SPA Container, verifique se você instalou:

* Java SE Development Kit 8 ou mais recente
* Apache Maven 3.3.1 ou mais recente
* Instância do autor AEM
* [Instância do autor do ](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) pacote complementar do AEM Forms 6.4.2

## Instalar o componente Contêiner do AEM Forms SPA {#install-aem-forms-spa-container-component}

Execute as etapas a seguir para instalar o componente AEM Forms SPA Container :

1. [Clonar ou baixar o componente AEM Forms para SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Instale o componente AEM Forms para SPA. As instruções para instalar o componente estão disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   O componente inclui um [componente de Reação de amostra](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) que pode ser usado para integrar SPA componente de contêiner com um projeto de SPA baseado em React.

1. [Clonar ou baixar um projeto](https://github.com/adobe/aem-sample-we-retail-journal) de SPA baseado em React.
1. Integre SPA componente de contêiner a um projeto de SPA baseado em React usando as instruções disponíveis no arquivo [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor).

   Depois de instalar o componente AEM Forms SPA Container e integrar o componente a um projeto de SPA baseado em React, você pode incorporar formulários adaptáveis e Comunicações interativas na página AEM Sites.

## Incorporar um formulário adaptável ou Comunicação interativa {#af-component}

Para incorporar um formulário adaptável ou uma Comunicação interativa usando o AEM Forms para SPA componente de Contêiner:

1. Abra a página Sites AEM, no modo de edição, na qual deseja incorporar um formulário adaptável ou Comunicação interativa.
1. Insira o componente **AEM Formulário para SPA** na página usando qualquer uma das seguintes opções:

   * Toque no contêiner de layout na página Sites , toque em **+** e selecione o componente **AEM Formulário para SPA** .

   * No painel Navegador de componentes , arraste e solte o componente **AEM Formulário para SPA** na página.
   * Procure um formulário adaptável ou Comunicação interativa no navegador Ativos e arraste-o e solte-o na página Sites . Ele incorpora o formulário em um AEM Forms para SPA contêiner de componente.

   >[!NOTE]
   >
   >Não há suporte para a renderização de vários componentes do Contêiner do AEM Forms SPA em uma página. Você pode ter vários contêineres de SPA do AEM Forms em uma página, mas apenas um componente é renderizado de cada vez. Certifique-se de que apenas um componente esteja visível em uma página para evitar discrepâncias.

1. Toque no componente AEM Forms SPA Container incorporado na página sites e toque em ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **Editar contêiner de SPA do AEM Forms** é aberta.
1. Na caixa de diálogo **Editar contêiner AEM Forms**, especifique o seguinte:

   * **Tipo de ativo:** selecione o tipo de ativo a ser incorporado. As opções são **Adaptive Form** e **Interative Communication**

   * **Caminho** do ativo: Navegue e selecione o formulário adaptável ou Comunicação interativa a ser incorporado. O campo será preenchido automaticamente se um formulário adaptável ou uma Comunicação interativa for inserido usando o navegador Ativos.
   * **Canal**  (somente comunicação interativa): Selecione o tipo de canal interativo a ser incorporado. As opções são **Canal da Web** e **Canal de impressão**.

   * **Tema**: Selecione um tema que defina o estilo de componentes do formulário adaptável ou da Comunicação interativa. O estilo inclui propriedades de aparência, como estilo de fonte, cor de plano de fundo, dimensões e alinhamento.

1. Toque em ![done_icon](assets/done_icon.png) para salvar as configurações. O formulário adaptável ou a Comunicação interativa agora é incorporado na página.

## Publicar formulário adaptável incorporado e Comunicação interativa {#publish-embedded-adaptive-form-and-interactive-communication}

Considere os seguintes cenários para publicar um ativo incorporado (formulário adaptável ou Comunicação interativa) na página do AEM Sites:

* Se você estiver publicando a página do AEM Sites pela primeira vez e ela incluir um formulário adaptável incorporado ou uma Comunicação interativa, publique a página Sites e o ativo incorporado.
* Se você modificou apenas o formulário adaptável incorporado ou a Comunicação interativa em uma página de Sites publicada, publique o ativo original e as alterações serão refletidas na página Sites publicados. A página Sites publicados inclui uma referência ao ativo e não requer a republicação da página.
* Se você modificou a página Sites e o formulário adaptável incorporado ou a Comunicação interativa, republique a página Sites e o ativo incorporado.

## Modificar formulário adaptável incorporado e Comunicação interativa {#modify-embedded-adaptive-form-and-interactive-communication}

AEM página de sites mantém uma referência ao formulário adaptável e Comunicação interativa no Contêiner do AEM Forms. Portanto, todas as configurações e propriedades, como tema, estilos e ação de envio, configuradas no formulário adaptável original e Comunicação interativa são mantidas no formulário adaptável incorporado e Comunicação interativa.

Para modificar qualquer configuração ou propriedade do formulário adaptável incorporado e da Comunicação interativa, execute um dos procedimentos a seguir.

* Abra o formulário original em formulários adaptáveis ou Comunicação interativa em seus respectivos editores e modifique-o.
* Toque no formulário adaptável ou na Comunicação interativa na página Sites no modo de edição e toque em **Editar em uma nova janela**. O formulário original é aberto no modo de edição.

## Considerações e práticas recomendadas {#considerations-and-best-practices}

Lembre-se dos seguintes pontos ao incorporar formulários adaptáveis em páginas de sites AEM:

* O cabeçalho e o rodapé no formulário original não são incluídos no formulário incorporado.
* Os rascunhos e envios de usuários de formulários incorporados são suportados e visíveis nas guias Rascunhos e Forms enviados no portal de formulários.
* A ação de envio configurada no formulário original é retida no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário original não funcionam no formulário incorporado. No entanto, você pode usar o direcionamento de experiência na página Sites para apresentar diferentes formulários com base nos perfis do usuário.
* Se o Adobe Analytics estiver configurado para o formulário original, os dados analíticos do formulário incorporado serão capturados no Adobe Analytics. No entanto, não está disponível no relatório de análise de formulários.

