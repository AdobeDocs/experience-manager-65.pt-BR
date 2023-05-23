---
title: Ferramenta AEM Repo
seo-title: AEM Repo Tool
description: A ferramenta AEM Repo é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Ferramenta AEM Repo{#aem-repo-tool}

A ferramenta AEM Repo é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante ao [Ferramenta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), mas é mais rápido, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao IntelliJ e ao Eclipse para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de um `jcr_root` estrutura filevault no sistema de arquivos, a ferramenta AEM Repo cria um pacote com um único filtro para toda a subárvore e o envia para o servidor (semelhante ao FTP `put`), o busca no servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não é compatível com vários caminhos de filtro ou com o `filter.xml`.

>[!CAUTION]
>
>Observe que a ferramenta AEM Repo sempre substituirá todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A variável [A ferramenta AEM Repo está disponível no GitHub por meio deste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) juntamente com instruções detalhadas de instalação e uso.

Se quiser baixar a fonte da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
