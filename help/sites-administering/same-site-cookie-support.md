---
title: Suporte a cookie do mesmo site para AEM 6.5
description: Suporte a cookie do mesmo site para AEM 6.5
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 55%

---

# Suporte a cookie do mesmo site para AEM 6.5 {#same-site-cookie-support-for-aem-65}

Desde a versão 80, o Chrome e, mais tarde, o Safari introduziram um novo modelo para segurança de cookies. Esse modo foi projetado para introduzir controles de segurança sobre a disponibilidade de cookies para sites de terceiros, por meio de uma configuração chamada `SameSite`. Para obter informações mais detalhadas, consulte este [artigo](https://web.dev/samesite-cookies-explained/).

O valor padrão dessa configuração (`SameSite=Lax`) pode fazer com que a autenticação entre instâncias ou serviços AEM não funcione. Isso ocorre porque os domínios ou as estruturas de URL desses serviços podem não se enquadrar nas restrições dessa política de cookie.

Para contornar isso, você precisa definir a variável `SameSite` atributo de cookie para `None` para o token de logon.

>[!CAUTION]
>
>O `SameSite=None` só é aplicada se o protocolo for seguro (HTTPS).
>
>Se o protocolo não for seguro (HTTP), a configuração será ignorada e o servidor exibirá esta mensagem AVISO:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Você pode adicionar a configuração seguindo as etapas abaixo:

1. Vá para o Console da Web em `http://serveraddress:serverport/system/console/configMgr`
1. Pesquise e clique em **Manipulador de autenticação de token do Adobe Granite**
1. Defina o **atributo SameSite para o cookie de token de logon** para `None`, conforme mostrado na imagem abaixo
   ![samesite](assets/samesite1.png)
1. Clique em Salvar
1. Depois que esta configuração for atualizada e os usuários forem desconectados e conectados novamente, os cookies `login-token` terão o atributo `None` definido e serão incluídos em solicitações entre sites.
