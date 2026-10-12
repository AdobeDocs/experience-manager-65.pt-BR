---
title: AEM Forms em grupos e privilégios OSGi
description: Atribuir usuários a grupos para gerenciar o Adobe Experience Manager (AEM) Forms no OSGi
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%
---
# AEM Forms em grupos e privilégios OSGi{#aem-forms-on-osgi-groups-and-privileges}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Você pode [criar grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) e atribuir políticas e [usuários](/help/sites-administering/user-group-ac-admin.md#user-administration) aos grupos no Adobe Experience Manager (AEM). Essas políticas controlam os privilégios dos usuários que fazem parte do grupo.

Após instalar o [pacote complementar do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), os grupos mencionados neste artigo, como usuários de formulários e usuário avançado de formulários, estarão automaticamente disponíveis para atribuição. A tabela a seguir lista as tarefas que um usuário pode executar para o AEM Forms no OSGi com base nas atribuições de grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tarefas</td> 
  </tr>
  <tr>
   <td>formulários-usuários <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Criar, visualizar, publicar e enviar formulários adaptáveis</li> 
     <li>Criar, visualizar e publicar comunicações interativas e fragmentos de documentos</li> 
     <li>Fazer upload de ativos para uma instância do AEM</li> 
     <li>Criar temas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Criar, visualizar, publicar e enviar formulários adaptáveis</li> 
     <li>Criar, visualizar e publicar comunicações interativas e fragmentos de documentos</li> 
     <li>Criar scripts para formulários adaptáveis usando um editor de código</li> 
     <li>Fazer upload de ativos, incluindo scripts</li> 
     <li>Criar temas</li> 
     <li>Importar pacotes que contêm XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>formulários-envio-revisores</td> 
   <td>
    <ul> 
     <li>Revisar envios</li> 
     <li>Aprovar ou rejeitar envios</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>autores-modelo <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Criar e visualizar formulários adaptáveis ou modelos de comunicações interativas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-autores</p> </td> 
   <td>
    <ul> 
     <li>Criar e modificar um modelo de dados de formulário</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Acessar cartas do Gerenciamento de correspondência ou comunicações interativas usando a interface do usuário do agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>Criar um aplicativo de caixa de entrada</li> 
     <li>Criar um modelo de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Use os aplicativos da Caixa de Entrada do AEM<br /> <strong>Observação: </strong>É necessário ter cm-agent-users e atribuições de grupo workflow-users para acessar a interface do usuário do Agente de Comunicações Interativas na Caixa de Entrada do AEM.</li> 
     <li>Gerenciar instâncias de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administradores</td> 
   <td>
    <ul> 
     <li>Configurar o gerador de PDF</li> 
     <li>Configurar a pasta monitorada</li> 
     <li>Gerenciar aplicativos de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. O usuário com privilégios de grupo de usuários de formulários não pode gravar scripts para formulários adaptáveis.
1. O usuário com privilégios de grupo de autores de modelo não pode gravar scripts para modelos.
