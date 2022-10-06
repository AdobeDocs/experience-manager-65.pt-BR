---
title: Solucionar problemas do AEM durante a criação
seo-title: Troubleshooting AEM when Authoring
description: Alguns problemas que podem ocorrer quando você usa o AEM
seo-description: Some issues that you might encounter when using AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# Solucionar problemas do AEM durante a criação  {#troubleshooting-aem-when-authoring}

A seção a seguir aborda alguns problemas que você poderá enfrentar ao usar o AEM, junto com sugestões sobre como resolvê-los.

>[!NOTE]
>
>Ao enfrentar problemas, também é válida a verificação da lista de [Problemas conhecidos](/help/release-notes/release-notes.md) para a sua instância (pacotes de versões e serviços).

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
