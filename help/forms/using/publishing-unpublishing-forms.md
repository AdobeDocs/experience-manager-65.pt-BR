---
title: Publicação e cancelamento de publicação de formulários e documentos
description: É possível agendar a publicação e o cancelamento da publicação de formulários. Os formulários publicados são replicados na instância de publicação.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Publicação e cancelamento de publicação de formulários e documentos{#publishing-and-unpublishing-forms-and-documents}

O AEM Forms permite criar, publicar e desfazer a publicação de formulários facilmente. Para obter mais informações sobre o AEM Forms, consulte [Introdução ao gerenciamento de formulários](../../forms/using/introduction-managing-forms.md).

O servidor do AEM Forms fornece duas instâncias: Autor e Publicar. A instância do autor é utilizada para criar e gerenciar ativos e recursos de formulários. A instância de publicação serve para manter ativos e recursos relacionados disponíveis para usuários finais. É possível importar XDP e PDF forms no modo Autor. Para obter mais informações, consulte [Obtenção de documentos XDP e PDF no AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Ativos compatíveis   {#supported-assets-nbsp}

O AEM Forms é compatível com os seguintes tipos de ativos:

* Formulários adaptáveis
* Documentos adaptáveis
* Fragmentos de formulário adaptável
* Temas
* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (documentos de PDF simples)
* Conjuntos de formulários
* Recurso (imagens, esquemas e folhas de estilos)

Inicialmente, todos os ativos estão disponíveis somente na instância do Autor. Um administrador ou autor de formulário pode publicar todos os ativos, exceto recursos.

Ao selecionar um formulário e publicá-lo, seus ativos e recursos relacionados também são publicados. No entanto, os ativos dependentes não são publicados. Neste contexto, ativos e recursos relacionados são ativos que um ativo publicado usa ou refere. Ativos dependentes são ativos que se referem a um ativo publicado.

O Adaptive Forms pode utilizar algumas configurações, configurações e personalizações que não são publicadas automaticamente. É recomendável publicar ou ativar esses recursos antes de publicar um formulário adaptável.

* Modelos de formulário adaptável editáveis
* Configurações de Cloud Service para os modelos de dados de formulário, Typekit, reCAPTCHA e Adobe Sign
* Outras configurações de serviços na nuvem são ativadas somente se o usuário tiver permissões de administrador.
* Personalizações. Isso inclui, mas não se limita a:

   * Layouts personalizados
   * Aparências personalizadas
   * Arquivo CSS - tomado como entrada na caixa de diálogo de propriedades do contêiner Formulário adaptável
   * Categoria da biblioteca do cliente - usada como entrada na caixa de diálogo de propriedades do contêiner de Formulário adaptável
   * Qualquer outra biblioteca do cliente que tenha sido incluída como parte do modelo de Formulário adaptável.
   * Caminhos de design

## Estados do ativo {#asset-states}

Um ativo pode ter os seguintes estados:

* **Não publicado:** Um ativo que nunca foi publicado (o estado não publicado é aplicável somente aos ativos do Forms. Os ativos do Gerenciamento de correspondências não têm um estado Não publicado.)
* **Publicado**: um ativo que foi publicado e está disponível na instância de publicação
* **Modificado**: um ativo que é modificado depois de ser publicado

## Publicar um ativo {#publish-an-asset}

1. Faça logon no servidor do AEM Forms.
1. Use um dos itens a seguir para selecionar e publicar um ativo.

   1. Mova o ponteiro sobre um ativo e selecione **[!UICONTROL Publish]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Siga um destes procedimentos e selecione Publicar:

      * Se estiver na exibição de cartão, selecione **[!UICONTROL Inserir seleção]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)e selecione o ativo. O ativo está selecionado.
      * Se você estiver na exibição em lista, marque a caixa de seleção de um ativo. O ativo está selecionado.
      * Selecione um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades da exibição ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >Não selecione vários ativos. Não é possível publicar vários ativos de uma só vez.

1. Quando o processo de publicação é iniciado, uma caixa de diálogo de confirmação é exibida listando todos os ativos e recursos relacionados. Na caixa de diálogo que contém ativos relacionados, selecione **[!UICONTROL Publish]**. O ativo é publicado e a caixa de diálogo Publicar sucesso de ativos é exibida.

   >[!NOTE]
   >
   >Para os formulários adaptáveis, juntamente com os ativos relacionados, o nome da página do formulário adaptável também é exibido.

   ![Um diálogo de confirmação com todos os ativos e recursos relacionados](assets/p4.png)

   Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados.

   >[!NOTE]
   >
   >Para o Forms Manager, se o usuário não tiver permissão para publicar os ativos listados, a ação Publicar será desativada. Um ativo que requer permissões adicionais é mostrado em vermelho.

   Depois que um ativo é publicado, as propriedades de metadados do ativo são copiadas para a instância de Publicação e o status do ativo é alterado para Publicado. O status dos ativos dependentes publicados também é alterado para Publicado.

   Depois de publicar um ativo, você pode usar o Portal do Forms para exibir todos os ativos em uma página da Web. Para obter mais informações, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Publicar todos os ativos do gerenciamento de correspondência {#publish-all-the-correspondence-management-assets}

O AEM Forms permite publicar todos os ativos do Gerenciamento de correspondência em um servidor de uma só vez. Os ativos publicados incluem todos os ativos do Gerenciamento de correspondências e dependências relacionadas.

Conclua as seguintes etapas para publicar todos os ativos do Gerenciamento de correspondências em um servidor:

1. Faça logon no servidor do AEM Forms.
1. Selecionar **Adobe Experience Manager** na barra de navegação global.
1. Selecionar ![ferramentas](assets/tools.png)e selecione **Forms**.
1. Selecionar **Publicar ativos do gerenciamento de correspondência**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   A página Publicar todos os ativos do gerenciamento de correspondência é exibida e mostra as informações sobre a última vez que o processo Publicar ativos do gerenciamento de correspondência foi tentado.

   ![publicar-última-execução-detalhes](assets/publish-last-run-details.png)

1. Selecionar **Publish** e, na mensagem de confirmação, selecione **OK**.

   Após a conclusão de um processo em lote, é possível exibir os detalhes da última execução. Isso inclui informações como o logon do Administrador e se a execução do lote foi bem-sucedida ou falhou.

   >[!NOTE]
   >
   >O processo de publicação não pode ser cancelado depois de iniciado. Além disso, enquanto a operação Publicar estiver em processo, não crie, exclua, modifique ou publique quaisquer ativos ou inicie a operação Exportar todos os ativos do gerenciamento de correspondência.

## Automatizar a publicação e o cancelamento da publicação de Forms e documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

O AEM Forms permite agendar a publicação e o cancelamento da publicação de ativos para o Forms e Documentos. Você pode especificar a programação no Editor de metadados. Para obter mais informações sobre o gerenciamento de metadados de formulário, consulte [Gerenciamento de metadados de formulário.](../../forms/using/manage-form-metadata.md)

Siga estas etapas para agendar a data e a hora de publicação e cancelamento da publicação dos ativos do Forms e do Documents:

1. Selecione um ativo e **[!UICONTROL Propriedades da exibição]**. A página Propriedades de metadados é aberta.
1. Na página Propriedades dos metadados, selecione **[!UICONTROL Avançado]** e selecione **[!UICONTROL Editar]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. No **[!UICONTROL Publicar no Prazo]** e **[!UICONTROL Publicar Fora do Tempo]** selecione a data e a hora.\
   Selecionar **[!UICONTROL Concluído]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar a publicação de um ativo {#unpublish-an-asset}

1. Selecione um ativo que seja publicado e **[!UICONTROL Cancelar publicação]** ![desfazer publicação](assets/unpublish.png).
1. Use um dos itens a seguir para selecionar e cancelar a publicação de um ativo.

   1. Mova o ponteiro sobre um ativo e selecione **[!UICONTROL Cancelar publicação]** ![desfazer publicação](assets/unpublish.png).
   1. Siga um destes procedimentos e selecione desfazer publicação:

      * Se estiver na exibição de cartão, selecione **[!UICONTROL Inserir seleção]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)e selecione o ativo. O ativo está selecionado.

      * Se estiver na exibição em lista, passe o mouse sobre um ativo e selecione ![seletassetcheckmark](assets/selectassetcheckmark.png) . O ativo está selecionado.

      * Selecione um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades da exibição ![viewproperties](assets/viewproperties.png).

1. Quando o processo de cancelamento de publicação for iniciado, uma caixa de diálogo de confirmação será exibida. Selecionar **[!UICONTROL Cancelar publicação]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado tem a publicação cancelada e seus ativos secundários e referenciados, se houver, não têm a publicação cancelada.

## Reverter um ativo ou uma carta para a versão publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Toda vez que você publica um ativo ou uma carta após a edição, uma versão do ativo ou da carta é criada. É possível reverter um ativo ou carta para uma versão publicada anteriormente. Talvez seja necessário fazer isso se algo der errado com a versão atual do ativo ou documento.

>[!NOTE]
>
>Não reverta uma carta para o último estado publicado se qualquer ativo dependente usado nessa carta publicada for excluído do sistema.

1. Selecione um ativo e **[!UICONTROL Reverter para a versão publicada anteriormente]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Antes de o ativo ser revertido, uma caixa de diálogo de confirmação é exibida. Selecionar **[!UICONTROL Reverter]**.

   O ativo ou a carta é revertido para a versão publicada anteriormente.

## Excluir um ativo {#delete-an-asset}

>[!NOTE]
>
>A exclusão de um ativo o remove da instância de publicação. A exclusão de um ativo também remove seu histórico de versões, exceto a versão base.

1. Selecione um ativo e **[!UICONTROL Excluir]** ![excluir](assets/delete.png).

   >[!NOTE]
   >
   >A opção Excluir também está disponível ao exibir detalhes do ativo tocando em um ativo ou ao exibir as propriedades de um ativo tocando em Propriedades de exibição ![viewproperties](assets/viewproperties.png).

1. Antes de excluir o ativo, uma caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado é excluído, e os ativos dependentes não são excluídos. Para verificar referências de um ativo, selecione ![referências](assets/references.png) e selecione um ativo.
   >
   >
   >Se o ativo que você está tentando excluir for um ativo filho de outro ativo, ele não será excluído. Para excluir um ativo como esse, remova as referências desse ativo de outros ativos e tente novamente.

## Formulários adaptáveis protegidos {#protected-adaptive-forms}

Você pode habilitar a autenticação para os formulários aos quais deseja que os usuários selecionados acessem. Quando você habilita a autenticação para seus formulários, os usuários veem uma tela de logon antes de acessá-los. Somente usuários com credenciais autorizadas podem acessar os formulários.

Para habilitar a autenticação para seus formulários:

1. No navegador, abra o configMgr na instância de publicação.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Na Configuração do console da Web do Adobe Experience Manager, clique em **Serviço de autenticação Apache Sling** para configurá-lo.
1. Na caixa de diálogo Apache Sling Authentication Service exibida, use o **+** botão para adicionar caminhos.\
   Quando você adiciona um caminho, o serviço de autenticação é ativado para formulários nesse caminho.
