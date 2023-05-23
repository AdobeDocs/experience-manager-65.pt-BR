---
title: Limites de contribuição do membro
seo-title: Member Contribution Limits
description: O recurso de limites de contribuição permite limitar as contribuições para proteger contra spam
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---

# Limites de contribuição do membro {#member-contribution-limits}

## Visão geral {#overview}

O recurso de limites de contribuição oferece a capacidade de limitar as contribuições dos membros da comunidade como um meio de proteção contra spam.

Quando um membro é limitado, qualquer postagem que exceda o número permitido de contribuições resultará em um alerta de que o limite foi excedido e a postagem é rejeitada. O membro da comunidade pode então ir para o centro de mensagens da comunidade e entrar em contato com um gerente da comunidade que pode remover os limites, se apropriado.

Os limites de contribuição podem ser habilitados individualmente do [Console de membros](members.md) e/ou configurada para ser ativada automaticamente quando os visitantes do site se tornarem novos membros.

Usando o console Membros, os limites de contribuição podem ser removidos de forma proativa para um membro por um gerente da comunidade a qualquer momento, ou removidos de forma reativa quando um membro envia uma mensagem a um gerente da comunidade que faz essa solicitação.

## Configuração de limites de contribuição de conteúdo gerado pelo usuário do AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Esta configuração OSGi:

* Define as características dos limites de contribuição (número de postagens em um período de tempo).
* Identifica quem o membro poderá enviar mensagens quando o limite for atingido.
* Identifica domínios que nunca precisam ser restritos.

Para acessar essa configuração OSGi:

* No editor principal:
* Faça logon com privilégios de administrador.
* Acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md).

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `AEM Communities User Generated Content Contribution Limits Configuration`.
* Selecione o ícone de edição.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Aplicar automaticamente limites de contribuição de UGC]**

   Se marcadas, definem automaticamente limites de contribuição para os usuários quando eles se registrarem como membros da comunidade. Isso é refletido no perfil do membro da comunidade e pode ser ativado/desativado no [console de membros](members.md). Novos membros com um endereço de email de um incluo na lista de permissões de domínios nunca são restritos.

   O padrão está desmarcado.

* **[!UICONTROL Limite de UGC]**

   Número máximo de contribuições.

   O padrão é 10 publicações.

* **[!UICONTROL Frequência limite de UGC]**

   O período que restringe o limite de UGC.

   O padrão é 60 minutos.

* **[!UICONTROL Domínios]**

   Uma lista de inclui na lista de permissões de um ou mais domínios de email. Selecione o ícone + para criar entradas adicionais.

   Lista de permissões Os usuários com endereços de email na pesquisa de domínios não são afetados quando os limites de contribuição UGC são aplicados automaticamente. Por exemplo, se o domínio `mycompany.com` é adicionado à lista de domínios e, em seguida, um membro com endereço de email `me@mycompany.com` nunca está restrito ao lançamento.

   O padrão é uma inclui na lista de permissões vazia.

* **[!UICONTROL Destinatários de mensagens]**

   Lista de uma ou mais IDs autorizadas de membros que podem modificar os limites de contribuição para membros. Selecione o ícone + para criar entradas adicionais.

   Os membros só podem alcançar membros especificados quando o limite foi atingido.

   O padrão é nenhum destinatário de mensagem.

Observação: a configuração padrão resulta em um limite de 10 publicações em um período de uma hora.
