---
title: '"Tutorial: Criar um formulário adaptável'''
seo-title: Create an adaptive form
description: Saiba como criar, criar layout e visualizar um formulário adaptável. Além disso, saiba como configurar ações de envio.
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# Tutorial: Criar um formulário adaptável {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial é uma etapa do [Criar seu primeiro formulário adaptável](/help/forms/using/create-your-first-adaptive-form.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

## Sobre o tutorial {#about-the-tutorial}

Os formulários adaptáveis são formulários de nova geração que são dinâmicos e responsivos. Você pode usar os Formulários adaptáveis para fornecer experiências personalizadas. Também é possível integrar formulários adaptáveis com [!DNL Adobe Analytics] para estatísticas de utilização e [!DNL Adobe Campaign] para gerenciamento de campanha. Para obter mais informações sobre recursos de formulários adaptáveis, consulte [Introdução à criação de formulários adaptáveis](/help/forms/using/introduction-forms-authoring.md).

É mais fácil criar e gerenciar formulários ao seguir um processo adequado. Neste artigo, você aprenderá a:

* [Crie um formulário adaptável que permita ao cliente adicionar um endereço de envio](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Campos de layout de um formulário adaptável para exibir e aceitar informações de um cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Criar ação de envio para enviar um email contendo conteúdo de formulário](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Visualizar e enviar um formulário adaptável](/help/forms/using/create-adaptive-form.md)

Você terá um formulário semelhante ao seguinte no final do artigo:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Etapa 1: Criar o formulário adaptável {#step-create-the-adaptive-form}

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**. O URL padrão é [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma opção para selecionar um modelo é exibida. Toque no **[!UICONTROL Em branco]** modelo para selecioná-lo e tocar **[!UICONTROL Próximo]**.

1. Uma opção para **[!UICONTROL Adicionar propriedades]** é exibido. O **[!UICONTROL Título]** e **[!UICONTROL Nome]** são obrigatórios:

   * **Título:** Especificar `Add new or update shipping address` no **[!UICONTROL Título]** campo. O campo title especifica o nome de exibição do formulário. O título ajuda a identificar o formulário no AEM [!DNL Forms] interface do usuário.
   * **Nome:** Especificar `shipping-address-add-update-form` no **[!UICONTROL Nome]** campo. O campo Name especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. À medida que você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.

1. Toque **[!UICONTROL Criar]**. Um formulário adaptável é criado, e uma caixa de diálogo para abrir o formulário para edição é exibida. Toque **[!UICONTROL Abrir]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição. Também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Para obter informações sobre a interface adaptável de criação de formulários e os componentes disponíveis, consulte [Introdução à criação de formulários adaptáveis](/help/forms/using/creating-adaptive-form.md).

   ![recém-criado-adaptive-form](assets/newly-created-adaptive-form.png)

## Etapa 2: Adicionar cabeçalho e rodapé {#step-add-header-and-footer}

AEM [!DNL Forms] O fornece vários componentes para exibir informações em um formulário adaptável. Os componentes Cabeçalho e Rodapé ajudam a fornecer uma aparência consistente a um formulário. Um cabeçalho normalmente inclui o logotipo de uma corporação, o título do formulário e o resumo. Um rodapé normalmente inclui informações de direitos autorais e links para outras páginas.

1. Toque ![painel lateral de alternância](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). O navegador de componentes é aberto. Arraste o **[!UICONTROL Cabeçalho]** componente do navegador de componentes para o formulário adaptável.
1. Toque **[!UICONTROL Logotipo]**. A barra de ferramentas é exibida. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) na barra de ferramentas, digite **We.Retail** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Toque em Imagem. A barra de ferramentas é exibida. Toque ![cmppr](assets/cmppr.png). O navegador de propriedades é aberto à esquerda da tela. **[!UICONTROL Procurar]** e faça upload da imagem do logotipo. Toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). A imagem aparece no cabeçalho.

   Você pode tocar em Obter arquivo para baixar o logotipo usado neste artigo se não tiver um.

[Obter arquivo](assets/logo.png)

1. Arraste o **[!UICONTROL Rodapé]** componente de ![treeexpandall](assets/treeexpandall.png) ao formulário adaptável. Nesse estágio, o formulário tem a seguinte aparência:

   ![formulário adaptável com cabeçalhos e rodapés](assets/adaptive-form-with-headers-and-footers.png)

## Etapa 3: Adicionar componentes para capturar e exibir informações {#step-add-components-to-capture-and-display-information}

Os componentes são blocos de construção de um formulário adaptável. AEM [!DNL Forms] O fornece vários componentes para capturar e exibir informações em um formulário adaptável. Você pode arrastar os componentes de ![treeexpandall](assets/treeexpandall.png) para um formulário. Para saber mais sobre os componentes disponíveis e a funcionalidade correspondente, consulte [Introdução à criação de formulários adaptáveis](/help/forms/using/introduction-forms-authoring.md).

1. Arraste o **[!UICONTROL Componente Caixa numérica]** ao formulário adaptável. Coloque-o antes do componente de rodapé. Abra as propriedades do componente, altere **[!UICONTROL Título]** do componente para **`Customer ID`**, alterar **[!UICONTROL Nome do elemento]** para **`customer_ID`**, ativar a **[!UICONTROL Campo obrigatório]** , ative a **[!UICONTROL Usar o tipo de entrada do número HTML5]** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Arraste três componentes de Caixa de texto para o formulário adaptável. Coloque-os antes do componente de rodapé. Defina as seguintes propriedades para essas caixas de texto.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propriedade</b></td> 
      <td><b>Caixa de Texto 1<br/></b></td> 
      <td><b>Caixa de Texto 2<br/></b></td> 
      <td><b>Caixa de Texto 3</b></td> 
     </tr> 
     <tr> 
      <td>Título</td> 
      <td>Nome<br /> </td> 
      <td>Endereço de envio</td> 
      <td>Estado</td> 
     </tr> 
     <tr> 
      <td>Nome do elemento</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>Campo obrigatório</td> 
      <td>Ativado</td> 
      <td>Ativado</td> 
      <td>Ativado</td> 
     </tr> 
     <tr> 
      <td>Permitir várias linhas<br /> </td> 
      <td>Desativado</td> 
      <td>Ativado</td> 
      <td>Desativado</td> 
     </tr> 
    </tbody> 
   </table>

1. Arraste um **[!UICONTROL Caixa numérica]** antes do componente de rodapé. Abra as propriedades do componente, defina os valores listados na tabela abaixo, Toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriedade | Valor |
   |---|---|
   | Título | Código postal |
   | Nome do elemento | customer_ZIPCode |
   | Número máximo de dígitos | 6 |
   | Campo obrigatório | Ativado |
   | Tipo de Padrão de Exibição | Sem padrão |

1. Arraste um **[!UICONTROL Email]** antes do componente de rodapé. Abra as propriedades do componente, defina os valores listados na tabela abaixo e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriedade | Valor |
   |---|---|
   | Título | Email |
   | Nome do elemento | customer_Email |
   | Campo obrigatório | Ativado |

1. Arraste um **[!UICONTROL Anexo de arquivo]** antes do componente de rodapé. Abra as propriedades do componente, defina os valores listados na tabela abaixo e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Propriedade</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Título</td> 
      <td>Prova de endereço aprovada pelo Governo<br /> </td> 
     </tr> 
     <tr> 
      <td>Nome do elemento</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>Campo obrigatório</td> 
      <td>Ativado</td> 
     </tr> 
    </tbody> 
   </table>

1. Arraste um **[!UICONTROL Botão Enviar]** para o formulário adaptável. Coloque-o antes do componente de rodapé. Abra as propriedades do componente, altere Nome do elemento para `address_addition_update_submit`, toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). O layout do formulário é concluído e o formulário tem a seguinte aparência:

   ![forma adaptável com todos os componentes](assets/adaptive-form-with-all-the-components.png)

## Etapa 4: Configurar a ação de envio para o formulário adaptável {#step-configure-submit-action-for-the-adaptive-form}

Uma ação Enviar é acionada quando um usuário toca no botão Enviar em um formulário adaptável. Você pode usar uma ação de envio para salvar dados de formulário no repositório local, enviar dados de formulário para um terminal REST, enviar dados de formulário como email e muito mais. Os formulários adaptáveis fornecem mais algumas ações de envio prontas para uso. Para obter informações detalhadas, consulte [Configuração da ação Enviar](/help/forms/using/configuring-submit-actions.md).

Usando as etapas a seguir, é possível configurar a ação de envio de email e a ação de envio de demonstração do formulário:

1. Configure o servidor de email. Para obter detalhes, consulte [Configuração de notificação por email](/help/sites-administering/notification.md).


1. Toque **[!UICONTROL Contêiner de formulário]** no navegador Conteúdo e toque em ![cmppr](assets/cmppr.png). O navegador de propriedades é aberto à esquerda.
1. Ir para **[!UICONTROL Submissão]** >  **[!UICONTROL Enviar ação]**. Selecionar **[!UICONTROL Enviar Email]**. Especifique os seguintes valores e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriedade | Valor |
   |--- |--- |
   | De | `donotreply@weretail.com` |
   | Para | `${customer_Email}` |
   | Assunto | Confirmação: Você adicionou o endereço de envio no site We.Retail. |
   | Modelo do e-mail | Oi `${customer_Name}`, o seguinte endereço é adicionado como o endereço de envio da sua conta: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Regards, We.Retail |
   | Incluir anexos | Ativado |

   Seu formulário está pronto. Agora, é possível visualizar o formulário e testar a funcionalidade. Se você tiver usado o nome mencionado o tutorial e acessar o formulário no computador que está executando o AEM [!DNL Forms] , o formulário estará disponível em [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Etapa 5: Visualizar e enviar o formulário adaptável {#step-preview-and-submit-the-adaptive-form}

Você pode usar o **[!UICONTROL Opção Visualizar]** para avaliar a aparência e o comportamento de um formulário. É possível enviar um formulário no modo de visualização e também verificar as validações aplicadas em um formulário. Por exemplo, se um erro for exibido quando um campo obrigatório for deixado em branco.

Formulários adaptáveis também oferecem uma opção para emular a experiência de um formulário para vários dispositivos. Por exemplo, iPhone, iPad e Desktop. Você pode usar ambos **[!UICONTROL Visualizar]** e **[!UICONTROL Emulador]** ![régua](assets/ruler.png) opções em conjunto entre si para visualizar um formulário para dispositivos de tamanhos de tela diferentes.

1. Toque no **[!UICONTROL Visualizar]** no lado direito do editor de formulários. O formulário é aberto no modo de visualização. Se você tiver usado o nome mencionado no tutorial, a URL de visualização do formulário será [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Use ![régua](assets/ruler.png) para exibir a aparência do formulário em vários dispositivos.
1. Preencha os campos do formulário e toque em **[!UICONTROL Enviar]**. O formulário é enviado e você é redirecionado para o padrão **Obrigado** página. Você também pode especificar uma página de agradecimento personalizada. Para obter detalhes, consulte [Configuração da página de redirecionamento](/help/forms/using/configuring-redirect-page.md).

O formulário adaptável para adicionar um endereço está pronto. Se você tiver usado o nome mencionado no tutorial e acessado o formulário em uma máquina que executa o servidor AEM Forms, o formulário estará disponível em [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
