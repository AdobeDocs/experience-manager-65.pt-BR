---
title: O Verificador de links externos
seo-title: O Verificador de links externos
description: Saiba mais sobre o Verificador de links externos no AEM.
seo-description: Saiba mais sobre o Verificador de links externos no AEM.
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# O Verificador de links externos{#the-external-link-checker}

Um verificador de links externo é fornecido no AEM. O verificador de links:

* verifica todas as páginas de conteúdo
* gera uma lista de todos os links válidos e inválidos
* marca links inválidos como quebrados in situ em páginas de conteúdo individuais

## Como validar links externos {#how-to-validate-external-links}

Para usar o verificador de links externos:

1. Usando **Navegação**, selecione **Ferramentas** e, em seguida, **Sites**.
1. Selecione **Verificador de links externos**, uma lista de todos os links externos é gerada.
1. Valide um link específico selecionando-o na lista e clicando em **Verificar**:

   ![](assets/telc-01.png)

   As informações são exibidas:

   * **** Status do link
   * **URL**
   * **Referenciador**
   * hora desde que o link foi **Última verificação** (validado)
   * **Último Estado** devolvido

   * desde que o link foi **Último Disponível**
   * desde que o link foi **Último acesso**

1. Nas páginas de conteúdo individuais, os links inválidos serão exibidos como quebrados:

   ![](assets/chlimage_1-143.png)