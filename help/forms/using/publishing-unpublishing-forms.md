---
title: Publicar e desfazer a publicação de formulários e documentos
seo-title: Publicar e desfazer a publicação de formulários e documentos
description: Você pode agendar a publicação e a despublicação de formulários. Os formulários publicados são replicados na instância de publicação.
seo-description: Você pode agendar a publicação e a despublicação de formulários. Os formulários publicados são replicados na instância de publicação.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Publicar e desfazer a publicação de formulários e documentos{#publishing-and-unpublishing-forms-and-documents}

O AEM Forms permite que você crie, publique e cancele a publicação de formulários facilmente. Para obter mais informações sobre o AEM Forms, consulte [Introdução ao gerenciamento de formulários](../../forms/using/introduction-managing-forms.md).

O servidor de formulários AEM fornece duas instâncias: Autor e publicação. A instância do autor serve para criar e gerenciar ativos e recursos de formulário. A instância de publicação é para manter ativos e recursos relacionados disponíveis para usuários finais. É possível importar formulários XDP e PDF no modo Autor. Para obter mais informações, consulte [Obtenção de documentos XDP e PDF no AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Ativos suportados {#supported-assets-nbsp}

O AEM Forms oferece suporte aos seguintes tipos de ativos:

* Formulários adaptáveis
* Documentos adaptativos
* Fragmentos de formulário adaptáveis
* Temas
* Modelos de formulário (formulários XFA)
* Formulários PDF
* Documento (documentos PDF simples)
* Conjuntos de formulários
* Recurso (imagens, esquemas e folhas de estilos)

Inicialmente, todos os ativos estão disponíveis somente na instância Autor. Um administrador ou autor de formulário pode publicar todos os ativos, exceto os recursos.

Quando você seleciona um formulário e o publica, seus ativos e recursos relacionados também são publicados. No entanto, ativos dependentes não são publicados. Neste contexto, ativos e recursos relacionados são ativos aos quais um ativo publicado usa ou se refere. Ativos dependentes são ativos que se referem a um ativo publicado.

Seus formulários adaptativos podem utilizar algumas configurações, configurações e personalizações que não são publicadas automaticamente. É recomendável publicar ou ativar esses recursos antes de publicar um formulário adaptável.

* Modelos de formulário adaptável editáveis
* Configurações do serviço em nuvem para Adobe Sign, Typekit, reCAPTCHA e modelos de dados de formulário
* Outras configurações de serviços da Cloud são ativadas somente se o usuário tiver permissões de administrador.
* Personalizações. Eles incluem, mas não estão limitados a:

   * Layouts personalizados
   * Aparências personalizadas
   * Arquivo CSS - aceito como entrada na caixa de diálogo Propriedades do contêiner de Formulário adaptável
   * Categoria da biblioteca do cliente - usada como entrada na caixa de diálogo Propriedades do contêiner de formulário adaptável
   * Qualquer outra biblioteca cliente que possa ter sido incluída como parte do modelo de Formulário adaptável.
   * Caminhos de design

## Estados do ativo {#asset-states}

Um ativo pode ter os seguintes estados:

* **** Não publicado: Um ativo que nunca foi publicado (o estado não publicado é aplicável somente aos ativos do Forms. Os ativos do Gerenciamento de correspondência não têm um estado Não publicado.)
* **Publicado**: Um ativo que foi publicado e está disponível na instância Publicar
* **Modificado**: Um ativo modificado após a publicação

## Publicar um ativo {#publish-an-asset}

1. Faça logon no servidor do AEM Forms.
1. Use uma das seguintes opções para selecionar e publicar um ativo.

   1. Mova o ponteiro sobre um ativo e toque em **[!UICONTROL Publicar]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Execute um dos procedimentos a seguir e toque em Publicar:

      * Se você estiver na exibição do cartão, toque em **[!UICONTROL Inserir seleção]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)e toque no ativo. O ativo é selecionado.
      * Se você estiver na exibição de lista, marque a caixa de seleção de um ativo. O ativo é selecionado.
      * Toque em um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades de exibição ![exibindo propriedades](assets/viewproperties.png).
      >[!NOTE]
      >
      >Não selecione vários ativos. Não há suporte para a publicação de vários ativos simultaneamente.


1. Quando o processo de publicação é iniciado, uma caixa de diálogo de confirmação é exibida listando todos os ativos e recursos relacionados. Na caixa de diálogo que contém ativos relacionados, toque em **[!UICONTROL Publicar]**. O ativo é publicado e a caixa de diálogo Publicar ativos bem-sucedidos é exibida.

   >[!NOTE]
   >
   >Para os formulários Adaptáveis, juntamente com os ativos relacionados, o nome da página Formulário Adaptável também é exibido.

   ![Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados](assets/p4.png)

   Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados.

   >[!NOTE]
   >
   >Para o Gerenciador de Formulários, se o usuário não tiver permissão para publicar os ativos listados, a ação Publicar será desativada. Um ativo que requer permissões extras é exibido em vermelho.

   Depois que um ativo é publicado, as propriedades de metadados do ativo são copiadas para a instância Publicar e o status do ativo é alterado para Publicado. O status dos ativos dependentes publicados também é alterado para Publicado.

   Depois de publicar um ativo, você pode usar o Portal de Formulários para exibir todos os ativos em uma página da Web. Para obter mais informações, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Publish all the Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

O AEM Forms permite que você publique todos os ativos de Gerenciamento de correspondência em um servidor de uma só vez. Os ativos publicados incluem todos os ativos do Gerenciamento de Correspondência e dependências relacionadas.

Complete as etapas a seguir para publicar todos os ativos do Gerenciamento de correspondência em um servidor:

1. Faça logon no servidor do AEM Forms.
1. Toque em **Adobe Experience Manager** na barra de navegação global.
1. Toque em ![ferramentas](assets/tools.png)e, em seguida, toque em **Formulários**.
1. Tap **Publish Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   A página Publicar todos os ativos de gerenciamento de correspondência é exibida e exibe as informações sobre a última vez que o processo Publicar ativos de gerenciamento de correspondência foi tentado.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Toque em **Publicar** e, na mensagem de confirmação, toque em **OK**.

   Depois que um processo em lote for concluído, você poderá exibir os detalhes da última execução. Isso inclui informações como o logon do Administrador e se o lote foi executado com êxito ou com falha.

   >[!NOTE]
   >
   >O processo de publicação não pode ser cancelado depois de iniciado. Além disso, enquanto a operação Publicar estiver em andamento, não crie, exclua, modifique ou publique ativos ou inicie a operação Exportar todos os ativos do Gerenciamento de correspondência.

## Automatizar a publicação e a despublicação para Formulários e Documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

O AEM Forms permite agendar a publicação e a despublicação de ativos para Formulários e Documentos. Você pode especificar o agendamento no Editor de metadados. Para obter mais informações sobre como gerenciar metadados de formulário, consulte [Gerenciamento de metadados de formulário.](../../forms/using/manage-form-metadata.md)

Siga estas etapas para agendar a data e a hora de publicar e desfazer a publicação de ativos de Formulários e Documentos:

1. Selecione um ativo e toque em **[!UICONTROL Exibir propriedades]**. A página Propriedades de metadados é aberta.
1. Na página Propriedades de metadados, toque em **[!UICONTROL Avançado]** e em **[!UICONTROL Editar]** ![ilustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. Nos campos **[!UICONTROL Publicar no horário]** e **[!UICONTROL Publicar no horário]** , selecione a data e a hora.\
   Toque em **[!UICONTROL Done]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar a publicação de um ativo {#unpublish-an-asset}

1. Selecione um ativo publicado e toque em **[!UICONTROL Cancelar publicação]** ![cancelar a publicação](assets/unpublish.png).
1. Use um dos seguintes para selecionar e cancelar a publicação de um ativo.

   1. Mova o ponteiro do mouse sobre um ativo e toque em **[!UICONTROL Cancelar publicação]** ![para cancelar a publicação](assets/unpublish.png).
   1. Execute um dos procedimentos a seguir e toque em Cancelar publicação:

      * Se você estiver na exibição do cartão, toque em **[!UICONTROL Inserir seleção]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)e toque no ativo. O ativo é selecionado.

      * Se você estiver na exibição de lista, passe o mouse sobre um ativo e toque em ![seletassetcheckmark](assets/selectassetcheckmark.png) . O ativo é selecionado.

      * Toque em um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades de exibição ![exibindo propriedades](assets/viewproperties.png).

1. Quando o processo Cancelar publicação for iniciado, uma caixa de diálogo de confirmação será exibida. Toque em **[!UICONTROL Cancelar publicação]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado não é publicado e seus ativos filho e referenciados, se houver, não são publicados.

## Reverter um ativo ou carta para a versão publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Sempre que você publicar um ativo ou uma carta após editá-lo, uma versão do ativo ou da carta será criada. Você pode reverter um ativo ou carta para uma versão publicada anteriormente. Talvez seja necessário fazer isso se algo der errado com a versão atual do ativo ou documento.

>[!NOTE]
>
>Não reverta uma carta para um último estado publicado se qualquer ativo dependente usado nessa carta publicada for excluído do sistema.

1. Selecione um ativo e toque em **[!UICONTROL Reverter para versão]** publicada anteriormente ![reverttoversão](assets/reverttopreviouslypublishedversion.png)publicada anteriormente.
1. Antes de o ativo ser revertido, uma caixa de diálogo de confirmação é exibida. Toque em **[!UICONTROL Reverter]**.

   O ativo ou a carta é revertida para sua versão publicada anteriormente.

## Excluir um ativo {#delete-an-asset}

>[!NOTE]
>
>A exclusão de um ativo o remove da instância de publicação. A exclusão de um ativo também remove seu histórico de versão, exceto a versão base.

1. Selecione um ativo e toque em **[!UICONTROL Excluir]** ![exclusão](assets/delete.png).

   >[!NOTE]
   >
   >A opção Excluir também está disponível quando você exibe os detalhes do ativo tocando em um ativo ou quando exibe as propriedades do ativo tocando em Exibir propriedades do ![visualizador](assets/viewproperties.png)Propriedades.

1. Antes de o ativo ser excluído, uma caixa de diálogo de confirmação é exibida. Toque em **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado é excluído e os ativos dependentes e não são excluídos. Para verificar referências de um ativo, toque em ![referências](assets/references.png) e selecione um ativo.
   >
   >
   >Se o ativo que você está tentando excluir for um ativo filho de outro ativo, ele não será excluído. Para excluir tal ativo, remova as referências desse ativo de outros ativos e tente novamente.

## Formulários adaptativos protegidos {#protected-adaptive-forms}

Você pode ativar a autenticação para formulários que deseja que os usuários selecionados acessem. Quando você habilita a autenticação para seus formulários, os usuários veem uma tela de logon antes de acessá-los. Somente usuários com credenciais autorizadas podem acessar os formulários.

Para ativar a autenticação para seus formulários:

1. No navegador, abra o configMgr na instância de publicação.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Na Configuração do console da Web do Adobe Experience Manager, clique em **Apache Sling Authentication Service** para configurá-lo.
1. Na caixa de diálogo Apache Sling Authentication Service exibida, use o botão **+** para adicionar caminhos.\
   Quando você adiciona um caminho, o serviço de autenticação é ativado para formulários nesse caminho.
