---
title: Práticas recomendadas de implantação
seo-title: Deploying Best Practices
description: Implantação e manutenção de práticas recomendadas.
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 16%

---

# Práticas recomendadas de implantação{#deploying-best-practices}

A implantação de práticas recomendadas descreve como implantar ou manter AEM da maneira mais eficiente e eficaz possível. Essa lista crescente de tópicos inclui uma variedade de áreas no AEM.

As áreas a seguir têm documentação disponível sobre a implantação e manutenção de práticas recomendadas e recomendações:

* [OAK](#oak)
* [Communities](#communities)
* [Interface](#ui)
* [Show](#performance)

Para obter as práticas recomendadas de administração, desenvolvimento ou criação, consulte um dos seguintes:

* [Práticas recomendadas de administração](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de desenvolvimento](/help/sites-developing/best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)

Documentos específicos estão descritos e vinculados nas tabelas a seguir.

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) é um repositório de conteúdo hierárquico escalável e de desempenho que é a base do AEM.

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidade, desempenho e recuperação de desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Desempenho e escalabilidade</a></td>
   <td>Fornece um white paper sobre a agilidade técnica, o alto desempenho e os recursos de recuperação de desastres sólidos</td>
  </tr>
  <tr>
   <td>Implantações OAK recomendadas</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implantações recomendadas</a></td>
   <td>Descreve cenários de implantação</td>
  </tr>
  <tr>
   <td>Topologia de Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Práticas recomendadas de topologia do Mongo</a></td>
   <td>Descreve a topologia de mongo - quando usar qual topologia.</td>
  </tr>
  <tr>
   <td>Opções de armazenamento de dados</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuração de nós e armazenamentos de dados</a></td>
   <td>Este documento explica as práticas recomendadas de armazenamento de dados binários e nós de conteúdo. Inclui informações sobre o uso do armazenamento de dados do Amazon S3.</td>
  </tr>
  <tr>
   <td>Pesquisar no OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Práticas recomendadas para consultas e indexação</a><br /> </td>
   <td>Descreve as práticas recomendadas sobre como indexar conteúdo.</td>
  </tr>
 </tbody>
</table>

## Comunidades {#communities}

O AEM Communities simplifica a criação e o gerenciamento de comunidades locais. As práticas recomendadas para o AEM Communities estão descritas aqui:

[Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md) - Discute o novo recurso de armazenamento compartilhado para conteúdo gerado pelo usuário (UGC) e as considerações para escolher o subjacente [topologia](/help/communities/topologies.md).

[Implantações recomendadas para comunidades](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Descreve as implantações recomendadas para Comunidades. |

## Interface {#ui}

As práticas recomendadas referentes à interface do usuário estão descritas abaixo:

[Recommendations da interface do usuário para clientes](/help/sites-deploying/ui-recommendations.md)

AEM atualmente tem duas interfaces de usuário: interface otimizada para toque e clássica na mesma versão. Portanto, os clientes devem tomar uma decisão sobre qual usar durante a implementação do projeto. Este documento tem como objetivo ajudar a encontrar a escolha certa.

## Show {#performance}

As práticas recomendadas de desempenho estão listadas aqui:

<table>
 <tbody>
  <tr>
   <td>Práticas recomendadas para garantia de qualidade</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Práticas recomendadas para garantia de qualidade</a></td>
   <td>Uma visão geral padronizada dos problemas envolvidos na definição de um Conceito de teste especificamente para testes de desempenho em seu <em>publicar</em> ambiente. Isso é de interesse principalmente para engenheiros de controle de qualidade, gerentes de projeto e administradores de sistema.</td>
  </tr>
  <tr>
   <td>Uso do Dispatcher com um CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Uso do Dispatcher com um CDN</a></td>
   <td>Uma rede de entrega de conteúdo (CDN), como Akamai Edge Delivery ou Amazon Cloud Front, fornece conteúdo de um local próximo ao usuário final.</td>
  </tr>
  <tr>
   <td>Otimização de desempenho</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Otimização de desempenho</a></td>
   <td>Um problema importante é o tempo que seu site leva para responder às solicitações do visitante.</td>
  </tr>
  <tr>
   <td>Teste de desempenho</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Práticas recomendadas para testes de desempenho</a></td>
   <td>Descreve as práticas recomendadas para executar testes de desempenho em uma implantação de AEM.<br /> </td>
  </tr>
 </tbody>
</table>
