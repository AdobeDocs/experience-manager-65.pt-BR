---
title: Exportar para CSV
seo-title: Export to CSV
description: Exportar informações sobre suas páginas para um arquivo CSV em seu sistema local
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 81%

---

# Exportar para CSV  {#export-to-csv}

**Criar relatórios de arquivos CSV** permite exportar informações sobre suas páginas para um arquivo CSV em seu sistema local.

* O arquivo baixado é chamado de `export.csv`
* Os conteúdos dependem das propriedades que você selecionar.
* É possível definir o caminho junto com o detalhamento da exportação.

>[!NOTE]
>
>O recurso para download e o destino padrão do seu navegador são usados.

A variável **Criar exportação de arquivos CSV** permite selecionar:

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

A opção criar **Relatório CSV** está disponível ao navegar pelo **Sites** console (na exibição de Lista): é uma opção da variável **Criar** menu suspenso:

![etc-02](assets/etc-02.png)

Para criar uma exportação de arquivos CSV:

1. Abra o console **Sites** e navegue até o local desejado, se necessário.
1. Na barra de ferramentas, selecione **Criar**, em seguida, **Relatórios de arquivos CSV** para abrir o assistente:

   ![etc-03](assets/etc-03.png)

1. Selecione as propriedades necessárias para exportar.
1. Selecione **Criar**.
