---
title: Solução de problemas AEM durante a criação
description: A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 29%

---

# Solucionar problemas do AEM durante a criação  {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Ao enfrentar problemas, também vale a pena verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (pacotes de versões e serviços).

>[!NOTE]
>
>Os usuários que tiverem privilégios de administrador e quiserem resolver problemas com o AEM, poderão utilizar os métodos de resolução de problemas descritos em [AEM de solução de problemas (para administradores)](/help/sites-administering/troubleshoot.md). Se você não tiver privilégios suficientes, consulte o administrador do sistema sobre AEM de solução de problemas.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Você fez alterações em uma página e replicou a página para o site de publicação, mas a variável *old* A versão da página ainda está sendo exibida no site de publicação.

* **Motivo**:

   * Isso pode ter várias causas, na maioria das vezes o cache (seu navegador local ou o Dispatcher), embora, às vezes, possa ser um problema com a fila de replicação.

* **Soluções**:

   * Há várias possibilidades aqui:
   * Confirme se a página foi replicada corretamente. Verifique o status da página e, se necessário, o estado da fila de replicação.
   * Limpar o cache no seu navegador local e acessar a página novamente.
   * Adicionar `?` ao final do URL da página. Por exemplo:

      `http://localhost:4502/sites.html/content?`

      Isso solicitará a página diretamente do AEM e ignorará o Dispatcher. Se você receber a página atualizada, isso será uma indicação de que é necessário limpar o cache do Dispatcher.

   * Entre em contato com o administrador do sistema se houver problemas com as filas de replicação.

## Sidekick não visível {#sidekick-not-visible}

* **Problema**:

   * O Sidekick não está visível ao editar uma página de conteúdo no ambiente do autor.

* **Motivo**:

   * Em casos raros, você pode ter posicionado o cabeçalho do sidekick fora do escopo da janela atual. Isso significa que não é possível reposicioná-lo novamente.

* **Solução**:

   * Faça logout da sessão atual e login novamente. O sidekick retornará à posição padrão.

## Localizar e substituir - nem todas as instâncias são substituídas {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Ao usar a variável **Localizar e Substituir** pode acontecer que nem todas as instâncias do `find` são substituídos em uma página.

* **Motivo**:

   * A capacidade de **Localizar e Substituir** depende de como o conteúdo é salvo e se ele pode ser pesquisado. Por exemplo, um texto de blog é armazenado em `jcr:text` propriedade que não está configurada para ser pesquisada. O escopo padrão do servlet localizar e substituir abrange as seguintes propriedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solução**:

   * Essas definições podem ser alteradas com a configuração de **Servlet Localizar e substituir do Day CQ WCM** usando o **Console da Web**; por exemplo, em

      `http://localhost:4502/system/console/configMgr`
