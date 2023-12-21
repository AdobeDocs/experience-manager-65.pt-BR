---
title: Diferenciação de recursos entre formulários HTML e PDF forms
description: Saiba mais sobre as diferenças de recursos entre formulários HTML5 e PDF forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# Diferenciação de recursos entre formulários HTML e PDF forms {#feature-differentiation-between-html-forms-and-pdf-forms}

A tabela a seguir especifica o suporte ao recurso fornecido para formulários HTML e PDF forms:

<table>
 <tbody>
  <tr>
   <th>Destaque</th>
   <th>Formulários HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Códigos de barras<br /> </td>
   <td>Não disponível no nível da interface do usuário. </td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Campo de assinatura<br /> </td>
   <td><strong>Assinaturas digitais</strong> não são compatíveis, mas uma nova <strong>Rabiscar a assinatura</strong> é adicionado para assinaturas tipo papel. É possível rabiscar a assinatura no formulário usando o <strong>Rabiscar a assinatura</strong> campo. A assinatura é salva no formulário como uma imagem. É possível salvar informações de geolocalização na <strong>Rabiscar a assinatura</strong> campo.</td>
   <td>Campo de assinatura disponível para <strong>Assinaturas digitais</strong>.</td>
  </tr>
  <tr>
   <td>Mesclagem de dados</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Imagens</td>
   <td>O esquema do URI de dados é usado para exibir imagens. Todas as versões modernas de navegadores suportam esse esquema, mas há diferenças na variedade de formatos de imagem compatíveis com cada navegador.<br /> </td>
   <td>Os formatos .gif, .png, .jpeg, .bmp e .tiff são suportados.</td>
  </tr>
  <tr>
   <td>Paginação<br /> </td>
   <td><p>Um formulário HTML é dividido em painéis e caixas para dar-lhe uma aparência semelhante a PDF forms. O tamanho da página é calculado dinamicamente. Se todo o conteúdo de uma página em um formulário HTML5 for excluído ou marcado como oculto, a página em branco ficará oculta. Um espaço vazio (espaço em branco) não é exibido entre as páginas acima e abaixo da página em branco.</p> <p>Se a mesclagem de dados ou os scripts adicionarem conteúdo a uma página, o comprimento da página se expandirá para acomodar o conteúdo recém-adicionado. Nenhuma página nova é adicionada ao formulário para acomodar o conteúdo recém-adicionado. </p> <p><strong>Nota:</strong> Quando todo o conteúdo de uma página em um formulário HTML5 é excluído ou marcado como oculto, a página em branco (espaço em branco) permanece visível entre a primeira e a segunda página, mas não entre as outras páginas.</p> </td>
   <td>A paginação no PDF depende do conteúdo de dados mesclado ou do conteúdo do usuário e a contagem de páginas é aumentada/reduzida com base nela.</td>
  </tr>
  <tr>
   <td>Cabeçalhos/Rodapés </td>
   <td>Compatível. <br /> <br /> Como os formulários móveis HTML5 não suportam quebras de página, os cabeçalhos e rodapés são exibidos apenas uma vez. No entanto, você pode configurá-los no layout para serem exibidos em vários lugares na pré-visualização de formulários para dispositivos móveis.<br /> </td>
   <td>Compatível.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>É possível personalizar widgets para aprimorar a experiência do usuário em dispositivos móveis.<br /> </td>
   <td>Todos os widgets estão bloqueados e nenhum widget personalizado pode ser conectado.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Oferece suporte às construções de script XFA mais usadas. Para obter uma lista detalhada de construções compatíveis, consulte <a href="/help/forms/using/scripting-support.md">suporte a script</a>.</td>
   <td>Suporta todas as construções de script XFA.</td>
  </tr>
  <tr>
   <td>APIs de script do Acrobat </td>
   <td>Os formulários HTML5 são compatíveis com as APIs mais usadas. Para obter detalhes, consulte <a href="/help/forms/using/scripting-support.md">suporte a script</a>.</td>
   <td>Se o arquivo de PDF for aberto no Acrobat ou Reader, ele também suportará todas as APIs de script que o Acrobat fornece.</td>
  </tr>
  <tr>
   <td>Suporte para idiomas da direita para a esquerda </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
