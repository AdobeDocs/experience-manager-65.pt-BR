---
title: Limites de contribuição dos membros
seo-title: Limites de contribuição dos membros
description: O recurso de limites de contribuição permite limitar as contribuições para proteção contra spam
seo-description: O recurso de limites de contribuição permite limitar as contribuições para proteção contra spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# Limites de contribuição dos membros {#member-contribution-limits}

## Visão geral {#overview}

O recurso de limites de contribuição oferece a capacidade de limitar as contribuições dos membros da comunidade como forma de proteção contra spam.

Quando um membro é limitado, qualquer postagem que exceda o número permitido de contribuições resultará em um alerta de que o limite foi excedido e a postagem é rejeitada. O membro da comunidade pode então ir ao centro de mensagens da comunidade e entrar em contato com um gerente da comunidade que pode remover os limites, se apropriado.

Os limites de contribuição podem ser ativados individualmente no console [](members.md) Membros e/ou configurados para serem automaticamente ativados quando os visitantes do site se tornarem novos membros.

Usando o console Membros, os limites de contribuição podem ser removidos de forma proativa para um membro por um gerente da comunidade a qualquer momento ou removidos de forma reativa quando um membro envia uma mensagem para um gerente da comunidade que faz tal solicitação.

## Configuração de limites de contribuição de conteúdo gerado pelo usuário do AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Esta configuração OSGi:

* Define as características dos limites de contribuição (número de postagens em um período).
* Identifica quem o membro poderá enviar uma mensagem quando o limite for atingido.
* Identifica domínios que nunca precisam ser restringidos.

Para atingir essa configuração do OSGi:

* No editor principal:
* Faça logon com privilégios de administrador.
* Acesse o Console [da Web](../../help/sites-deploying/configuring-osgi.md).

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize `AEM Communities User Generated Content Contribution Limits Configuration`.
* Selecione o ícone de edição.

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL Aplicar automaticamente limites de contribuição UGC]**

   Se marcada, defina automaticamente os limites de contribuição para os usuários quando eles se registrarem como membros da comunidade. Isso se reflete no perfil do membro da comunidade e pode ser ativado/desativado no console [de](members.md)membros. Os novos membros com um endereço de email de um domínio listado em branco nunca são restringidos.

   O padrão está desmarcado.

* **[!UICONTROL Limite UGC]**

   Número máximo de contribuições.

   O padrão é 10 postagens.

* **[!UICONTROL Frequência limite UGC]**

   O período que restringe o limite de UGC.

   O padrão é 60 minutos.

* **[!UICONTROL Domínios]**

   Uma lista branca de um ou mais domínios de email. Selecione o ícone + para fazer entradas adicionais.

   Os usuários com endereços de email nos domínios da lista branca não são afetados quando os limites de contribuição UGC são aplicados automaticamente. Por exemplo, se o domínio `mycompany.com` for adicionado à lista de domínios, um membro com endereço de email nunca `me@mycompany.com` será restringido à publicação.

   O padrão é uma lista branca vazia.

* **[!UICONTROL Recipient de mensagens]**

   Lista de uma ou mais IDs autorizadas de membros capazes de alterar os limites de contribuição dos membros. Selecione o ícone + para fazer entradas adicionais.

   Os membros só podem alcançar determinados membros quando o seu limite tiver sido atingido.

   O padrão não é nenhum recipient de mensagem.

Observação: A configuração padrão resulta em um limite de 10 publicações dentro de um período de uma hora.
