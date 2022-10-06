---
title: Personalização do console de boas-vindas (interface clássica)
seo-title: Customizing the Welcome Console (Classic UI)
description: O console de boas-vindas fornece uma lista de links para os vários consoles e funcionalidades no AEM
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 9%

---

# Personalização do console de boas-vindas (interface clássica){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Esta página lida com a interface clássica.
>
>Consulte [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md) para obter detalhes sobre a interface de usuário padrão habilitada para toque.

O console de boas-vindas fornece uma lista de links para os vários consoles e funcionalidades no AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

É possível configurar os links que estão visíveis. Isso pode ser definido para usuários e/ou grupos específicos. As ações a serem tomadas dependem do tipo de target (que correlaciona-se com a seção do console em que estão):

* [Consoles principais](#links-in-main-console-left-pane) - Links no console principal (painel esquerdo)
* [Recursos, documentação e referência, recursos](#links-in-sidebar-right-pane) - Links na barra lateral (painel direito)

## Links no console principal (painel esquerdo) {#links-in-main-console-left-pane}

Isso lista os consoles principais de AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Configuração se os links do console principal estão visíveis {#configuring-whether-main-console-links-are-visible}

As permissões de nível de nó determinam se o link pode ser visto ou não. Os nós em questão são:

* **Sites:** `/libs/wcm/core/content/siteadmin`

* **Ativos digitais:** `/libs/wcm/core/content/damadmin`

* **Comunidade:** `/libs/collab/core/content/admin`

* **Campanhas:** `/libs/mcm/content/admin`

* **Caixa de entrada:** `/libs/cq/workflow/content/inbox`

* **Usuários:** `/libs/cq/security/content/admin`

* **Ferramentas:** `/libs/wcm/core/content/misc`

* **Marcação:** `/libs/cq/tagging/content/tagadmin`

Por exemplo:

* Para restringir o acesso a **Ferramentas**, remover acesso de leitura de

   `/libs/wcm/core/content/misc`

Consulte a [Seção Segurança](/help/sites-administering/security.md) para obter mais informações sobre como definir as permissões desejadas.

### Links na barra lateral (painel direito) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Esses links se baseiam na existência de *e* acesso de leitura a nós sob o seguinte caminho:

`/libs/cq/core/content/welcome`

Há três seções (espaçadas ligeiramente entre si) fornecidas por padrão:

<table>
 <tbody>
  <tr>
   <td><strong>Recursos</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Services</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Fluxos de trabalhos</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Gerenciamento de tarefas</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Replicação</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Relatórios</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Publicações</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manuscritos</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Documentação e referência</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Documentação</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Recursos do desenvolvedor</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Recursos</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Pacotes</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Compartilhamento de pacotes</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Gerando cluster</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Backup</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Console da Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Dumping de status do Console da Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Configuração da exibição dos links na barra lateral {#configuring-whether-sidebar-links-are-visible}

É possível ocultar um link de usuários ou grupos específicos removendo o acesso de leitura aos nós que representam o link.

* Recursos - remova o acesso a:

   `/libs/cq/core/content/welcome/resources/<link-target>`

* Documentos - remover acesso a:

   `/libs/cq/core/content/welcome/docs/<link-target>`

* Recursos - remova o acesso a:

   `/libs/cq/core/content/welcome/features/<link-target>`

Por exemplo:

* Para remover o link para **Relatórios**, remover acesso de leitura de

   `/libs/cq/core/content/welcome/resources/reports`

* Para remover o link para **Pacotes**, remover acesso de leitura de

   `/libs/cq/core/content/welcome/features/packages`

Consulte a [Seção Segurança](/help/sites-administering/security.md) para obter mais informações sobre como definir as permissões desejadas.

### Mecanismo de seleção de links {#link-selection-mechanism}

Em `/libs/cq/core/components/welcome/welcome.jsp` é feita [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), que executa uma consulta em nós que têm a propriedade :

* `jcr:mixinTypes` com o valor: `cq:Console`

>[!NOTE]
>
>Execute o seguinte query para ver a lista existente:
>
>* `select * from cq:Console`
>


Quando um usuário ou grupo não tem permissão de leitura em um nó com o mixin `cq:Console`, esse nó não é recuperado pelo `ConsoleUtil` , portanto, não está listado no console.

### Adicionar um item personalizado {#adding-a-custom-item}

O [mecanismo de seleção de links](#link-selection-mechanism) pode ser usada para adicionar seu próprio item personalizado à lista de links.

Adicione seu item personalizado à lista adicionando o `cq:Console` mixin no seu widget ou recurso. Isso é feito definindo a propriedade:

* `jcr:mixinTypes` com o valor: `cq:Console`
