---
title: Solução de problemas do AEM durante a criação
description: A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 25%
---
# Solucionar problemas do AEM durante a criação{#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Quando você tiver problemas, também vale a pena verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (versão e service packs).

>[!NOTE]
>
>Os usuários que têm privilégios de administrador e que desejam solucionar problemas com o AEM podem usar os métodos de solução de problemas descritos em [Solução de problemas do AEM (para Administradores)](/help/sites-administering/troubleshoot.md). Se você não tiver privilégios suficientes, consulte o administrador do sistema para obter informações sobre como solucionar problemas do AEM.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:

  * Você fez alterações em uma página e a replicou para o site de publicação, mas a versão *antiga* da página ainda está sendo exibida no site de publicação.

* **Motivo**:

  * Isso pode ter várias causas, mais frequentemente o cache (o navegador local ou o Dispatcher), embora possa, às vezes, ser um problema com a fila de replicação.

* **Soluções**:

  * Há várias possibilidades aqui:
  * Confirme se a página foi replicada corretamente. Verifique o status da página e, se necessário, o estado da fila de replicação.
  * Limpar o cache no seu navegador local e acessar a página novamente.
  * Adicionar `?` ao final da URL da página. Por exemplo:

    `http://localhost:4502/sites.html/content?`

    Isso solicitará a página diretamente do AEM e ignorará o Dispatcher. Se você receber a página atualizada, isso será uma indicação de que é necessário limpar o cache do Dispatcher.

  * Entre em contato com o administrador do sistema se houver problemas com as filas de replicação.

## Sidekick não visível {#sidekick-not-visible}

* **Problema**:

  * O Sidekick não fica visível ao editar uma página de conteúdo no ambiente de criação.

* **Motivo**:

  * Em casos raros, você pode ter posicionado o cabeçalho do seu sidekick fora do escopo da sua janela atual. Isso significa que não é possível reposicioná-lo novamente.

* **Solução**:

  * Faça logout da sessão atual e login novamente. O Sidekick retornará à posição padrão.

## Localizar e substituir - nem todas as instâncias são substituídas {#find-replace-not-all-instances-are-replaced}

* **Problema:**

  * Ao usar a opção **Localizar e Substituir**, pode acontecer que nem todas as instâncias do termo `find` sejam substituídas em uma página.

* **Motivo**:

  * A capacidade de **Localizar e substituir** depende de como o conteúdo é salvo e se ele pode ser pesquisado. Por exemplo, um texto de blog é armazenado na propriedade `jcr:text`, que não está configurada para ser pesquisada. O escopo padrão para o servlet localizar e substituir abrange as seguintes propriedades:

    * `jcr:title`
    * `jcr:description`
    * `jcr:text`
    * `text`

* **Solução**:

  * Essas definições podem ser alteradas com a configuração para o **Day CQ WCM Find Replace Servlet** usando o **Console da Web**; por exemplo, em

    `http://localhost:4502/system/console/configMgr`
