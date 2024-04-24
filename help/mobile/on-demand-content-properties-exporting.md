---
title: Uso das propriedades de conteúdo para exportar conteúdo
description: A página a seguir mostra as Propriedades e os Nós do aplicativo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 3%

---

# Uso das propriedades de conteúdo para exportar conteúdo{#using-content-properties-to-export-content}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos são representados como *cq:Pages* no AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer *cq:Page* além de outros mostrados abaixo que representam propriedades de suporte à integração.

## Propriedades do aplicativo {#app-properties}

A tabela a seguir mostra **Nós e propriedades do aplicativo**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>Sequência:Caminho</td>
   <td><p>Caminho para um Cloud Service do Mobile On-Demand configurado. Usado para ações do AEM Mobile para o Mobile On-Demand (invocação da API)</p> <p>Essa associação é configurada por meio do bloco Gerenciar conexão quando um autor escolhe um Cloud Service do Mobile On-Demand ao qual associar o aplicativo.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Sequência:Caminho</td>
   <td><p>Caminho das configurações de exportação do aplicativo. A configuração de exportação é uma pasta com dois modelos de configuração de exportação filhos do ContentSync;</p> <p><i>dps-article</i>: configuração de exportação do ContentSync para exportar o conteúdo do artigo</p> <p><i>dps-HTMLResources</i>: configuração de exportação do ContentSync para exportar recursos compartilhados de aplicativo/artigo</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>String</td>
   <td><p>ID/URI do projeto do Mobile On-Demand ao qual este aplicativo está vinculado/ligado.</p> <p>Essa associação é configurada por meio do bloco Gerenciar conexão quando um autor escolhe o projeto em uma lista de projetos disponíveis para o Cloud Service Mobile On-Demand associado.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>String</td>
   <td>Título do aplicativo.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>String</td>
   <td>Tipo de conteúdo.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Data</td>
   <td>Data do último upload de recursos compartilhados do AEM para a AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>Cadeia de caracteres:ID do usuário</td>
   <td>ID do usuário que realizou o último upload de solicitação de recursos compartilhados do AEM para o AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>Sequência:Caminho</td>
   <td>Caminho para uma configuração de painel. O caminho pode ser redirecionado para uma configuração de painel personalizada, conforme necessário.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Sequência:Caminho</td>
   <td><p>Caminho para um cq:Component que é ou estende <i>mobileapps/core/components/instance.</i></p> <p>Isso fornece a presença e a renderização no Catálogo de aplicativos.</p> </td>
  </tr>
 </tbody>
</table>

Você pode usar ***Propriedades de conteúdo*** para criar conteúdo. Consulte os seguintes recursos para criar e exportar artigos e recursos compartilhados:

* [Propriedades de conteúdo](/help/mobile/content-properties.md)
* [Criação da configuração de exportação do artigo](/help/mobile/creating-article-export-configuration.md)
* [Criação da Configuração de Exportação de Recursos Compartilhados](/help/mobile/creating-shared-resources-export-configuration.md)
