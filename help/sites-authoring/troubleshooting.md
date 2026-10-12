---
title: Solução de problemas ao criar páginas no AEM
description: Alguns problemas que você pode encontrar ao usar o AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 39%
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

    * `http://localhost:4502/sites.html/content?`
    * Isso solicitará a página diretamente do AEM e ignorará o Dispatcher. Se você receber a página atualizada, isso será uma indicação de que é necessário limpar o cache do Dispatcher.

  * Entre em contato com o administrador do sistema se houver problemas com as filas de replicação.

## Ações de componentes não visíveis na barra de ferramentas {#component-actions-not-visible-on-toolbar}

* **Problema**:

  * A ampla variedade de ações aplicáveis do componente não é visível ao editar uma página de conteúdo no ambiente do autor.

* **Motivo**:

  * Em casos raros, uma ação anterior pode afetar a barra de ferramentas.

* **Solução**:

  * Atualize a página.
