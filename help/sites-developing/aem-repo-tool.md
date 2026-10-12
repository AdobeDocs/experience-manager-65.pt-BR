---
title: Ferramenta AEM Repo
description: A ferramenta AEM Repo é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor do AEM por meio da linha de comando comparável ao FTP. A ferramenta AEM Repo é semelhante à ferramenta Jackrabbit FileVault, mas é mais rápida, tem dependências mínimas e é um script bash simples.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%
---
# Ferramenta AEM Repo{#aem-repo-tool}

A AEM Repo Tool é uma solução simples para transferir conteúdo JCR entre seu sistema de arquivos local e o servidor do AEM por meio da linha de comando comparável ao FTP. A AEM Repo Tool é semelhante à [ferramenta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), mas é mais rápida, tem dependências mínimas e é um script bash simples.

Essa ferramenta simplifica a transferência de arquivos para o desenvolvedor e também pode ser integrada ao IntelliJ e ao Eclipse para tornar o desenvolvimento ainda mais eficiente.

## Visão geral {#overview}

Para um determinado caminho dentro de uma estrutura de cofre de arquivos `jcr_root` no sistema de arquivos, a Ferramenta de Repositório do AEM cria um pacote com um único filtro para toda a subárvore e o envia por push ao servidor (semelhante ao FTP `put`), o busca no servidor ( `get`) ou compara as diferenças ( `status` e `diff`).

A ferramenta não oferece suporte a vários caminhos de filtro ou ao `filter.xml` do FileVault.

>[!CAUTION]
>
>A AEM Repo Tool sempre substitui todo o arquivo ou diretório especificado.

## Download e documentação {#download-and-documentation}

A [AEM Repo Tool está disponível no GitHub neste link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo), juntamente com instruções detalhadas de instalação e uso.

Se quiser baixar a origem da ferramenta AEM Repo, consulte o projeto GitHub vinculado abaixo.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto de ferramentas no GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
