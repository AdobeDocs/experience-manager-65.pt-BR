---
title: Manuseio básico
description: Uma visão geral do manuseio básico ao usar o ambiente do autor de AEM. Usa o console Sites como base.
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 6%

---

# Manuseio básico{#basic-handling}

>[!NOTE]
>
>* Esta página foi criada para fornecer uma visão geral do manuseio básico ao usar o ambiente de criação do AEM. Usa o console **Sites** como base.
>
>* Algumas funcionalidades não estão disponíveis em todos os consoles, e/ou a funcionalidade adicional está disponível em alguns consoles. Informações específicas sobre os consoles individuais e sua funcionalidade relacionada serão abordadas com mais detalhes em outras páginas.
>* Os atalhos de teclado estão disponíveis em todo o AEM. Principalmente ao [usar páginas de console](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) e [edição](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>


## A tela de boas-vindas {#the-welcome-screen}

A interface clássica fornece uma seleção de consoles, usando mecanismos bem conhecidos para navegação e inicialização de ações, incluindo clique, duplo clique e [menus de contexto](#context-menus).

Após o logon, a tela de Boas-vindas será exibida, isso fornece uma lista de links para consoles e serviços:

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Consoles {#consoles}

Os consoles principais são:

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Propósito</strong></td>
  </tr>
  <tr>
   <td><strong>Bem-vindo</strong></td>
   <td>Fornece uma visão geral e acesso direto (via links) à funcionalidade principal do AEM.</td>
  </tr>
  <tr>
   <td><strong>Ativos digitais</strong><br /> </td>
   <td>Esses consoles permitem importar e <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gerenciar ativos digitais</a> como imagens, vídeos, documentos e arquivos de áudio. Esses ativos podem ser usados por um site em execução na mesma instância do AEM. </td>
  </tr>
  <tr>
   <td><strong>Lançamentos</strong></td>
   <td>Isso ajuda a gerenciar o <a href="/help/sites-classic-ui-authoring/classic-launches.md">inicializações</a>; esses itens permitem desenvolver o conteúdo de uma versão futura de uma ou mais páginas ativadas pela Web.<br /> <i>Observação: Na interface habilitada para toque, grande parte da mesma funcionalidade está disponível no console Sites, juntamente com o painel Referências .</i> <i>Se necessário, esse console estará disponível no console Ferramentas; selecione Operações e, em seguida, Lançamentos.</i></td>
  </tr>
  <tr>
   <td><strong>Caixa de entrada </strong></td>
   <td>Em muitos casos, há algumas pessoas envolvidas em subtarefas de um fluxo de trabalho e cada uma delas deve concluir sua etapa antes de entregar o trabalho para a próxima pessoa. A Caixa de entrada permite visualizar notificações relacionadas a essas tarefas. Consulte <a href="/help/sites-administering/workflows.md">Trabalhar com fluxos de trabalho</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Marcação com tags</strong></td>
   <td>Os consoles Marcação permitem administrar as tags. Tags são nomes curtos ou frases que podem ser usadas para classificar e anotar partes do conteúdo, facilitando sua localização e organização. Para obter mais informações, consulte <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Uso e gerenciamento de tags</a>.</td>
  </tr>
  <tr>
   <td><strong>Ferramentas</strong></td>
   <td>O <a href="/help/sites-administering/tools-consoles.md">consoles Ferramentas</a> forneça acesso a várias ferramentas e consoles especializados que ajudam a administrar seus sites, ativos digitais e outros aspectos do seu repositório de conteúdo.</td>
  </tr>
  <tr>
   <td><strong>Usuários</strong></td>
   <td>Esses consoles permitem gerenciar direitos de acesso para usuários e grupos. Para obter detalhes completos, consulte <a href="/help/sites-administering/security.md">Administração e segurança do usuário</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Sites</strong></td>
   <td>Os consoles Sites/Sites permitem <a href="/help/sites-classic-ui-authoring/classic-page-author.md">criar, exibir e gerenciar sites</a> em execução na instância de AEM. Por meio desses consoles, você pode criar, copiar, mover e excluir páginas de site, iniciar fluxos de trabalho e ativar (publicar) páginas. Também é possível abrir uma página para edição.<br /> </td>
  </tr>
  <tr>
   <td><strong>Fluxos de trabalhos</strong></td>
   <td>Um workflow é uma série de etapas definidas que descrevem o processo de conclusão de alguma tarefa. Em muitos casos, há algumas pessoas envolvidas em uma tarefa e cada uma delas deve concluir sua etapa antes de entregar o trabalho para a próxima pessoa. O console Fluxo de trabalho permite criar modelos de fluxo de trabalho e gerenciar a execução de instâncias de fluxo de trabalho. Consulte <a href="/help/sites-administering/workflows.md">Trabalhar com fluxos de trabalho</a>.<br /> </td>
  </tr>
 </tbody>
</table>

O **Sites** O console fornece dois painéis para que você navegue e gerencie suas páginas:

* Painel esquerdo

   Isso mostra a estrutura em árvore de seus sites e as páginas nesses sites.

   Ele também mostra informações sobre outros aspectos ou AEM, incluindo projetos, blueprints e ativos.

* Painel direito

   Isso mostra as páginas (no local selecionado no painel esquerdo) e pode ser usado para executar ações.

Aqui você pode [gerenciar suas páginas](/help/sites-authoring/managing-pages.md) usando a barra de ferramentas, um menu de contexto ou abrindo uma página para outras ações.

>[!NOTE]
>
>O manuseio básico é o mesmo em todos os consoles. Esta seção concentra-se no **Sites** console, pois é o principal console usado durante a criação.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Acessar ajuda   {#accessing-help}

Em vários consoles (por exemplo, Sites) também há **Ajuda** estiver disponível, isso abrirá o Compartilhamento de pacotes ou o site da documentação.

![chlimage_1-10](assets/chlimage_1-10a.png)

Ao editar uma página, a variável [o sidekick também tem um botão para acessar a ajuda](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navegação com o console Sites {#navigating-with-the-websites-console}

O **Sites** O console lista as páginas de conteúdo em uma estrutura em árvore (painel do lado esquerdo). Para facilitar a navegação, as seções da estrutura em árvore podem ser expandidas (+) ou recolhidas (-), conforme necessário:

* Um único clique no nome da página (no painel esquerdo) irá:

   * Listar as páginas secundárias no painel direito
   * Expanda também a estrutura no painel esquerdo.

      Por motivos de desempenho, essa ação depende do número de nós secundários. Com uma instalação padrão, esse método de expansão funciona quando há `30` ou menos nós secundários.

* Um clique duplo no nome da página (painel esquerdo) também expandirá a árvore, embora a página seja aberta ao mesmo tempo, esse efeito não seja tão óbvio.

>[!NOTE]
>
>Esse valor padrão ( `30`) pode ser alterado por console nas configurações específicas do seu aplicativo do widget siteadmin:
>
>No nó siteadmin:
>
>Defina o valor da propriedade:
>`treeAutoExpandMax`
>ligado:
>`/apps/wcm/core/content/siteadmin`
>
>Ou globalmente no tema:
>Defina o valor de:
>`TREE_AUTOEXPAND_MAX`
>em:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Consulte [SiteAdmin na API do widget CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin) para obter mais detalhes.

## Informações da página no console Sites {#page-information-on-the-websites-console}

O painel direito do **Sites** O console fornece uma exibição de lista com informações sobre as páginas:

![page-info](assets/page-info.png)

Estão disponíveis os seguintes elementos: um subconjunto desses campos é mostrado como padrão:

<table>
 <tbody>
  <tr>
   <td><strong>Coluna</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Miniatura </td>
   <td>Mostra uma miniatura da página.</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>O título exibido na página</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>O nome AEM se refere à página</td>
  </tr>
  <tr>
   <td>Publicado</td>
   <td>Indica se a página foi publicada e fornece a data e hora de publicação.</td>
  </tr>
  <tr>
   <td>Modificado</td>
   <td>Indica se a página foi modificada e fornece a data e a hora de modificação. Para salvar qualquer modificação, você deve ativar a página.</td>
  </tr>
  <tr>
   <td>Publicação no Scene7</td>
   <td>Indica se a página foi publicada no Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Status</td>
   <td>Indica o status atual da página, por exemplo, se ela faz parte de um fluxo de trabalho ou cópia ativa, ou se está bloqueada no momento.</td>
  </tr>
  <tr>
   <td>Impressões</td>
   <td>Mostra a atividade em uma página em número de ocorrências.</td>
  </tr>
  <tr>
   <td>Modelo</td>
   <td>Indica o modelo no qual uma página se baseia.</td>
  </tr>
  <tr>
   <td>No fluxo de trabalho</td>
   <td>Indica quando a página está em um fluxo de trabalho.</td>
  </tr>
  <tr>
   <td>Bloqueado por</td>
   <td>Mostra quando uma página foi bloqueada e a conta de usuário que a bloqueou.</td>
  </tr>
  <tr>
   <td>Live Copy </td>
   <td>Indica quando a página faz parte de uma live copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Para selecionar as colunas visíveis, passe o mouse sobre um título de coluna. Um menu suspenso será exibido, nele é possível usar a variável **Colunas** opção.

As cores ao lado das páginas na **Publicado** e **Modificado** as colunas indicam o status da publicação:

| **Coluna** | **Cor** | **Descrição** |
|---|---|---|
| Publicado | Verde | A publicação foi bem-sucedida. O conteúdo é publicado. |
| Publicado | Amarelo | A publicação está pendente. A confirmação da publicação ainda não foi recebida pelo sistema. |
| Publicado | Vermelho | Falha ao publicar. Não há conexão com a instância de publicação. Isso também pode significar que o conteúdo foi desativado. |
| Publicado | *blank* | Esta página nunca foi publicada. |
| Modificado | Azul | A página foi modificada desde a última publicação. |
| Modificado | *blank* | Esta página nunca foi modificada ou não foi modificada desde a última publicação. |

## Menus de contexto {#context-menus}

A interface clássica usa mecanismos bem conhecidos para navegação e inicialização de ações, incluindo clique e duplo clique. Dependendo da situação atual, uma variedade de menus de contexto (geralmente abertos com o botão direito do mouse) também estará disponível:

![chlimage_1-11](assets/chlimage_1-11a.png)
