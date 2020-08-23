---
title: Exportação de fragmentos de experiência para o Adobe Target
seo-title: Exportação de fragmentos de experiência para o Adobe Target
description: Exportação de fragmentos de experiência para o Adobe Target
seo-description: Exportação de fragmentos de experiência para o Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Exportação de fragmentos de experiência para o Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Algumas funcionalidades nesta página exigem a aplicação do AEM 6.5.3.0.
>
>6.5.3.0
>
>* **Domínios** do Externalizador agora podem ser selecionados.
>
>
6.5.2.0:
>
>* Fragmentos de experiência podem ser exportados para:
   >
   >   
   * a área de trabalho padrão.
   >   * um espaço de trabalho nomeado, especificado na Configuração da nuvem.
   >   * **Observação:** Exportar para espaços de trabalho específicos requer o Adobe Target Premium.
>
>* AEM deve ser [integrado ao Adobe Target usando E/S](/help/sites-administering/integration-ims-adobe-io.md)do Adobe.

>
>

AEM 6.5.0.0 e 6.5.1.0:
>
>* Os Fragmentos de experiência AEM são exportados para a área de trabalho padrão do Adobe Target.
>* AEM deve ser integrado ao Adobe Target de acordo com as instruções em [Integração com o Adobe Target](/help/sites-administering/target.md).


Você pode exportar Fragmentos [de](/help/sites-authoring/experience-fragments.md)experiência criados no Adobe Experience Manager (AEM) para o Adobe Target (Público alvo). Eles podem ser usados como ofertas em atividades Públicos alvos, para testar e personalizar experiências em escala.

Há três opções de formato disponíveis para exportar um Fragmento de experiência para o Adobe Target:

* HTML (padrão): Suporte para delivery de conteúdo da Web e híbrido
* JSON: Suporte para delivery de conteúdo sem cabeçalho
* HTML e JSON

AEM Fragmentos de experiência podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário para o Adobe Target. Isso é feito via E/S do Adobe, para o qual AEM deve ser [integrado ao Adobe Target usando E/S](/help/sites-administering/integration-ims-adobe-io.md)do Adobe.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e, em seguida, selecionados para uso em soluções que usam integrações de E/S de Adobe.

>[!NOTE]
>
>Os espaços de trabalho Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades apenas para essa organização; sem dar acesso a outros usuários. Por exemplo, organizações específicas a cada país dentro de uma preocupação global.

>[!NOTE]
>
>Para obter mais informações, consulte também:
>
>* [Desenvolvimento Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componentes principais - Fragmentos de experiência](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

>



## Pré-requisitos {#prerequisites}

>[!CAUTION]
>
>Algumas funcionalidades nesta página exigem a aplicação do AEM 6.5.3.0.

Várias ações são obrigatórias:

1. É necessário [integrar AEM com a Adobe Target usando E/S](/help/sites-administering/integration-ims-adobe-io.md)Adobe.
2. Os Fragmentos de experiência são exportados da instância do autor AEM, portanto, é necessário [Configurar o AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que quaisquer referências no Fragmento de experiência sejam externalizadas para o delivery da Web.

   >[!NOTE]
   >
   >Para a regravação de links não abordada pelo padrão, o Provedor [](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) do Experience Fragment Link Rewriter está disponível. Com isso, regras personalizadas podem ser desenvolvidas para sua instância.

## Adicionar a configuração da nuvem {#add-the-cloud-configuration}

Antes de exportar um fragmento, é necessário adicionar a Configuração **da** nuvem para **Adobe Target** ao fragmento ou pasta. Isso também permite que você:

* especificar as opções de formato a serem usadas para a exportação
* selecionar um espaço de trabalho de Público alvo como destino
* selecione um domínio do externalizador para regravar referências no Fragmento de experiência (opcional)

As opções necessárias podem ser selecionadas em Propriedades **da** página da pasta e/ou fragmento necessários; a especificação será herdada conforme necessário.

1. Navigate to the **Experience Fragments** console.

1. Abra Propriedades **da** página para a pasta ou fragmento apropriado.

   >[!NOTE]
   >
   >Se você adicionar a configuração de nuvem à pasta pai do Fragmento de experiência, a configuração será herdada por todos os filhos.
   >
   >
   >Se você adicionar a configuração de nuvem ao próprio Fragmento de experiência, a configuração será herdada por todas as variações.

1. Selecione a guia **Cloud Services** .

1. Em Configuração **do** Cloud Service, selecione **Adobe Target** na lista suspensa.

   >[!NOTE]
   >
   >O formato JSON de uma oferta de fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente de Fragmento de experiência do cliente e anote como exportar suas propriedades no componente Sling Model.
   >
   >Consulte o componente principal:
   >
   >[Componentes principais - Fragmentos de experiência](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Em **Adobe Target** selecione:

   * a configuração apropriada
   * a opção de formato necessária
   * um espaço de trabalho Adobe Target
   * se necessário - o domínio do externalizador

   >[!CAUTION]
   >
   >O domínio do externalizador é opcional. Um AEM externalizador é configurado quando você deseja que o conteúdo exportado aponte para um domínio de *publicação* específico. Para obter mais detalhes, consulte [Configuração do AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).

   Por exemplo, para uma pasta:

   ![Pasta - Cloud](assets/xf-target-integration-01.png "ServicesFolder - Cloud Services")

1. **Salvar e fechar**.

## Exportação de um fragmento de experiência para o Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para ativos de mídia, como imagens, apenas uma referência é exportada para o Público alvo. O ativo em si permanece armazenado no AEM Assets e é entregue da instância de publicação AEM.
>
>Devido a isso, o Fragmento de experiência, com todos os ativos relacionados, precisa ser publicado antes de exportar para o Público alvo.

Para exportar um fragmento de experiência de AEM para Público alvo (depois de especificar a Configuração da nuvem):

1. Navegue até o console Fragmento de experiência.
1. Selecione o Fragmento de experiência que deseja exportar para o público alvo.

   >[!NOTE]
   >
   >Deve ser uma variação da Web do Fragmento de experiência.

1. Toque/clique em **Exportar para Adobe Target**.

   >[!NOTE]
   >
   >Se o Fragmento de experiência já tiver sido exportado, selecione **Atualizar no Adobe Target**.

1. Toque/clique em **Exportar sem publicar** ou **Publicar** , conforme necessário.

   >[!NOTE]
   >
   >Selecionar **Publicar** publicará o fragmento da experiência imediatamente e o enviará para o Público alvo.

1. Toque/clique em **OK** na caixa de diálogo de confirmação.

   Seu fragmento de experiência agora deve estar no Público alvo.

   >[!NOTE]
   >
   >[Vários detalhes](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) da exportação podem ser vistos na Visualização **de** Lista do console e **Propriedades**.

   >[!NOTE]
   >
   >Ao exibir um Fragmento de experiência no Adobe Target, a *última data modificada* vista é a data em que o fragmento foi modificado pela última vez em AEM, e não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

>[!NOTE]
>
>Como alternativa, você pode executar a exportação do editor de páginas, usando comandos comparáveis no menu Informações [da](/help/sites-authoring/author-environment-tools.md#page-information) página.

## Uso de fragmentos de experiência no Adobe Target {#using-your-experience-fragments-in-adobe-target}

Depois de executar as tarefas anteriores, o fragmento de experiência é exibido na página Ofertas no Público alvo. Consulte a documentação [](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) específica do Público alvo para saber mais sobre o que você pode alcançar.

>[!NOTE]
>
>Ao exibir um Fragmento de experiência no Adobe Target, a *última data modificada* vista é a data em que o fragmento foi modificado pela última vez em AEM, e não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

## Excluir um fragmento de experiência já exportado para o Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

A exclusão de um fragmento de experiência que já foi exportado para o Público alvo pode causar problemas se o fragmento já estiver sendo usado em uma oferta no Público alvo. A exclusão do fragmento tornaria a oferta inutilizável, pois o conteúdo do fragmento está sendo entregue pela AEM.

Para evitar tais situações:

* Se o Fragmento de experiência não estiver sendo usado em uma atividade no momento, AEM permite que o usuário exclua o fragmento sem uma mensagem de aviso.
* Se o Fragmento de experiência estiver sendo usado por uma atividade no Público alvo, uma mensagem de erro avisará o usuário AEM sobre possíveis consequências que a exclusão do fragmento terá na atividade.

   A mensagem de erro no AEM não proíbe que o usuário (force-)exclua o Fragmento de experiência. Se o Fragmento de experiência for excluído:

   * A oferta do Público alvo com AEM Fragmento de experiência pode mostrar um comportamento indesejado

      * A oferta provavelmente ainda será renderizada, pois o HTML do fragmento de experiência foi enviado para o Público alvo
      * Qualquer referência no Fragmento de experiência pode não funcionar corretamente se os ativos referenciados também tiverem sido excluídos no AEM.
   * É claro, quaisquer modificações adicionais no Fragmento de experiência são impossíveis, pois o Fragmento de experiência não existe mais no AEM.