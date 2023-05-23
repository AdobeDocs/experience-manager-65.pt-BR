---
title: Testes - quando e com quem?
seo-title: Testing - when and with whom?
description: É possível envolver várias funções nos testes e em vários estágios do desenvolvimento do projeto
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '274'
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
   <td>Equipe de controle de qualidade</td>
   <td><p>Você precisará de uma Equipe de garantia de qualidade (de qualquer tamanho, se apropriado) para testes funcionais e de desempenho.</p> <p>São testadores neutros e dedicados - uma regra de ouro do software sempre afirma que um desenvolvedor nunca deve testar seu próprio trabalho.</p> <p>Os membros dessa equipe podem ser retirados da equipe do projeto Day, do parceiro e/ou da equipe do cliente.</p> </td>
   <td><p>A primeira versão da função deve ser disponibilizada aos testadores (assim que for realisticamente possível). Embora uma versão provisória antecipada possa gerar muitos bugs, ela pode fornecer feedback antecipado sobre problemas críticos.</p> </td>
  </tr>
  <tr>
   <td>Equipe de teste do cliente</td>
   <td><p>Dependendo do Modelo de projeto selecionado, pode ser planejado que membros da equipe do cliente estejam envolvidos no teste, especialmente autores do site do cliente.</p> <p>O é vantajoso, pois:</p>
    <ul>
     <li><p>Fornece ao cliente experiência do projeto que está sendo desenvolvido.</p> </li>
     <li><p>Fornece feedback antecipado do cliente.</p> </li>
     <li><p>Os usuários muitas vezes expressam seus requisitos em termos de experiência anterior; envolver os clientes em testes o mais cedo possível aumenta sua experiência com o novo projeto em termos de <i>práticos</i> experiência.</p> </li>
    </ul> </td>
   <td><p>Novamente, o envolvimento antecipado é bom, embora qualquer versão que os clientes usem deva ser estável, com funcionalidade razoável.</p> <p>As primeiras impressões são sempre importantes.</p> </td>
  </tr>
 </tbody>
</table>
