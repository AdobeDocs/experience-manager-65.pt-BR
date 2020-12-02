---
title: Ferramenta AEM Repo
seo-title: Ferramenta AEM Repo
description: A ferramenta AEM Repo é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM pela linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
seo-description: A ferramenta AEM Repo é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM pela linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Ferramenta AEM Repo{#aem-repo-tool}

A ferramenta AEM Repo é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM pela linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à [ferramenta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), mas é mais rápida, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao IntelliJ e ao Eclipse para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de uma estrutura de arquivo `jcr_root` no sistema de arquivos, AEM ferramenta Repo cria um pacote com um único filtro para toda a subárvore e o empurra para o servidor (similar ao FTP `put`), o obtém do servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não suporta vários caminhos de filtro ou `filter.xml` do FileVault.

>[!CAUTION]
>
>Observe que a ferramenta AEM Repo sempre substituirá todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A [AEM Ferramenta de acordo de recompra está disponível no GitHub por meio deste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto com instruções detalhadas de instalação e uso.

Se desejar baixar a fonte da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

