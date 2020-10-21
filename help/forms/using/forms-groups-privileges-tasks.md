---
title: AEM Forms em grupos e privilégios OSGi
seo-title: AEM Forms em grupos e privilégios OSGi
description: Atribuir usuários aos grupos para gerenciar o AEM Forms no OSGi
seo-description: Atribuir usuários aos grupos para gerenciar o AEM Forms no OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 494551d3d886c1ed70d252a28b03cfa9d8e82a6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# AEM Forms em grupos e privilégios OSGi{#aem-forms-on-osgi-groups-and-privileges}

Você pode [criar grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) e atribuir políticas e [usuários](/help/sites-administering/user-group-ac-admin.md#user-administration) aos grupos no AEM. Essas políticas controlam os privilégios dos usuários que fazem parte do grupo.

Após instalar o pacote [complementar do](../../forms/using/installing-configuring-aem-forms-osgi.md)AEM Forms, os grupos mencionados neste artigo, como usuários de formulários e usuários avançados de formulários, ficam automaticamente disponíveis para atribuição. A tabela a seguir lista as tarefas que um usuário pode executar para o AEM Forms no OSGi com base nas atribuições do grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tarefas</td> 
  </tr>
  <tr>
   <td>usuários de formulários <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Criar, pré-visualização, publicar e enviar formulários adaptativos</li> 
     <li>Criar, pré-visualização e publicar comunicações interativas e fragmentos de documento</li> 
     <li>Fazer upload de ativos para uma instância AEM</li> 
     <li>Criar temas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>usuário avançado de formulários</td> 
   <td>
    <ul> 
     <li>Criar, pré-visualização, publicar e enviar formulários adaptativos</li> 
     <li>Criar, pré-visualização e publicar comunicações interativas e fragmentos de documento</li> 
     <li>Criar scripts para formulários adaptáveis usando o editor de código</li> 
     <li>Fazer upload de ativos incluindo scripts</li> 
     <li>Criar temas</li> 
     <li>Importar pacotes que contêm XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>formulários-submissão-revisores</td> 
   <td>
    <ul> 
     <li>Reexame de envios</li> 
     <li>Aprovar ou rejeitar submissões</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>autores-modelo <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Criar e pré-visualização formulários adaptáveis ou modelos de comunicação interativa</li> 
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
     <li>Acesse cartas de gerenciamento de correspondência ou comunicações interativas usando a interface do usuário do agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>editores de fluxo de trabalho</p> </td> 
   <td>
    <ul> 
     <li>Criar um aplicativo de caixa de entrada</li> 
     <li>Criar um modelo de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>usuários do fluxo de trabalho</td> 
   <td>
    <ul> 
     <li>Usar aplicativos<br /> de caixa de entrada AEM <strong>Nota: </strong>É necessário ter atribuições de grupos de usuários-agente-cm e usuários-fluxo de trabalho para acessar a interface do usuário do Agente do Interative Communications na caixa de entrada AEM.</li> 
     <li>Gerenciar instâncias de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>administradores de fd</td> 
   <td>
    <ul> 
     <li>Configurar o gerador de PDF</li> 
     <li>Configurar pasta assistida</li> 
     <li>Gerenciar aplicativos de fluxo de trabalho</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. O usuário com privilégios de grupo de usuários de formulários não pode gravar scripts para formulários adaptáveis.
1. O usuário com privilégios de grupo de autores de modelo não pode gravar scripts para modelos.

