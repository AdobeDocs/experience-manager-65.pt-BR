---
title: Solução de problemas do AEM durante a criação
description: A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 29%

---

# Solucionar problemas do AEM durante a criação  {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Em caso de problemas, vale a pena também verificar a lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para sua instância (versão e service packs).

>[!NOTE]
>
>Os usuários que têm privilégios de administrador e desejam solucionar problemas com AEM podem usar os métodos de solução de problemas descritos em [Solução de problemas do AEM (para administradores)](/help/sites-administering/troubleshoot.md). Se você não tiver privilégios suficientes, consulte o administrador do sistema para obter informações sobre como solucionar problemas de AEM.

## A versão antiga da página ainda está no site publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Você fez alterações em uma página e a replicou para o site de publicação, mas a variável *antigo* A versão da página ainda está sendo exibida no site de publicação.

* **Motivo**:

   * Isso pode ter várias causas, mais frequentemente o cache (seu navegador local ou o Dispatcher), embora possa, às vezes, ser um problema com a fila de replicação.

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

   * O Sidekick não é visível ao editar uma página de conteúdo no ambiente de criação.

* **Motivo**:

   * Em casos raros, você pode ter posicionado o cabeçalho do seu sidekick fora do escopo da sua janela atual. Isso significa que não é possível reposicioná-lo novamente.

* **Solução**:

   * Faça logout da sessão atual e login novamente. Sidekick retornará à posição padrão.

## Localizar e substituir - nem todas as instâncias são substituídas {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Ao usar o **Localizar e substituir** opção, pode acontecer que nem todas as instâncias da `find` termo são substituídos em uma página.

* **Motivo**:

   * A capacidade de **Localizar e substituir** depende de como o conteúdo é salvo e se ele pode ser pesquisado. Por exemplo, um texto de blog é armazenado em `jcr:text` propriedade que não está configurada para ser pesquisada. O escopo padrão para o servlet localizar e substituir abrange as seguintes propriedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solução**:

   * Essas definições podem ser alteradas com a configuração para **Servlet Localizar e Substituir CQ do Dia** usando o **Console da Web**; por exemplo, em

     `http://localhost:4502/system/console/configMgr`
