---
title: Perguntas frequentes sobre os formulários HTML5
description: Perguntas frequentes sobre layout, suporte a scripts e escopo dos formulários HTML5.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 0%

---


# Perguntas frequentes sobre os formulários HTML5{#frequently-asked-questions-faq-for-html-forms}

Há algumas perguntas frequentes sobre layout, suporte a scripts e escopo dos formulários HTML5.

## Layout {#layout}

1. Por que os códigos de barras e o campo de assinatura no não aparecem no meu formulário?

   Resposta: os campos Códigos de barras e assinaturas não são relevantes em cenários de HTML ou móveis. Esses campos aparecem como uma área não interativa. No entanto, o AEM Forms Designer fornece um novo campo de rabisco de assinatura que pode ser usado em vez do campo de assinatura. Também é possível adicionar um [widget personalizado](../../forms/using/custom-widgets.md) para códigos de barras e integre-o.

1. O Rich Text é compatível com o campo de texto XFA?

   Resposta: O campo XFA, que permite conteúdo avançado no AEM Forms Designer, não é compatível e é renderizado como texto normal sem suporte para estilizar o texto na interface do usuário. Além disso, os campos XFA com propriedade comb são exibidos como um campo normal, embora ainda haja restrições no número de caracteres permitidos com base no valor de dígitos comb.

1. Existem limitações relacionadas ao uso de subformulários repetíveis?

   Resposta: Subformulários repetíveis devem ter uma contagem inicial de 1 ou mais. Subformulários repetíveis com uma contagem inicial de zero não são compatíveis. Você também pode optar por usar um Subformulário repetível e não exibi-lo quando o formulário for carregado. Para obter o caso de uso:

   1. Defina a contagem inicial do Subformulário repetível como 1.

      ![contagem inicial](assets/intial-count.png)

   1. Use o evento de inicialização do formulário para ocultar a instância principal do Subformulário. Por exemplo, o código abaixo oculta a instância primária do Subformulário na inicialização do formulário. Ele também verifica o tipo de aplicativo para garantir que o script seja executado somente no lado do cliente:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Abra o script para adicionar uma instância do Subformulário para edição. Adicione o código como o abaixo para adicionar uma instância do script Subformulário.

      O código abaixo verifica a instância oculta do Subformulário. Se a instância oculta do Subformulário for encontrada, exclua a instância oculta do subformulário e insira uma nova instância do Subformulário. Se a instância oculta do Subformulário não for encontrada, basta inserir uma nova instância do Subformulário.

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. Abra o script para remover uma instância do Subformulário para edição. Adicione o código como o seguinte para remover uma instância do script Subformulário.

      O código verifica a contagem dos Subformulários. Se a contagem do Subformulário atingir 1, o código oculta o subformulário em vez de excluir o Subformulário.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Abra o evento de pré-envio do formulário para edição. Adicione o script a seguir ao evento para remover a instância oculta do script antes de editar. Isso impede o envio de dados do Subformulário oculto no envio.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Há alguma limitação relacionada ao uso de subformulários ocultos?

   Resposta: um subformulário oculto com hierarquia complexa que é dividido entre páginas causa problemas de layout. Uma solução alternativa é marcar o subformulário inicialmente visível e, em seguida, ocultá-lo em um script de inicialização com base em alguma lógica ou dados.

1. Por que alguns textos estão truncados ou são exibidos incorretamente no HTML5?

   Resposta: quando um elemento de texto Desenho ou Legenda não tiver espaço suficiente para exibir conteúdo, o texto aparecerá truncado na representação móvel do formulário. Esse truncamento também é visível na visualização Design do AEM Forms Designer. Embora esse truncamento possa ser manipulado nos PDF, ele não pode ser manipulado nos formulários HTML5. Para evitar o problema, forneça espaço suficiente para desenhar ou legendar o texto de modo que ele não fique truncado no modo de design do AEM Forms Designer.

1. Estou observando problemas de layout relacionados a conteúdo ausente ou sobreposição de conteúdo. Qual é o motivo?

   Resposta: se houver um elemento Desenhar Texto ou Desenhar Imagem junto com outro elemento sobreposto na mesma posição (digamos um Retângulo), o conteúdo Desenhar Texto não ficará visível se for exibido posteriormente na ordem do documento (na exibição Hierarquia do AEM Forms Designer). O PDF suporta camadas transparentes, mas o HTML/navegadores não suportam camadas transparentes.

1. Por que algumas fontes exibidas no formulário HTML são diferentes daquelas usadas durante a criação do formulário?

   Resposta: o HTML5 Forms não permite a incorporação de fontes (em contraste com os PDF forms em que as fontes são incorporadas dentro do formulário). Para que a versão do HTML de um formulário seja renderizada conforme esperado, verifique se as fontes estão disponíveis no Repositório CRX (Repositório de conteúdo AEM) do servidor AEM Forms AEM e na máquina que tem o Designer instalado. Quando as fontes não estão disponíveis no Repositório CRX do seu servidor AEM Forms ou no local onde o AEM Designer está instalado, o formulário é renderizado com fontes de fallback.

1. Os atributos Alinhar e Alinhar são suportados em formulários de HTML?

   Resposta: Sim, os atributos Alinhar e Alinhar são compatíveis. O atributo Alinhar não é compatível com o Internet Explorer e com campos de várias linhas.

1. Os formulários HTML5 suportam caracteres hebraicos?

   Resposta: os formulários HTML5 suportam caracteres hebraicos em todos os navegadores, exceto no Microsoft Internet Explorer.

1. Os formulários HTML5 têm limitações no campo numérico?

   Resposta: Sim, os formulários HTML5 têm algumas limitações. Se o número de dígitos for maior que a contagem especificada na cláusula picture, os números não estão localizados e são exibidos no local em inglês.

1. Por que os formulários HTML são maiores que os PDF forms?

   Resposta: Várias estruturas de dados intermediários e objetos como form dom, data dom e layout dom são necessários para renderizar um XDP para um formulário HTML.

   Para PDF forms, o Adobe Acrobat tem um mecanismo XTG integrado para criar estruturas de dados e objetos intermediários. A Acrobat também cuida do layout e dos scripts.

   Para formulários HTML5, os navegadores não têm um mecanismo XTG incorporado para criar estruturas de dados intermediárias e objetos de bytes XDP brutos. Assim, para formulários HTML5, as estruturas intermediárias são geradas no servidor e enviadas ao cliente. No cliente, o mecanismo de layout e script baseado em JavaScript usa essas estruturas intermediárias.

   O tamanho da estrutura intermediária depende do tamanho do XDP original e dos dados mesclados com o XDP.

1. Existem limitações relacionadas ao uso de tabelas no meu xdp?

   Resposta: Tabelas complexas causam problemas na renderização.

   * Não há suporte para seção (SubformSet) dentro de uma tabela.
   * As linhas de cabeçalho ou rodapé em algumas tabelas são marcadas para repetição. A divisão dessas tabelas em várias páginas pode gerar alguns problemas.

1. As tabelas acessíveis têm limitações?

   Resposta: Sim, as tabelas acessíveis têm as seguintes limitações:

   * Não há suporte para tabelas aninhadas e subformulários dentro de uma tabela.
   * Os cabeçalhos só são suportados para a linha superior ou colunas à esquerda da tabela. Os cabeçalhos não são compatíveis com elementos mid-table. É possível aplicar cabeçalhos a várias linhas e cabeçalhos de colunas, desde que todas essas linhas e colunas estejam junto com a linha mais acima ou mais à esquerda da tabela.
   * `Rowspan`e `colspan`de um local aleatório dentro da tabela não é suportado.

   * Não é possível adicionar ou remover dinamicamente a ocorrência de linhas que contêm elementos com o valor de rowspan maior que 1.

1. Qual é a ordem de leitura da dica de ferramenta e da legenda para leitores de tela?

   Resposta:
   * Quando a legenda e a dica de ferramenta estiverem presentes, a única legenda será lida. Se a legenda não estiver disponível, a dica de ferramenta será lida. Você também pode especificar a precedência para leitura em um XDP usando o designer de formulários
   * Quando você passa o mouse sobre um elemento, a dica de ferramenta é exibida. Se a dica de ferramenta não estiver disponível, o texto da fala será exibido. Se o texto de fala não estiver disponível, o nome do campo será exibido.

1. Quando você passa o mouse sobre um campo, uma dica de ferramenta é exibida. Como desativá-lo?

   Resposta: Para desativar a dica de ferramenta ao passar o mouse, selecione Nenhum no painel de acessibilidade do Designer.

1. No Designer, um usuário pode configurar propriedades de aparência personalizadas de botões de opção e caixas de seleção. Ao renderizar os formulários, os formulários HTML5 levam em conta essas propriedades de aparência personalizadas?

   Resposta: os formulários HTML5 ignoram as propriedades personalizadas de aparência do botão de opção e das caixas de seleção. Os botões de opção e as caixas de seleção são exibidos de acordo com as especificações do navegador subjacente.

1. Quando um Formulário HTML5 é aberto em um navegador compatível, a borda dos campos colocados adjacentemente não é alinhada corretamente ou os subformulários aparecem sobrepostos. Quando o mesmo Formulário HTML5 é visualizado no Forms Designer, os campos e o layout não aparecem desalinhados e os subformulários aparecem na posição correta. Como corrigir o problema?

   Resposta: quando um subformulário é definido para conteúdo de fluxo e o subformulário tem um elemento de borda oculto, a borda dos campos colocados adjacentes não é alinhada corretamente ou os subformulários aparecem sobrepostos. Para resolver o problema, você pode remover ou comentar o &lt;border> elementos do XDP correspondente. Por exemplo, o seguinte &lt;border> o elemento está marcado como um comentário:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Por que os leitores de tela não funcionam corretamente com o objeto de campo Data/Hora?

   Resposta: os leitores de tela não são compatíveis com campos de data/hora. No entanto, é possível inserir manualmente a data/hora no campo para que o leitor de tela o leia. Use dica de ferramenta ou texto de leitor de tela para instruir o usuário a selecionar manualmente a data/hora do campo.

1. Os formulários HTML5 suportam padrões de exibição para campos flutuantes?

   Resposta: os formulários HTML5 não suportam padrões de exibição para campos flutuantes.

1. Qual é o formato do campo Data no HTML5 Forms?

Resposta: O campo Data aceita o formato ISO, AAAA-MM-DD. Se você especificar uma data em algum outro formato, o Campo de data não aceitará a formatação até que o usuário saia do campo.

### Script {#scripting}

1. Existem limitações na implementação do JavaScript para o HTML Forms?

   Resposta:

   * Há suporte limitado para o script xfa.connectionSet. Para connectionSet, somente a invocação do serviço Web no lado do servidor é suportada. Para obter informações detalhadas, consulte [Suporte a script](/help/forms/using/scripting-support.md).
   * Não há suporte para $record e $data em scripts do cliente. No entanto, se os scripts forem gravados em um bloco formReady, layoutReady, os scripts ainda funcionarão, pois esses eventos são executados no lado do servidor.
   * Os scripts específicos de elemento XFA Draw, como a alteração do texto Draw (ou do texto Caption, se houver campos), não são compatíveis.

1. Existem limitações no uso do formCalc?

   Resposta: Apenas um subconjunto dos scripts formCalc está implementado no momento. Para obter informações detalhadas, consulte [Suporte a script](/help/forms/using/scripting-support.md).

1. Existe alguma convenção de nomenclatura recomendada e alguma palavra-chave reservada para evitar?

   Resposta:
   * No AEM Forms Designer, é recomendável não começar o nome de um objeto (como um subformulário ou um campo de texto) com um sublinhado (_). Para usar sublinhado no início do nome, adicione um prefixo depois do sublinhado,_&lt;prefix>&lt;objectname>.
   * Todas as APIs de formulários HTML5 são palavras-chave reservadas. Para APIs/funções personalizadas, use um nome diferente de [APIs de formulários HTML5](/help/forms/using/scripting-support.md).

1. Os formulários HTML5 são compatíveis com campos flutuantes?

   Resposta: Sim, o HTML5 Forms suporta campos flutuantes. Para ativar campos flutuantes, adicione a seguinte propriedade ao perfil de renderização:

   >[!NOTE]
   >
   >Por padrão, os campos não estão ativados para flutuante. Você pode usar o Forms Designer para definir a propriedade flutuante dos campos.

   1. Abra o CRXde lite e acesse o `/content/xfaforms/profiles/default` nó.
   1. Adicionar uma propriedade do `mfDataDependentFloatingField`do tipo String e defina o valor da propriedade como `true`.
   1. Clique em **Salvar tudo**. Agora os campos flutuantes são ativados para o HTML Forms usando o perfil de renderização atualizado.

      >[!NOTE]
      >
      >Para ativar campos flutuantes para um formulário específico sem atualizar o perfil de renderização, passe a propriedade mfDataDependentFloatingField=true como um parâmetro de URL.

1. Os formulários HTML5 executam o script de inicialização e o evento de formulário pronto várias vezes?

   Resposta: Sim, os scripts de inicialização e os eventos de formulário pronto são executados várias vezes, pelo menos uma vez no servidor e outra no lado do cliente. É recomendável gravar scripts como inicializar ou formulário:eventos prontos com base em alguma lógica de negócios (dados de formulário ou de campo) para que a ação seja executada com base no estado dos dados e idempotente (se os dados forem iguais).

### Design de XDP {#designing-xdp}

1. Existem palavras-chave reservadas em formulários HTML5?

   Resposta: Todas as APIs de formulários HTML5 são palavras-chave reservadas. Para APIs/funções personalizadas, use um nome diferente de [APIs de formulários HTML5](/help/forms/using/scripting-support.md). Além das palavras-chave reservadas, se você usar nomes de objeto que começam com um sublinhado (_), será recomendável adicionar um prefixo exclusivo após o sublinhado. Adicionar um prefixo ajuda a evitar qualquer possível conflito com as APIs internas do HTML5 Forms. Por exemplo, `_fpField1`
