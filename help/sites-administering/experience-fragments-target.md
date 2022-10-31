---
title: Exportar fragmentos de experiência para o Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: Exportar fragmentos de experiência para o Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 81%

---

# Exportar fragmentos de experiência para o Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Algumas funcionalidades nesta página exigem a aplicação do AEM 6.5.3.0 (ou posterior).
>
>6.5.3.0:
>
>* **Domínios do Externalizador** agora pode ser selecionado.
   >  **Observação:** Domínios do Externalizador são relevantes somente para o conteúdo do Fragmento de experiência que é enviado ao Target, e não para metadados como Exibir conteúdo da oferta.
>
>6.5.2.0:
>
>* Os Fragmentos de experiência podem ser exportados para:
   >
   >   * o espaço de trabalho padrão.
   >   * um espaço de trabalho nomeado, especificado na Configuração da nuvem.
   >   * **Observação:** A exportação para espaços de trabalho específicos requer o Adobe Target Premium.
>
>* AEM deve ser [integrado ao Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 e 6.5.1.0:
>
>* Os Fragmentos de experiência do AEM são exportados para o espaço de trabalho padrão do Adobe Target.
>* O AEM deve estar integrado ao Adobe Target, de acordo com as instruções na seção [Integração com o Adobe Target](/help/sites-administering/target.md).


Você pode exportar [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md), criado no Adobe Experience Manager (AEM), no Adobe Target (Target). Eles podem ser usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.

Há três opções de formato disponíveis para exportar um Fragmento de experiência para o Adobe Target:

* HTML (padrão): suporte para entrega de conteúdo da Web e híbrido
* JSON: suporte para entrega de conteúdo headless
* HTML e JSON

AEM Fragmentos de experiência podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário no Adobe Target. Isso é feito usando o Console do Adobe Developer, para o qual AEM deve ser [integrado ao Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e, em seguida, selecionados para uso nas soluções usando integrações do Adobe Developer Console.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades somente para essa organização, sem conceder acesso a outros usuários. Por exemplo, organizações específicas de cada país dentro de uma preocupação global.

>[!NOTE]
>
>Para obter mais informações, consulte também:
>
>* [Desenvolvimento do Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componentes principais - Fragmentos de experiência](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## Pré-requisitos {#prerequisites}

>[!CAUTION]
>
>Algumas funcionalidades nesta página exigem a aplicação do AEM 6.5.3.0.

Várias ações são necessárias:

1. Você tem que [integrar AEM com o Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).
2. Os fragmentos de experiência são exportados da instância do autor do AEM, portanto, é necessário [Configurar o Externalizador de links do AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que todas as referências do fragmento de experiência sejam externalizadas para entrega na Web.

   >[!NOTE]
   >
   >Para a regravação de links não coberta por padrão, o [Provedor de regravação de link do fragmento de experiência](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) está disponível. Com isso, regras personalizadas podem ser desenvolvidas para sua instância.

## Adicionar a configuração da nuvem {#add-the-cloud-configuration}

Antes de exportar um fragmento, é necessário adicionar a **Configuração da nuvem** do **Adobe Target** ao fragmento ou pasta. Isso também permite:

* especificar as opções de formato a serem usadas para a exportação
* selecionar um espaço de trabalho do Target como destino
* selecionar um domínio externalizador para regravação de referências no fragmento de experiência (opcional)

As opções necessárias podem ser selecionadas nas **Propriedades de página** da pasta e/ou fragmento necessários; a especificação será herdada conforme necessário.

1. Navegue até o console **Fragmentos de experiência**.

1. Abra as **Propriedades de página** da pasta ou fragmento apropriado.

   >[!NOTE]
   >
   >Se você adicionar a configuração da nuvem à pasta principal do fragmento de experiência, a configuração será herdada pelas pastas secundárias.
   >
   >
   >Se você adicionar a configuração da nuvem ao próprio fragmento de experiência, a configuração será herdada por todas as variações.

1. Selecione a guia **Cloud Services**.

1. Em **Configuração do Cloud Service**, selecione **Adobe Target** na lista suspensa.

   >[!NOTE]
   >
   >O formato JSON de uma oferta de fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente do fragmento de experiência do cliente e anote como exportar suas propriedades no componente Modelo do Sling.
   >
   >Consulte o componente principal:
   >
   >[Componentes principais - Fragmentos de experiência](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Em **Adobe Target**, selecione:

   * a configuração apropriada
   * a opção de formato exigida
   * um espaço de trabalho do Adobe Target
   * se necessário, o domínio externalizador

   >[!CAUTION]
   >
   >O domínio externalizador é opcional.
   >
   >Um externalizador do AEM é configurado quando você deseja que o conteúdo exportado aponte para um domínio de *publicação* específico. Para obter mais detalhes, consulte [Configurar o Externalizador de links do AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   >Observe também que os domínios do externalizador são relevantes somente para o conteúdo do fragmento de experiência que é enviado ao Target, e não para metadados como Visualizar conteúdo da oferta.

   Por exemplo, para uma pasta:

   ![Pasta - Cloud Services](assets/xf-target-integration-01.png "Pasta - Cloud Services")

1. **Salvar e fechar**.

## Exportar um fragmento de experiência para o Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para ativos de mídia, como imagens, somente uma referência é exportada para o Target. O ativo em si permanece armazenado no AEM Assets e é entregue a partir da instância de publicação do AEM.
>
>Devido a isso, o fragmento de experiência, com todos os ativos relacionados, precisa ser publicado antes da exportação para o Target.

Para exportar um fragmento de experiência do AEM para o Target (depois de especificar a configuração da nuvem):

1. Navegue até o console Fragmento de experiência.
1. Selecione o fragmento de experiência que deseja exportar para o Target.

   >[!NOTE]
   >
   >Ele deve ser uma variação web do fragmento de experiência.

1. Toque/clique em **Exportar para o Adobe Target**.

   >[!NOTE]
   >
   >Se o fragmento de experiência já tiver sido exportado, selecione **Atualizar no Adobe Target**.

1. Toque/clique em **Exportar sem publicar** ou em **Publicar**, conforme necessário.

   >[!NOTE]
   >
   >Selecionar **Publicar** publicará o fragmento de experiência imediatamente e o enviará para o Target.

1. Toque ou clique em **OK** na caixa de diálogo de confirmação.

   Seu fragmento de experiência agora deve estar no Target.

   >[!NOTE]
   >
   >[Vários detalhes](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) da exportação podem ser vistos na **Exibição de lista** do console e nas **Propriedades**.

   >[!NOTE]
   >
   >Ao visualizar um fragmento de experiência no Adobe Target, a data da *última modificação* vista é a data em que o fragmento foi modificado pela última vez no AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

>[!NOTE]
>
>Como alternativa, você pode executar a exportação a partir do editor de páginas, usando comandos comparáveis no menu [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information).

## Usar os fragmentos de experiência no Adobe Target {#using-your-experience-fragments-in-adobe-target}

Depois de executar as tarefas anteriores, o fragmento de experiência é exibido na página Ofertas do Target. Consulte a [documentação específica do Target](https://experiencecloud.adobe.com/resources/help/pt_BR/target/target/aem-experience-fragments.html) para saber mais sobre o que você pode realizar lá.

>[!NOTE]
>
>Ao visualizar um fragmento de experiência no Adobe Target, a data da *última modificação* vista é a data em que o fragmento foi modificado pela última vez no AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

## Excluir um fragmento de experiência já exportado para o Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Excluir um fragmento de experiência que já foi exportado para o Target pode causar problemas se o fragmento já estiver sendo usado em uma oferta no Target. A exclusão do fragmento tornaria a oferta inutilizável, pois o conteúdo do fragmento estaria sendo entregue pelo AEM.

Para evitar essas situações:

* Se o fragmento de experiência não estiver sendo usado atualmente em uma atividade, o AEM permite que o usuário exclua o fragmento sem mostrar uma mensagem de aviso.
* Se o Fragmento de experiência estiver sendo usado atualmente por uma atividade no Target, uma mensagem de erro avisará o usuário do AEM sobre as possíveis consequências que a exclusão do fragmento terá na atividade.

   A mensagem de erro no AEM não proíbe que o usuário exclua (à força) o fragmento de experiência. Se o fragmento de experiência for excluído:

   * A oferta do Target com o fragmento de experiência do AEM pode exibir um comportamento indesejado

      * A oferta provavelmente ainda será renderizada, pois o HTML do fragmento de experiência foi enviado para o Target
      * Qualquer referência no fragmento de experiência pode não funcionar corretamente se os ativos referenciados também tiverem sido excluídos no AEM.
   * É impossível realizar qualquer alteração adicional no fragmento de experiência, pois ele não existe mais no AEM.
