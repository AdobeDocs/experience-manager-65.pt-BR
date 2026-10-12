---
title: Suporte a cookies Same Site para o AEM 6.5
description: Saiba mais sobre o Suporte a cookies do mesmo site para o AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 78%
---
# Suporte a cookies Same Site para o AEM 6.5 {#same-site-cookie-support-for-aem-65}

Desde a versão 80, o Chrome e, mais tarde, o Safari introduziram um novo modelo para segurança de cookies. Esse modo é projetado para introduzir controles de segurança em torno da disponibilidade de cookies para sites de terceiros, por meio de uma configuração chamada `SameSite`. Para obter informações mais detalhadas, consulte este artigo [web.dev - SameSite cookies explained](https://web.dev/samesite-cookies-explained/).

O valor padrão dessa configuração (`SameSite=Lax`) pode fazer com que a autenticação entre instâncias ou serviços AEM não funcione. Isso ocorre porque os domínios ou as estruturas de URL desses serviços podem não se enquadrar nas restrições dessa política de cookie.

Para contornar isso, você precisa definir o atributo de cookie `SameSite` como `None` para o token de logon.

>[!CAUTION]
>
>A configuração `SameSite=None` só é aplicada se o protocolo for seguro (HTTPS).
>
>Se o protocolo não for seguro (HTTP), a configuração será ignorada e o servidor exibirá esta mensagem de AVISO:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

É possível adicionar a configuração seguindo as etapas abaixo:

1. Vá para o Console da Web em `http://serveraddress:serverport/system/console/configMgr`
1. Pesquise e clique em **Manipulador de autenticação de token do Adobe Granite**
1. Defina o **atributo SameSite para o cookie de token de logon** para `None`, conforme mostrado na imagem abaixo
   ![samesite](assets/samesite1.png)
1. Clique em Salvar
1. Depois que esta configuração for atualizada e os usuários forem desconectados e conectados novamente, os cookies `login-token` terão o atributo `None` definido e serão incluídos em solicitações entre sites.
