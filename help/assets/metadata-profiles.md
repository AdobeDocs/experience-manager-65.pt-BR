---
title: Perfis de metadados para personalizar os requisitos de metadados dos ativos
description: Saiba mais sobre perfis de metadados para ativos. Saiba como criar um perfil de metadados e aplicá-lo aos ativos da pasta.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9658fbf8c918b9051a35e7477afa01af7722a662

---


# Metadata profiles {#metadata-profiles}

Um perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um perfil de metadados e aplique-o a uma pasta. Qualquer ativo carregado posteriormente para a pasta herda os metadados padrão configurados no perfil de metadados.

## Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegue até **[!UICONTROL Ferramentas > Ativos > Perfis]** de metadados e toque em **[!UICONTROL Criar]**.
1. Insira um título para o Perfil de metadados, por exemplo Metadados de amostra, e toque em **[!UICONTROL Criar]**. O [!UICONTROL formulário] de edição para o perfil de metadados é exibido.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Clique em um componente e configure suas propriedades na guia **[!UICONTROL Configurações]** . Por exemplo, clique no componente **[!UICONTROL Descrição]** e edite suas propriedades.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Edite as seguintes propriedades para o componente **[!UICONTROL Descrição]** :

   * **[!UICONTROL Rótulo]** do campo - o nome de exibição da propriedade de metadados. É apenas para a referência do usuário.

   * **[!UICONTROL Mapear para propriedade]** - o valor dessa propriedade fornece o caminho/nome relativo para o nó do ativo no qual ele é salvo no repositório. O valor deve sempre começar com `./` porque indica que o caminho está sob o nó do ativo.
   ![chlimage_1-199](assets/chlimage_1-482.png)

   O valor especificado para **[!UICONTROL Mapear para propriedade]** é armazenado como uma propriedade no nó de metadados do ativo. Por exemplo, se você especificar . `/jcr:content/metadata/dc:desc` como o nome do **[!UICONTROL Mapa para a propriedade]**, os ativos AEM armazenam o valor `dc:desc` no nó de metadados do ativo.

   * **[!UICONTROL Valor]** padrão - Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Adicionar um valor padrão a uma nova propriedade de metadados (que ainda não existe no . `/jcr:content/metadata` nó) não exibe a propriedade e seu valor na página Propriedades do ativo por padrão. Para exibir a nova propriedade na página [!UICONTROL Propriedades] dos ativos, modifique o formulário de esquema correspondente.

1. (Opcional) Adicione mais componentes ao formulário de edição na guia **[!UICONTROL Criar formulário]** e configure suas propriedades na guia **[!UICONTROL Configurações]** . As seguintes propriedades estão disponíveis na guia **[!UICONTROL Criar formulário]** :

| Componente | Propriedades |
|---|---|
| [!UICONTROL Título da seção] | Rótulo do campo, <br> Descrição |
| [!UICONTROL Texto em linha única] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Texto multivalor] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Número] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Data] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Tags padrão] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão, <br> Descrição |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Toque/ clique em **[!UICONTROL Concluído]**. O Perfil de metadados é adicionado à lista de perfis na página Perfis **[!UICONTROL de]** metadados.<br>


   ![Perfil de metadados adicionado à página Perfis de metadados](assets/MetadataProfiles-page.png)

## Copiar um perfil de metadados {#copying-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um perfil de metadados para fazer uma cópia dele.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Toque em **[!UICONTROL Copiar]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Copiar perfil]** de metadados, digite um título para a nova cópia do perfil de metadados.
1. Toque em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página Perfis **[!UICONTROL de]** metadados.

   ![Uma cópia do perfil de metadados adicionada na página Perfis de metadados](assets/copy-metadata-profile.png)

## Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um perfil a ser excluído.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Para[] **[!UICONTROL Excluir perfis]** de metadados na barra de ferramentas.
1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

## Aplicar um perfil de metadados a pastas {#applying-a-metadata-profile-to-folders}

Quando você atribui um perfil de metadados a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir somente um perfil de metadados a uma pasta. Assim, considere cuidadosamente a estrutura de pastas de onde você carrega, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de metadados diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos adicionados posteriormente à pasta.

As pastas que têm um perfil atribuído a ele são indicadas na interface do usuário pelo nome do perfil que aparece no nome do cartão.

![chlimage_1-205](assets/chlimage_1-489.png)

Você pode aplicar perfis de metadados a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de metadados a pastas específicas {#applying-metadata-profiles-to-specific-folders}

Você pode aplicar um perfil de metadados a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de metadados a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a ele são indicadas pela exibição do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

#### Aplicar perfis de metadados a pastas da interface de usuário Perfis {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Siga as etapas para aplicar o perfil de metadados:

1. Toque no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis]** de metadados.
1. Selecione o perfil de metadados que deseja aplicar a uma pasta ou várias pastas.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Toque em **[!UICONTROL Aplicar perfil de metadados às pastas e selecione a pasta ou várias pastas que deseja usar para receber os ativos carregados recentemente e toque em]** Concluído ****. As pastas que têm um perfil já atribuído a ele são indicadas pela exibição do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de metadados a pastas a partir de Propriedades {#applying-metadata-profiles-to-folders-from-properties}

1. No painel esquerdo, toque em **[!UICONTROL Ativos]** e navegue até a pasta à qual deseja aplicar um perfil de metadados.
1. Na pasta, toque ou clique na marca de seleção para selecioná-la e, em seguida, toque ou clique em **[!UICONTROL Propriedades]**.

1. Selecione a guia Perfis **[!UICONTROL de]** metadados e selecione o perfil no menu suspenso e toque em **[!UICONTROL Salvar]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   As pastas que têm um perfil já atribuído a ele são indicadas pela exibição do nome do perfil logo abaixo do nome da pasta.

### Aplicar um perfil de metadados globalmente {#applying-a-metadata-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado em ativos AEM em qualquer pasta tenha o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

**Para aplicar um perfil de metadados globalmente, execute um dos procedimentos a seguir**

* Navegue até `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e toque em **[!UICONTROL Salvar]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* Navegue até CRXDE Lite até o seguinte nó: `/content/dam/jcr:content`. Adicione a propriedade `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` e toque em **Salvar tudo**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Remover um perfil de metadados das pastas {#removing-a-metadata-profile-from-folders}

Quando você remove um perfil de metadados de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Você pode remover um perfil de metadados de uma pasta do menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, das **[!UICONTROL Propriedades]**. Esta seção descreve como remover perfis de metadados de pastas de ambas as maneiras.

### Remover perfis de metadados de pastas por meio da interface de usuário Perfis {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Toque ou clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis]** de metadados.
1. Selecione o perfil de metadados que deseja remover de uma pasta ou de várias pastas.
1. Toque em **[!UICONTROL Remover perfil de metadados das pastas e selecione a pasta ou várias pastas que deseja usar para remover um perfil e toque em]** Concluído ****.

   Você pode confirmar que o perfil de metadados não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remover perfis de metadados de pastas por meio de Propriedades {#removing-metadata-profiles-from-folders-via-properties}

1. Toque no logotipo do AEM e navegue pelos **[!UICONTROL Ativos]** e, em seguida, até a pasta da qual deseja remover um perfil de metadados.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Selecione a guia Perfis **[!UICONTROL de]** metadados e selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a ele são indicadas pela exibição do nome do perfil logo abaixo do nome da pasta.

>[!MORELIKETHIS]
>
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md)
>* [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md)

