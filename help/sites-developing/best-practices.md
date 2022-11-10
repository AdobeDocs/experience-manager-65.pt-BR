---
title: Práticas recomendadas
seo-title: Best Practices
description: As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores do AEM
seo-description: Adobe Engineering and Consulting teams have developed a comprehensive set of best practices for AEM developers
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 19%

---

# Práticas recomendadas    {#best-practices}

## Práticas recomendadas para desenvolvedores - Introdução {#best-practices-for-developers-getting-started}

As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores do AEM. Os desenvolvedores do Adobe seguem essas práticas recomendadas, pois desenvolvem as principais atualizações de produtos AEM e o código do cliente para implementações de clientes.

Antes de iniciar seu projeto de desenvolvimento de AEM, revise primeiro essas práticas recomendadas:

* [Práticas de desenvolvimento](/help/sites-developing/development-practices.md)
* [Arquitetura de conteúdo](/help/sites-developing/content-architecture.md)
* [Arquitetura de software](/help/sites-developing/software-architecture.md)
* [Dicas de codificação](/help/sites-developing/coding-tips.md)
* [Armadilhas de código](/help/sites-developing/code-pitfalls.md)
* [Interação JCR](/help/sites-developing/jcr-integration.md)
* [Pacotes do OSGi](/help/sites-developing/osgi-bundles.md)
* [Práticas recomendadas da API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informações adicionais sobre práticas recomendadas {#additional-best-practices-information}

As seguintes áreas têm documentação disponível específica para o desenvolvimento de práticas recomendadas:

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Ferramentas/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Documentos específicos estão descritos e vinculados nas tabelas a seguir.

Para obter as práticas recomendadas de administração, implantação e manutenção ou criação, consulte um dos seguintes:

* [Práticas recomendadas de administração](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)
* [Práticas recomendadas de implantação](/help/sites-deploying/best-practices.md)

## Sites {#sites}

O gerenciamento e a criação do conteúdo do seu site incluem algumas práticas recomendadas descritas a seguir:

<table>
 <tbody>
  <tr>
   <td>Parte da teoria por trás da interface de usuário padrão e habilitada para toque.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interface habilitada para toque: Conceitos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interface habilitada para toque: Estrutura</a></p> </td>
   <td>Esses documentos fornecem uma visão geral dos conceitos e da estrutura da interface do usuário habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: Personalização de consoles </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalização de consoles de interface de usuário habilitada para toque</a></td>
   <td>Este documento descreve a melhor maneira de estender os consoles para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: Personalização da criação de página</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalização da criação de página da interface habilitada para toque</a></td>
   <td>Descreve como estender a criação de página para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desenvolvimento e extensão de workflows</a></td>
   <td><p>Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM) e podem representar uma grande quantidade do processamento que ocorre em um ambiente AEM, portanto, é altamente recomendável planejar as implementações dos workflows com cuidado.</p> </td>
  </tr>
 </tbody>
</table>

## Comunidades {#communities}

[AEM Communities](/help/communities/overview.md) simplifica a criação e o gerenciamento de comunidades locais.

Algumas práticas recomendadas para Comunidades são descritas abaixo:

|  |  |  |
|---|---|---|
| Práticas recomendadas para trabalhar com conteúdo gerado pelo usuário (UGC) | [Diretrizes de codificação](/help/communities/code-guide.md) | Diretrizes para o desenvolvimento de código flexível e portátil para a [estrutura de componentes sociais](/help/communities/scf.md) (CCAH). |
| Exemplo de uso de componentes de Comunidades | [Guia de componentes da comunidade](/help/communities/components-guide.md) | Uma ferramenta de desenvolvimento interativo. |

## Ferramentas/HTL {#tooling-htl}

A Linguagem de modelo de HTML (HTL) é um novo sistema de modelo de HTML, introduzido com o AEM 6.0. Substitui o JSP e o ESP como o sistema de modelos preferido de AEM.

|  |  |  |
|---|---|---|
| Visão geral do HTL | [Visão geral e sintaxe do HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | Este documento descreve o que é HTL, como mover para HTL, um projeto de amostra, sintaxe, expressões e instruções |
| Uso da API no java | [API de uso do Java do HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | A API de uso do Java do HTL habilita um arquivo HTL para acessar métodos de ajuda em uma classe Java personalizada. |

>[!NOTE]
>
>O tutorial em várias partes a seguir pode ser de interesse para a prática recomendada de configurar um novo projeto de AEM, detalhando os Componentes principais, Modelos editáveis, Bibliotecas de clientes e desenvolvimento de componentes:
>[Introdução ao AEM Sites - Tutorial do WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
