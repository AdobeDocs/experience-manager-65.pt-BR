---
title: 'Estilo do formulário adaptável '
seo-title: 'Estilo do formulário adaptável '
description: 'Saiba como criar um tema personalizado, criar um estilo para componentes individuais e usar fontes da Web em um tema '
seo-description: 'Saiba como criar um tema personalizado, criar um estilo para componentes individuais e usar fontes da Web em um tema '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 263a25b70fe4a3e7de65b47f07932d2e5f3d0197
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 8%

---


# Estilo do formulário adaptável {#do-not-publish-style-your-adaptive-form}

Saiba como criar um tema personalizado, criar um estilo para componentes individuais e usar fontes da Web em um tema

![](do-not-localize/08-style_your_adaptiveformmain.png)

Este tutorial é uma etapa da série [Criar seu primeiro formulário adaptável](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso do tutorial completo.

## Sobre o tutorial {#about-the-tutorial}

É possível usar temas para fornecer uma aparência e um estilo exclusivos a um formulário adaptável. Você pode aplicar temas prontos para uso fornecidos com o editor de formulários adaptáveis ou criar temas personalizados próprios. AEM [!DNL Forms] fornece um [editor de temas](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) para criar temas personalizados. Um único tema pode fornecer uma aparência diferente ao mesmo formulário adaptável aberto em dispositivos móveis, tablets ou desktop. Nenhum conhecimento anterior de CSS ou LESS é necessário para usar o editor de temas, mas é desejado.

Ao final do tutorial, você aprenderá a:

* Aplicar um tema predefinido a um formulário adaptável
* Criar um tema para formulário adaptável usando o editor de temas
* Estilo de componentes individuais
* Seção de bônus: Usar fontes da Web em um tema personalizado

O formulário será semelhante ao seguinte depois que você concluir o tutorial:

![Formulário com um tema personalizado](assets/styled-adaptive-form.png)

## Antes de você iniciar {#before-you-start}

Baixe as imagens de estilo cabeçalho e logotipo, fornecidas abaixo, em sua máquina local. O cabeçalho do formulário adaptativo `shipping-address-add-update-form` usa as imagens de estilo de cabeçalho e logotipo. A imagem estilo cabeçalho é exibida no lado direito do cabeçalho.

[Obter arquivo](assets/header-style.png)

[Obter arquivo](assets/logo-1.png)

## Etapa 1: Aplicar um tema ao formulário adaptável {#step-apply-a-theme-to-your-adaptive-form}

O editor de formulários adaptativos fornece vários temas prontos para uso. Se você planeja não usar um estilo personalizado para seu formulário adaptável, também pode publicar seus formulários adaptáveis com um tema predefinido. Os temas são independentes das formas adaptativas. É possível aplicar o mesmo tema a vários formulários adaptáveis. Para aplicar um tema a um formulário adaptável:

1. Abra o formulário adaptável para edição.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Abra as propriedades de **[!UICONTROL container de formulário adaptável]**. No navegador de propriedades, navegue até **[!UICONTROL Básico]** > **[!UICONTROL Tema de formulário adaptável]**. O campo **[!UICONTROL Tema de formulário adaptável]** lista todos os temas predefinidos e personalizados. Por padrão, o tema Tela de desenho é aplicado.
1. Selecione um tema no campo **[!UICONTROL Tema de formulário adaptável]**. Por exemplo, **tema de Pesquisa**. Toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para aplicar o tema selecionado.

   ![Formulário adaptável com o tema padrão](assets/default-adaptive-form.png)

   **Figura: Formulário** *adaptável com o tema padrão*

   ![Formulário adaptável com o tema Pesquisa](assets/adaptive-form-with-survey-theme.png)

   **Figura: Formulário** *adaptável com o tema Pesquisa*

## Etapa 2: Atualize seu formulário adaptável {#step-update-your-adaptive-form}

O design exibido acima requer alterações no texto do espaço reservado e no logotipo do formulário adaptativo existente. Execute as seguintes etapas para fazer as alterações necessárias:

1. Altere o logotipo e o texto do cabeçalho existentes. Para remover o logotipo:

   1. Abra o formulário no editor de formulários.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Toque na imagem do logotipo no componente [!UICONTROL header] e toque em ![cmppr](assets/cmppr.png) **[!UICONTROL properties]**. Na propriedade [!UICONTROL image], toque em X para remover a imagem do logotipo existente.
   1. Toque em **[!UICONTROL carregar]**, selecione o logo.png e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para salvar as alterações. A imagem foi baixada na seção [Antes do start](/help/forms/using/style-your-adaptive-form.md#before-you-start).
   1. Toque no texto do cabeçalho, `We.Retail` e toque em ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Altere o texto do cabeçalho para `we retail`. Aplique a formatação em negrito somente a `we`em `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Remova o título e adicione texto de espaço reservado:

   1. Toque no campo ID do cliente e toque em ![cmppr](assets/cmppr.png) propriedades.
   1. Copie o conteúdo do campo **[!UICONTROL Title]** para o campo **[!UICONTROL Texto do espaço reservado]**.
   1. Exclua o conteúdo do campo **[!UICONTROL Title]** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Repita as três etapas anteriores para todas as caixas de texto, caixa numérica e campo de email no formulário.

      ![forma adaptativa atualizada](assets/updated-adaptive-form.png)

## Etapa 3: Criar um tema personalizado para o formulário adaptável {#step-create-a-custom-theme-for-your-adaptive-form}

Você pode usar [editor de temas](/help/forms/using/themes.md) para criar temas personalizados. O editor de temas é um editor WYSIWYG poderoso. É um método visual para aplicar o CSS a vários componentes de um formulário adaptável. Ele fornece controles mais finos para estilizar componentes e painéis de um formulário adaptável.

Um tema é uma entidade separada, como formas adaptativas. Ele contém estilos (CSS) para os componentes e painéis de um formulário adaptável. Os estilos incluem propriedades CSS, como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando um tema é aplicado, o estilo especificado é aplicado aos componentes correspondentes de um formulário adaptável.

Neste tutorial, você estilizará o cabeçalho e o rodapé, os componentes de texto e numéricos, o componente de anexo e os botões. Vamos start na criação de um tema:

### Criar um tema {#create-a-theme}

1. Faça logon na instância do autor AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temas]**. O URL padrão é [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Toque em **[!UICONTROL Criar]** e selecione **[!UICONTROL Tema]**. A página [!UICONTROL Criar tema] com os campos necessários para criar um tema é exibida. Os campos **[!UICONTROL Title]** e **[!UICONTROL Nome]** são obrigatórios:

   * **Título:** especifique um título do tema. Por exemplo, **Tema Global.** O título ajuda a identificar o tema a partir da lista de temas.
   * **Nome:** especifique o nome do tema. Por exemplo, **Tema Global.** Um nó com o nome especificado é criado no repositório. À medida que você digita um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hífens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.

1. Toque em **[!UICONTROL Criar]**. Um tema é criado e uma caixa de diálogo para abrir o formulário para edição é exibida. Toque em **[!UICONTROL Abrir]** para abrir o tema recém-criado em uma nova guia. O tema abre no editor de temas. Para estilizar, o editor de temas usa um formulário adaptativo pronto para uso enviado com AEM [!DNL Forms].

   Para obter informações sobre como usar a interface do editor de temas, consulte [Sobre o editor de temas](/help/forms/using/themes.md#aboutthethemeeditor).

1. Toque em **[!UICONTROL Opções de Temas]** ![opções de tema](assets/theme-options.png) > **[!UICONTROL Configurar]**. No campo **[!UICONTROL Formulário de Pré-visualização]**, selecione o formulário adaptável **Shipping-address-add-update-form**, toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png), toque em **[!UICONTROL Salvar]**. Agora, o editor de temas está configurado para usar seu próprio formulário adaptativo em vez do formulário adaptativo padrão. Toque em **[!UICONTROL Cancelar]** para retornar ao editor de temas.

   ![tema personalizado](assets/custom-theme.png)

   **Figura:Editor de** *temas com o formulário adaptável de formulário de entrega-address-add-update-form*

   ![criar um tema](assets/create-a-theme.png)

   **Figura: Formulário** *adaptável com o formulário padrão*

### Cabeçalho e rodapé de estilo {#style-header-and-footer}

O cabeçalho e o rodapé fornecem uma aparência consistente e distinta para um formulário adaptável. Geralmente, o cabeçalho contém o logotipo e o nome da organização, o rodapé contém informações de direitos autorais e permanecem idênticos em várias formas de uma organização. Para estilizar o cabeçalho e o rodapé do formulário adaptável de formulário de entrega-address-add-update-form:

1. Navegue até a opção **[!UICONTROL Cabeçalho]** > **[!UICONTROL Texto]** no painel Seletores. O painel Seletores fica à esquerda do editor de temas. Se o painel não estiver visível, toque em ![alternar painel lateral](assets/toggle-side-panel.png) Alternar painel lateral.

1. Defina as seguintes propriedades no acordeão **[!UICONTROL Texto]** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriedade | Valor |
   |---|---|
   | Família da fonte | Arial |
   | Cor da fonte | FFFFFF |
   | Tamanho da Fonte | 54 px |

1. Toque no widget [!UICONTROL header] e toque em **[!UICONTROL Cabeçalho]**. As opções para estilizar o widget Cabeçalho são exibidas à esquerda. Expanda a tabela **[!UICONTROL Dimension e Posição]**, defina **[!UICONTROL Altura]** como `120px` e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Expanda a opção **[!UICONTROL Plano de Fundo]** do widget de cabeçalho, defina **[!UICONTROL Cor de Plano de Fundo]** como `F6921E.`

   Passe o cursor do mouse sobre **[!UICONTROL Imagem e gradiente]** > **[!UICONTROL + Adicionar]**, toque em **[!UICONTROL Imagem]**. Defina as seguintes propriedades e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propriedade | Valor |
   |---|---|
   | imagem | Carregue o header-style.png. A imagem foi baixada na seção [Antes do start](/help/forms/using/style-your-adaptive-form.md#before-you-start). |
   | Posição | Parte Inferior Direita |
   | Lado a lado | Sem Repetição |

1. No editor de temas, toque no logotipo no cabeçalho e toque em **[!UICONTROL Logotipo do cabeçalho]**. Expanda a opção Dimension e posição, defina as seguintes propriedades e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Imagem</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Imagem</td> 
      <td> 
       <ul> 
        <li>Parte superior: 1,5rem</li> 
        <li>Parte inferior: -35 px</li> 
        <li>Esquerda: 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>Dica: </strong> toque no ícone de  <img src="assets/link.png"> link para fornecer um valor diferente para cada campo.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Altura</td> 
      <td>4,75 rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Toque no widget de rodapé e toque em **[!UICONTROL Rodapé]**. Expanda a opção **[!UICONTROL Plano de fundo]**, defina **[!UICONTROL Cor do plano de fundo]** como `F6921E` e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Estilo do componente de captura de dados e aplicar um plano de fundo ao formulário adaptável {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

É possível usar vários componentes em um formulário adaptável para capturar dados. Por exemplo, caixa de texto e caixa numérica. Você pode fornecer um estilo idêntico a todos os componentes de captura de dados ou estilo separado para cada componente. Neste tutorial, um estilo idêntico é aplicado a caixas numéricas (ID do cliente, CEP) e caixas de texto (ID do cliente, nome, endereço de envio, estado, e-mail). Para estilizar os componentes de captura de dados:

1. Toque no campo **[!UICONTROL ID do cliente]** e toque na opção **[!UICONTROL Widget de campo]**. Defina as seguintes propriedades e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Menu sanfonado</b></td> 
      <td><b>Propriedade</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Cor da Borda</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Raio da Borda </td> 
      <td> 
       <ul> 
        <li>Parte superior: 7px<br /> </li> 
        <li>Direita: 7px<br /> </li> 
        <li>Parte inferior: 7px<br /> </li> 
        <li>Esquerda: 7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Família da fonte</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Cor da fonte</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamanho da Fonte</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Dimension e posição</td> 
      <td>Largura</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension e posição</td> 
      <td>Imagem</td> 
      <td> 
       <ul> 
        <li>Esquerda: 10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Toque na área vazia acima do campo **[!UICONTROL ID do cliente]** e toque em **[!UICONTROL Container do painel responsivo]**. Defina **[!UICONTROL Plano de fundo]** > **[!UICONTROL Cor de plano de fundo]** como F1F2F2. Toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Estilo dos botões {#style-the-buttons}

Você pode usar um tema personalizado para aplicar um estilo idêntico a todos os botões do formulário adaptável e [estilo incorporado](/help/forms/using/inline-style-adaptive-forms.md) para aplicar um estilo a um botão específico. Para aplicar estilo aos botões:

1. Toque no botão **[!UICONTROL Enviar]** e toque na opção **[!UICONTROL Botão]**. Defina as seguintes propriedades e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Menu sanfonado</b></td> 
      <td><b>Propriedade</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Segundo plano</td> 
      <td>Cor do Plano de Fundo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borda<br /> </td> 
      <td>Cor da Borda</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Raio da Borda </td> 
      <td> 
       <ul> 
        <li>Parte superior: 7px<br /> </li> 
        <li>Direita: 7px<br /> </li> 
        <li>Parte inferior: 7px<br /> </li> 
        <li>Esquerda: 7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Texto<br /> </td> 
      <td>Família da fonte</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Cor da fonte</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamanho da Fonte</td> 
      <td>18 px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Aplique o tema](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form) personalizado, Tema global, ao formulário adaptável. Se o estilo não refletir no formulário adaptável, limpe o cache do navegador e tente novamente.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Etapa 4: Estilo de componentes individuais {#step-style-individual-components}

Alguns estilos se aplicam somente a um componente específico. Esses componentes são estilizados no editor de formulários adaptáveis.

1. Abra o formulário adaptável para edição. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. Na barra superior, selecione a opção **[!UICONTROL Estilo]**.

   ![opção de estilo](assets/style-option.png)

1. Toque no botão **[!UICONTROL Anexar]** e toque no ícone ![aem_6_3_edit](assets/aem_6_3_edit.png). Defina as seguintes propriedades na tabela **[!UICONTROL Dimension e Position]**:

   | Propriedade | Valor |
   |---|---|
   | Flutuar | À esquerda |
   | Largura | 10% |

1. Toque na opção **[!UICONTROL prova de endereço aprovada pelo governo]** e toque no ícone ![aem_6_3_edit](assets/aem_6_3_edit.png). Defina as seguintes propriedades:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Menu sanfonado</b></td> 
      <td><b>Propriedade</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Dimensões e Posição</td> 
      <td>Flutuar</td> 
      <td>À esquerda</td> 
     </tr> 
     <tr> 
      <td>Dimensões e Posição</td> 
      <td>Largura</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>Dimensões e Posição</td> 
      <td>Preenchimento</td> 
      <td> 
       <ul> 
        <li>Esquerda: 10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensões e Posição</td> 
      <td>Altura</td> 
      <td>40 px</td> 
     </tr> 
     <tr> 
      <td>Dimensões e Posição<br /> </td> 
      <td>Imagem</td> 
      <td><br /> 
       <ul> 
        <li>Direita: 2rem</li> 
        <li>Esquerda: 10rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Segundo plano</td> 
      <td>Cor do Plano de Fundo</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Largura da Borda</td> 
      <td>1 px</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Estilo de Borda</td> 
      <td>Sólido</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Cor da Borda</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Raio da Borda</td> 
      <td>7 px</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Família da fonte</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Cor da fonte</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Tamanho da Fonte</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Texto</td> 
      <td>Altura da Linha</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Toque no botão **[!UICONTROL Enviar]** e toque no ícone ![aem_6_3_edit](assets/aem_6_3_edit.png). Defina as seguintes propriedades:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Menu sanfonado</b></td> 
      <td><b>Propriedade</b></td> 
      <td><b>Valor</b></td> 
     </tr> 
     <tr> 
      <td>Dimension e posição</td> 
      <td>Flutuar</td> 
      <td>Direito</td> 
     </tr> 
     <tr> 
      <td>Dimension e posição</td> 
      <td>Imagem</td> 
      <td> 
       <ul> 
        <li>Parte superior: 5rem</li> 
        <li>Direita: 14rem</li> 
        <li>Parte inferior: 20 px</li> 
        <li>Esquerda: 20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Segundo plano</td> 
      <td>Cor do Plano de Fundo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Borda</td> 
      <td>Cor da Borda</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Etapa 5: Seção de bônus: Usar fontes da Web em um tema personalizado {#step-bonus-section-using-web-fonts-in-a-custom-theme}

É possível usar várias fontes para criar um formulário adaptável. Nem todos os dispositivos nos quais o formulário adaptativo é exibido podem ter as fontes usadas para projetar o formulário adaptável. Você pode usar um serviço de fontes da Web para fornecer as fontes necessárias ao dispositivo de público alvo.

[!DNL Adobe Fonts] é um serviço de fontes da Web. Você pode configurar e usar o serviço com formulários adaptáveis. Para usar [!DNL Adobe Fonts] em um formulário adaptável:

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsé agora chamado de Adobe Fonts e está incluído no Creative Cloud e em outras subscrições. [Saiba mais](https://fonts.adobe.com/).

1. Crie uma conta [Adobe Fonts](https://typekit.com/), crie um kit, adicione a fonte Myriad Pro ao kit, publique o kit e obtenha a ID do Kit. É necessário usar [!DNL Adobe Fonts] (fontes da Web) em um formulário adaptável.
1. No servidor AEM [!DNL Forms], navegue até ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Agora, abra uma pasta de configuração. Se uma configuração já estiver disponível, clique no botão **[!UICONTROL Criar]** para criar uma nova instância.

   Na caixa de diálogo Criar configuração, especifique um **Título** para a configuração e clique em **[!UICONTROL Criar]**. Você é redirecionado para a página de configuração. Na caixa de diálogo [!UICONTROL Editar Componente] que é exibida, forneça sua **ID do Kit** e clique em **[!UICONTROL OK]**.

1. Configure seu tema para usar a configuração [!DNL Adobe Fonts]. Na instância do autor, abra **[!UICONTROL Tema global]** no editor de temas. No editor de temas, navegue até **[!UICONTROL Opções de tema]** ![opções de tema](assets/theme-options.png) > **[!UICONTROL Configurar]**. No campo **[!UICONTROL Configuração do Adobe Fonts]**, selecione o kit e clique em **[!UICONTROL Salvar]**.

   As fontes adicionadas ao **[!UICONTROL Adobe Fonts]** estão disponíveis para seleção na tabela **[!UICONTROL Texto]** de todos os componentes.

