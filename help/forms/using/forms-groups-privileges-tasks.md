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
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 6%

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
     <li>Fazer upload de ativos para uma instância AEM</li> 
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
     <li>Use aplicativos da Caixa de Entrada de AEM<br /> <strong>Observação: </strong>Você deve ter atribuições de grupo cm-agent-users e workflow-users para acessar a interface do usuário do Agente de Comunicações Interativas na Caixa de Entrada de AEM.</li> 
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
