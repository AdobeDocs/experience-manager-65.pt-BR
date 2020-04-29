---
title: 'Práticas recomendadas  '
seo-title: 'Práticas recomendadas  '
description: As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores do AEM
seo-description: As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores do AEM
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: e562939f1c64d8345b4c2a28e4b882200d9e4c07

---


# Práticas recomendadas  {#best-practices}

## Práticas recomendadas para desenvolvedores - Introdução {#best-practices-for-developers-getting-started}

As equipes de engenharia e consultoria da Adobe desenvolveram um conjunto abrangente de práticas recomendadas para desenvolvedores do AEM. Os desenvolvedores da Adobe seguem essas práticas recomendadas ao desenvolver atualizações de produtos AEM e código do cliente para implementações de clientes.

Antes de start de seu projeto de desenvolvimento do AEM, analise primeiro essas práticas recomendadas:

* [Práticas de desenvolvimento](/help/sites-developing/development-practices.md)
* [Arquitetura de conteúdo](/help/sites-developing/content-architecture.md)
* [Arquitetura de software](/help/sites-developing/software-architecture.md)
* [Dicas de codificação](/help/sites-developing/coding-tips.md)
* [Opções de código](/help/sites-developing/code-pitfalls.md)
* [Interação JCR](/help/sites-developing/jcr-integration.md)
* [Pacotes OSGi](/help/sites-developing/osgi-bundles.md)
* [Práticas recomendadas da API Java](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informações adicionais sobre práticas recomendadas {#additional-best-practices-information}

As seguintes áreas têm documentação disponível específica para o desenvolvimento de práticas recomendadas:

* [Sites](#sites)
* [Comunidades](/help/sites-developing/best-practices.md#communities)
* [Ferramenta/HTL](/help/sites-developing/best-practices.md#tooling-htl)

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
   <td>Algumas das teorias por trás da interface de usuário padrão, habilitada para toque.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interface habilitada para toque: Conceitos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interface habilitada para toque: Estrutura</a></p> </td>
   <td>Esses documentos fornecem uma visão geral dos conceitos e da estrutura da interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: Personalização de consoles </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalização de consoles de interface de usuário habilitados para toque</a></td>
   <td>Este documento descreve a melhor maneira de estender os consoles para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Interface habilitada para toque: Personalização da criação de página</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalização da criação de página da interface habilitada para toque</a></td>
   <td>Descreve como estender a criação de páginas para a interface habilitada para toque.</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desenvolvimento e extensão de Workflows</a></td>
   <td><p>Os Workflows permitem que você automatize as atividades do Adobe Experience Manager (AEM) e podem representar uma grande quantidade de processamento que ocorre em um ambiente AEM, portanto, é altamente recomendável planejar suas implementações de workflows com cuidado.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[O AEM Communities](/help/communities/overview.md) simplifica a criação e o gerenciamento de comunidades locais.

Algumas práticas recomendadas para Comunidades são descritas aqui:

|  |  |  |
|---|---|---|
| Práticas recomendadas para trabalhar com conteúdo gerado pelo usuário (UGC) | [Diretrizes de codificação](/help/communities/code-guide.md) | Orientações para o desenvolvimento de códigos flexíveis e portáteis para o quadro [de componentes](/help/communities/scf.md) sociais (SCF). |
| Exemplo de uso de componentes de Comunidades | [Guia de componentes da comunidade](/help/communities/components-guide.md) | Uma ferramenta interativa de desenvolvimento. |

## Ferramenta/HTL {#tooling-htl}

A Linguagem de modelo HTML (HTL) é um novo sistema de modelo HTML, introduzido com o AEM 6.0. Substitui o JSP e o ESP como o sistema de modelo preferencial do AEM.

|  |  |  |
|---|---|---|
| Visão geral do HTL | [Visão geral e sintaxe HTL](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html) | Este documento descreve o que é HTL, como mover para HTL, um projeto de amostra, sintaxe, expressões e declarações |
| Uso da API no java | [API de uso do Java do HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | A HTL Java Use-API permite que um arquivo HTL acesse métodos auxiliares em uma classe Java personalizada. |

>[!NOTE]
>
>O tutorial de várias partes a seguir pode ser de interesse para a prática recomendada de configurar um novo projeto AEM, detalhando os componentes principais, modelos editáveis, bibliotecas de clientes e desenvolvimento de componentes:
>[Getting Started with AEM Sites - WKND Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

