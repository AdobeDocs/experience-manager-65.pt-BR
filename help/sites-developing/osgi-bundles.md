---
title: Pacotes OSGI
seo-title: Pacotes OSGI
description: Dicas para gerenciar seus pacotes OSGi
seo-description: Dicas para gerenciar seus pacotes OSGi
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Pacotes OSGI{#osgi-bundles}

## Usar controle de versão semântico {#use-semantic-versioning}

As práticas recomendadas para a numeração semântica de versão aprovadas podem ser encontradas em [https://semver.org/](https://semver.org/).

## Não incorpore mais classes e jars do que o estritamente necessário em pacotes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

As bibliotecas comuns devem ser integradas em pacotes separados. Isso permitirá que eles sejam reutilizados em seus pacotes. Ao vincular um *JAR* em um pacote OSGI, verifique as fontes online para ver se alguém já fez isso antes. Alguns locais comuns para encontrar invólucros de pacotes existentes são: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Receitas do pacote Eclipse e o Repositório do pacote SpringSource Enterprise.

## Depende das versões de pacote mais baixas necessárias {#depend-on-the-lowest-needed-bundle-versions}

Para as dependências de tempo de compilação em arquivos POM, sempre dependa da versão mais baixa necessária que exponha a API necessária. Isso permitirá uma maior compatibilidade com versões anteriores e facilitará as correções de backporting para versões mais antigas.

## Exportar um conjunto mínimo de pacotes de pacotes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Assim que um pacote é exportado, criamos uma API para que outras pessoas dependam. Certifique-se de exportar o mínimo possível e verifique se o que está sendo exportado é uma API. É muito mais fácil pegar um método/classe privado e torná-lo público do que pegar algo que antes era exportado e torná-lo privado.

As implementações devem ser sempre colocadas em um pacote separado *impl*. Por padrão, o *maven-bundle-plugin* exportará qualquer item no projeto que não tenha um *impl* no seu nome.

## Sempre definir explicitamente uma versão semântica para cada pacote exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Isso permitirá que os consumidores de sua API evoluam junto com você. Ao fazer isso, siga sempre as práticas recomendadas de controle de versão semântica. Isso permitirá que os consumidores de sua API saibam que tipos de alterações devem ser esperadas em uma nova versão.

## Incluir informações de metatótipo quando exposto {#include-metatype-information-where-exposed}

Ao especificar informações significativas de metatótipo, seus serviços e componentes serão mais fáceis de entender no console do Felix. Uma lista de anotações e atributos SCR pode ser encontrada em: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
