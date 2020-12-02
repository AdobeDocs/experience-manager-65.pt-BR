---
title: Designs e o Designer
seo-title: Designs e o Designer
description: Você precisará criar um design para seu site e, no AEM, usará o Designer
seo-description: Você precisará criar um design para seu site e, no AEM, usará o Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Designs e o Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Este artigo descreve como criar um site com base na interface clássica. A Adobe recomenda aproveitar as tecnologias AEM mais recentes para seus sites, conforme descrito em detalhes no artigo [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md).

Você precisará criar um design para seu site e, no AEM, usará o Designer.

>[!NOTE]
>
>Para obter mais informações sobre acessibilidade da Web, consulte [AEM e as Diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md).

## Uso do Designer {#using-the-designer}

Seu design pode ser definido na seção **designs** da guia **Ferramentas**:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aqui, você pode criar a estrutura necessária para armazenar o design e, em seguida, fazer upload das folhas de estilos e imagens em cascata necessárias.

Os designs são armazenados em `/etc/designs`. O caminho para o design a ser usado para um site é especificado usando a propriedade `cq:designPath` do nó `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todas as alterações feitas em uma página no modo de design são mantidas abaixo do nó de design do site e são automaticamente aplicadas a todas as páginas que têm o mesmo design.

## Do que você precisará {#what-you-will-need}

Para realizar seu design, você precisará:

**CSS**  - As folhas de estilos em cascata definem os formatos de áreas específicas em suas páginas.
**Imagens**  - quaisquer imagens que você usa para recursos como planos de fundo, botões.

### Considerações ao projetar seu site {#considerations-when-designing-your-website}

Ao desenvolver um site, é altamente recomendável armazenar imagens e arquivos CSS em `/etc/design/<project>` para que você possa fazer referência a seus recursos com base no design atual, como descrito pelo seguinte trecho.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

O exemplo anterior oferta vários benefícios:

* Os componentes podem ter uma aparência diferente com base em cada site usando um caminho de design diferente.
* O redesign do site pode ser feito simplesmente apontando o caminho do design para um nó diferente na raiz do site de `design/v1` para `design/v2.`

* `/etc/designs` e  `/content` são os únicos URLs externos que o navegador vê protegendo você de um usuário externo que está curioso sobre o que está abaixo da sua  `/apps` árvore. Os benefícios do URL acima também ajudam o administrador do sistema a configurar melhor segurança, pois você está limitando a exposição dos ativos a alguns locais distintos.

