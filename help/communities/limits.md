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
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Limites de contribuição dos membros {#member-contribution-limits}

## Visão geral {#overview}

O recurso de limites de contribuição oferece a capacidade de limitar as contribuições dos membros da comunidade como meio de proteger contra spam.

Quando um membro é limitado, qualquer postagem que exceda o número permitido de contribuições resultará em um alerta de que o limite foi excedido e a postagem é rejeitada. O membro da comunidade pode então ir para o centro de mensagens da comunidade e entrar em contato com um gerente da comunidade que pode remover os limites, se apropriado.

Os limites de contribuição podem ser ativados individualmente a partir do [console Membros](members.md) e/ou configurados para serem ativados automaticamente quando os visitantes do site se tornam novos membros.

Usando o console Membros , os limites de contribuição podem ser removidos de forma proativa para um membro por um gerente de comunidade a qualquer momento ou removidos de forma reativa quando um membro envia uma mensagem para um gerente de comunidade que faz tal solicitação.

## Configuração dos limites de contribuição de conteúdo gerado pelo usuário do AEM Communities {#aem-communities-user-generated-content-contribution-limits-configuration}

Essa configuração OSGi:

* Define as características dos limites de contribuição (número de lugares em um período).
* Identifica quem o membro poderá enviar a mensagem quando o limite for atingido.
* Identifica domínios que nunca precisam ser restritos.

Para acessar essa configuração do OSGi:

* No editor principal:
* Faça logon com privilégios de administrador.
* Acesse o [Console da Web](../../help/sites-deploying/configuring-osgi.md).

   * Por exemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localize `AEM Communities User Generated Content Contribution Limits Configuration`.
* Selecione o ícone de edição.

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL Aplicar automaticamente limites de contribuição de UGC]**

   Se marcada, defina automaticamente os limites de contribuição para os usuários quando eles se registrarem como membros da comunidade. Isso é refletido no perfil do membro da comunidade e pode ser ativado/desativado no [console de membros](members.md). Os novos membros com um endereço de email de uma lista de permissões de domínios nunca são restritos.

   O padrão está desmarcado.

* **[!UICONTROL Limite de UGC]**

   Número máximo de contribuições.

   O padrão é 10 publicações.

* **[!UICONTROL Frequência do limite UGC]**

   O período que restringe o limite de UGC.

   O padrão é 60 minutos.

* **[!UICONTROL Domínios]**

   Uma lista de  lista de permissões de um ou mais domínios de email. Selecione o ícone + para fazer entradas adicionais.

   Os usuários com endereços de email na lista de permissões de domínios não são afetados quando os limites de contribuição do UGC são aplicados automaticamente. Por exemplo, se o domínio `mycompany.com` for adicionado à lista de domínios, um membro com endereço de email `me@mycompany.com` nunca será restrito da publicação.

   O padrão é uma  lista de permissões vazia.

* **[!UICONTROL Recipients de mensagens]**

   Lista de um ou mais IDs autorizados de membros que podem alterar os limites de contribuição dos membros. Selecione o ícone + para fazer entradas adicionais.

   Os membros só podem alcançar membros específicos quando o seu limite tenha sido atingido.

   O padrão não é destinatários de mensagens.

Observação: A configuração padrão resulta em um limite de 10 publicações dentro de um período de uma hora.
