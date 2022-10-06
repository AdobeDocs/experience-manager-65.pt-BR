---
title: Componentes de rascunhos e envios
seo-title: Drafts and submissions component
description: Os rascunhos e os componentes de envios listam os formulários que estão no estado de rascunho e já estão enviados. Você pode personalizar a aparência e o estilo do componente.
seo-description: Drafts and submissions component lists forms that are in the draft state and are already submitted. You can customize appearance and style of the component.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Componentes de rascunhos e envios{#drafts-and-submissions-component}

O componente Rascunhos e envios lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados. O componente tem seções (guias) separadas para rascunhos e formulários enviados. Os usuários podem exibir somente seus rascunhos e formulários enviados.

## Configurar o componente {#configuring-the-component}

O componente Rascunhos e envios tem duas guias: Rascunhos e envios.

Para permitir que o envio de um formulário adaptável apareça na guia envios, defina a variável **Enviar ação** para **[Ação de envio do portal do Forms](../../forms/using/configuring-submit-actions.md). Em alternativa,** habilite a opção Enviar pelo portal do Forms. Sempre que um usuário envia o formulário, ele é adicionado à guia envios.

A funcionalidade de rascunhos é ativada imediatamente. Quando um usuário clica em **Salvar** em um formulário adaptável, o formulário é adicionado à guia rascunhos.

Execute as etapas a seguir para adicionar e configurar um componente Rascunhos e envios :

1. Arraste e solte a **Rascunhos e envios** na categoria Serviços de documento no navegador de componentes na página.
1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar do componente.

   ![Componente Rascunhos e envio](assets/drafts-submissions-edit.png)

1. Na caixa de diálogo Editar , especifique os seguintes detalhes e toque em **Concluído** para salvar as configurações.

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
   <td>Especifica o número máximo de resultados a serem exibidos. Se a contagem de resultados aumentar o limite de Total de Resultados, uma <strong>Mais </strong>é exibido na parte inferior do componente. Clicar <strong>Mais </strong>mostra todos os formulários. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica o estilo do componente. Você pode especificar <strong>Sem estilo</strong>, <strong>Estilo padrão</strong>ou <strong>Estilo personalizado</strong> para listar os formulários. Para a Opção de estilo personalizado, você pode especificar o caminho do arquivo CSS personalizado na variável <strong>Caminho de estilo personalizado </strong>campo<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Caminho de estilo personalizado</td>
   <td>Se você escolher <strong>Estilo personalizado</strong> na <strong>Tipo de estilo</strong> use o <strong>Caminho de estilo personalizado</strong> para especificar o caminho do arquivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opções de exibição</td>
   <td><p>Especifica as guias a serem exibidas. É possível optar por exibir formulários de rascunho, formulários enviados ou ambos. </p> <p><strong>Observação</strong>:<em> Para <strong>Opções de exibição</strong>, se você selecionar uma opção diferente de <strong>Ambos</strong>, o <strong>Guia Padrão</strong> não é usada.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Guia Padrão</td>
   <td>Especifica a guia a ser exibida quando a página do portal de formulários for carregada. Você pode escolher entre <strong>Guia Forms de rascunho</strong> e <strong>Guia Forms Enviada</strong>.</td>
  </tr>
  <tr>
   <td>Configuração da guia Rascunho do Forms</td>
   <td>Título personalizado</td>
   <td>Especifica o título da variável <strong>Forms de rascunho</strong> guia . O valor padrão é <strong>Forms de rascunho.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado na lista Forms de rascunho.</td>
  </tr>
  <tr>
   <td>Configuração da guia Forms enviada</td>
   <td>Título personalizado </td>
   <td>Especifica o título da variável <strong>Forms enviado </strong>guia . O valor padrão é <strong>Forms enviado.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado para o Forms Enviado<strong> </strong>lista. </td>
  </tr>
 </tbody>
</table>

## Personalização do armazenamento {#customizing-the-storage}

Quando você usa a ação de envio do Portal do Forms ou habilita a opção Armazenar dados no portal de formulários em um formulário adaptável, os dados do formulário são armazenados AEM repositório. Em um ambiente de produção, é recomendável não armazenar dados de rascunho ou de formulário enviado em AEM repositório. Em vez disso, é necessário integrar os rascunhos e o componente de envio a um armazenamento seguro, como o banco de dados corporativo, para armazenar rascunhos e dados de formulários enviados.

O portal do Forms permite armazenar dados no repositório AEM local, no repositório AEM remoto ou em um banco de dados. O AEM Forms permite personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Você pode substituir métodos padrão para especificar como os dados de rascunho e envios são armazenados em um armazenamento de sua escolha. Por exemplo, você pode armazenar os dados em um armazenamento de dados implementado atualmente em sua organização.

O portal do Forms fornece serviços prontos para uso (APIs) para armazenar dados no repositório crx de instâncias de publicação locais e remotas do AEM Forms. É possível substituir as implementações padrão, descritas em [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md) artigo, com implementações personalizadas para substituir a funcionalidade padrão. Para obter informações detalhadas sobre os métodos necessários em uma implementação personalizada para armazenar conteúdo em um local seguro, consulte [Personalização de serviços de dados de rascunho e envio](/help/forms/using/custom-draft-submission-data-services.md) e [Armazenamento personalizado para rascunhos e componentes de envios.](/help/forms/using/adding-custom-storage-provider-forms.md)

A documentação do AEM Forms fornece um [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md). Você pode usar a implementação de amostra para desenvolver sua própria implementação personalizada.

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e Envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
