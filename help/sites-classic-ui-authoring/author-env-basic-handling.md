---
title: Manuseio básico
description: Uma visão geral do manuseio básico ao usar o ambiente de autor do Adobe Experience Manager. Usa o console Sites como base.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 4%

---

# Manuseio básico{#basic-handling}

>[!NOTE]
>
>* Esta página foi projetada para fornecer uma visão geral do manuseio básico ao usar o ambiente de autor do Adobe Experience Manager (AEM). Usa o console **Sites** como base.
>
>* Algumas funcionalidades não estão disponíveis em todos os consoles e funcionalidades adicionais estão disponíveis em alguns consoles. Informações específicas sobre os consoles individuais e suas funcionalidades relacionadas são abordadas com mais detalhes em outras páginas.
>* Atalhos de teclado estão disponíveis em todo o AEM. Em especial, quando [uso de consoles](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) e [editar páginas](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>

## A tela de boas-vindas {#the-welcome-screen}

A interface clássica fornece uma seleção de consoles, usando mecanismos conhecidos para navegar e iniciar ações, incluindo clique, clique duplo e [menus de contexto](#context-menus).

Após o logon, a tela Bem-vindo é exibida. Ela fornece uma lista de links para consoles e serviços:

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Consoles {#consoles}

Os principais consoles são:

<table>
 <tbody>
  <tr>
   <td><strong>Console</strong></td>
   <td><strong>Propósito</strong></td>
  </tr>
  <tr>
   <td><strong>Bem-vindo</strong></td>
   <td>Fornece uma visão geral e acesso direto (via links) à principal funcionalidade do AEM.</td>
  </tr>
  <tr>
   <td><strong>Ativos digitais</strong><br /> </td>
   <td>Esses consoles permitem importar e <a href="/help/sites-classic-ui-authoring/classicui-assets.md">gerenciar ativos digitais</a> como imagens, vídeos, documentos e arquivos de áudio. Esses ativos podem ser usados por um site em execução na mesma instância do AEM. </td>
  </tr>
  <tr>
   <td><strong>Lançamentos</strong></td>
   <td>Isso ajuda a gerenciar o <a href="/help/sites-classic-ui-authoring/classic-launches.md">lançamentos</a>; elas permitem desenvolver o conteúdo de uma versão futura de uma ou mais páginas da Web ativadas.<br /> <i>Observação: na interface habilitada para toque, grande parte da mesma funcionalidade está disponível no console Sites, juntamente com o painel Referências.</i> <i>Se necessário, esse console estará disponível no console Ferramentas; selecione Operações e, em seguida, Inicializações.</i></td>
  </tr>
  <tr>
   <td><strong>Caixa de entrada </strong></td>
   <td>Muitas vezes, várias pessoas estão envolvidas nas subtarefas de um fluxo de trabalho e cada pessoa deve concluir sua etapa antes de entregar o trabalho para a próxima pessoa. A Caixa de entrada permite que você veja notificações relacionadas a essas tarefas. Consulte <a href="/help/sites-administering/workflows.md">Trabalhar com fluxos de trabalho</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Marcação com tags</strong></td>
   <td>Os consoles Marcação permitem administrar tags. Tags são nomes curtos ou frases que você pode usar para classificar e anotar partes do conteúdo, facilitando sua localização e organização. Para obter mais informações, consulte <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Uso e gerenciamento de tags</a>.</td>
  </tr>
  <tr>
   <td><strong>Ferramentas</strong></td>
   <td>A variável <a href="/help/sites-administering/tools-consoles.md">Console Ferramentas</a> fornecer acesso a várias ferramentas e consoles especializados que ajudam a administrar seus sites, ativos digitais e outros aspectos do seu repositório de conteúdo.</td>
  </tr>
  <tr>
   <td><strong>Usuários</strong></td>
   <td>Esses consoles permitem gerenciar direitos de acesso para usuários e grupos. Para obter detalhes completos, consulte <a href="/help/sites-administering/security.md">Administração e segurança do usuário</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Sites</strong></td>
   <td>Os consoles Sites/Sites permitem <a href="/help/sites-classic-ui-authoring/classic-page-author.md">criar, exibir e gerenciar sites</a> em execução na instância do AEM. Por meio desses consoles, você pode criar, copiar, mover e excluir páginas do site, iniciar fluxos de trabalho e ativar (publicar) páginas. Também é possível abrir uma página para edição.<br /> </td>
  </tr>
  <tr>
   <td><strong>Fluxos de trabalhos</strong></td>
   <td>Um fluxo de trabalho é uma série definida de etapas que descreve o processo de conclusão de alguma tarefa. Muitas vezes, várias pessoas estão envolvidas em uma tarefa e cada pessoa deve concluir sua etapa antes de entregar o trabalho para a próxima pessoa. O console Fluxo de trabalho permite criar modelos de fluxo de trabalho e gerenciar instâncias de fluxo de trabalho em execução. Consulte <a href="/help/sites-administering/workflows.md">Trabalhar com fluxos de trabalho</a>.<br /> </td>
  </tr>
 </tbody>
</table>

A variável **Sites** O console do fornece dois painéis para você navegar e gerenciar suas páginas:

* Painel esquerdo

  Isso mostra a estrutura em árvore dos sites e das páginas dentro deles.

  Ela também mostra informações sobre outros aspectos do AEM, incluindo projetos, blueprints e ativos.

* Painel direito

  Mostra as páginas (no local selecionado no painel esquerdo) e pode ser usado para realizar ações.

Aqui é possível [gerenciar suas páginas](/help/sites-authoring/managing-pages.md) usando a barra de ferramentas, um menu de contexto ou abrindo uma página para outras ações.

>[!NOTE]
>
>O manuseio básico é o mesmo em todos os consoles. A presente seção centra-se na **Sites** console, pois é o console principal usado durante a criação.

![chlimage_1-9](assets/chlimage_1-9a.png)

## Acessar ajuda   {#accessing-help}

Em vários consoles (por exemplo, Sites), um **Ajuda** botão está disponível. Clicando **Ajuda** abre o Package Share ou o site de documentação.

![chlimage_1-10](assets/chlimage_1-10a.png)

Ao editar uma página, a variável [o sidekick também possui um botão para acessar ajuda](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navegação com o console Sites {#navigating-with-the-websites-console}

A variável **Sites** o console lista suas páginas de conteúdo em uma estrutura de árvore (painel esquerdo). Para facilitar a navegação, as seções da estrutura da árvore podem ser expandidas (+) ou recolhidas (-), conforme necessário:

* Clicar no nome da página no painel esquerdo faz o seguinte:

   * Lista as páginas secundárias no painel direito
   * Expande a estrutura no painel esquerdo.

     Por motivos de desempenho, essa ação depende do número de nós filhos. Com uma instalação padrão, esse método de expansão funciona quando há `30` ou menos nós filhos.

* Clicar duas vezes no nome da página (painel esquerdo) expande a árvore, embora, como a página é aberta ao mesmo tempo, esse efeito não seja tão óbvio.

>[!NOTE]
>
>Este valor padrão ( `30`) pode ser alterada por console nas configurações específicas do aplicativo do widget siteadmin:
>
>No nó siteadmin:
>
>Defina o valor da propriedade:
>`treeAutoExpandMax`
>em:
>`/apps/wcm/core/content/siteadmin`
>
>Ou globalmente no tema:
>Defina o valor de:
>`TREE_AUTOEXPAND_MAX`
>em:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Consulte [SiteAdmin na API do widget CQ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) para obter mais detalhes.

## Informações da página no console Sites {#page-information-on-the-websites-console}

O painel direito do **Sites** O console do fornece uma exibição de lista com informações sobre páginas:

![page-info](assets/page-info.png)

Os itens a seguir estão disponíveis; um subconjunto desses campos é mostrado como padrão:

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
   <td>O título que aparece na página</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>O nome AEM se refere à página</td>
  </tr>
  <tr>
   <td>Publicado</td>
   <td>Indica se a página foi publicada e fornece a data e a hora da publicação.</td>
  </tr>
  <tr>
   <td>Modificado</td>
   <td>Indica se a página foi modificada e fornece a data e a hora da modificação. Para salvar qualquer modificação, você deve ativar a página.</td>
  </tr>
  <tr>
   <td>Scene7 Publish</td>
   <td>Indica se a página foi publicada no Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Status</td>
   <td>Indica o status da página, por exemplo, se a página faz parte de um fluxo de trabalho ou uma live copy, ou se uma página está bloqueada.</td>
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
   <td>Indica quando a página está em um workflow.</td>
  </tr>
  <tr>
   <td>Bloqueado por</td>
   <td>Mostra quando uma página foi bloqueada e a conta de usuário que a bloqueou.</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>Indica quando a página faz parte de uma live copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Para selecionar as colunas visíveis, passe o mouse sobre um título de coluna. Um menu suspenso é exibido e aqui você pode usar o **Colunas** opção.

As cores ao lado das páginas no **Publicado** e **Modificado** as colunas indicam o status da publicação:

| **Coluna** | **Cor** | **Descrição** |
|---|---|---|
| Publicado | Verde | Publicação bem-sucedida. O conteúdo é publicado. |
| Publicado | Amarelo | A publicação está pendente. A confirmação da publicação ainda não foi recebida pelo sistema. |
| Publicado | Vermelho | Falha na publicação. Não há conexão com a instância de publicação. Isso também pode significar que o conteúdo foi desativado. |
| Publicado | *blank* | Esta página nunca foi publicada. |
| Modificado | Azul | A página foi modificada desde a última publicação. |
| Modificado | *blank* | Esta página nunca foi modificada ou não foi modificada desde a última publicação. |

## Menus de contexto {#context-menus}

A interface clássica usa mecanismos conhecidos para navegar e iniciar ações, incluindo clicar e clicar duas vezes. Dependendo da situação atual, uma variedade de menus de contexto (abertos com o botão direito do mouse) também estão disponíveis:

![chlimage_1-11](assets/chlimage_1-11a.png)
