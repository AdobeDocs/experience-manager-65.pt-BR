---
title: Gerenciar metadados do formulário
seo-title: Manage form metadata
description: Os metadados permitem a categorização e a organização mais fáceis de ativos e ajudam os usuários que estão procurando por um ativo específico.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
role: Admin
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 1%

---

# Gerenciar metadados do formulário{#manage-form-metadata}

## Visão geral  {#overview-nbsp}

Os metadados permitem a categorização e a organização mais fáceis de ativos e ajudam os usuários que estão procurando por um ativo específico.

O AEM Forms, por padrão, fornece um conjunto definido de metadados para cada tipo de ativo. Além dos metadados padrão, você pode adicionar metadados personalizados a cada um dos tipos de ativos. O AEM Forms também fornece o meio certo de criar, gerenciar e trocar todos esses metadados de maneira eficiente para seus formulários.

Se você for um desenvolvedor ou um proprietário de site, poderá personalizar o Forms Portal, a interface de usuário final do AEM Forms para refletir os metadados que você está usando em sua organização. Para obter mais informações sobre o Forms Portal, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Metadados no AEM Forms {#metadata-in-aem-forms}

No AEM Forms, a lista de propriedades de metadados associadas a um ativo depende de seu tipo. Além disso, se você adicionar uma propriedade de metadados personalizada, ela será adicionada em todos os ativos do tipo em que os metadados personalizados foram adicionados.

### Tipos de ativos {#asset-types}

Os seguintes tipos de ativos são compatíveis com o AEM Forms:

* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (PDF simples)
* Formulários adaptáveis
* Recursos
* XFS

#### Lista abrangente de metadados {#extensive-list-of-metadata}

Veja a seguir uma extensa lista de propriedades de metadados compatíveis com o AEM Forms:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nome da propriedade</strong></td> 
   <td><strong>Tipo de ativo</strong></td> 
   <td><strong>Descrição</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Todos menos recursos</td> 
   <td>Nome de exibição do formulário.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrição</td> 
   <td>Todos menos recursos</td> 
   <td>Descrição do formulário. O usuário pode especificar esse valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos</td> 
   <td><p>Um valor somente leitura especificando o tipo de ativo. Ele pode ter um dos seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário</li> 
     <li>PDF form, PDF form (Acroform) ou PDF (Signed)</li> 
     <li>Documento, Documento (Assinado)</li> 
     <li>Formulários adaptáveis</li> 
     <li>Recurso</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Criado</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura especificando o horário de criação do ativo.</td> 
  </tr> 
  <tr> 
   <td>Data da última modificação</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura especificando a hora em que o ativo foi modificado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos menos recursos</td> 
   <td><p>Um valor somente leitura automaticamente calculado com base no tipo de formulário.</p> 
    <ul> 
     <li>PDF/Form template/Document - buscado no arquivo binário carregado.</li> 
     <li>Formulário adaptável - Usuário conectado no momento da criação do formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>Todos menos recursos</td> 
   <td><p> Um valor somente leitura que define um dos seguintes estados de um formulário:</p> 
    <ul> 
     <li>Nenhum valor: Se um formulário nunca tiver sido publicado.</li> 
     <li>Publicado: Quando um formulário é publicado.</li> 
     <li>Modificado: Quando um formulário foi modificado depois de ter sido publicado uma vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data da última publicação</td> 
   <td>Todos menos recursos</td> 
   <td>Um valor somente leitura especificando a hora em que o formulário foi publicado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Tempo de ativação/desativação da publicação</td> 
   <td>Todos menos recursos</td> 
   <td><p>Hora em que o formulário é agendado para publicação/publicação automática. O usuário define esse valor na edição de metadados.</p> 
    <ul> 
     <li>Tanto o Tempo de ativação quanto o Tempo de desativação devem estar além da data atual. </li> 
     <li>O tempo de desativação da publicação deve estar além do tempo de ativação da publicação. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Enviar URL</td> 
   <td><p>Modelo de formulário</p> <p>formulário PDF</p> </td> 
   <td><p>Para configurar um URL especificado pelo usuário para enviar dados de formulário a um servlet.</p> <p>O URL de envio pode ser configurado usando qualquer um dos métodos a seguir, listados em ordem de precedência:</p> 
    <ul> 
     <li>Especifique um URL de envio diretamente em um Modelo de formulário usando o botão Enviar por HTTP ao criar um formulário XFA no AEM Forms Designer.</li> 
     <li>Na interface do usuário do AEM Forms, selecione um formulário e especifique um URL de envio sobre a edição das propriedades de metadados.</li> 
     <li>No Portal do Forms, edite o componente Pesquisar e lister e especifique um URL de envio na guia Link de formulário .</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Perfil de renderização de HTML</td> 
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
   <td>Todos menos recursos</td> 
   <td>Rótulos associados ao formulário para facilitar a pesquisa rápida e fácil.</td> 
  </tr> 
  <tr> 
   <td>Referências</td> 
   <td><p>Formulários adaptáveis</p> <p>Modelo de formulário</p> <p>Recurso</p> </td> 
   <td><p>Lista de ativos (outros formulários ou recursos) aos quais este formulário está relacionado. Esses ativos podem se encaixar nas duas categorias a seguir:</p> 
    <ul> 
     <li>Refere-se a: Ativos aos quais o formulário atual se refere.</li> 
     <li>Referido por: Ativos que se referem ao ativo atual.</li> 
    </ul> <p>Esses ativos são exibidos como links e seus metadados podem ser acessados diretamente ao clicar neles.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Seleção do modelo de formulário (XDP/XSD)</td> 
   <td>Formulários adaptáveis</td> 
   <td><p>Especifica o modelo de formulário a ser usado durante a criação do formulário adaptável. Essa propriedade pode ter os seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário: Um template de formulário é selecionado dentre os existentes no repositório. Esse valor pode ser atualizado.</li> 
     <li>Esquema XML: Um arquivo XSD é carregado. Esse valor pode ser atualizado.</li> 
     <li>Nenhum</li> 
    </ul> 
    <div>
      Um modelo de formulário selecionado pode ser atualizado, mas não removido. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir metadados do formulário {#view-form-metadata}

Os ativos têm valores de propriedade existentes, que podem ser exibidos no modo somente leitura. Esses metadados são originários no momento do upload ou da criação do formulário.

1. Navegue até o local do ativo para o qual deseja exibir metadados.

1. Abra a página de propriedades usando uma das seguintes maneiras:

   1. Clique nas Propriedades da exibição ![e_revismode_properties_n](assets/e_reviewmode_properties_n.png) ícone de Ações rápidas.

      >[!NOTE]
      >
      >As Ações rápidas são os itens de ação exibidos em uma miniatura ao passar o mouse.

   1. Selecione o formulário e clique em Propriedades da exibição ![e_revismode_properties_n](assets/e_reviewmode_properties_n.png) ícone que aparece na barra de ferramentas.
   1. Navegue até a página de detalhes do formulário clicando na miniatura do formulário quando não estiver no modo de seleção. Agora, clique no botão ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) ícone de olho no canto superior direito e clique em Propriedades na lista abaixo.

1. A página de propriedade que é aberta exibe um esquema contendo apenas as propriedades de metadados que possuem algum valor.

   A página de propriedades tem uma barra de ferramentas contendo dois ícones de ação:

   * Editar: ![aem6forms_edit](assets/aem6forms_edit.png) Editar os valores de propriedade de metadados
   * Exibir: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navegue até a página de detalhes do formulário, que abre o formulário no modo de visualização.

   A parte do conteúdo é dividida em duas partes:

   * O painel esquerdo contém a miniatura do formulário
   * O painel direito contém propriedades de metadados no modo somente leitura, distribuído por várias guias.


## Adicionar/atualizar valores de metadados de formulário {#add-update-form-metadata-values}

É possível editar o valor das propriedades de metadados existentes ou adicionar novos valores a um campo de propriedade de metadados existente (por exemplo, quando um campo de metadados está em branco).

### Atualizar valores de propriedade de metadados {#update-metadata-property-values}

1. Siga as etapas mencionadas na seção anterior para abrir a página de propriedades, onde os metadados existentes do formulário selecionado podem ser visualizados.

1. Na barra de ferramentas, clique no ícone editar ![aem6forms_edit](assets/aem6forms_edit.png) para alterar o modo da página de somente leitura para leitura/gravação.

1. A página de propriedades que é aberta contém um esquema que contém uma combinação de campos de entrada editáveis e texto estático.

1. As propriedades exibidas no texto estático são as que não podem ser editadas.

1. É possível navegar para outras guias para encontrar campos de entrada para propriedades de metadados colocadas sob elas.

   Esta página tem uma barra de ferramentas contendo dois ícones de ação diferentes daqueles no modo de exibição:

   * Cancelar: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancelar quaisquer alterações feitas nos valores de propriedade de metadados até o momento
   * Feito em: ![aem6forms_check](assets/aem6forms_check.png) Salvar todas as alterações feitas nos valores de propriedade de metadados até o momento

   Ambas as ações direcionam o usuário para o modo somente leitura da página de propriedades que contém os valores atualizados.

### Atualizar a miniatura do formulário {#update-the-form-thumbnail}

O painel esquerdo na página de propriedades exibe a miniatura do formulário. Por padrão, a miniatura exibida é a gerada no momento da criação do formulário (formulário adaptável) ou no momento do upload do formulário.

Para todos os tipos de formulário, você tem a opção de carregar uma imagem clicando em **[!UICONTROL Carregar imagem]** e procurar um arquivo de imagem do diretório local. A imagem selecionada é usada como uma miniatura em vez da padrão.

Para formulários adaptáveis, é fornecida uma funcionalidade adicional, que permite ao usuário gerar uma miniatura como um instantâneo da visualização de formulário adaptável atual. Como o AEM Forms também suporta a criação de formulários adaptáveis, a visualização do formulário adaptável pode mudar sempre que você alterar o formulário adaptável. Essa funcionalidade para gerar uma miniatura ajuda a obter uma nova miniatura do formulário adaptável com base no status de visualização atual. Clique em **[!UICONTROL Gerar visualização]** para executar esta ação.

>[!NOTE]
>
>* Use uma imagem quadrada para a miniatura. Ao usar uma imagem não quadrada e exibir a miniatura na exibição em lista, a miniatura aparece cortada.
>* Depois que uma nova imagem é carregada ou gerada, a miniatura é substituída por essa imagem e não pode ser redefinida para a imagem anterior.
>


## Adicionar metadados personalizados {#add-custom-metadata}

Além dos metadados fornecidos prontos para uso, o AEM Forms suporta novos metadados personalizados.

Uma ferramenta (Editor de esquema de metadados) é fornecida para definir o esquema para o layout dos metadados; ou seja, o layout do que aparece na variável **[!UICONTROL Propriedades]** de um formulário. O Editor de esquema de metadados permite adicionar ou modificar um esquema personalizado para seus ativos.

O AEM Forms expõe os esquemas de metadados dos tipos de formulários suportados nesta ferramenta. Dessa forma, você pode acessar esses esquemas e usar a funcionalidade fornecida no editor de esquema de metadados para adicionar propriedades personalizadas.

### Navegar no editor de esquema de metadados {#navigate-the-metadata-schema-editor}

1. Navegar para **[!UICONTROL Ferramentas > Ativos > Esquemas de metadados]**.

1. Clique em **[!UICONTROL formulários]** nos formulários de esquema listados.

1. Na lista que é aberta, clique no tipo de ativo para o qual deseja adicionar metadados personalizados.

   >[!NOTE]
   >
   >Esses esquemas contêm propriedades de metadados que são fornecidas prontas e não devem ser alteradas/editadas (marcando a caixa de seleção e clicando em Editar na barra de ferramentas) para evitar problemas funcionais.

1. Qualquer tipo de ativo clicado abre uma lista que contém a variável `extendedmetadata` opção. Edite este esquema.

1. Marque a caixa de seleção ao lado `extendedmetadata` e, em seguida, clique em editar ![aem6forms_edit](assets/aem6forms_edit.png) ícone que aparece na barra de ferramentas.

1. O AEM Forms abre o editor de esquema de metadados/construtor de formulários do tipo de ativo selecionado (neste caso, formulário adaptável).

   ![Editor de esquema de metadados para o tipo de formulário adaptável](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor de metadados

   1. O painel esquerdo contém seções com guias onde os campos são colocados e o painel direito exibe todos os componentes da interface do usuário disponíveis e as propriedades do campo selecionado no painel esquerdo.

   1. A seção bloqueada não é editável e contém campos para todas as propriedades de metadados fornecidas imediatamente.

   1. É possível adicionar outras guias, clicando no símbolo +.

   1. Você pode adicionar um campo personalizado do tipo desejado arrastando o componente de campo do **[!UICONTROL Criar formulário]** na página do schema.
   1. As especificações para este campo podem ser fornecidas no **[!UICONTROL Configurações]** depois de clicar no campo .

### Adicionar propriedade de metadados personalizada no editor de esquema {#add-custom-metadata-property-in-schema-editor}

1. Navegue até a guia (existente ou nova) na qual deseja adicionar a propriedade personalizada.

1. Arraste um componente do tipo desejado da **[!UICONTROL Criar formulário]** para o painel esquerdo e coloque em um local conveniente.

   >[!NOTE]
   >
   >Não é possível mover as seções bloqueadas, mas você pode colocar o componente em qualquer um dos espaços vazios.

1. Clique em um componente que acabou de arrastar. Na guia Configurações que é aberta no painel direito, preencha as informações dos seguintes campos:

   1. Especifique um Rótulo de campo que será usado como um nome de exibição acima do campo colocado no esquema (Por exemplo: Departamento)
   1. No campo Mapear para propriedade , é possível ver um valor pré-preenchido **&quot;./jcr:content/metadata/default&#39;**. Altere o valor de **default**&quot; para um nome de propriedade desejado, que é usado para armazenar a propriedade no repositório crx (por exemplo: &quot;./jcr:content/metadata/Department&#39;)

      >[!NOTE]
      >
      >Não altere o prefixo ‘./jcr:content/metadata/&#39;, pois define o caminho onde a propriedade é armazenada.
      >
      >Além disso, o nome da propriedade deve ser exclusivo para evitar a gravação de valores para duas ou mais propriedades no mesmo local no repositório. Portanto, é recomendável alterar o valor &quot;padrão&quot;.

   1. Preencha outras configurações com base no requisito. Por exemplo: selecione a opção Obrigatório se desejar tornar o campo obrigatório.
   1. Para excluir um campo adicionado, selecione o campo e clique no botão Excluir ![delete-1](assets/delete-1.png) ícone .

1. Se necessário, siga as etapas de 1 a 3 para adicionar outra propriedade.
1. Clique em **Concluído** depois de fazer todas as alterações.

   Você adicionou com êxito uma propriedade de metadados personalizada.

Todos os formulários adaptáveis no AEM Forms agora contêm essa propriedade de metadados adicional. Você pode editá-lo na página de propriedades.
