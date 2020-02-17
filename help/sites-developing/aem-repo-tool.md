---
title: Ferramenta AEM Repo
seo-title: Ferramenta AEM Repo
description: A AEM Repo Tool é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
seo-description: A AEM Repo Tool é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ferramenta AEM Repo{#aem-repo-tool}

A AEM Repo Tool é uma solução simples para transferir o conteúdo do JCR entre o sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A AEM Repo Tool é semelhante à ferramenta [](/help/sites-developing/ht-vlttool.md)Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao IntelliJ e ao Eclipse para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de uma estrutura de `jcr_root` filevault no sistema de arquivos, a AEM Repo Tool cria um pacote com um único filtro para toda a subárvore e empurra-o para o servidor (semelhante ao FTP `put`), o obtém do servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não oferece suporte a vários caminhos de filtro ou ao FileVault `filter.xml`.

>[!CAUTION]
>
>Observe que a AEM Repo Tool sempre substituirá o arquivo ou diretório inteiro especificado.

## Download e documentação {#download-and-documentation}

A ferramenta [AEM Repo está disponível no GitHub por meio deste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) , juntamente com instruções detalhadas de instalação e uso.

Se desejar baixar a fonte da AEM Repo Tool, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

