---
title: Atualizar Definições do Veículo de Liberação
seo-title: Atualizar Definições do Veículo de Liberação
description: Este artigo detalha os vários tipos de versões de AEM, incluindo versões completas, pacotes de recursos e pacotes de serviços.
seo-description: Este artigo detalha os vários tipos de versões de AEM, incluindo versões completas, pacotes de recursos e pacotes de serviços.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 3%

---


# AEM Atualizar Definições do Veículo de Liberação{#update-release-vehicle-definitions}

Este documento inclui detalhes sobre os vários tipos de versões do Adobe Experience Manager (AEM), incluindo versões completas, pacotes de recursos e pacotes de serviços que o Adobe fornece aos seus clientes.

>[!NOTE]
>
>Para obter o cronograma de lançamento de AEM atualizações, consulte o roteiro de versões de atualização [AEM](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## Versão completa {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>Definição</strong></td>
   <td>
    <ul>
     <li>Versão programada</li>
     <li>Suporta caminhos de atualização para versões específicas, que são definidos nas notas de versão</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nomeação</strong></td>
   <td>
    <ul>
     <li>Os números de versão das principais versões aumentam com base na fórmula X+1.Y.Z. </li>
     <li>Os números de versão para versões secundárias aumentam com base na fórmula X.Y+1.Z</li>
    </ul> <p>Onde X é o número da versão primária, Y é o número da versão secundária e Z o número do patch.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusões</strong></td>
   <td>
    <ul>
     <li>Novos recursos</li>
     <li>Melhorias</li>
     <li>Correções de erros</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentação</strong></td>
   <td>
    <ul>
     <li>As notas de versão estão disponíveis no portal de documentação</li>
     <li>A documentação sobre recursos, melhorias e correções de erros está disponível no portal de documentação</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadência</strong></td>
   <td>Anualmente</td>
  </tr>
  <tr>
   <td><strong>Disponibilidade e instalação</strong></td>
   <td>
    <ul>
     <li>Fornecido como instalador de produto independente</li>
     <li>Disponível no site de licenciamento e no site de licenciamento da Managed Services</li>
     <li>Pode exigir migração do repositório de conteúdo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nível de teste</strong></td>
   <td>Totalmente validado pelo controle de qualidade</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definição</strong></td>
   <td>
    <ul>
     <li>Versão programada</li>
     <li>Atualmente, não é possível reverter</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nomeação</strong></td>
   <td>
    <ul>
     <li>O número de versão do patch é um número de um único dígito</li>
     <li>Após a instalação, aumentará o dígito de correção do número de versão instalado, com base na fórmula X.Y.Z.SPx</li>
     <li>Onde X é o número da versão primária, Y é o número da versão secundária e Z o número do patch. x é o número do service pack.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusões</strong></td>
   <td>
    <ul>
     <li>Novos recursos</li>
     <li>Melhorias</li>
     <li>Correções de erros</li>
     <li>Pacotes de recursos de interesse comum (se houver)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentação</strong></td>
   <td>
    <ul>
     <li>Notas de versão disponíveis no portal de documentação</li>
     <li>Documentação sobre recursos, melhorias, correções de erros no portal de documentação</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadência</strong></td>
   <td>Trimestral</td>
  </tr>
  <tr>
   <td><strong>Disponibilidade e instalação</strong></td>
   <td>
    <ul>
     <li>Entregue como um pacote</li>
     <li>Disponível no Compartilhamento de pacotes</li>
     <li>Requer instalação funcional existente</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nível de teste</strong></td>
   <td>
    <ul>
     <li>Todas as correções validadas</li>
     <li>Sanidade geral do pacote com execuções de automação</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Cumulative Fix Pack  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Definição</strong></td>
   <td>
    <ul>
     <li>Modelo de delivery único para liberação de correções</li>
     <li>Pacote de conteúdo do agregador contendo o pacote de conteúdo de componentes individuais</li>
     <li>Os CFPs são sobrepostos de hot fixes e nenhuma melhoria faz parte dele.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nomeação</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Onde X é o número da versão primária, Y é o número da versão secundária e Z o número do patch. x é o número cumulativo do service pack.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusões</strong></td>
   <td><p>CFP é um pacote de correções cumulativo que contém correções de todos os componentes em datas especificadas. Por exemplo, se um cliente aplicar CFP3, então CFP3 = CFP1 + CFP2.</p> </td>
  </tr>
  <tr>
   <td><strong>Documentação</strong></td>
   <td>Notas de versão disponíveis no portal de documentação</td>
  </tr>
  <tr>
   <td><strong>Cadência</strong></td>
   <td>Quaterly</td>
  </tr>
  <tr>
   <td><strong>Disponibilidade e instalação</strong></td>
   <td>
    <ul>
     <li>Entregue como um pacote</li>
     <li>Disponível no Compartilhamento de pacotes</li>
     <li>Dependendo do service pack mais recente lançado</li>
     <li>A PCP é autodependente. Os clientes não precisam se preocupar em encontrar/resolver dependências. O CFP deve ser instalado no Service Pack lançado mais recentemente.</li>
     <li>O CFP pode ser instalado como um único pacote, o que melhora a experiência do cliente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nível de teste</strong></td>
   <td>Garantia de qualidade validada no nível de integração e teste de regressão</td>
  </tr>
 </tbody>
</table>

## Sobreposição {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>Definição</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Nomeação</strong></td>
   <td>overlay-&lt;ID do tíquete&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusões</strong></td>
   <td>Correção de erros para um arquivo JS ou JSP</td>
  </tr>
  <tr>
   <td><strong>Documentação</strong></td>
   <td>Nenhum</td>
  </tr>
  <tr>
   <td><strong>Cadência</strong></td>
   <td>Se necessário</td>
  </tr>
  <tr>
   <td><strong>Disponibilidade e instalação</strong></td>
   <td>
    <ul>
     <li>Entregue como pacote pelo Atendimento ao cliente AEM</li>
     <li>Não necessariamente incluído em service packs ou versões completas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nível de teste</strong></td>
   <td>Validado pelo Atendimento ao cliente</td>
  </tr>
 </tbody>
</table>

## Pacote de recursos {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definição</strong></td>
   <td>
    <ul>
     <li>Pacotes de recursos são funcionalidades complementares e são fornecidos por Service Packs. Se uma versão AEM tiver lançado seu último service pack, o Adobe não fornecerá nenhum pacote de recursos para ele no futuro.</li>
     <li>Os FPs contêm aprimoramentos de produtos, programados para uma versão subsequente do produto, mas fornecidos antecipadamente com base na decisão do Gerenciamento de produto Adobe.</li>
     <li>Os recursos são sempre mesclados com a próxima versão principal e depois suportados para a versão AEM exigida pelo cliente</li>
     <li>Os pacotes de recursos de interesse comum e GA são mesclados no próximo service pack</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nomeação</strong></td>
   <td>cq-&lt;Versão da versão&gt;-featurepack-&lt;ID do Featurepack&gt;-&lt;versão do Featurepack&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusões</strong></td>
   <td>
    <ul>
     <li>Novos recursos</li>
     <li>Melhorias</li>
     <li>Correções de erros (atualizações de produtos incrementais)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentação</strong></td>
   <td>A documentação está disponível em helpx.adobe.com.</td>
  </tr>
  <tr>
   <td><strong>Cadência</strong></td>
   <td>Varia com a área do Produto</td>
  </tr>
  <tr>
   <td><strong>Disponibilidade e instalação</strong></td>
   <td>
    <ul>
     <li>Entregue por Service Packs</li>
     <li>Disponível em Compartilhamento de pacotes. Os clientes aceitam Termos e Condições por meio do Compartilhamento de pacotes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nível de teste</strong></td>
   <td>Os pacotes de recursos de disponibilidade geral são validados pelo controle de qualidade</td>
  </tr>
 </tbody>
</table>

* [1]: As correções OAK não são entregues como hot fixes individuais. No entanto, eles estão incluídos na correção Cumulative Oak subsequente. Se necessário, uma compilação de diagnóstico sobre o COFP mais recente pode ser disponibilizada. A condição prévia é que o cliente tenha o COFP mais recente em execução. As compilações de diagnóstico fornecem somente o mesmo nível de garantia de qualidade que uma correção. Portanto, eles não fornecem o mesmo nível de garantia de qualidade que um pacote de correções cumulativo, service pack ou versão do produto. A correção final é feita com o próximo CFP.

