---
title: Caracteres especiais personalizados no Gerenciamento de correspondência
seo-title: Custom special characters in Correspondence Management
description: Saiba como adicionar caracteres especiais personalizados no Gerenciamento de correspondência.
seo-description: Learn how to add custom special characters in Correspondence Management.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Caracteres especiais personalizados no Gerenciamento de correspondência{#custom-special-characters-in-correspondence-management}

## Visão geral {#overview}

O Gerenciamento de correspondência tem suporte incorporado padrão para 210 caracteres especiais que podem ser inseridos facilmente em letras.

Por exemplo, você pode inserir os seguintes caracteres especiais:

* Símbolos monetários como €, ¥ e £
* Símbolos matemáticos como ∑, Lei e ^
* Símbolos de pontuação como ‟ e &quot;

É possível inserir caracteres especiais em letras:

* No [editor de texto](/help/forms/using/document-fragments.md#createtext)
* Em um [módulo editável em linha em uma correspondência](../../forms/using/create-correspondence.md#managecontent)

![especialcaractersinilemodule](assets/specialcharactersinlinemodule.png)

O administrador pode adicionar suporte para caracteres especiais mais/personalizados por personalização. Este artigo fornece instruções sobre como você pode adicionar suporte para caracteres especiais adicionais e personalizados.

## Adicionar ou modificar o suporte para caracteres especiais personalizados no Gerenciamento de correspondência {#creatingfolderstructure}

Use as etapas a seguir para adicionar suporte a caracteres especiais personalizados:

1. Ir para `https://'[server]:[port]'/[ContextPath]/crx/de` e faça logon como Administrador.
1. Na pasta apps, crie uma pasta chamada **[!UICONTROL caracteres especiais]** com caminho/estrutura semelhante à pasta de caracteres especiais (localizada na pasta textEditorConfig em libs):

   1. Clique com o botão direito do mouse no **caracteres especiais** no caminho a seguir e selecione **Nó de sobreposição**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **Localização da sobreposição:** /apps/

      **Corresponder tipos de nó:** Verificado

      >[!NOTE]
      >
      >Não faça alterações na ramificação /libs. As alterações feitas podem ser perdidas, pois essa ramificação pode ser alterada sempre que você:
      >
      >
      >
      >    * Atualizar na sua instância
      >    * Aplicar um hotfix
      >    * Instalar um pacote de recursos


   1. Clique em **OK** e, em seguida, clique em **Salvar tudo**. A pasta de caracteres especiais é criada no caminho especificado.

      Depois de criar a sobreposição, verifique as tags de estrutura do nó. Cada nó criado em /apps usando a sobreposição deve ter a mesma classe e propriedades definidas em /libs para esse nó. Se alguma propriedade ou tag estiver ausente na estrutura do nó no local /apps, sincronize suas tags com o nó correspondente em /libs.

1. Certifique-se de que **[!UICONTROL textEditorConfig]** tem as seguintes propriedades e valores:

   | Nome | Tipo | Valor |
   |---|---|---|
   | cmConfigurationType | Sequência de caracteres | cmTextEditorConfiguration |
   | cssPath | Sequência de caracteres | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Clique com o botão direito do mouse no **[!UICONTROL caracteres especiais]** no caminho a seguir e selecione **Criar > Nó filho** e, em seguida, clique em **Salvar tudo**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. Atualize a página Editor de texto\Criar interface de usuário de correspondência . O nó adicionado é o último na lista de caracteres Especiais na interface do usuário.
1. Clique em **Salvar tudo**.
1. Faça as alterações nos caracteres especiais, conforme necessário:

<table>
 <tbody>
  <tr>
   <td><strong>Para...</strong></td>
   <td><strong>Complete as etapas a seguir</strong></td>
  </tr>
  <tr>
   <td>Adicionar um caractere especial personalizado</td>
   <td>
    <ol>
     <li>Adicione um nó filho em "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" com as propriedades obrigatórias.</li>
     <li>Clique em Salvar tudo</li>
     <li>Atualize o Editor de texto\Criar interface de usuário de correspondência para ver as alterações.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Atualizar as propriedades de um caractere especial existente</td>
   <td>
    <ol>
     <li>Sobreponha o nó a ser atualizado conforme explicado acima e verifique as tags e classes.</li>
     <li>Altere quaisquer valores, como legenda, valor, endValue e multipleCaption. </li>
     <li>Clique em Salvar tudo. </li>
     <li>Atualize o Editor de texto\Criar interface de usuário de correspondência para ver as alterações.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar um caractere especial</td>
   <td>
    <ol>
     <li>Sobreponha o nó a ser oculto em "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters"</li>
     <li>Adicione a propriedade sling:hideResource (Boolean) ao nó (em aplicativos) para ser oculta. </li>
     <li>Clique em Salvar tudo. </li>
     <li>Atualize o Editor de texto\Criar interface de usuário de correspondência para ver as alterações.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar vários caracteres especiais</td>
   <td>
    <ol>
     <li>Adicione a propriedade "sling:hideChildren (String ou String[])" para "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter". </li>
     <li>Adicione nomes de nó (caracteres especiais a serem ocultos) como valores para a propriedade "sling:hideChildren". </li>
     <li>Clique em Salvar tudo. </li>
     <li>Atualize o Editor de texto\Criar interface de usuário de correspondência para ver as alterações.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Solicitar caracteres especiais</td>
   <td>
    <ol>
     <li>Adicione um nó filho em "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" com as propriedades obrigatórias. </li>
     <li>Adicione a propriedade "sling:orderBefore (String)" ao nó filho recém-criado. </li>
     <li>Adicione o nome do nó como o valor antes do qual o caractere especial recém-adicionado deve ser exibido. </li>
     <li>Clique em Salvar tudo. </li>
     <li>Atualize o Editor de texto\Criar interface de usuário de correspondência para ver as alterações.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
