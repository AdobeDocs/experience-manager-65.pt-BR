---
title: 'Solucionar problemas do AEM durante a criação  '
seo-title: 'Solucionar problemas do AEM durante a criação  '
description: A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.
seo-description: A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 95%

---


# Solucionar problemas do AEM durante a criação  {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Ao enfrentar problemas, também é válida a verificação da lista de [Problemas conhecidos](/help/release-notes/known-issues.md) para a sua instância (pacotes de versões e serviços).

>[!NOTE]
>
>Os usuários que tiverem privilégios de administrador e quiserem resolver os problemas com o AEM, poderão utilizar os métodos de resolução de problemas descritos em [Resolução de problemas do AEM (para administradores)](/help/sites-administering/troubleshoot.md). Se você não tiver privilégios suficientes, consulte o administrador do sistema sobre como resolver os problemas do AEM.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Você fez alterações em uma página e a replicou para o site de publicação, mas a *versão antiga* da página está sendo mostrada no site de publicação.

* **Motivo**:

   * Isso pode ter várias causas, a mais frequente é o cache (o navegador local ou o Dispatcher), embora, às vezes, possa haver um problema com a fila de replicação.

* **Soluções**:

   * Há várias possibilidades aqui:
   * Confirmar se a página foi replicada corretamente. Verificar o status da página e, se necessário, o estado da fila de replicação.
   * Limpar o cache no seu navegador local e acessar a página novamente.
   * Adicionar `?` ao final do URL da página. Por exemplo:

      `http://localhost:4502/sites.html/content?`

      Isso solicitará a página diretamente do AEM e ignorará o Dispatcher. Se você receber a página atualizada, isso será uma indicação de que é necessário limpar o cache do Dispatcher.

   * Entre em contato com o administrador do sistema se houver problemas com as filas de replicação.

## Sidekick não visível {#sidekick-not-visible}

* **Problema**:

   * O sidekick não está visível durante a edição de uma página de conteúdo no ambiente de criação.

* **Motivo**:

   * Em casos raros, pode ser que você tenha posicionado o cabeçalho do sidekick fora do escopo da janela atual. Isso significa que não é possível reposicioná-lo novamente.

* **Solução**:

   * Faça logout da sessão atual e logon novamente. O sidekick retornará para a posição padrão.

## Localizar e substituir - nem todas as instâncias são substituídas {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Ao usar a opção **Localizar e substituir**, pode acontecer que nem todas as instâncias do termo `find` sejam substituídas em uma página.

* **Motivo**:

   * A capacidade de **Localizar e substituir** depende de como o conteúdo é salvo e se ele pode ser pesquisado. Por exemplo, o texto de um blog é armazenado na propriedade `jcr:text` , que não está configurada para ser pesquisada. O escopo padrão do servlet localizar e substituir abrange as seguintes propriedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solução**:

   * Essas definições podem ser alteradas com a configuração do **Servlet Localizar e substituir do Day CQ WCM** usando o **Console da Web**; por exemplo, em

      `http://localhost:4502/system/console/configMgr`

