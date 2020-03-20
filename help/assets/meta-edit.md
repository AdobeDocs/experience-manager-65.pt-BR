---
title: Como editar ou adicionar metadados
description: Saiba mais sobre metadados de ativos no AEM Assets e sobre várias maneiras pelas quais você pode editar metadados de ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91818198032de0580fe04d09fdd567dc470c021d

---


# Como editar ou adicionar metadados {#how-to-edit-or-add-metadata}

Metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ele é extraído automaticamente quando você carrega uma imagem. Você pode editar os metadados existentes ou adicionar novas propriedades de metadados a campos existentes (por exemplo, quando um campo de metadados estiver em branco).

Como as empresas precisam de vocabulários de metadados controlados e confiáveis, os ativos AEM não permitem a adição ad hoc de novas propriedades de metadados. Embora os autores não possam adicionar novos campos de metadados para ativos, os desenvolvedores podem. Consulte [Criar nova propriedade de metadados para ativos](meta-edit.md#editing-metadata-schema).

## Editar metadados para um ativo {#editing-metadata-for-an-asset}

Para editar metadados:

1. Faça uma das seguintes opções:

   * Na interface do usuário do Assets, selecione o ativo e clique/toque no ícone **[!UICONTROL Exibir propriedades]** na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida **[!UICONTROL Exibir propriedades]** .
   * Na página do ativo, clique/toque no ícone **[!UICONTROL Exibir propriedades]** na barra de ferramentas.
      ![chlimage_1-168](assets/chlimage_1-168.png)
      *Figura: Ícone Propriedades*
   A página do ativo exibe todos os metadados do ativo. Esses metadados foram extraídos automaticamente quando foram carregados (assimilados) nos ativos AEM.

   ![selecione Propriedades do ativo para exibir metadados](assets/asset-metadata.png)


   *Figura: Editar ou adicionar metadados na página Propriedades do ativo*

1. Faça edições nos metadados em várias guias, conforme necessário, e quando concluído, clique/toque em **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações. Clique/toque em **[!UICONTROL Fechar]** para retornar à interface da Web do Assets.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há metadados definidos. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas de volta no binário original como parte de seus dados XMP. Isso é feito por meio do fluxo de trabalho de gravação de metadados do AEM. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e as propriedades recém-criadas (incluindo propriedades personalizadas como `cq:tags`) são adicionadas ao esquema.

A gravação XMP é suportada e ativada para as plataformas e formatos de arquivo descritos nos requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar esquema de metadados {#editing-metadata-schema}

Para obter detalhes sobre como editar o esquema de metadados, consulte [Editar formulários](metadata-schemas.md#edit-metadata-schema-forms)de esquema de metadados.

## Registrar um namespace personalizado no AEM {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces no AEM. Assim como há namespaces predefinidos, como cq, jcr e sling, você pode ter um namespace para os metadados do repositório e o processamento xml.

1. Vá para a página de administração do tipo de nó `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Clique ou toque em **[!UICONTROL Namespaces]** na parte superior da página. A página de administração do namespace é exibida em uma janela.

1. Para adicionar um namespace, clique ou toque em **[!UICONTROL Novo]** na parte inferior.
1. Especifique um namespace personalizado na convenção de namespace XML (especifique a id no formato de um URI e um prefixo associado para a id) e clique ou toque em **[!UICONTROL Salvar]**.
