---
title: Diretrizes de codificação
description: Diretrizes, dicas e truques do desenvolvedor do Communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Diretrizes de codificação {#coding-guidelines}

## Diretrizes, dicas e truques {#guidelines-tips-and-tricks}

O trabalho com o AEM Communities evoluiu de uma dependência intensa das Java Server Pages para a flexibilidade na escolha de linguagens de script de modelo, em que a lógica de negócios, o estilo e o conteúdo da página são distintos entre si.

Mais flexibilidade ao trabalhar com conteúdo gerado pelo usuário (UGC) é por meio da API SocialResourceProvider, o que elimina a necessidade de saber quais [SRP](srp.md) foi escolhida para a implantação.

A seguir, estão várias diretrizes e práticas recomendadas de codificação para desenvolvedores do AEM Communities:

### Código {#code}

* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - como evitar a gravação de um aplicativo que funciona somente quando o UGC é armazenado em JCR (JSRP).
* [Refatoração de SocialUtils](socialutils.md) - métodos de utilitário para SRP que substituem SocialUtils.
* [Convenções de nomenclatura](naming-conventions.md) - convenções de nomenclatura para classes Java personalizadas.

### Scripts {#scripts}

* [Componentes de comunidades de sideload](sideloading.md) - como adicionar um componente dinamicamente depois que a página é carregada.
* [Fundamentos do Editor de Rich Text](rte.md) - como personalizar a interface do usuário de rich text fornecida aos membros para conteúdo de publicação.

### IDE {#ide}

* [Uso do Maven para comunidades](maven.md) - como incluir o jar da API do Communities.
* [Refatoração de SocialUtils](socialutils.md) - métodos de utilitário para SRP que substituem SocialUtils.
