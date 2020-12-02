---
title: Uso das propriedades do conteúdo para exportar conteúdo
seo-title: Uso das propriedades do conteúdo para exportar conteúdo
description: A página a seguir mostra Propriedades e nós do aplicativo.
seo-description: A página a seguir mostra Propriedades e nós do aplicativo.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---


# Uso das propriedades do conteúdo para exportar conteúdo{#using-content-properties-to-export-content}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Os aplicativos são representados como *cq:Pages* no AEM.

Eles compartilham as mesmas propriedades comuns encontradas em qualquer *cq:Page*, além de outras mostradas abaixo que representam as propriedades de suporte da integração.

## Propriedades do aplicativo {#app-properties}

A tabela a seguir mostra **Propriedades do aplicativo e nós**.

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
   <td><p>Caminho para um Cloud Service Mobile On-Demand configurado. Usado para ações sob demanda do AEM Mobile para dispositivos móveis (invocação da API)</p> <p>Essa associação é configurada pelo bloco Gerenciar conexão quando um autor escolhe um Cloud Service Mobile On-Demand para associar o aplicativo.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Sequência:Caminho</td>
   <td><p>Caminho para as configurações de exportação do aplicativo. A configuração de exportação é uma pasta com 2 modelos filho de configuração de exportação do ContentSync;</p> <p><i>dps-article</i>: Configuração de exportação do ContentSync para exportar conteúdo do artigo</p> <p><i>dps-HTMLResources</i>: Configuração de exportação do ContentSync para exportar recursos compartilhados do aplicativo/artigo</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Sequência de caracteres</td>
   <td><p>Id/URI do projeto Mobile On-Demand ao qual este aplicativo está vinculado/vinculado.</p> <p>Essa associação é configurada pelo bloco Gerenciar conexão quando um autor escolhe o projeto a partir de uma lista de projetos disponíveis para o Cloud Service Mobile On-Demand associado.</p> </td>
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
   <td>Data do último carregamento de recursos compartilhados do AEM para a AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>Id do usuário que realizou o último upload da solicitação de recursos compartilhados da AEM para a AEM Mobile.</td>
  </tr>
  <tr>
   <td>pge-painel-config</td>
   <td>Sequência:Caminho</td>
   <td>Caminho para uma configuração de painel. O caminho pode ser redirecionado para uma configuração de painel personalizada, conforme necessário.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Sequência:Caminho</td>
   <td><p>Caminho para um cq:Componente que é ou estende <i>mobileapps/core/components/instance.</i></p> <p>Isso fornece a presença e a renderização no catálogo de aplicativos.</p> </td>
  </tr>
 </tbody>
</table>

Você pode usar ***Propriedades do conteúdo*** para criar conteúdo. Consulte os seguintes recursos para criar e exportar artigos e recursos compartilhados:

* [Propriedades do conteúdo](/help/mobile/content-properties.md)
* [Criando Configuração de Exportação de Artigo](/help/mobile/creating-article-export-configuration.md)
* [Criando Configuração de Exportação de Recursos Compartilhados](/help/mobile/creating-shared-resources-export-configuration.md)
