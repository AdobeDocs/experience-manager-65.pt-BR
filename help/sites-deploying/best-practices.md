---
title: Práticas recomendadas de implantação
seo-title: Práticas recomendadas de implantação
description: Implantação e manutenção de práticas recomendadas.
seo-description: Implantação e manutenção de práticas recomendadas.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 15%

---


# Implantação de práticas recomendadas{#deploying-best-practices}

A implantação de práticas recomendadas descreve como implantar ou manter AEM da maneira mais eficiente e eficaz possível. Essa lista crescente de tópicos inclui uma variedade de áreas no AEM.

As seguintes áreas têm documentação disponível sobre a implantação e manutenção de práticas recomendadas e recomendações:

* [OAK](#oak)
* [Comunidades](#communities)
* [Interface](#ui)
* [Show](#performance)

Para obter as práticas recomendadas de administração, desenvolvimento ou criação, consulte um dos seguintes:

* [Práticas recomendadas de administração](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de desenvolvimento](/help/sites-developing/best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)

Documentos específicos estão descritos e vinculados nas tabelas a seguir.

## OAK {#oak}

[O ](/help/sites-deploying/platform.md) Oakis é um repositório de conteúdo hierárquico escalável e com desempenho que é a base do AEM.

<table>
 <tbody>
  <tr>
   <td><p>Escalabilidade, desempenho e recuperação de desastres</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Desempenho e escalabilidade</a></td>
   <td>Fornece uma publicação técnica que discute a agilidade técnica, o alto desempenho e os recursos de recuperação de desastres sólidos</td>
  </tr>
  <tr>
   <td>Implantações OAK recomendadas</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Implantações recomendadas</a></td>
   <td>Descreve cenários de implantação</td>
  </tr>
  <tr>
   <td>Topologia de Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Práticas recomendadas de topologia de Mongo</a></td>
   <td>Descreve a topologia do mongo - quando usar qual topologia.</td>
  </tr>
  <tr>
   <td>Opções de armazenamento de dados</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuração de nós e armazenamentos de dados</a></td>
   <td>Este documento explica as práticas recomendadas para armazenar dados binários e nós de conteúdo. Inclui informações sobre como usar o armazenamento de dados Amazon S3.</td>
  </tr>
  <tr>
   <td>Pesquisar no OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Práticas recomendadas para Query e indexação</a><br /> </td>
   <td>Descreve as práticas recomendadas sobre como indexar conteúdo.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

A AEM Communities simplifica a criação e o gerenciamento de comunidades locais. As práticas recomendadas para AEM Communities estão descritas aqui:

[Community Content Store](/help/communities/working-with-srp.md)  - discute o novo recurso de armazenamento compartilhado para conteúdo gerado pelo usuário (UGC) e as considerações para escolher a  [topologia](/help/communities/topologies.md) subjacente.

[Implantações recomendadas para comunidades](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  - descreve as implantações recomendadas para comunidades. |

## Interface {#ui}

As práticas recomendadas na interface do usuário são descritas aqui:

[Interface do usuário Recommendations para clientes](/help/sites-deploying/ui-recommendations.md)

AEM possui duas interfaces de usuário no momento: interface otimizada para toque e clássica na mesma versão. Por conseguinte, os clientes têm de tomar uma decisão sobre qual utilizar durante a implementação do projeto. Este documento tem como objetivo ajudar a encontrar a escolha certa.

## Show {#performance}

As práticas recomendadas de desempenho estão listadas aqui:

<table>
 <tbody>
  <tr>
   <td>Práticas recomendadas para garantia de qualidade</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Práticas recomendadas para garantia de qualidade</a></td>
   <td>Uma visão geral padronizada dos problemas envolvidos na definição de um conceito de teste especificamente para testes de desempenho em seu ambiente <em>publish</em>. Isso interessa principalmente aos engenheiros de controle de qualidade, gerentes de projeto e administradores de sistema.</td>
  </tr>
  <tr>
   <td>Uso do Dispatcher com um CDN</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Uso do Dispatcher com um CDN</a></td>
   <td>Uma rede de entrega de conteúdo (CDN), como Akamai Edge Delivery ou Amazon Cloud Front, fornece conteúdo de um local próximo ao usuário final.</td>
  </tr>
  <tr>
   <td>Otimização do desempenho</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Otimização do desempenho</a></td>
   <td>Um problema chave é o tempo que seu site leva para responder às solicitações do visitante.</td>
  </tr>
  <tr>
   <td>Teste de desempenho</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Práticas recomendadas para testes de desempenho</a></td>
   <td>Descreve as práticas recomendadas para executar testes de desempenho em uma implantação AEM.<br /> </td>
  </tr>
 </tbody>
</table>

