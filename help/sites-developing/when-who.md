---
title: Testes - quando e com quem?
description: Várias funções podem ser envolvidas em testes e em vários estágios de desenvolvimento do projeto.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%
---
# Testes - quando e com quem?{#testing-when-and-with-whom}

Várias funções podem ser envolvidas em testes e em vários estágios de desenvolvimento do projeto.

<table>
 <tbody>
  <tr>
   <td>Equipe de teste</td>
   <td>Responsável por... </td>
   <td>Quando...</td>
  </tr>
  <tr>
   <td>Equipe de desenvolvimento</td>
   <td>A equipe de desenvolvimento é responsável pelos testes de unidade e por alguns testes de integração.</td>
   <td>Esses testes são os primeiros na cadeia, embora sejam repetidos/estendidos durante o desenvolvimento.</td>
  </tr>
  <tr>
   <td>Equipe do Quality Assurance</td>
   <td><p>Você precisa de uma Equipe do Quality Assurance (de qualquer tamanho, se apropriado) para testes funcionais e de desempenho.</p> <p>São testadores neutros e dedicados - uma regra de ouro do software sempre afirma que um desenvolvedor nunca deve testar seu próprio trabalho.</p> <p>Os membros dessa equipe podem ser retirados da equipe do projeto Day, do parceiro e/ou da equipe do cliente.</p> </td>
   <td><p>A primeira versão da função deve ser disponibilizada aos testadores (quando for possível). Embora uma versão provisória antecipada possa gerar muitos bugs, ela pode fornecer feedback antecipado sobre problemas críticos.</p> </td>
  </tr>
  <tr>
   <td>Equipe de teste do cliente</td>
   <td><p>Dependendo do Modelo de projeto selecionado, pode ser planejado que membros da equipe do cliente estejam envolvidos no teste, especialmente autores do site do cliente.</p> <p>Isso é vantajoso porque:</p>
    <ul>
     <li><p>O cliente recebe experiência do projeto que está sendo desenvolvido.</p> </li>
     <li><p>Fornece feedback antecipado do cliente.</p> </li>
     <li><p>Os usuários muitas vezes expressam seus requisitos em termos de experiência anterior; envolver os clientes em testes o mais cedo possível aumenta sua experiência com o novo projeto em termos de experiência <i>prática</i>.</p> </li>
    </ul> </td>
   <td><p>Novamente, o envolvimento antecipado é bom, embora qualquer versão que os clientes usem deva ser estável, com funcionalidade razoável.</p> <p>As primeiras impressões são sempre importantes.</p> </td>
  </tr>
 </tbody>
</table>
