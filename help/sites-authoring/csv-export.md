---
title: Exportar para CSV
description: Exportar informações sobre suas páginas para um arquivo CSV em seu sistema local
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 74%
---
# Exportar para CSV{#export-to-csv}

**Criar relatórios de arquivos CSV** permite exportar informações sobre suas páginas para um arquivo CSV em seu sistema local.

* O arquivo baixado é chamado de `export.csv`
* Os conteúdos dependem das propriedades que você selecionar.
* É possível definir o caminho junto com o detalhamento da exportação.

>[!NOTE]
>
>O recurso para download e o destino padrão do seu navegador são usados.

O assistente **Criar exportação de arquivos CSV** permite selecionar:

* Propriedades para exportar
  * Metadados
    * Nome
    * Modificado
    * Publicado
    * Modelo
    * Fluxo de trabalho
  * Tradução
    * Traduzido
  * Analytics
    * Visualizações de página
    * Visitantes únicos
    * Tempo na página
* Profundidade
  * Caminho principal
  * Apenas filhos diretos
  * Níveis adicionais de filhos
  * Níveis

O arquivo `export.csv` resultante pode ser aberto no Excel ou qualquer outro aplicativo compatível.

![etc-01](assets/etc-01.png)

A opção criar **Relatório CSV** está disponível ao navegar pelo console **Sites** (no modo de exibição de Lista): é uma opção do menu suspenso **Criar**:

![etc-02](assets/etc-02.png)

Para criar uma exportação de arquivos CSV:

1. Abra o console **Sites** e navegue até o local desejado, se necessário.
1. Na barra de ferramentas, selecione **Criar**, em seguida, **Relatórios de arquivos CSV** para abrir o assistente:

   ![etc-03](assets/etc-03.png)

1. Selecione as propriedades necessárias para exportar.
1. Selecione **Criar**.
