---
title: Designs e Designer
seo-title: Designs e Designer
description: Será necessário criar um design para o seu site e, no AEM, fazer isso usando o Designer
seo-description: Será necessário criar um design para o seu site e, no AEM, fazer isso usando o Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
translation-type: tm+mt
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Designs e Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Este artigo descreve como criar um site com base na interface clássica. O Adobe recomenda o aproveitamento das tecnologias de AEM mais recentes para seus sites, conforme descrito detalhadamente no artigo [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md).

O Designer é usado para criar um design para seu site usando a [Interface clássica](/help/release-notes/touch-ui-features-status.md) no AEM.

>[!NOTE]
>
>Para obter mais informações sobre acessibilidade da Web, consulte [AEM e as Web Accessibility Guidelines](/help/managing/web-accessibility.md).

## Uso do Designer {#using-the-designer}

Seu design pode ser definido na seção **designs** da guia **Ferramentas**:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aqui, você pode criar a estrutura necessária para armazenar o design e, em seguida, fazer upload das folhas de estilos em cascata e imagens necessárias.

Os designs são armazenados em `/apps/<your-project>`. O caminho para o design a ser usado para um site é especificado usando a propriedade `cq:designPath` do nó `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todas as alterações feitas em uma página no modo de design são mantidas abaixo do nó de design do site e são automaticamente aplicadas a todas as páginas que têm o mesmo design.

## O que é necessário {#what-you-will-need}

Para realizar seu design, você precisará:

**CSS**  - As folhas de estilos em cascata definem os formatos de áreas específicas nas páginas.
**Imagens**  - Qualquer imagem que você use para recursos como planos de fundo, botões.

### Considerações ao criar seu site {#considerations-when-designing-your-website}

Ao desenvolver um site, é altamente recomendável armazenar imagens e arquivos CSS em `/apps/<your-project>` para que você possa fazer referência aos recursos com base no design atual, como descrito pelo seguinte trecho.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

O exemplo anterior oferece vários benefícios:

* Os componentes podem ter uma aparência diferente com base em cada site usando um caminho de design diferente.
* A recriação do site pode ser simplesmente feita apontando o caminho do design para um nó diferente na raiz do site de `design/v1` para `design/v2.`

* `/etc/designs` e  `/content` são as únicas URLs externas que o navegador vê protegendo você de um usuário externo ficando curioso sobre o que está em sua  `/apps` árvore. Os benefícios do URL acima também ajudam o Administrador do sistema a configurar melhor segurança, pois você está limitando a exposição dos ativos a alguns locais distintos.
