---
title: Gerenciar metadados de formulário
description: Os metadados facilitam a categorização e a organização de ativos e ajudam os usuários que procuram um ativo específico.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 2%

---

# Gerenciar metadados de formulário{#manage-form-metadata}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/manage-form-metadata.html) |
| AEM 6.5 | Este artigo |

## Visão geral  {#overview-nbsp}

Os metadados facilitam a categorização e a organização de ativos e ajudam os usuários que procuram um ativo específico.

Por padrão, o AEM Forms fornece um conjunto definido de metadados para cada tipo de ativo. Além dos metadados padrão, é possível adicionar metadados personalizados a cada um dos tipos de ativos. O AEM Forms também fornece o meio certo de criar, gerenciar e trocar todos esses metadados de forma eficiente para seus formulários.

Se você for um desenvolvedor ou um proprietário de site, poderá personalizar o Forms Portal, a interface do usuário final do AEM Forms para refletir os metadados que está usando em sua organização. Para obter mais informações sobre o Forms Portal, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Metadados no AEM Forms {#metadata-in-aem-forms}

No AEM Forms, a lista de propriedades de metadados associada a um ativo depende do seu tipo. Além disso, se você adicionar qualquer propriedade de metadados personalizada, ela será adicionada em todos os ativos do tipo em que os metadados personalizados foram adicionados.

### Tipos de ativos {#asset-types}

Os seguintes tipos de ativos são compatíveis com o AEM Forms:

* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (PDF simples)
* Formulários adaptáveis
* Recursos
* XFS

#### Ampla lista de metadados {#extensive-list-of-metadata}

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
   <td>Todos, exceto o recurso</td> 
   <td>Nome de exibição do formulário.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descrição</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Descrição do formulário. O usuário pode especificar esse valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos</td> 
   <td><p>Um valor somente leitura que especifica o tipo de ativo. Ele pode ter um dos seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário</li> 
     <li>formulário PDF, formulário PDF (Acroform) ou formulário PDF (Signed)</li> 
     <li>Documento, Documento (Assinado)</li> 
     <li>Formulários adaptáveis</li> 
     <li>Recurso</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Criado</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura que especifica o tempo de criação do ativo.</td> 
  </tr> 
  <tr> 
   <td>Data da última modificação</td> 
   <td>Todos</td> 
   <td>Um valor somente leitura que especifica a hora em que o ativo foi modificado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p>Um valor somente leitura que é automaticamente calculado com base no tipo de formulário.</p> 
    <ul> 
     <li>PDF/Modelo de formulário/Documento - obtido do arquivo binário carregado.</li> 
     <li>Formulário adaptável - Usuário conectado no momento da criação do formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p> Um valor somente leitura que define um dos seguintes estados de um formulário:</p> 
    <ul> 
     <li>Nenhum valor: se um formulário nunca foi publicado.</li> 
     <li>Publicado: quando um formulário é publicado.</li> 
     <li>Modificado: quando um formulário foi modificado depois de ter sido publicado uma vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Data da última publicação</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Um valor somente leitura que especifica a hora em que o formulário foi publicado pela última vez.</td> 
  </tr> 
  <tr> 
   <td>Horário ligado/desligado do Publish</td> 
   <td>Todos, exceto o recurso</td> 
   <td><p>Hora em que o formulário está agendado para ser publicado/despublicado automaticamente. O usuário define esse valor ao editar metadados.</p> 
    <ul> 
     <li>Os horários de ativação e desativação do Publish devem estar após a data atual. </li> 
     <li>O Tempo de desativação do Publish deve estar além do tempo de ativação da publicação. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Enviar URL</td> 
   <td><p>Modelo de formulário</p> <p>formulário PDF</p> </td> 
   <td><p>Para configurar uma URL especificada pelo usuário para enviar dados de formulário a um servlet.</p> <p>O URL de envio pode ser configurado usando qualquer um dos métodos a seguir, listados em ordem de precedência:</p> 
    <ul> 
     <li>Especifique um URL de envio diretamente em um Modelo de formulário usando o botão Enviar HTTP ao criar um formulário XFA no AEM Forms Designer.</li> 
     <li>Na interface do usuário do AEM Forms, selecione um formulário e especifique uma URL de envio ao editar as propriedades dos metadados.</li> 
     <li>No Forms Portal, edite o componente de Pesquisa e Lister e especifique um URL de envio na guia Link de formulário.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Perfil de renderização do HTML</td> 
   <td>Modelo de formulário</td> 
   <td>O perfil de renderização de HTML usado ao renderizar um Modelo de Formulário no formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Renderizar formato</td> 
   <td><p>Modelo de formulário</p> <p>Formulários adaptáveis</p> </td> 
   <td><p>Essa opção permite que o usuário especifique o formato de renderização do formulário quando os formulários forem publicados:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Ambos</li> 
    </ul> <p>Essa opção é usada para restringir o formato de renderização dos formulários somente no portal de formulários onde eles estão visíveis para o usuário final.</p> </td> 
  </tr> 
  <tr> 
   <td>Tags</td> 
   <td>Todos, exceto o recurso</td> 
   <td>Rótulos associados ao formulário para facilitar a pesquisa rápida e fácil.</td> 
  </tr> 
  <tr> 
   <td>Referências</td> 
   <td><p>Formulários adaptáveis</p> <p>Modelo de formulário</p> <p>Recurso</p> </td> 
   <td><p>Lista de ativos (outros formulários ou recursos) aos quais este formulário está relacionado. Esses ativos podem estar nas duas categorias a seguir:</p> 
    <ul> 
     <li>Refere-se: ativos aos quais o formulário atual se refere.</li> 
     <li>Referenciado por: Ativos que se referem ao ativo atual.</li> 
    </ul> <p>Esses ativos são exibidos como links e seus metadados podem ser acessados diretamente clicando neles.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Seleção do modelo de formulário (XDP/XSD)</td> 
   <td>Formulários adaptáveis</td> 
   <td><p>Especifica qual modelo de formulário é usado durante a criação do formulário adaptável. Essa propriedade pode ter os seguintes valores:</p> 
    <ul> 
     <li>Modelo de formulário: um modelo de formulário é selecionado entre os existentes no repositório. Esse valor pode ser atualizado.</li> 
     <li>Esquema XML: um arquivo XSD é carregado. Esse valor pode ser atualizado.</li> 
     <li>Nenhum</li> 
    </ul> 
    <div>
      Um modelo de formulário depois de selecionado pode ser atualizado, mas não removido. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir metadados de formulário {#view-form-metadata}

Os ativos têm valores de propriedade existentes, que podem ser exibidos no modo somente leitura. Esses metadados são originados no momento do upload ou da criação do formulário.

1. Navegue até o local do ativo para o qual deseja exibir metadados.

1. Abra a página de propriedades usando uma das seguintes maneiras:

   1. Clique em Propriedades da exibição ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) ícone de Ações rápidas.

      >[!NOTE]
      >
      >As Ações rápidas são itens de ação exibidos ao passar o mouse sobre uma miniatura.

   1. Selecione o formulário e clique em Propriedades da exibição ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) ícone que aparece na barra de ferramentas.
   1. Navegue até a página de detalhes do formulário clicando na miniatura do formulário quando não estiver no modo de seleção. Agora, clique no link ![aem6forms_eye_view_win](assets/aem6forms_eye_viewon.png) ícone de olho no canto superior direito e, em seguida, clique em Propriedades na lista abaixo.

1. A página de propriedades que é aberta exibe um esquema que contém apenas as propriedades de metadados que têm algum valor.

   A página de propriedades tem uma barra de ferramentas contendo dois ícones de ação:

   * Editar: ![aem6forms_edit](assets/aem6forms_edit.png) Editar os valores da propriedade de metadados
   * Exibir: ![aem6forms_eye_view_win](assets/aem6forms_eye_viewon.png) Navegue até a página de detalhes do formulário, que abre o formulário no modo de visualização.

   A parte de conteúdo é dividida em duas partes:

   * O painel esquerdo contém a miniatura do formulário
   * O painel direito contém propriedades de metadados no modo somente leitura, distribuídas em várias guias.

## Adicionar/atualizar valores de metadados de formulário {#add-update-form-metadata-values}

É possível editar o valor das propriedades de metadados existentes ou adicionar novos valores a um campo de propriedade de metadados existente (por exemplo, quando um campo de metadados está em branco).

### Atualizar valores de propriedade de metadados {#update-metadata-property-values}

1. Siga as etapas mencionadas na seção anterior para abrir a página de propriedades, onde os metadados existentes do formulário selecionado podem ser visualizados.

1. Na barra de ferramentas, clique no ícone de edição ![aem6forms_edit](assets/aem6forms_edit.png) para alterar o modo da página de somente leitura para leitura/gravação.

1. A página de propriedades que é aberta contém um esquema que contém uma combinação de campos de entrada editáveis e texto estático.

1. As propriedades exibidas em texto estático são aquelas que não podem ser editadas.

1. É possível navegar para outras guias para localizar campos de entrada para propriedades de metadados colocadas sob elas.

   Esta página tem uma barra de ferramentas contendo dois ícones de ação diferentes daqueles no modo de exibição:

   * Cancelar: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancelar todas as alterações feitas nos valores de propriedade de metadados até o momento
   * Concluído: ![aem6forms_check](assets/aem6forms_check.png) Salvar todas as alterações feitas nos valores de propriedade de metadados até o momento

   Ambas as ações direcionam o usuário de volta ao modo somente leitura da página de propriedades que contém os valores atualizados.

### Atualizar a miniatura do formulário {#update-the-form-thumbnail}

O painel esquerdo na página de propriedades exibe a miniatura do formulário. Por padrão, a miniatura exibida é a gerada no momento da criação do formulário (formulário adaptável) ou no momento do upload do formulário.

Para todos os tipos de formulário, você tem a opção de carregar uma imagem clicando em **[!UICONTROL Fazer upload de imagem]** e procure um arquivo de imagem no diretório local. A imagem selecionada é usada como uma miniatura em vez da padrão.

Para formulários adaptáveis, é fornecida uma funcionalidade adicional, que permite que o usuário gere uma miniatura como um instantâneo da visualização atual do formulário adaptável. Como o AEM Forms também oferece suporte à criação de formulários adaptáveis, a visualização do formulário adaptável pode mudar sempre que você alterar o formulário adaptável. Essa funcionalidade de gerar uma miniatura ajuda a obter uma nova miniatura para o formulário adaptável com base no status de visualização atual. Clique em **[!UICONTROL Gerar visualização]** para executar esta ação.

>[!NOTE]
>
>* Use uma imagem quadrada para a miniatura. Quando você usa uma imagem não quadrada e visualiza a miniatura na exibição em lista, a miniatura aparece cortada.
>* Depois que uma nova imagem é carregada ou gerada, a miniatura é substituída por essa imagem e não pode ser redefinida para a imagem anterior.
>

## Adicionar metadados personalizados {#add-custom-metadata}

Além dos metadados fornecidos prontos para uso, o AEM Forms é compatível com novos metadados personalizados.

Uma ferramenta (Editor de esquema de metadados) é fornecida para definir o esquema para o layout de metadados; ou seja, o layout do que aparece no **[!UICONTROL Propriedades]** página de um formulário. O Editor de esquema de metadados permite adicionar ou modificar um esquema personalizado para seus ativos.

O AEM Forms expõe os esquemas de metadados dos tipos de formulários compatíveis nesta ferramenta. Dessa forma, você pode acessar esses esquemas e usar a funcionalidade fornecida no editor de esquema de metadados para adicionar propriedades personalizadas.

### Navegar pelo editor de esquema de metadados {#navigate-the-metadata-schema-editor}

1. Navegue até **[!UICONTROL Ferramentas > Ativos > Esquemas de metadados]**.

1. Clique em **[!UICONTROL formulários]** dos formulários de esquema listados.

1. Na lista aberta, clique no tipo de ativo ao qual deseja adicionar metadados personalizados.

   >[!NOTE]
   >
   >Esses esquemas contêm propriedades de metadados que são fornecidas prontas para uso e não devem ser alteradas/editadas (marque a caixa de seleção e clique em editar na barra de ferramentas) para evitar problemas funcionais.

1. Qualquer tipo de ativo clicado abre uma lista contendo o `extendedmetadata` opção. Editar este esquema.

1. Marque a caixa de seleção ao lado de `extendedmetadata` e, em seguida, clique no botão editar ![aem6forms_edit](assets/aem6forms_edit.png) ícone que aparece na barra de ferramentas.

1. O AEM Forms abre o editor de esquema de metadados/construtor de formulários do tipo de ativo selecionado (nesse caso, formulário adaptável).

   ![Editor de esquema de metadados para o tipo de Formulário adaptável](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor de metadados

   1. O painel esquerdo contém seções com abas, onde os campos são posicionados, e o painel direito exibe todos os componentes de interface do usuário disponíveis e as propriedades do campo selecionado no painel esquerdo.

   1. A seção bloqueada não é editável e contém campos para todas as propriedades de metadados fornecidas imediatamente.

   1. Você pode adicionar guias adicionais clicando no símbolo +.

   1. Você pode adicionar um campo personalizado do tipo desejado arrastando o componente de campo da **[!UICONTROL Formulário de criação]** na página do esquema.
   1. As especificações desse campo podem ser fornecidas no **[!UICONTROL Configurações]** depois de clicar no campo.

### Adicionar propriedade de metadados personalizada no editor de esquema {#add-custom-metadata-property-in-schema-editor}

1. Navegue até a guia (existente ou nova) onde deseja adicionar a propriedade personalizada.

1. Arraste um componente do tipo desejado da **[!UICONTROL Formulário de criação]** seção para o painel esquerdo e coloque-o em um local conveniente.

   >[!NOTE]
   >
   >Não é possível mover as seções bloqueadas, mas você pode colocar o componente em qualquer um dos espaços vazios.

1. Clique em um componente que você acabou de arrastar. Na guia Configurações que é aberta no painel direito, preencha as informações dos seguintes campos:

   1. Especifique um Rótulo de campo que seja usado como um nome de exibição acima do campo colocado no esquema (Por exemplo: Departamento)
   1. No campo Mapear para propriedade, é possível ver um valor pré-preenchido **&#39;./jcr:content/metadata/default&#39;**. Altere o ‘**padrão**&quot; para um nome de propriedade desejado, que é usado para armazenar a propriedade no repositório crx (Por exemplo: &#39;./jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >Não altere o prefixo ‘./jcr:content/metadata/&#39;, pois define o caminho onde a propriedade é armazenada.
      >
      >Além disso, o nome da propriedade deve ser exclusivo para evitar a gravação de valores para duas ou mais propriedades no mesmo local no repositório. Portanto, é recomendável alterar o valor &quot;padrão&quot;.

   1. Preencha outras configurações com base no requisito. Por exemplo: selecione a opção Obrigatório se desejar tornar o campo obrigatório.
   1. Para excluir um campo adicionado, selecione-o e clique no link excluir ![delete-1](assets/delete-1.png) ícone.

1. Se necessário, siga as etapas 1 a 3 para adicionar outra propriedade.
1. Clique em **Concluído** depois de fazer todas as alterações.

   Você adicionou uma propriedade de metadados personalizada com êxito.

Todos os formulários adaptáveis no AEM Forms agora contêm essa propriedade de metadados adicional. Você pode editá-lo na página de propriedades.
