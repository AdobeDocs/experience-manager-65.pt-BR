---
title: Pacotes OSGI
seo-title: OSGI Bundles
description: Dicas para gerenciar seus pacotes OSGi
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Pacotes OSGI{#osgi-bundles}

## Usar controle de versão semântico {#use-semantic-versioning}

As práticas recomendadas acordadas para a numeração semântica de versão podem ser encontradas em [https://semver.org/](https://semver.org/).

## Não incorpore mais classes e jars do que o estritamente necessário em pacotes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Bibliotecas comuns devem ser fatoradas em pacotes separados. Isso permitirá que eles sejam reutilizados em seus pacotes. Ao envolver um *JAR* em um pacote OSGI, verifique as fontes online para ver se alguém já fez isso antes. Alguns locais comuns para encontrar wrappers de pacote existentes são: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e SpringSource Enterprise Bundle Repository.

## Depende das versões mais baixas necessárias do pacote {#depend-on-the-lowest-needed-bundle-versions}

Para dependências de tempo de compilação em arquivos POM, sempre dependa da versão mais baixa necessária que expõe a API necessária. Isso permitirá maior compatibilidade com versões anteriores e facilita as correções para versões anteriores.

## Exportar um conjunto mínimo de pacotes de pacotes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Assim que um pacote é exportado, criamos uma API da qual outros podem depender. Exporte o mínimo possível e verifique se o que está sendo exportado é uma API. É muito mais fácil pegar um método/classe privado e torná-lo público do que pegar algo que foi exportado anteriormente e torná-lo privado.

As implementações devem sempre ser colocadas em uma *impl* pacote. Por padrão, a variável *maven-bundle-plugin* exportará qualquer item do projeto que não tenha uma *impl* em seu nome.

## Sempre defina explicitamente uma versão semântica para cada pacote exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Isso permitirá que os consumidores da sua API evoluam junto com você. Ao fazer isso, sempre siga as práticas recomendadas de controle de versão semântico. Isso permitirá que os consumidores da API saibam quais tipos de alterações esperar em uma nova versão.

## Incluir informações de metatipo quando expostas {#include-metatype-information-where-exposed}

Especificando informações significativas do metatipo, os seus serviços e componentes serão mais fáceis de entender no console Felix. Uma lista de anotações e atributos de SCR pode ser encontrada em: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
