---
title: Pacotes OSGi
description: Saiba mais sobre algumas dicas para gerenciar seus pacotes OSGi no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Pacotes OSGi{#osgi-bundles}

## Usar controle de versão semântico {#use-semantic-versioning}

As práticas recomendadas acordadas para a numeração semântica de versão podem ser encontradas em [https://semver.org/](https://semver.org/).

## Não incorpore mais classes e jars do que o estritamente necessário em pacotes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Bibliotecas comuns devem ser fatoradas em pacotes separados. Isso permite que eles sejam reutilizados em seus pacotes. Ao envolver um *JAR* em um pacote OSGi, verifique as fontes online para ver se alguém já fez isso antes. Alguns locais comuns para encontrar wrappers de pacote existentes são: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e SpringSource Enterprise Bundle Repository.

## Depende das versões mais baixas necessárias do pacote {#depend-on-the-lowest-needed-bundle-versions}

Para dependências de tempo de compilação em arquivos POM, sempre dependa da versão mais baixa necessária que expõe a API necessária. Isso permite maior compatibilidade com versões anteriores e facilita as correções nas versões anteriores.

## Exportar um conjunto mínimo de pacotes de pacotes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Quando um pacote é exportado, uma API é criada para que outras pessoas dependam dele. Exporte o mínimo possível e verifique se o que está sendo exportado é uma API. É muito mais fácil pegar um método/classe privado e torná-lo público do que pegar algo que foi exportado anteriormente e torná-lo privado.

Sempre coloque as implementações em uma *impl* pacote. Por padrão, a variável *maven-bundle-plugin* exporta qualquer item no projeto que não tenha uma *impl* em seu nome.

## Sempre defina explicitamente uma versão semântica para cada pacote exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Isso permite que os consumidores da API evoluam junto com você. Ao fazer isso, sempre siga as práticas recomendadas de controle de versão semântico. Isso permite que os consumidores da API saibam quais tipos de alterações esperar em uma nova versão.

## Incluir informações de metatipo quando expostas {#include-metatype-information-where-exposed}

Especificando informações significativas de metatipo, facilita a compreensão de seus serviços e componentes no console Felix. Uma lista de anotações e atributos de SCR pode ser encontrada em: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
