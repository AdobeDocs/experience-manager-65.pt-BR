---
title: Exportar Fragmentos de experiência para o Adobe Target
description: Saiba como exportar fragmentos de experiência do Adobe Experience Manager (AEM) para o Adobe Target.
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 41%

---

# Exportar Fragmentos de experiência para o Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Algumas funcionalidades desta página exigem a aplicação do AEM 6.5.3.0 (ou posterior).
>
>6.5.3.0:
>
>* **Domínios externalizadores** agora pode ser selecionado.
>  **Nota:** Os domínios do externalizador são relevantes somente para o conteúdo do fragmento de experiência que é enviado ao Target, e não para metadados como Exibir conteúdo da oferta.
>
>6.5.2.0
>
>* Os fragmentos de experiência podem ser exportados para:
>
>   * o espaço de trabalho padrão.
>   * um espaço de trabalho nomeado, especificado na Configuração na nuvem.
>   * **Nota:** A exportação para espaços de trabalho específicos exige o Adobe Target Premium.
>
>* AEM deve ser [integrado ao Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 e 6.5.1.0:
>
>* Os Fragmentos de experiência do AEM são exportados para o espaço de trabalho padrão do Adobe Target.
>* O AEM deve estar integrado ao Adobe Target, de acordo com as instruções na seção [Integração com o Adobe Target](/help/sites-administering/target.md).

Você pode exportar [Fragmentos de experiência](/help/sites-authoring/experience-fragments.md), criado no Adobe Experience Manager (AEM), para o Adobe Target (Target). Eles podem ser usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.

Há três opções de formato disponíveis para exportar um fragmento de experiência para o Adobe Target:

* HTML (padrão): suporte para entrega de conteúdo da Web e híbrido
* JSON: suporte para entrega de conteúdo headless
* HTML e JSON

Os fragmentos de experiência do AEM podem ser exportados para o espaço de trabalho padrão no Adobe Target ou para espaços de trabalho definidos pelo usuário para o Adobe Target. Isso é feito usando o Console do Adobe Developer, para o qual o AEM deve ser [integrado ao Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target não existem no próprio Adobe Target. Eles são definidos e gerenciados no Adobe IMS (Identity Management System) e depois selecionados para uso nas soluções que usam integrações do console do Adobe Developer.

>[!NOTE]
>
>Os espaços de trabalho do Adobe Target podem ser usados para permitir que membros de uma organização (grupo) criem e gerenciem ofertas e atividades somente para essa organização, sem conceder acesso a outros usuários. Por exemplo, organizações específicas de cada país dentro de uma preocupação global.

>[!NOTE]
>
>Para obter mais informações, consulte também:
>
>* [Desenvolvimento do Adobe Target](https://developers.adobetarget.com/)
>* [Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)
>

## Pré-requisitos {#prerequisites}

>[!CAUTION]
>
>Algumas funcionalidades desta página requerem a aplicação do AEM 6.5.3.0.

Várias ações são necessárias:

1. Você precisa [integrar o AEM ao Adobe Target usando IMS](/help/sites-administering/integration-target-ims.md).
2. Os fragmentos de experiência são exportados da instância do autor do AEM, portanto, [Configurar o Externalizador de links de AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) na instância do autor para garantir que todas as referências do fragmento de experiência sejam externalizadas para entrega na Web.

   >[!NOTE]
   >
   >Para a regravação de links não coberta por padrão, o [Provedor de regravação de link do fragmento de experiência](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) está disponível. Com isso, regras personalizadas podem ser desenvolvidas para sua instância.

## Adicionar a configuração da nuvem {#add-the-cloud-configuration}

Antes de exportar um fragmento, é necessário adicionar o **Configuração na nuvem** para **Adobe Target** ao fragmento ou pasta. Isso também permite:

* especificar as opções de formato a serem usadas para a exportação
* selecionar um espaço de trabalho do Target como destino
* selecionar um domínio Externalizador para regravação de referências no Fragmento de experiência (opcional)

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
   >O formato JSON de uma oferta de fragmento de experiência pode ser personalizado. Para fazer isso, defina um componente de Fragmento de experiência do cliente e anote como exportar suas propriedades no componente Modelo do Sling.
   >
   >Consulte o componente principal:
   >
   >[Componentes principais - Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)

   Em **Adobe Target**, selecione:

   * a configuração apropriada
   * a opção de formato exigida
   * um espaço de trabalho do Adobe Target
   * se necessário, o domínio Externalizer

   >[!CAUTION]
   >
   >O domínio Externalizer é opcional.
   >
   >Um Externalizador de AEM é configurado quando você deseja que o conteúdo exportado aponte para um *publicar* domínio. Para obter mais detalhes, consulte [Configurar o Externalizador de links de AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
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
>Por isso, o fragmento de experiência, com todos os ativos relacionados, deve ser publicado antes da exportação para o Target.

Para exportar um fragmento de experiência do AEM para o Target (depois de especificar a configuração da nuvem):

1. Navegue até o console Fragmento de experiência.
1. Selecione o fragmento de experiência que deseja exportar para o Target.

   >[!NOTE]
   >
   >Ele deve ser uma variação web do fragmento de experiência.

1. Clique em **Exportar para o Adobe Target**.

   >[!NOTE]
   >
   >Se o fragmento de experiência já tiver sido exportado, selecione **Atualizar no Adobe Target**.

1. Clique em **Exportar sem publicar** ou **Publish** conforme necessário.

   >[!NOTE]
   >
   >Selecionar **Publish** O publica o fragmento de experiência imediatamente e o envia para o Target.

1. Clique em **OK** no diálogo de confirmação.

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

Depois de executar as tarefas anteriores, o Fragmento de experiência é exibido na página Ofertas do Adobe Target. Olhe para o [documentação específica do Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html) para saber mais sobre o que você pode realizar lá.

>[!NOTE]
>
>Ao visualizar um fragmento de experiência no Adobe Target, a data da *última modificação* vista é a data em que o fragmento foi modificado pela última vez no AEM, não a data em que o fragmento foi exportado pela última vez para o Adobe Target.

## Excluir um fragmento de experiência já exportado para o Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Excluir um fragmento de experiência que já foi exportado para o Target pode causar problemas se o fragmento já estiver sendo usado em uma oferta no Adobe Target. A exclusão do fragmento tornaria a oferta inutilizável, pois o conteúdo do fragmento estaria sendo entregue pelo AEM.

Para evitar essas situações:

* Se o fragmento de experiência não estiver sendo usado atualmente em uma atividade, o AEM permite que o usuário exclua o fragmento sem mostrar uma mensagem de aviso.
* Se o Fragmento de experiência estiver sendo usado por uma atividade no Adobe Target, uma mensagem de erro avisará o usuário AEM sobre as possíveis consequências que a exclusão do fragmento terá na atividade.

  A mensagem de erro no AEM não proíbe que o usuário exclua (à força) o fragmento de experiência. Se o fragmento de experiência for excluído:

   * A oferta do Target com o fragmento de experiência do AEM pode exibir um comportamento indesejado

      * A oferta provavelmente ainda será renderizada, pois o HTML do fragmento de experiência foi enviado para o Target
      * Qualquer referência no fragmento de experiência pode não funcionar corretamente se os ativos referenciados também tiverem sido excluídos no AEM.

   * É impossível fazer mais modificações no fragmento de experiência, pois ele não existe mais no AEM.


## Remoção de ClientLibs dos Fragmentos de experiência exportados para o Target {#removing-clientlibs-from-fragments-exported-target}

Os Fragmentos de experiência contêm tags html completas e todas as Bibliotecas de clientes (CSS/JS) necessárias para renderizar o fragmento exatamente como ele foi criado pelo Autor de conteúdo do fragmento de experiência. Isto é um projeto.

Ao usar uma Oferta de fragmento de experiência com o Adobe Target em uma página que está sendo entregue pelo AEM, a página Direcionado já contém todas as Bibliotecas de clientes necessárias. Além disso, o html irrelevante na oferta de fragmento de experiência também não é necessário (consulte [Considerações](#considerations)).

Veja a seguir um pseudo exemplo do html em uma Oferta de fragmento de experiência:

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

Em um alto nível, quando o AEM exporta um fragmento de experiência para o Adobe Target, ele faz isso usando vários seletores Sling adicionais. Por exemplo, o URL do Fragmento de experiência exportado pode ser semelhante ao seguinte (aviso `nocloudconfigs.atoffer`):

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

A variável `nocloudconfigs` O seletor é definido usando HTL e pode ser sobreposto copiando-o de:

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

A variável `atoffer` o seletor é aplicado após o processamento usando [Sling Rewriter](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Ambos podem ser usados para remover as bibliotecas de clientes.

### Exemplo {#example}

Para o propósito aqui, vamos ilustrar como fazer isso com `nocloudconfigs`.

>[!NOTE]
>
>Consulte [Modelos editáveis](/help/sites-developing/templates.md#editable-templates) para obter mais detalhes.

#### Sobreposições {#overlays}

Neste exemplo específico, a variável [sobreposições](/help/sites-developing/overlays.md) ser incluído removerá as Bibliotecas de clientes *e* o html irrelevante. Pressupõe-se que você já tenha criado o tipo de modelo do fragmento de experiência. Os arquivos necessários que precisam ser copiados do `/libs/cq/experience-fragments/components/xfpage/` incluem:

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### Sobreposições do tipo de modelo {#template-type-overlays}

Para o propósito deste exemplo, vamos para a seguinte estrutura:

![Sobreposições do tipo de modelo](assets/xf-target-integration-02.png "Sobreposições do tipo de modelo")

O conteúdo desses arquivos é o seguinte:

* `body.nocloudconfigs.html`

  ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

  ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

  ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>Para usar `data-sly-unwrap` para remover a marca body, é necessário `nocloudconfigs.html`.

### Considerações {#considerations}

Se você precisar oferecer suporte a sites AEM e não AEM usando Ofertas de fragmento de experiência no Adobe Target, será necessário criar dois fragmentos de experiência (dois tipos de modelo diferentes):

* Um com a sobreposição para remover clientlibs/html extra

* Uma que não tenha a sobreposição e, portanto, inclua as clientlibs necessárias