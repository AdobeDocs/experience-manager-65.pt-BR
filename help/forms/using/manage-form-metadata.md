---
title: Gerenciar metadados do formulário
seo-title: Gerenciar metadados do formulário
description: Os metadados permitem a classificação e organização mais fáceis de ativos e ajudam os usuários que estão procurando por um ativo específico.
seo-description: Os metadados permitem a classificação e organização mais fáceis de ativos e ajudam os usuários que estão procurando por um ativo específico.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# Gerenciar metadados do formulário{#manage-form-metadata}

## Visão geral  {#overview-nbsp}

Os metadados permitem a classificação e organização mais fáceis de ativos e ajudam os usuários que estão procurando por um ativo específico.

O AEM Forms, por padrão, fornece um conjunto definido de metadados para cada tipo de ativo. Além dos metadados padrão, você pode adicionar metadados personalizados a cada um dos tipos de ativos. O AEM Forms também fornece os meios certos de criar, gerenciar e trocar todos esses metadados de forma eficiente para seus formulários.

Se você for um desenvolvedor ou proprietário de um site, poderá personalizar o Portal do Forms , a interface do usuário final do AEM Forms , para refletir os metadados que você está usando em sua organização. Para obter mais informações sobre o Portal de formulários, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Metadados no AEM Forms {#metadata-in-aem-forms}

No AEM Forms, a lista de propriedades de metadados associadas a um ativo depende de seu tipo. Além disso, se você adicionar qualquer propriedade de metadados personalizados, ela será adicionada em todos os ativos do tipo em que os metadados personalizados foram adicionados.

### Asset types {#asset-types}

Os seguintes tipos de ativos são suportados no AEM Forms:

* Modelos de formulário (formulários XFA)
* Formulários PDF
* Documento (PDFs simples)
* Formulários adaptáveis
* Recursos
* XFS

#### Lista extensa de metadados {#extensive-list-of-metadata}

A seguir está uma extensa lista de propriedades de metadados compatíveis com o AEM Forms:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome da propriedade</strong></td> 
   <td><strong>Tipo de ativo</strong></td> 
   <td><strong>Descrição</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Todos exceto recursos</td> 
   <td>Nome de exibição do formulário.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrição</td> 
   <td>Todos exceto recursos</td> 
   <td>Descrição do formulário. O usuário pode especificar esse valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos os pacotes</td> 
   <td><p>Um valor somente leitura que especifica o tipo de ativo. Ele pode ter um dos seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário</li> 
     <li>Formulário PDF, formulário PDF (Acroform) ou formulário PDF (Assinado)</li> 
     <li>Documento, Documento (Assinado)</li> 
     <li>Formulários adaptáveis</li> 
     <li>Recurso</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Criado</td> 
   <td>Todos os pacotes</td> 
   <td>Um valor somente leitura que especifica o tempo de criação do ativo.</td> 
  </tr> 
  <tr> 
   <td>Data da última modificação</td> 
   <td>Todos os pacotes</td> 
   <td>Um valor somente leitura que especifica a hora em que o ativo foi modificado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos exceto recursos</td> 
   <td><p>Um valor somente leitura que é automaticamente calculado com base no tipo de formulário.</p> 
    <ul> 
     <li>PDF/Form template/Document - extraído do arquivo binário carregado.</li> 
     <li>Formulário adaptável - usuário conectado no momento da criação do formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>Todos exceto recursos</td> 
   <td><p> Um valor somente leitura que define um dos seguintes estados de um formulário:</p> 
    <ul> 
     <li>Nenhum valor: Se um formulário nunca tiver sido publicado.</li> 
     <li>Publicado: Quando um formulário é publicado.</li> 
     <li>Modificado: Quando um formulário foi modificado depois de ter sido publicado uma vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data da última publicação</td> 
   <td>Todos exceto recursos</td> 
   <td>Um valor somente leitura que especifica a hora em que o formulário foi publicado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Tempo de ativação/desativação da publicação</td> 
   <td>Todos exceto recursos</td> 
   <td><p>Hora em que o formulário está programado para ser publicado/não publicado automaticamente. O usuário define esse valor na edição de metadados.</p> 
    <ul> 
     <li>Tanto a hora de Ativar quanto a de Desativar devem estar além da data atual. </li> 
     <li>O tempo de Publicar desligado deve estar além do tempo de publicação ligado. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Enviar URL</td> 
   <td><p>Modelo de formulário</p> <p>formulário PDF</p> </td> 
   <td><p>Para configurar um URL especificado pelo usuário para enviar dados de formulário para um servlet.</p> <p>O URL de envio pode ser configurado usando qualquer um dos seguintes métodos, listados em ordem de precedência:</p> 
    <ul> 
     <li>Especifique um URL de envio diretamente em um Modelo de formulário usando o botão Enviar por HTTP ao criar um formulário XFA no AEM Forms Designer.</li> 
     <li>Na interface do usuário do AEM Forms, selecione um formulário e especifique um URL de envio para editar as propriedades de metadados.</li> 
     <li>No Portal de Formulários, edite o componente Pesquisar e Lister e especifique um URL de envio na guia Link de Formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Perfil de renderização HTML</td> 
   <td>Modelo de formulário</td> 
   <td>O perfil de renderização HTML usado ao renderizar um Modelo de formulário no formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato de renderização</td> 
   <td><p>Modelo de formulário</p> <p>Formulários adaptáveis</p> </td> 
   <td><p>Essa opção permite que o usuário especifique o formato de renderização do formulário quando os formulários forem publicados:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Ambos</li> 
    </ul> <p>Essa opção é usada para restringir o formato de renderização dos formulários somente no portal de formulários, onde eles estão visíveis para o usuário final.</p> </td> 
  </tr> 
  <tr> 
   <td>Tags</td> 
   <td>Todos exceto recursos</td> 
   <td>Rótulos associados ao formulário para facilitar a pesquisa rápida e fácil.</td> 
  </tr> 
  <tr> 
   <td>Referências</td> 
   <td><p>Formulários adaptáveis</p> <p>Modelo de formulário</p> <p>Recurso</p> </td> 
   <td><p>Lista de ativos (outros formulários ou recursos) aos quais este formulário está relacionado. Esses ativos podem ser incluídos nas duas categorias a seguir:</p> 
    <ul> 
     <li>Refere-se: Ativos aos quais o formulário atual se refere.</li> 
     <li>Referenciado por: Ativos que se referem ao ativo atual.</li> 
    </ul> <p>Esses ativos são exibidos como links e seus metadados podem ser acessados diretamente clicando neles.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Seleção do modelo de formulário (XDP/XSD)</td> 
   <td>Formulários adaptáveis</td> 
   <td><p>Especifica qual modelo de formulário é usado durante a criação do formulário adaptável. Essa propriedade pode ter os seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário: Um modelo de formulário é selecionado entre os existentes no repositório. Este valor pode ser atualizado.</li> 
     <li>Esquema XML: Um arquivo XSD é carregado. Este valor pode ser atualizado.</li> 
     <li>Nenhum</li> 
    </ul> 
    <div>
      Um modelo de formulário selecionado uma vez pode ser atualizado, mas não removido. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir metadados do formulário {#view-form-metadata}

Os ativos têm valores de propriedade existentes, que podem ser exibidos no modo somente leitura. Esses metadados são originários no momento do upload ou da criação do formulário.

1. Navegue até o local do ativo para o qual deseja exibir metadados.

1. Abra a página de propriedades usando uma das seguintes maneiras:

   1. Clique no ícone Propriedades de exibição ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) em Ações rápidas.

      >[!NOTE]
      >
      >As Ações rápidas são os itens de ação que são exibidos em uma miniatura ao passar o mouse.

   1. Selecione o formulário e clique no ícone Exibir propriedades ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) que aparece na barra de ferramentas.
   1. Navegue até a página de detalhes do formulário clicando na miniatura do formulário quando não estiver no modo de seleção. Agora, clique no ícone de olho ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) no canto superior direito e clique em Propriedades na lista abaixo dele.

1. A página de propriedade que é aberta exibe um esquema que contém apenas as propriedades de metadados que possuem algum valor.

   A página de propriedades tem uma barra de ferramentas que contém dois ícones de ação:

   * Editar: ![aem6forms_edit](assets/aem6forms_edit.png) Editar os valores de propriedade de metadados
   * Exibir: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navegue até a página de detalhes do formulário, que abre o formulário no modo de visualização.
   A parte do conteúdo é dividida em duas partes:

   * O painel esquerdo contém a miniatura do formulário
   * O painel direito contém propriedades de metadados no modo somente leitura, distribuídas por várias guias.


## Adicionar/atualizar valores de metadados do formulário {#add-update-form-metadata-values}

Você pode editar o valor das propriedades de metadados existentes ou adicionar novos valores a um campo de propriedade de metadados existente (por exemplo, quando um campo de metadados está em branco).

### Atualizar valores de propriedade de metadados {#update-metadata-property-values}

1. Siga as etapas mencionadas na seção anterior para abrir a página de propriedades na qual os metadados existentes do formulário selecionado podem ser exibidos.

1. Na barra de ferramentas, clique no ícone de edição ![aem6forms_edit](assets/aem6forms_edit.png) para alterar o modo da página de somente leitura para leitura/gravação.

1. A página de propriedades que é aberta contém um esquema que contém uma combinação de campos de entrada editáveis e texto estático.

1. As propriedades exibidas no texto estático são aquelas que não podem ser editadas.

1. É possível navegar para outras guias para localizar campos de entrada para propriedades de metadados colocadas sob elas.

   Esta página tem uma barra de ferramentas que contém dois ícones de ação diferentes daqueles no modo de exibição:

   * Cancelar: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancelar quaisquer alterações feitas nos valores de propriedade de metadados até o momento
   * Feito: ![aem6forms_check](assets/aem6forms_check.png) Salvar todas as alterações feitas nos valores de propriedade de metadados até o momento
   Ambas as ações direcionam o usuário de volta para o modo somente leitura da página de propriedades que contém os valores atualizados.

### Atualizar a miniatura do formulário {#update-the-form-thumbnail}

O painel esquerdo na página de propriedades exibe a miniatura do formulário. Por padrão, a miniatura exibida é a gerada no momento da criação do formulário (formulário adaptativo) ou no momento do upload do formulário.

Para todos os tipos de formulário, você tem a opção de carregar uma imagem clicando em **[!UICONTROL Carregar imagem]** e procurando um arquivo de imagem do diretório local. A imagem selecionada é usada como uma miniatura em vez da padrão.

Para formulários adaptáveis, é fornecida uma funcionalidade adicional, que permite ao usuário gerar uma miniatura como um instantâneo da visualização do formulário adaptável atual. Como o AEM Forms também suporta a criação de formulários adaptáveis, a visualização do formulário adaptável pode ser alterada sempre que você alterar o formulário adaptável. Essa funcionalidade para gerar uma miniatura ajuda a obter uma miniatura nova para o formulário adaptável com base no status de visualização atual. Clique em **[!UICONTROL Gerar visualização]** para executar esta ação.

>[!NOTE]
>
>* Use uma imagem quadrada para a miniatura. Quando você usa uma imagem não quadrada e exibe a miniatura na exibição de lista, a miniatura aparece cortada.
>* Quando uma nova imagem é carregada ou gerada, a miniatura é substituída por essa imagem e não pode ser redefinida para a imagem anterior.
>



## Adicionar metadados personalizados {#add-custom-metadata}

Além dos metadados fornecidos prontamente, o AEM Forms oferece suporte a novos metadados personalizados.

Uma ferramenta (Editor de esquema de metadados) é fornecida para definir o esquema para o layout dos metadados; ou seja, o layout do que aparece na página **[!UICONTROL Propriedades]** de um formulário. O Editor de esquema de metadados permite que você adicione ou modifique um esquema personalizado para seus ativos.

O AEM Forms expõe os esquemas de metadados dos tipos de formulários suportados nesta ferramenta. Dessa forma, você pode acessar esses esquemas e usar a funcionalidade fornecida no editor de esquema de metadados para adicionar propriedades personalizadas.

### Navegar no editor de esquema de metadados {#navigate-the-metadata-schema-editor}

1. Navegue até **[!UICONTROL Ferramentas > Ativos > Esquemas]** de metadados.

1. Clique em **[!UICONTROL formulários]** dos formulários de esquema listados.

1. Na lista que é aberta, clique no tipo de ativo para o qual deseja adicionar metadados personalizados.

   >[!NOTE]
   >
   >Esses esquemas contêm propriedades de metadados que são fornecidas prontamente e não devem ser alteradas/editadas (marcando a caixa de seleção e clicando em editar na barra de ferramentas) para evitar problemas funcionais.

1. Qualquer tipo de ativo clicado abre uma lista que contém a `extendedmetadata` opção. Edite este esquema.

1. Marque a caixa de seleção ao lado `extendedmetadata` e clique no ícone de edição ![aem6forms_edit](assets/aem6forms_edit.png) exibido na barra de ferramentas.

1. O AEM Forms abre o editor de esquema de metadados/construtor de formulários do tipo de ativo selecionado (neste caso, formulário adaptável).

   ![Editor de esquema de metadados para o tipo de formulário adaptável](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor de metadados

   1. O painel esquerdo contém seções com guias nas quais os campos são posicionados e o painel direito exibe todos os componentes da interface de usuário disponíveis e as propriedades do campo selecionado no painel esquerdo.

   1. A seção bloqueada não é editável e contém campos para todas as propriedades de metadados que são fornecidas da caixa.

   1. Você pode adicionar outras guias, clicando no símbolo +.

   1. É possível adicionar um campo personalizado do tipo desejado arrastando o componente de campo da seção **[!UICONTROL Criar formulário]** para a página de esquema.
   1. As especificações desse campo podem ser fornecidas na seção **[!UICONTROL Configurações]** depois de clicar no campo.

### Adicionar propriedade de metadados personalizados no editor de esquema {#add-custom-metadata-property-in-schema-editor}

1. Navegue até a guia (existente ou nova) na qual deseja adicionar a propriedade personalizada.

1. Arraste um componente do tipo desejado da seção **[!UICONTROL Criar formulário]** para o painel esquerdo e posicione-o em um local conveniente.

   >[!NOTE]
   >
   >Não é possível mover as seções bloqueadas, mas é possível colocar seu componente em qualquer um dos espaços vazios.

1. Clique em um componente que acabou de arrastar. Na guia Configurações que é aberta no painel direito, preencha as informações dos seguintes campos:

   1. Especifique um Rótulo de campo que será usado como um nome de exibição acima do campo colocado no esquema (por exemplo: Departamento)
   1. Em Mapear para o campo de propriedade, você pode ver um valor pré-preenchido **&#39;./jcr:content/metadata/default&#39;**. Altere o &quot;**padrão**&quot; para um nome de propriedade desejado, que é usado para armazenar a propriedade no repositório do crx (por exemplo: &quot;./jcr:content/metadata/Department&#39;)

      >[!NOTE]
      >
      >Não altere o prefixo ‘./jcr:content/metadata/’, pois define o caminho onde a propriedade é armazenada.
      >
      >Além disso, o nome da propriedade deve ser exclusivo para evitar a gravação de valores para duas ou mais propriedades no mesmo local no repositório. Portanto, é recomendável alterar o valor &#39;padrão&#39;.

   1. Preencha outras configurações com base no requisito. Por exemplo: selecione a opção Obrigatório se desejar tornar o campo obrigatório.
   1. Para excluir um campo adicionado, selecione-o e clique no ícone Excluir ![exclusão-1](assets/delete-1.png) .

1. Se necessário, siga as etapas de 1 a 3 para adicionar outra propriedade.
1. Clique em **Concluído** após fazer todas as alterações.

   Você adicionou com êxito uma propriedade de metadados personalizada.

Todos os formulários adaptáveis no AEM Forms agora contêm essa propriedade de metadados adicional. Você pode editá-lo na página de propriedades.
