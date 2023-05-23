---
title: Diretrizes de codificação
seo-title: Coding Guidelines
description: Diretrizes, dicas e truques do desenvolvedor do Communities
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
