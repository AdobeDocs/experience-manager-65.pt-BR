---
title: Diretrizes de codificação
seo-title: Diretrizes de codificação
description: Orientações, dicas e truques do desenvolvedor das comunidades
seo-description: Orientações, dicas e truques do desenvolvedor das comunidades
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Diretrizes de codificação {#coding-guidelines}

## Diretrizes, dicas e truques {#guidelines-tips-and-tricks}

Trabalhar com a AEM Communities evoluiu de uma grande dependência das Páginas do Java Server para uma flexibilidade na escolha de modelar as linguagens de script, onde a lógica comercial, o estilo e o conteúdo da página são distintos entre si.

Mais flexibilidade ao trabalhar com conteúdo gerado pelo usuário (UGC) é através da API do SocialResourceProvider, que elimina a necessidade de saber qual opção [SRP](srp.md) foi escolhida para a implantação.

Veja a seguir várias diretrizes de codificação e práticas recomendadas para desenvolvedores AEM Communities:

### Código {#code}

* [Acessar o UGC com SRP](accessing-ugc-with-srp.md)  - como evitar gravar um aplicativo que só funciona quando o UGC é armazenado no JCR (JSRP).
* [Refatoração](socialutils.md)  SocialUtils - métodos de utilitário para SRP que substituem SocialUtils.
* [Convenções](naming-conventions.md)  de nomenclatura - convenções de nomenclatura para classes Java personalizadas.

### Scripts {#scripts}

* [Componentes](sideloading.md)  de comunidades de sideload - como adicionar dinamicamente um componente após o carregamento da página.
* [Rich Text Editor Essentials](rte.md)  - como personalizar a interface de usuário Rich Text fornecida aos membros para publicação de conteúdo.

### IDE {#ide}

* [Usando o Maven for Communities](maven.md)  - como incluir o pod de API Communities.
* [Refatoração](socialutils.md)  SocialUtils - métodos de utilitário para SRP que substituem SocialUtils.

