---
title: Componentes de rascunhos e envios
seo-title: Componentes de rascunhos e envios
description: Os rascunhos e os envios de componentes listas formulários que estão no estado de rascunho e já foram enviados. Você pode personalizar a aparência e o estilo do componente.
seo-description: Os rascunhos e os envios de componentes listas formulários que estão no estado de rascunho e já foram enviados. Você pode personalizar a aparência e o estilo do componente.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Componentes de rascunhos e envios{#drafts-and-submissions-component}

O componente Rascunhos e envios lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados. O componente tem seções separadas (guias) para rascunhos e formulários enviados. Os usuários podem visualização somente seus rascunhos e formulários enviados.

## Configurar o componente {#configuring-the-component}

O componente Rascunhos e envios tem duas guias: Rascunhos e submissões.

Para permitir que o envio de um formulário adaptável apareça na guia envios, defina **Enviar ação** como **[Ação de envio do Forms Portal](../../forms/using/configuring-submit-actions.md). Como alternativa,** ative a opção Enviar do portal do Forms. Sempre que um usuário envia o formulário, ele é adicionado à guia Envios.

A funcionalidade de rascunhos é ativada automaticamente. Quando um usuário clica em **Salvar** em um formulário adaptável, o formulário é adicionado à guia rascunhos.

Execute as seguintes etapas para adicionar e configurar um componente Rascunhos e envios:

1. Arraste e solte o componente **Rascunhos e envios** na categoria Serviços de Documento no navegador de componentes na sua página.
1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar do componente.

   ![Componente Rascunhos e envio](assets/drafts-submissions-edit.png)

1. Na caixa de diálogo Editar, especifique os detalhes a seguir e toque em **Concluído** para salvar as configurações.

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
   <td>Especifica o número máximo de resultados a serem exibidos. Se a contagem de resultados aumentar o limite Total de resultados, um link <strong>Mais </strong>aparecerá na parte inferior do componente. Clicar em <strong>Mais </strong>mostra todos os formulários. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica o estilo do componente. Você pode especificar <strong>Sem estilo</strong>, <strong>Estilo padrão</strong> ou <strong>Estilo personalizado</strong> para listar os formulários. Para Opção de estilo personalizado, você pode especificar o caminho do arquivo CSS personalizado em <strong>Caminho de estilo personalizado </strong>field<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Caminho de estilo personalizado</td>
   <td>Se você escolher a opção <strong>Estilo personalizado</strong> no campo <strong>Tipo de estilo</strong>, use o campo <strong>Caminho de estilo personalizado</strong> para especificar o caminho do arquivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opções de exibição</td>
   <td><p>Especifica as guias a serem exibidas. É possível optar por exibir formulários de rascunho, formulários enviados ou ambos. </p> <p><strong>Observação</strong>:<em> para opções <strong> de </strong>Exibição, se você selecionar uma opção diferente de  <strong>Ambas</strong>, a opção  <strong>Padrão </strong> de campo de tabela não será usada.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Guia Padrão</td>
   <td>Especifica a guia a ser exibida quando a página do portal de formulários for carregada. Você pode escolher entre <strong>Guia Forms Rascunho</strong> e <strong>Guia Forms Submetida</strong>.</td>
  </tr>
  <tr>
   <td>Configuração da guia Rascunho Forms</td>
   <td>Título personalizado</td>
   <td>Especifica o título da guia <strong>Rascunho Forms</strong>. O valor padrão é <strong>Draft Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado para a lista do Forms Draft.</td>
  </tr>
  <tr>
   <td>Configuração de guia do Forms enviada</td>
   <td>Título personalizado </td>
   <td>Especifica o título da guia <strong>Enviado do Forms </strong>. O valor padrão é <strong>Forms Submetido.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Especifica o layout a ser usado para a lista Envio Forms<strong> </strong>. </td>
  </tr>
 </tbody>
</table>

## Personalização do armazenamento {#customizing-the-storage}

Quando você usa a ação de envio do Forms Portal ou habilita a opção Armazenar dados no portal de formulários em forma adaptável, os dados do formulário são armazenados AEM repositório. Em um ambiente de produção, é recomendável não armazenar dados de formulário preliminares ou enviados AEM repositório. Em vez disso, é necessário integrar os rascunhos e o componente de envio a um armazenamento seguro como o banco de dados corporativo para armazenar rascunhos e dados de formulários enviados.

O portal da Forms permite que você armazene dados no repositório AEM local, no repositório AEM remoto ou em um banco de dados. A AEM Forms permite personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Você pode substituir métodos padrão para especificar como os dados de rascunho e envio são armazenados em um armazenamento de sua escolha. Por exemplo, você pode armazenar os dados em um armazenamento de dados implementado atualmente em sua organização.

O portal da Forms fornece serviços prontos para uso (APIs) para armazenar dados no repositório crx de instâncias de publicação locais e remotas do AEM Forms. É possível substituir as implementações padrão, descritas em [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md) artigo, por implementações personalizadas para substituir a funcionalidade padrão. Para obter informações detalhadas sobre os métodos necessários em uma implementação personalizada para armazenar conteúdo em um local seguro, consulte [Personalizando serviços de dados de Rascunho e Envio](/help/forms/using/custom-draft-submission-data-services.md) e [armazenamento personalizado para componentes de rascunhos e envios.](/help/forms/using/adding-custom-storage-provider-forms.md)

A documentação da AEM Forms fornece uma [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md). Você pode usar a implementação de amostra para desenvolver sua própria implementação personalizada.

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Lista de formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
