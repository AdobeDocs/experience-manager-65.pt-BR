---
title: Práticas recomendadas para desenvolvedores do AEM
description: As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores de AEM.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# Práticas recomendadas{#best-practices}

## Práticas recomendadas para desenvolvedores - Introdução {#best-practices-for-developers-getting-started}

As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores de AEM. os desenvolvedores do Adobe seguem essas práticas recomendadas ao desenvolverem atualizações de produtos AEM principais e código do cliente para implementações de clientes.

Antes de iniciar o projeto de desenvolvimento do AEM, revise primeiro essas práticas recomendadas:

* [Práticas de desenvolvimento](/help/sites-developing/development-practices.md)
* [Arquitetura de conteúdo](/help/sites-developing/content-architecture.md)
* [Arquitetura de software](/help/sites-developing/software-architecture.md)
* [Dicas de codificação](/help/sites-developing/coding-tips.md)
* [Armadilhas de código](/help/sites-developing/code-pitfalls.md)
* [Interação JCR](/help/sites-developing/jcr-integration.md)
* [Pacotes OSGi](/help/sites-developing/osgi-bundles.md)
* [Práticas recomendadas da API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informações adicionais sobre práticas recomendadas {#additional-best-practices-information}

As seguintes áreas têm documentação disponível específica para o desenvolvimento de práticas recomendadas:

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Ferramentas/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Os documentos específicos são descritos e vinculados nas tabelas seguintes.

Para obter as práticas recomendadas sobre administração, implantação e manutenção ou criação, consulte uma das seguintes opções:

* [Administração de práticas recomendadas](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)
* [Implantação de práticas recomendadas](/help/sites-deploying/best-practices.md)

## Sites {#sites}

O gerenciamento e a criação do conteúdo do seu site têm algumas práticas recomendadas descritas a seguir:

<table>
 <tbody>
  <tr>
   <td>Alguma da teoria por trás da interface habilitada para toque padrão.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interface de usuário habilitada para toque: conceitos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interface de usuário habilitada para toque: estrutura</a></p> </td>
   <td>Esses documentos fornecem uma visão geral dos conceitos e da estrutura da interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: personalização de consoles </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalização de consoles de interface de usuário habilitados para toque</a></td>
   <td>Este documento descreve a melhor maneira de estender os consoles para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: personalização da criação de página</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalização da criação de página com interface habilitada para toque</a></td>
   <td>Descreve como estender a criação de página para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desenvolvimento e extensão de workflows</a></td>
   <td><p>Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM) e podem representar uma grande quantidade do processamento que ocorre em um ambiente do AEM. Portanto, é altamente recomendável planejar as implementações dos workflows com cuidado.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

O [AEM Communities](/help/communities/overview.md) simplifica a criação e o gerenciamento de Comunidades locais.

Algumas práticas recomendadas para comunidades estão descritas aqui:

|  |  |  |
|---|---|---|
| Práticas recomendadas para trabalhar com conteúdo gerado pelo usuário (UGC) | [Diretrizes de codificação](/help/communities/code-guide.md) | Diretrizes para o desenvolvimento de código flexível e portátil para a [estrutura de componente social](/help/communities/scf.md) (SCF). |
| Exemplo de uso de componentes do Communities | [Guia de Componentes da Comunidade](/help/communities/components-guide.md) | Uma ferramenta de desenvolvimento interativa. |

## Ferramentas/HTL {#tooling-htl}

A Linguagem de modelo de HTML (HTL) é um novo sistema de modelos de HTML, introduzido com AEM 6.0. Ele substitui JSP e ESP como o sistema de modelo preferido do AEM.

|  |  |  |
|---|---|---|
| Visão geral do HTL | [Visão geral e sintaxe do HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) | Este documento descreve o que é o HTL, como mover para HTL, um projeto de amostra, sintaxe, expressões e instruções |
| Utilização da API em java | [API de uso do Java do HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | A API de uso Java do HTL permite que um arquivo HTL acesse métodos de ajuda em uma classe Java personalizada. |

>[!NOTE]
>
>Seguir um tutorial com várias partes pode ser de interesse para a prática recomendada de configurar um novo projeto AEM, detalhando os Componentes principais, Modelos editáveis, Bibliotecas de clientes e desenvolvimento de componentes:
>[Introdução ao AEM Sites - Tutorial WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
