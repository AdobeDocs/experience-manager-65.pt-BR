---
title: Fundamentos das Atribuições
seo-title: Fundamentos das Atribuições
description: Visão geral do recurso Atribuições para comunidades de ativação
seo-description: Visão geral do recurso Atribuições para comunidades de ativação
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 13%

---

# Fundamentos das Atribuições {#assignments-essentials}

Leia para saber mais sobre as informações essenciais para trabalhar com o recurso de atribuições dos sites [comunidade de ativação](/help/communities/overview.md#enablement-community).

O recurso de atribuições é a capacidade de atribuir recursos de ativação e caminhos de aprendizado aos membros das comunidades de ativação.

## Fundamentos para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ativation/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incondicional</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="/help/communities/assignments.md">Recurso Atribuições</a></td>
  </tr>
 </tbody>
</table>

### Status de conclusão e sucesso {#completion-and-success-status}

Status de conclusão e sucesso são usados em relatórios e banners de status em Atribuições.

Status de conclusão:

* Não atribuído
* Não Iniciado (Novo)
* Em andamento
* Concluir

Status de sucesso:

* Desconhecido
* Aprovado
* Falha

As únicas combinações possíveis de Conclusão e Status de Sucesso são:

| **Conclusão** | **Sucesso** |
|---|---|
| Não iniciado | Desconhecido |
| Em andamento | Desconhecido |
| Concluir | Aprovado |
| Concluir | Falha |

## Fundamentos para o lado do servidor {#essentials-for-server-side}

### Função das atribuições {#assignments-function}

Uma estrutura de site da comunidade que inclui a função [Atribuições](/help/communities/functions.md#assignments-function), inclui um componente ` [assignments](/help/communities/assignments.md)` configurado.

### APIs de referência {#reference-apis}

* [API de ativação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de relatórios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de relatórios do Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
