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
source-git-commit: a33d46bcfcf901fb774b742c0fc972265401a56e
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

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
>* AEM deve ser [integrado ao Adobe Target usando o Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).
>
>AEM 6.5.0.0 e 6.5.1.0:
>
>* Os Fragmentos de experiência AEM são exportados para o espaço de trabalho padrão do Adobe Target.
>* AEM deve ser integrado ao Adobe Target de acordo com as instruções em [Integração com o Adobe Target](/help/sites-administering/target.md).


Você pode exportar [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md), criado no Adobe Experience Manager (AEM), no Adobe Target (Target). Eles podem ser usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.

Há três opções de formato disponíveis para exportar um Fragmento de experiência para o Adobe Target:

* HTML (padrão): Suporte para entrega de conteúdo da Web e híbrido
* JSON: Suporte para entrega de conteúdo sem periféricos
* HTML e JSON

AEM Fragmentos de experiência podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário no Adobe Target. Isso é feito via Adobe I/O, para o que AEM deve ser [integrado ao Adobe Target usando o Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e, em seguida, selecionados para uso em soluções que usam integrações Adobe I/O.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades somente para essa organização; sem conceder acesso a outros usuários. Por exemplo, organizações específicas de cada país dentro de uma preocupação global.

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

1. Você tem que [integrar AEM com o Adobe Target usando o Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).
2. Os Fragmentos de experiência são exportados da instância do autor do AEM, portanto, é necessário [Configurar o AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que todas as referências no Fragmento de experiência sejam externalizadas para entrega na Web.

   >[!NOTE]
   >
   >Para a reescrita de links não coberta pelo padrão, a variável [Provedor de regravação do link do fragmento de experiência](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) está disponível. Com isso, regras personalizadas podem ser desenvolvidas para sua instância.

## Adicionar a configuração da nuvem {#add-the-cloud-configuration}

Antes de exportar um fragmento, é necessário adicionar o **Configuração na nuvem** para **Adobe Target** ao fragmento ou pasta. Isso também permite:

* especificar as opções de formato a serem usadas para exportar
* selecione um espaço de trabalho do Target como destino
* selecione um domínio externalizador para reescrever referências no Fragmento de experiência (opcional)

As opções necessárias podem ser selecionadas em **Propriedades da página** da pasta e/ou fragmento necessários; a especificação será herdada conforme necessário.

1. Navegue até o **Fragmentos de experiência** console.

1. Abrir **Propriedades da página** para a pasta ou fragmento apropriado.

   >[!NOTE]
   >
   >Se você adicionar a configuração de nuvem à pasta pai do Fragmento de experiência, a configuração será herdada por todos os filhos.
   >
   >
   >Se você adicionar a configuração da nuvem ao próprio Fragmento de experiência, a configuração será herdada por todas as variações.

1. Selecione o **Cloud Services** guia .

1. Em **Configuração Cloud Service**, selecione **Adobe Target** na lista suspensa.

   >[!NOTE]
   >
   >O formato JSON de uma oferta de Fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente de Fragmento de experiência do cliente e anote como exportar suas propriedades no componente Modelo do Sling.
   >
   >Consulte o componente principal:
   >
   >[Componentes principais - Fragmentos de experiência](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Em **Adobe Target** selecione:

   * a configuração apropriada
   * a opção de formato necessária
   * um espaço de trabalho Adobe Target
   * se necessário - o domínio externalizador

   >[!CAUTION]
   >
   >O domínio externalizador é opcional.
   >
   > Um AEM externalizador é configurado quando você deseja que o conteúdo exportado aponte para um *publicar* domínio. Para obter mais detalhes, consulte [Configurar o AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   > Observe também que os Domínios do Externalizador são relevantes somente para o conteúdo do Fragmento de experiência que é enviado ao Target, e não para metadados como Exibir conteúdo da oferta.

   Por exemplo, para uma pasta:

   ![Pasta - Cloud Services](assets/xf-target-integration-01.png "Pasta - Cloud Services")

1. **Salvar e fechar**.

## Exportar um fragmento de experiência para o Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para ativos de mídia, como imagens, somente uma referência é exportada para o Target. O próprio ativo permanece armazenado no AEM Assets e é entregue a partir da instância de publicação do AEM.
>
>Devido a isso, o Fragmento de experiência, com todos os ativos relacionados, precisa ser publicado antes da exportação para o Target.

Para exportar um fragmento de experiência do AEM para o Target (depois de especificar a configuração da nuvem):

1. Navegue até o console Fragmento de experiência .
1. Selecione o Fragmento de experiência que deseja exportar para o target.

   >[!NOTE]
   >
   >Deve ser uma variação Web de Fragmento de experiência.

1. Toque/clique **Exportar para o Adobe Target**.

   >[!NOTE]
   >
   >Se o Fragmento de experiência já tiver sido exportado, selecione **Atualização no Adobe Target**.

1. Toque/clique **Exportar sem publicação** ou **Publicar** conforme necessário.

   >[!NOTE]
   >
   >Selecionar **Publicar** O publicará o fragmento de experiência imediatamente e o enviará para o Target.

1. Toque/clique **OK** na caixa de diálogo de confirmação.

   Seu fragmento de experiência agora deve estar no Target.

   >[!NOTE]
   >
   >[Vários detalhes](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) da exportação pode ser **Exibição de lista** do console e **Propriedades**.

   >[!NOTE]
   >
   >Ao visualizar um fragmento de experiência no Adobe Target, a variável *última modificação* data vista é a data em que o fragmento foi modificado pela última vez em AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

>[!NOTE]
>
>Como alternativa, você pode executar a exportação do editor de páginas, usando comandos comparáveis no [Informações da página](/help/sites-authoring/author-environment-tools.md#page-information) menu.

## Uso dos Fragmentos de experiência no Adobe Target {#using-your-experience-fragments-in-adobe-target}

Depois de executar as tarefas anteriores, o fragmento de experiência é exibido na página Ofertas no Target. Dê uma olhada no [documentação específica do Target](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) para saber mais sobre o que você pode alcançar lá.

>[!NOTE]
>
>Ao visualizar um fragmento de experiência no Adobe Target, a variável *última modificação* data vista é a data em que o fragmento foi modificado pela última vez em AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

## Excluir um fragmento de experiência já exportado para o Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Excluir um fragmento de experiência que já foi exportado para o Target pode causar problemas se o fragmento já estiver sendo usado em uma oferta no Target. A exclusão do fragmento tornaria a oferta inutilizável, pois o conteúdo do fragmento está sendo entregue pelo AEM.

Para evitar essas situações:

* Se o Fragmento de experiência não estiver sendo usado atualmente em uma atividade, o AEM permite que o usuário exclua o fragmento sem uma mensagem de aviso.
* Se o Fragmento de experiência estiver sendo usado atualmente por uma atividade no Target, uma mensagem de erro avisará o usuário AEM sobre possíveis consequências que a exclusão do fragmento terá na atividade.

   A mensagem de erro no AEM não proíbe que o usuário (force-)exclua o Fragmento de experiência. Se o Fragmento de experiência for excluído:

   * A oferta do Target com AEM fragmento de experiência pode mostrar um comportamento indesejado

      * A oferta provavelmente ainda será renderizada, pois o HTML do Fragmento de experiência foi enviado para o Target
      * Qualquer referência no Fragmento de experiência pode não funcionar corretamente se os ativos referenciados também tiverem sido excluídos no AEM.
   * É claro que qualquer alteração adicional no Fragmento de experiência é impossível, pois o Fragmento de experiência não existe mais no AEM.
