---
title: Suporte a cookie do mesmo site para AEM 6.5
description: Suporte a cookie do mesmo site para AEM 6.5
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Suporte a cookies do mesmo site para AEM 6.5 {#same-site-cookie-support-for-aem-65}

Desde a versão 80, Chrome e posterior Safari, introduziu um novo modelo para segurança de cookies. Esse modo foi projetado para introduzir controles de segurança sobre a disponibilidade de cookies para sites de terceiros, por meio de uma configuração chamada `SameSite`. Para obter informações mais detalhadas, consulte este [artigo](https://web.dev/samesite-cookies-explained/).

O valor padrão dessa configuração (`SameSite=Lax`) pode fazer com que a autenticação entre instâncias ou serviços AEM não funcione. Isso ocorre porque os domínios ou as estruturas de URL desses serviços podem não se enquadrar nas restrições dessa política de cookie.

Para contornar isso, você precisa definir o atributo de cookie SameSite como `None` para o token de logon.

Você pode fazer isso seguindo as etapas abaixo:

1. Vá para o Console da Web em `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Manipulador de Autenticação de Token do Adobe Granite**
1. Defina o atributo **SameSite para o cookie de token de login** como `None`, conforme mostrado na imagem abaixo
   ![samesite](assets/samesite1.png)
1. Clique em Salvar
1. Depois que essa configuração for atualizada e os usuários forem desconectados e conectados novamente, os cookies `login-token` terão o atributo `None` definido e serão incluídos nas solicitações entre sites.
