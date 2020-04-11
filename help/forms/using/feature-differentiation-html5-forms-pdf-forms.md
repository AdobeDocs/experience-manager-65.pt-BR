---
title: Diferenciação de recursos entre formulários HTML5 e formulários PDF
seo-title: Diferenciação de recursos entre formulários HTML5 e formulários PDF
description: Recurso compatível com formulários HTML5 e PDF
seo-description: Recurso compatível com formulários HTML5 e PDF
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Diferenciação de recursos entre formulários HTML5 e formulários PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

A tabela a seguir especifica o suporte ao recurso fornecido para formulários HTML5 e PDF:

<table>
 <tbody>
  <tr>
   <th>Recurso</th>
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
   <td><strong>Assinaturas</strong> digitais não são suportadas, mas um novo campo de assinatura <strong></strong> Scribble é adicionado para assinaturas como em papel. É possível escrever sua assinatura no formulário usando o campo Assinatura <strong>em forma de script</strong> . A assinatura é salva no formulário como uma imagem. É possível salvar informações de localização geográfica no campo Assinatura <strong></strong> em forma de script.</td>
   <td>Campo de assinatura disponível para Assinaturas <strong>digitais</strong>.</td>
  </tr>
  <tr>
   <td>Mesclagem de dados</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Imagens</td>
   <td>O esquema de URI de dados é usado para exibir imagens. Todas as versões modernas dos navegadores suportam esse esquema, mas há diferenças no intervalo de formatos de imagem que cada navegador suporta.<br /> </td>
   <td>Os formatos .gif, .png, .jpeg, .bmp e .tiff são suportados.</td>
  </tr>
  <tr>
   <td>Paginação<br /> </td>
   <td><p>Um formulário HTML5 é dividido em painéis e caixas para dar a ele uma aparência semelhante aos formulários PDF. O tamanho da página é calculado dinamicamente. Se todo o conteúdo de uma página em um formulário HTML5 for excluído ou marcado como oculto, a página em branco ficará oculta e um espaço vazio (espaço em branco) não será exibido entre as páginas acima e abaixo da página em branco.</p> <p>Se os scripts ou mesclagens de dados adicionarem conteúdo a uma página, o tamanho da página será expandido para acomodar o conteúdo recém-adicionado. Nenhuma nova página é adicionada ao formulário para acomodar o conteúdo recém-adicionado. </p> <p><strong>Observação:</strong> Quando todo o conteúdo de uma página em um formulário HTML5 é excluído ou marcado como oculto, a página em branco (espaço em branco) permanece visível entre a 1ª e a 2ª página, mas não entre quaisquer outras páginas.</p> </td>
   <td>A paginação no PDF depende da união do conteúdo de dados ou do conteúdo do usuário e a contagem de páginas é aumentada/reduzida com base nele.</td>
  </tr>
  <tr>
   <td>Cabeçalhos/rodapés </td>
   <td>Compatível. <br /> <br /> Como os formulários móveis HTML5 não suportam quebras de página, os cabeçalhos e rodapés são exibidos apenas uma vez. Entretanto, é possível configurá-los no layout para serem exibidos em vários lugares na pré-visualização de formulários móveis.<br /> </td>
   <td>Compatível.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>É possível personalizar widgets para aprimorar a experiência do usuário em dispositivos móveis.<br /> </td>
   <td>Todos os widgets são bloqueados e nenhum widget personalizado pode ser conectado.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Suporta as construções de script XFA mais usadas. Para obter detalhes sobre a lista de construções compatíveis, consulte suporte <a href="/help/forms/using/scripting-support.md">a</a>scripts.</td>
   <td>Suporta todas as construções de script XFA.</td>
  </tr>
  <tr>
   <td>Acrobat Script APIs </td>
   <td>Os formulários HTML5 suportam as APIs mais usadas. Para obter detalhes, consulte suporte a <a href="/help/forms/using/scripting-support.md">scripts</a>.</td>
   <td>Se o arquivo PDF for aberto dentro do Acrobat ou Reader, ele também oferecerá suporte a todas as APIs de script fornecidas pelo Acrobat.</td>
  </tr>
  <tr>
   <td>Suporte para idiomas da direita para a esquerda </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
