---
title: Uso das propriedades de conteúdo para exportar conteúdo
seo-title: Using Content Properties to Export Content
description: A página a seguir mostra as Propriedades e os nós do aplicativo.
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# Uso das propriedades de conteúdo para exportar conteúdo{#using-content-properties-to-export-content}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos são representados como *cq:Pages* em AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer *cq:Page* além de outras mostradas abaixo que representam as propriedades de suporte da integração.

## Propriedades do aplicativo {#app-properties}

A tabela a seguir mostra **Propriedades e nós do aplicativo**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String:Path</td>
   <td><p>Caminho para um Cloud Service móvel sob demanda configurado. Usado para ações sob demanda do AEM Mobile para dispositivos móveis (invocação de API)</p> <p>Essa associação é configurada por meio do bloco Gerenciar conexão , quando um autor escolhe um Cloud Service Mobile On-Demand para associar o aplicativo.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>Caminho para as configurações de exportação do aplicativo. A configuração de exportação é uma pasta com 2 templates de configuração de exportação do ContentSync filho;</p> <p><i>dps-article</i>: Configuração de exportação do ContentSync para exportar conteúdo do artigo</p> <p><i>dps-HTMLResources</i>: Configuração de exportação do ContentSync para exportar recursos compartilhados aplicativo/artigo</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Sequência de caracteres</td>
   <td><p>Id/URI do projeto Mobile On-Demand ao qual este Aplicativo está vinculado/vinculado.</p> <p>Essa associação é configurada por meio do bloco Gerenciar conexão , quando um autor escolhe o projeto a partir de uma lista de projetos disponíveis para o Cloud Service Mobile On-Demand associado.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Sequência de caracteres</td>
   <td>Título do aplicativo.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Sequência de caracteres</td>
   <td>Tipo de conteúdo.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Data</td>
   <td>Data do último upload de recursos compartilhados do AEM para o AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>ID do usuário que realizou o último upload da solicitação de recursos compartilhados do AEM para o AEM Mobile.</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String:Path</td>
   <td>Caminho para uma configuração de painel. O caminho pode ser redirecionado para uma configuração de painel personalizada, conforme necessário.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>Caminho para um cq:Componente que é ou estende <i>mobileapps/core/components/instance.</i></p> <p>Isso fornece a presença e renderização no Catálogo de aplicativos.</p> </td>
  </tr>
 </tbody>
</table>

Você pode usar ***Propriedades de conteúdo*** para criar conteúdo. Consulte os seguintes recursos para criar e exportar artigos e recursos compartilhados:

* [Propriedades de conteúdo](/help/mobile/content-properties.md)
* [Criação da configuração de exportação de artigo](/help/mobile/creating-article-export-configuration.md)
* [Criando Configuração de Exportação de Recursos Compartilhados](/help/mobile/creating-shared-resources-export-configuration.md)
