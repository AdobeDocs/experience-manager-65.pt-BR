---
title: Formulários AEM em grupos e privilégios OSGi
seo-title: Formulários AEM em grupos e privilégios OSGi
description: Atribua usuários aos grupos para gerenciar formulários AEM no OSGi
seo-description: Atribua usuários aos grupos para gerenciar formulários AEM no OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: dbb99875cc6f3c8810670ffe923756f7c13d4ace
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# Formulários AEM em grupos e privilégios OSGi{#aem-forms-on-osgi-groups-and-privileges}

Você pode [criar grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) e atribuir políticas e [usuários](/help/sites-administering/user-group-ac-admin.md#user-administration) aos grupos no AEM. Essas políticas controlam os privilégios dos usuários que fazem parte do grupo.

Depois de instalar o pacote [complementar do](../../forms/using/installing-configuring-aem-forms-osgi.md)AEM Forms, os grupos mencionados neste artigo, como usuário de formulários e usuário avançado de formulários, ficam automaticamente disponíveis para atribuição. A tabela a seguir lista as tarefas que um usuário pode executar para o AEM Forms no OSGi com base nas atribuições do grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tarefas</td> 
  </tr>
  <tr>
   <td>usuário de formulários <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Criar, pré-visualização, publicar e enviar formulários adaptativos</li> 
     <li>Criar, pré-visualização e publicar comunicações interativas e fragmentos de documento</li> 
     <li>Fazer upload de ativos para uma instância do AEM</li> 
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
     <li>Usar aplicativos<br /> da caixa de entrada do AEM <strong>Observação: </strong>É necessário ter usuários com agente de cm e atribuições de grupo de usuários de fluxo de trabalho para acessar a interface do usuário do agente do Interative Communications na caixa de entrada do AEM.</li> 
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

