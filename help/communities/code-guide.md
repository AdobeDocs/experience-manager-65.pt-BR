---
title: Diretrizes de codificação
description: Diretrizes, dicas e truques do desenvolvedor do Communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Diretrizes de codificação {#coding-guidelines}

## Diretrizes, dicas e truques {#guidelines-tips-and-tricks}

O trabalho com o AEM Communities evoluiu de uma dependência intensa das Java Server Pages para a flexibilidade na escolha de linguagens de script de modelo, em que a lógica de negócios, o estilo e o conteúdo da página são distintos entre si.

Mais flexibilidade ao trabalhar com conteúdo gerado pelo usuário (UGC) é por meio da API SocialResourceProvider, o que elimina a necessidade de saber qual opção [SRP](srp.md) foi escolhida para a implantação.

A seguir, estão várias diretrizes e práticas recomendadas de codificação para desenvolvedores do AEM Communities:

### Código {#code}

* [Acessando o UGC com SRP](accessing-ugc-with-srp.md) - como evitar a gravação de um aplicativo que funciona somente quando o UGC está armazenado em JCR (JSRP).
* [Refatoração de SocialUtils](socialutils.md) - métodos de utilitário para SRP que substituem SocialUtils.
* [Convenções de nomenclatura](naming-conventions.md) - convenções de nomenclatura para classes Java personalizadas.

### Scripts {#scripts}

* [Sideload de componentes das comunidades](sideloading.md) - como adicionar dinamicamente um componente após o carregamento da página.
* [Fundamentos do Editor de Rich Text](rte.md) - como personalizar a interface do usuário rich text fornecida aos membros para conteúdo de publicação.

### IDE {#ide}

* [Uso do Maven para comunidades](maven.md) - como incluir o jar da API das comunidades.
* [Refatoração de SocialUtils](socialutils.md) - métodos de utilitário para SRP que substituem SocialUtils.
