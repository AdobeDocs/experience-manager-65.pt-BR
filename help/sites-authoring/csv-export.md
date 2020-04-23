---
title: 'Exportar para CSV  '
seo-title: 'Exportar para CSV  '
description: Exportar informações sobre suas páginas em um arquivo CSV em seu sistema local
seo-description: Exportar informações sobre suas páginas em um arquivo CSV em seu sistema local
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 317093bce043ff2aaa5b5ceb8499f057fa9fa24b

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

* Propriedades a serem exportadas
   * Metadados
      * Nome
      * Modificado
      * Publicado
      * Modelo
      * Fluxo de trabalho
   * Tradução
      * Traduzido
   * Análise
      * Exibições da página
      * Visitantes únicos
      * Tempo na página
* Profundidade
   * Caminho pai
   * Apenas secundários diretos
   * Níveis adicionais de secundários
   * Níveis

O arquivo `export.csv` resultante pode ser aberto no Excel ou qualquer outro aplicativo compatível.

![etc-01](assets/etc-01.png)

The create **CSV Report** option is available when browsing the **Sites** console (in List view): it is an option of the **Create** drop down menu:

![etc-02](assets/etc-02.png)

Para criar uma exportação de arquivos CSV:

1. Abra o console **Sites** e navegue até o local desejado, se necessário.
1. Na barra de ferramentas, selecione **Criar**, em seguida, **Relatórios de arquivos CSV** para abrir o assistente:

   ![etc-03](assets/etc-03.png)

1. Selecione as propriedades desejadas para exportar.
1. Selecione **Criar**.
