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
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 74%

---

# Exportar para CSV  {#export-to-csv}

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
   * Apenas secundários diretos
   * Níveis adicionais de secundários
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
