---
title: AEM Forms em grupos e privilégios OSGi
seo-title: AEM Forms on OSGi Groups and Privileges
description: Atribuir usuários aos grupos para gerenciar o AEM Forms no OSGi
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# AEM Forms em grupos e privilégios OSGi{#aem-forms-on-osgi-groups-and-privileges}

Você pode [criar grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) e atribuir políticas e [usuários](/help/sites-administering/user-group-ac-admin.md#user-administration) aos grupos no AEM. Essas políticas controlam os privilégios dos usuários que fazem parte do grupo.

Depois de instalar [Pacote complementar do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), os grupos mencionados neste artigo, como forms-users e forms-power-user, estão automaticamente disponíveis para atribuição. A tabela a seguir lista as tarefas que um usuário pode executar para o AEM Forms no OSGi com base nas atribuições de grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tarefas</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
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
     <li>Criar scripts para formulários adaptáveis usando o editor de código</li> 
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
     <li>Usar aplicativos da caixa de entrada do AEM<br /> <strong>Nota: </strong>Você deve ter atribuições de grupo cm-agent-users e workflow-users para acessar a interface do usuário do Agente de comunicações interativas na caixa de entrada do AEM.</li> 
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
