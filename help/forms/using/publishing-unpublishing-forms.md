---
title: Publicar e desfazer a publicação de formulários e documentos
seo-title: Publishing and unpublishing forms and documents
description: Você pode agendar a publicação e o cancelamento da publicação de formulários. Formulários publicados são replicados na instância de publicação.
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Publicar e desfazer a publicação de formulários e documentos{#publishing-and-unpublishing-forms-and-documents}

O AEM Forms permite criar, publicar e desfazer a publicação de formulários com facilidade. Para obter mais informações sobre o AEM Forms, consulte [Introdução ao gerenciamento de formulários](../../forms/using/introduction-managing-forms.md).

O servidor do AEM Forms fornece duas instâncias: Autor e publicação. A instância de autor é para criar e gerenciar ativos e recursos de formulário. A instância de publicação serve para manter ativos e recursos relacionados disponíveis para usuários finais. Você pode importar XDP e PDF forms no modo Autor. Para obter mais informações, consulte [Obter documentos XDP e PDF no AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Ativos compatíveis   {#supported-assets-nbsp}

O AEM Forms é compatível com os seguintes tipos de ativos:

* Formulários adaptáveis
* Documentos adaptáveis
* Fragmentos de formulário adaptáveis
* Temas
* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (documentos de PDF simples)
* Conjuntos de formulários
* Recurso (imagens, esquemas e folhas de estilos)

Inicialmente, todos os ativos estão disponíveis somente na instância Autor . Um administrador ou autor de formulário pode publicar todos os ativos, exceto recursos.

Ao selecionar um formulário e publicá-lo, seus ativos e recursos relacionados também são publicados. No entanto, os ativos dependentes não são publicados. Neste contexto, os ativos e recursos relacionados são ativos aos quais um ativo publicado usa ou se refere. Os ativos dependentes são ativos que se referem a um ativo publicado.

Seu Adaptive Forms pode utilizar algumas configurações, configurações e personalizações que não são publicadas automaticamente. É recomendável publicar ou ativar esses recursos antes de publicar um formulário adaptável.

* Modelos de formulário adaptável editáveis
* Configurações do Cloud Service para Adobe Sign, Typekit, reCAPTCHA e Modelos de dados de formulário
* Outras configurações dos serviços da Cloud só serão ativadas se o usuário tiver permissões de administrador.
* Personalizações. Isso inclui, mas não se limita a:

   * Layouts personalizados
   * Exibições personalizadas
   * Arquivo CSS - usado como entrada na caixa de diálogo de propriedades do contêiner de formulário adaptável
   * Categoria da biblioteca do cliente - tomada como entrada na caixa de diálogo de propriedades do contêiner de formulário adaptável
   * Qualquer outra biblioteca do cliente que possa ter sido incluída como parte do modelo de Formulário adaptável.
   * Caminhos de design

## Estados do ativo {#asset-states}

Um ativo pode ter os seguintes estados:

* **Não publicado:** Um ativo que nunca foi publicado (o estado não publicado é aplicável somente aos ativos do Forms. Os ativos de Gerenciamento de correspondência não têm um estado Não publicado.)
* **Publicado**: Um ativo que foi publicado e está disponível na instância de publicação
* **Modificado**: Um ativo que é modificado após ser publicado

## Publicar um ativo {#publish-an-asset}

1. Faça logon no servidor do AEM Forms.
1. Use um dos seguintes para selecionar e publicar um ativo.

   1. Mova o ponteiro sobre um ativo e toque **[!UICONTROL Publicar]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Siga um destes procedimentos e toque em Publicar:

      * Se você estiver na exibição de cartão, toque em **[!UICONTROL Inserir seleção]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)e toque no ativo. O ativo é selecionado.
      * Se você estiver na exibição de lista, marque a caixa de seleção de um ativo. O ativo é selecionado.
      * Toque em um ativo para exibir seus detalhes.
      * Exibir as propriedades de um ativo tocando em Propriedades da exibição ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >Não selecione vários ativos. Não há suporte para a publicação de vários ativos ao mesmo tempo.


1. Quando o processo de publicação é iniciado, uma caixa de diálogo de confirmação é exibida listando todos os ativos e recursos relacionados. Na caixa de diálogo que contém os ativos relacionados, toque em **[!UICONTROL Publicar]**. O ativo é publicado e a caixa de diálogo Publicar ativos bem-sucedidos é exibida.

   >[!NOTE]
   >
   >Para os formulários adaptáveis, juntamente com os ativos relacionados, o nome da página Formulário adaptável também é exibido.

   ![Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados](assets/p4.png)

   Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados.

   >[!NOTE]
   >
   >Para o Forms Manager, se o usuário não tiver permissão para publicar os ativos listados, a ação Publicar estará desativada. Um ativo que requer permissões extras é exibido em vermelho.

   Depois que um ativo é publicado, as propriedades de metadados do ativo são copiadas para a instância Publicar e o status do ativo é alterado para Publicado. O status dos ativos dependentes publicados também é alterado para Publicado.

   Depois de publicar um ativo, você pode usar o Portal do Forms para exibir todos os ativos em uma página da Web. Para obter mais informações, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Publicar todos os ativos de gerenciamento de correspondência {#publish-all-the-correspondence-management-assets}

O AEM Forms permite publicar todos os ativos de Gerenciamento de correspondência em um servidor de uma só vez. Os ativos publicados incluem todos os ativos de Gerenciamento de correspondência e dependências relacionadas.

Complete as etapas a seguir para publicar todos os ativos de Gerenciamento de correspondência em um servidor:

1. Faça logon no servidor do AEM Forms.
1. Toque **Adobe Experience Manager** na barra de navegação global.
1. Toque ![ferramentas](assets/tools.png)e toque em **Forms**.
1. Toque **Publicar ativos de gerenciamento de correspondência**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   A página Publicar todos os ativos de gerenciamento de correspondência é exibida e exibe as informações sobre a última vez que o processo Publicar ativos de gerenciamento de correspondência foi tentado.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Toque **Publicar** e, na mensagem de confirmação, toque em **OK**.

   Após concluir um processo em lote, é possível exibir os detalhes da última execução. Isso inclui informações como o login do Administrador e se o lote foi executado com êxito ou falhou.

   >[!NOTE]
   >
   >O processo de publicação não pode ser cancelado uma vez iniciado. Além disso, enquanto a operação Publicar estiver em andamento, não crie, exclua, modifique ou publique quaisquer ativos ou inicie a operação Exportar todos os ativos de gerenciamento de correspondência.

## Automatizar a publicação e o cancelamento da publicação para Forms e documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

O AEM Forms permite agendar a publicação e o cancelamento da publicação de ativos para Forms &amp; Documents. Você pode especificar o agendamento no Editor de metadados. Para obter mais informações sobre o gerenciamento de metadados de formulário, consulte [Gerenciamento de metadados do formulário.](../../forms/using/manage-form-metadata.md)

Siga estas etapas para programar a data e a hora da publicação e do cancelamento da publicação dos ativos do Forms &amp; Documents:

1. Selecione um ativo e toque em **[!UICONTROL Propriedades da exibição]**. A página Propriedades de metadados é aberta.
1. Na página Propriedades de metadados , toque em **[!UICONTROL Avançado]** e toque em **[!UICONTROL Editar]** ![ilustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. No **[!UICONTROL Publicar a tempo]** e **[!UICONTROL Hora de publicar]** selecione a data e a hora.\
   Toque **[!UICONTROL Concluído]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar a publicação de um ativo {#unpublish-an-asset}

1. Selecione um ativo publicado e toque em **[!UICONTROL Cancelar publicação]** ![cancelar publicação](assets/unpublish.png).
1. Use um dos seguintes para selecionar e cancelar a publicação de um ativo.

   1. Mova o ponteiro sobre um ativo e toque **[!UICONTROL Cancelar publicação]** ![cancelar publicação](assets/unpublish.png).
   1. Siga um destes procedimentos e toque em Cancelar publicação:

      * Se você estiver na exibição de cartão, toque em **[!UICONTROL Inserir seleção]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)e toque no ativo. O ativo é selecionado.

      * Se você estiver na exibição de lista, passe o mouse sobre um ativo e toque em ![seletassetcheckmark](assets/selectassetcheckmark.png) . O ativo é selecionado.

      * Toque em um ativo para exibir seus detalhes.
      * Exibir as propriedades de um ativo tocando em Propriedades da exibição ![viewproperties](assets/viewproperties.png).

1. Quando o processo Cancelar publicação é iniciado, uma caixa de diálogo de confirmação é exibida. Toque **[!UICONTROL Cancelar publicação]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado não tem publicação e sua publicação secundária e os ativos referenciados, se houver, não têm publicação cancelada.

## Reverter um ativo ou carta para a versão publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Toda vez que você publica um ativo ou uma carta depois de editá-lo, uma versão do ativo ou carta é criada. Você pode reverter um ativo ou carta para uma versão publicada anteriormente. Talvez seja necessário fazer isso se algo der errado com a versão atual do ativo ou documento.

>[!NOTE]
>
>Não reverta uma carta para um último estado publicado se qualquer ativo dependente usado nessa carta publicada for excluído do sistema.

1. Selecione um ativo e toque em **[!UICONTROL Reverter para versão publicada anteriormente]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Antes de o ativo ser revertido, uma caixa de diálogo de confirmação é exibida. Toque **[!UICONTROL Reverter]**.

   O ativo ou a carta é revertida para a versão publicada anteriormente.

## Excluir um ativo {#delete-an-asset}

>[!NOTE]
>
>Excluir um ativo o remove da instância de publicação. A exclusão de um ativo também remove seu histórico de versões, exceto a versão base.

1. Selecione um ativo e toque em **[!UICONTROL Excluir]** ![excluir](assets/delete.png).

   >[!NOTE]
   >
   >A opção Excluir também está disponível ao exibir detalhes do ativo tocando em um ativo ou ao exibir as propriedades de um ativo ao tocar em Propriedades da exibição ![viewproperties](assets/viewproperties.png).

1. Antes de o ativo ser excluído, uma caixa de diálogo de confirmação é exibida. Toque **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado é excluído, e os ativos dependentes e não são excluídos. Para verificar referências de um ativo, toque em ![referências](assets/references.png) e, em seguida, selecione um ativo.
   >
   >
   >Se o ativo que você está tentando excluir for um ativo filho de outro ativo, ele não será excluído. Para excluir esse ativo, remova as referências desse ativo de outros ativos e tente novamente.

## Formulários adaptáveis protegidos {#protected-adaptive-forms}

Você pode habilitar a autenticação para formulários que você deseja que usuários selecionados acessem. Ao habilitar a autenticação para seus formulários, os usuários veem uma tela de logon antes de acessá-los. Somente usuários com credenciais autorizadas podem acessar os formulários.

Para habilitar a autenticação para seus formulários:

1. No seu navegador, abra configMgr na instância de publicação.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Na Configuração do Console da Web do Adobe Experience Manager, clique em **Serviço de autenticação do Apache Sling** para configurá-lo.
1. Na caixa de diálogo Apache Sling Authentication Service exibida, use **+** para adicionar caminhos.\
   Quando você adiciona um caminho, o serviço de autenticação é ativado para formulários nesse caminho.
