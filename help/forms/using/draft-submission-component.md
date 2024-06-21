---
title: Rascunhos e componentes de envios
description: O componente Rascunhos e Envios lista os formulários que estão no estado de rascunho e já foram enviados. É possível personalizar a aparência e o estilo do componente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Rascunhos e componentes de envios{#drafts-and-submissions-component}

O componente Rascunhos e envios lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados. O componente tem seções (guias) separadas para rascunhos e formulários enviados. Os usuários podem exibir apenas seus rascunhos e formulários enviados.

## Configuração do componente {#configuring-the-component}

O componente Rascunhos e envios tem duas guias: Rascunhos e envios.

Para habilitar o envio de um formulário adaptável para aparecer na guia envios, defina o **Enviar ação** para **[Ação de envio do portal do Forms](../../forms/using/configuring-submit-actions.md). Alternativamente,** habilite a opção Enviar do Forms Portal. Sempre que um usuário enviar o formulário, ele será adicionado à guia Envios.

A funcionalidade rascunhos é ativada imediatamente. Quando um usuário clica em **Salvar** em um formulário adaptável, o formulário é adicionado à guia rascunhos.

Execute as seguintes etapas para adicionar e configurar um componente Rascunhos e Envios:

1. Arraste e solte a variável **Rascunhos e envios** componente na categoria Serviços de documento no navegador de componentes na sua página.
1. Selecione o componente e selecione ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar do componente.

   ![Rascunhos e componente de envio](assets/drafts-submissions-edit.png)

1. Na caixa de diálogo Editar, especifique os seguintes detalhes e selecione **Concluído** para salvar as configurações.

<table>
 <tbody>
  <tr>
   <th>Guia</th>
   <th>Configuração</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Geral</td>
   <td>Resultado total</td>
   <td>Especifica o número máximo de resultados a serem exibidos. Se a contagem de resultados aumentar o limite Resultado Total, uma variável <strong>Mais </strong>é exibido na parte inferior do componente. Clicando <strong>Mais </strong>mostra todos os formulários. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica o estilo do componente. Você pode especificar <strong>Sem Estilo</strong>, <strong>Estilo padrão</strong>ou <strong>Estilo personalizado</strong> para listar os formulários. Para a opção Estilo personalizado, você pode especificar o caminho do arquivo CSS personalizado no <strong>Caminho de estilo personalizado </strong>campo<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Caminho de estilo personalizado</td>
   <td>Se você escolher <strong>Estilo personalizado</strong> opção no <strong>Tipo de estilo</strong> , use o <strong>Caminho de estilo personalizado</strong> para especificar o caminho do arquivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opções de Exibição</td>
   <td><p>Especifica as guias a serem exibidas. Você pode optar por exibir formulários de rascunho, formulários enviados ou ambos. </p> <p><strong>Nota</strong>:<em> Para <strong>Opções de exibição</strong>, se você selecionar uma opção diferente de <strong>Ambos</strong>, o <strong>Guia Padrão</strong> opção de campo não é usada.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Guia Padrão</td>
   <td>Especifica a guia a ser exibida quando a página do portal de formulários for carregada. Você pode escolher entre <strong>Guia Forms de rascunho</strong> e <strong>Guia Forms enviada</strong>.</td>
  </tr>
  <tr>
   <td>Configuração da guia Forms de rascunho</td>
   <td>Título personalizado</td>
   <td>Especifica o título do <strong>Forms de rascunho</strong> guia. O valor padrão é <strong>Forms de rascunho.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado para a lista Forms de rascunho.</td>
  </tr>
  <tr>
   <td>Configuração da guia Forms enviada</td>
   <td>Título personalizado </td>
   <td>Especifica o título do <strong>Forms enviado </strong>guia. O valor padrão é <strong>Forms enviado.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado para o Forms enviado<strong> </strong>lista. </td>
  </tr>
 </tbody>
</table>

## Personalização do armazenamento {#customizing-the-storage}

Ao usar a ação enviar do Portal do Forms ou ativar a opção Armazenar dados no portal de formulários no formulário adaptável, os dados do formulário são armazenados no repositório AEM. Em um ambiente de produção, é recomendável não armazenar dados de rascunho ou de formulário enviados no repositório do AEM. Em vez disso, você deve integrar o componente de rascunhos e envio a um armazenamento seguro, como o banco de dados corporativo, para armazenar rascunhos e dados de formulários enviados.

O Forms portal permite armazenar dados em um repositório AEM local, em um repositório AEM remoto ou em um banco de dados. O AEM Forms permite personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Você pode substituir métodos padrão para especificar como os dados de rascunho e envio são armazenados em um armazenamento de sua escolha. Por exemplo, você pode armazenar os dados em um armazenamento de dados implementado atualmente em sua organização.

O Forms portal fornece serviços (APIs) prontos para armazenar dados no repositório crx de instâncias de publicação locais e remotas do AEM Forms. Você pode substituir as implementações padrão, descritas em [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md) artigo, com implementações personalizadas para substituir a funcionalidade padrão. Para obter informações detalhadas sobre os métodos necessários em uma implementação personalizada para armazenar conteúdo em um local seguro, consulte [Personalização de serviços de dados de Rascunho e Submissão](/help/forms/using/custom-draft-submission-data-services.md) e [Armazenamento personalizado para componentes de rascunhos e envios.](/help/forms/using/adding-custom-storage-provider-forms.md)

A documentação do AEM Forms fornece uma [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md). Você pode usar a implementação de amostra para desenvolver sua própria implementação personalizada.

## Artigos relacionados

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
