---
title: Suporte XFA em formulários adaptáveis baseados em XDP
seo-title: Suporte XFA em formulários adaptáveis baseados em XDP
description: O Lista suportou eventos XFA, propriedades, scripts e validação em formulários adaptáveis.
seo-description: O Lista suportou eventos XFA, propriedades, scripts e validação em formulários adaptáveis.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 7%

---


# Suporte XFA em formulários adaptáveis baseados em XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Introdução {#introduction}

Formulários adaptáveis oferecem suporte para vários eventos XFA, propriedades, scripts e validações definidos em um arquivo XDP, incluindo:

* Execução de scripts definidos em eventos no arquivo XDP.
* Captura de valores padrão e propriedades comportamentais para campos no arquivo XDP.
* Execução de scripts de validação definidos no arquivo XDP.

Quando um formulário adaptável é criado com base em um arquivo XDP, as propriedades, os eventos e as validações são preenchidos automaticamente na interface de criação do formulário. No entanto, os autores de formulários podem substituir alguns desses elementos para criar uma experiência alternativa.

Este artigo lista eventos, propriedades e validações XFA suportados em formulários adaptáveis e explica como substituí-los em formulários adaptáveis.

## Elementos XFA suportados e seu mapeamento em formulários adaptáveis {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### Fields {#fields}

Quando um formulário adaptável é criado usando um arquivo XDP, você pode arrastar e soltar um campo XFA no formulário adaptável. A tabela a seguir lista como os campos XFA são mapeados para campos de formulário adaptáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Campo ou container XFA</strong></p> </td>
   <td><p><strong>Componente de formulário adaptável correspondente</strong></p> </td>
  </tr>
  <tr>
   <td><p>Botão </p> </td>
   <td><p>Botão</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de seleção </p> </td>
   <td><p>Caixa de seleção</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de listagem </p> </td>
   <td><p>Lista suspensa</p> </td>
  </tr>
  <tr>
   <td><p>Campo de data/hora </p> </td>
   <td><p>Seletor de datas</p> </td>
  </tr>
  <tr>
   <td><p>Gráfico de assinatura</p> </td>
   <td><p>Rabiscar a assinatura</p> </td>
  </tr>
  <tr>
   <td><p>Campo numérico </p> </td>
   <td><p>Caixa numérica</p> </td>
  </tr>
  <tr>
   <td><p>Campo decimal</p> </td>
   <td><p>Caixa numérica</p> </td>
  </tr>
  <tr>
   <td><p>Campo de texto </p> </td>
   <td><p>Caixa de texto</p> </td>
  </tr>
  <tr>
   <td><p>Campo de senha </p> </td>
   <td><p>Caixa Senha</p> </td>
  </tr>
  <tr>
   <td><p>Imagem</p> </td>
   <td><p>Imagem</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>Texto</p> </td>
  </tr>
  <tr>
   <td><p>Subformulário </p> </td>
   <td><p>Painel</p> </td>
  </tr>
  <tr>
   <td><p>Área (Grupo)</p> </td>
   <td><p>Painel</p> </td>
  </tr>
  <tr>
   <td><p>Conjunto de subformulários </p> </td>
   <td><p>Painel</p> </td>
  </tr>
 </tbody>
</table>

### Propriedades {#properties}

A tabela a seguir captura como vários scripts XFA definidos nos arquivos XDP se comportam em formulários adaptáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Propriedades do componente XFA</strong></p> </td>
   <td><p><strong>Comportamento correspondente em formulários adaptáveis</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Mapeado para a propriedade Bind reference (bindRef) no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>Mapeado para a propriedade visível em forma adaptável. É possível substituí-lo usando a expressão de visibilidade.</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>Mapeado para a propriedade enabled em forma adaptável. Você pode substituí-la usando a expressão Access.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: função </p> </td>
   <td><p>Mapeado para a propriedade role no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: speakPriority </p> </td>
   <td><p>Mapeado para a propriedade speakPriority no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: speakText</p> </td>
   <td><p>Mapeado para o texto personalizado de Acessibilidade em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Acessibilidade: toolTip </p> </td>
   <td><p>Mapeado para a propriedade de descrição curta no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>legenda<em> (todos os tipos de campo)</em></p> </td>
   <td><p>Mapeado para a propriedade Title no formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (todos os tipos de Campo)</em></p> </td>
   <td><p>Mapeado para o Padrão de exibição em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (todos os tipos de campo)</em></p> </td>
   <td><p>Mapeada para a propriedade value em Formulário adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>itens<em> (Caixa de Lista, Caixa de seleção)</em></p> </td>
   <td><p>Mapeada para a propriedade options em forma adaptável. É possível substituí-lo usando a expressão Opções.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (Campo de texto)</em></p> </td>
   <td><p>Mapeado para a propriedade Máximo de caracteres permitidos na forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>várias linhas<em> (Campo de texto)</em></p> </td>
   <td><p>Mapeado para a propriedade Permitir várias linhas na forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (Campo numérico, Campo decimal)</em></p> </td>
   <td><p>Mapeado para a propriedade de dígitos do Frac em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (Campo numérico, Campo decimal)</em></p> </td>
   <td><p>Mapeado para a propriedade de dígitos de cliente potencial em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (Caixa de Lista)</em></p> </td>
   <td><p>Mapeado para a propriedade de seleção múltipla no formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Scripts {#scripts}

A tabela a seguir captura como vários scripts XFA definidos no arquivo XDP se comportam em formulários adaptáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>eventos de script XFA</strong></p> </td>
   <td><p><strong>Comportamento correspondente em formulários adaptáveis</strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>Mapeado para a expressão Calculate na forma adaptativa.</p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>Mapeado para a expressão Validação em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.<br /> </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>clique (campos de botão)</p> </td>
   <td><p>Mapeado para a expressão Click do botão.</p> </td>
  </tr>
  <tr>
   <td><p>Suporte para script no servidor</p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Suporte para serviços da Web</p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.</p> </td>
  </tr>
  <tr>
   <td><p>Alteração (campo de script, botão de opção, caixa de seleção)</p> </td>
   <td><p>Este script é executado em tempo de execução e não pode ser substituído em forma adaptável.</p> </td>
  </tr>
 </tbody>
</table>

### Validações {#validations}

A tabela a seguir captura como as validações XFA mapeiam para validações em formulários adaptáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Validação XFA</strong></p> </td>
   <td><p><strong>Validação correspondente em forma adaptável</strong></p> </td>
  </tr>
  <tr>
   <td><p>Padrão de validação (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Mensagem de padrão de validação (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Obrigatório (nullTest )</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>Mensagem vazia (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Validar script (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Mensagem de script de validação (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Não é possível substituir a propriedade obrigatória para botões de opção de formulário adaptável e grupos de caixas de seleção vinculados aos botões de seleção XFA.

