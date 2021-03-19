---
title: Perguntas frequentes para formulários HTML5
seo-title: Perguntas frequentes para formulários HTML5
description: Perguntas frequentes sobre layout, suporte a scripts e escopo de formulários HTML5.
seo-description: Perguntas frequentes sobre layout, suporte a scripts e escopo de formulários HTML5.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Formulários para publicação de conteúdo para dispositivos móveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 0%

---


# Perguntas frequentes para formulários HTML5{#frequently-asked-questions-faq-for-html-forms}

Há algumas perguntas frequentes sobre layout, suporte a scripts e escopo de formulários HTML5.

## Layout {#layout}

1. Por que os códigos de barras e o campo de assinatura no não aparecem no meu formulário?

   Resposta: Os campos de códigos de barras e assinaturas não são relevantes em cenários HTML ou móveis. Esses campos são exibidos como uma área não interativa. No entanto, o AEM Forms Designer fornece um novo campo de rabisco de assinatura que pode ser usado em vez do campo de assinatura. Também é possível adicionar um [widget personalizado](../../forms/using/custom-widgets.md) para códigos de barras e integrá-lo.

1. O Rich Text é compatível com o Campo de texto XFA?

   Resposta: O campo XFA, que permite conteúdo avançado no AEM Forms Designer, não é suportado e é renderizado como texto normal sem suporte para estilo de texto na interface do usuário. Além disso, os campos XFA com propriedade de combinação são exibidos como um campo normal, embora ainda haja restrições no número de caracteres permitidos com base no valor de dígitos de combinação.

1. Existem limitações no uso de subformulários repetíveis?

   Resposta: Subformulários repetíveis devem ter uma contagem inicial de 1 ou mais. Não há suporte para subformulários repetidos com uma contagem inicial de zero. Também é possível optar por usar um Subformulário repetível e não exibi-lo quando o formulário for carregado. Para obter o caso de uso:

   1. Defina a contagem inicial do subformulário repetível como 1.

      ![contagem inicial](assets/intial-count.png)

   1. Use o evento initialize do formulário para ocultar a instância primária do Subformulário. Por exemplo, o código abaixo oculta a instância primária do Subformulário na inicialização do formulário. Também verifica o tipo de aplicativo para garantir que o script seja executado somente no lado do cliente:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Abra o script para adicionar uma instância do Subformulário para edição. Adicione o código como o abaixo para adicionar uma instância do script Subform.

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

   1. Abra o script para remover uma instância do Subformulário para edição. Adicione o código da seguinte maneira para remover uma instância do script Subform.

      O código verifica a contagem dos Subformulários. Se a contagem do Subformulário atingir 1, o código ocultará o subformulário em vez de excluir o Subformulário.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Abra o evento de apresentação de formulário para edição. Adicione o script a seguir ao evento para remover a instância oculta do script antes de editar. Impede o envio de dados do Subformulário oculto no envio.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Existem limitações no uso de subformulários ocultos?

   Resposta: Um subformulário oculto com hierarquia complexa que é dividida entre páginas causa problemas de layout. Uma solução alternativa é marcar o subformulário inicialmente visível e ocultá-lo em um script de inicialização com base em alguma lógica ou dado.

1. Por que alguns textos estão truncados ou são exibidos incorretamente no HTML5?

   Resposta: Quando um elemento de texto Desenhar ou Legenda não tem espaço suficiente para exibir o conteúdo, o texto aparece truncado na representação do formulário móvel. Esse truncamento também é visível na visualização Design do AEM Forms Designer. Embora esse truncamento possa ser tratado nos PDFs, ele não pode ser tratado nos formulários HTML5. Para evitar o problema, forneça espaço suficiente para Desenhar ou Texto de legenda para que ele não trunque no modo de design do AEM Forms Designer.

1. Estou observando problemas de layout relacionados à falta de conteúdo ou sobreposição de conteúdo. Qual é a razão?

   Resposta: Se houver um elemento Desenhar texto ou Desenhar imagem junto com outro elemento sobreposto na mesma posição (digamos um retângulo), o conteúdo Desenhar texto não estará visível se aparecer posteriormente na ordem do documento (na exibição Hierarquia do AEM Forms Designer). O PDF é compatível com camadas transparentes, mas os navegadores HTML/navegadores não são compatíveis com camadas transparentes.

1. Por que algumas fontes são exibidas no formulário HTML diferentes das usadas ao projetar o formulário?

   Resposta: Os formulários HTML5 não incorporam fontes (em contraste com PDF forms, onde as fontes são incorporadas dentro do formulário). Para que a versão HTML do formulário seja renderizada conforme esperado, verifique se as fontes especificadas no XDP estão disponíveis no servidor e na máquina cliente. Se as fontes necessárias não estiverem disponíveis no servidor, as fontes de fallback serão usadas. Além disso, se você usar fontes no Modelo de formulário que não estão disponíveis no dispositivo cliente, as fontes padrão do navegador serão usadas para renderizar o texto.

1. Os atributos vAlign e hAlign são suportados em formulários HTML?

   Sim, os atributos vAlign e hAlign são compatíveis. O atributo vAlign não é compatível com o Internet Explorer e no campo de várias linhas.

1. Os formulários HTML5 são compatíveis com caracteres hebraicos?

   Os formulários HTML5 são compatíveis com caracteres hebraicos em todos os navegadores, exceto o Microsoft Internet Explorer.

1. Os formulários HTML5 têm limitações no campo numérico?

   Resposta: Sim, os formulários HTML5 têm algumas limitações. Se o número de dígitos for superior à contagem especificada na cláusula de imagem, os números não serão localizados e serão exibidos em localidade inglesa.

1. Por que os formulários HTML são maiores que os PDF forms?

   Muitas estruturas de dados e objetos intermediários, como dom de formulário, dom de dados e dom de layout, são necessários para renderizar um XDP em um formulário HTML.

   Para PDF forms, a Adobe Acrobat tem um mecanismo XTG integrado para criar estruturas de dados e objetos intermediários. O Acrobat também cuida do layout e dos scripts.

   Para formulários HTML5, os navegadores não têm um mecanismo XTG integrado para criar estruturas de dados intermediárias e objetos de bytes XDP brutos. Assim, para formulários HTML5, estruturas intermediárias são geradas no servidor e enviadas ao cliente. No cliente, o script baseado em JavaScript e o mecanismo de layout usam essas estruturas intermediárias.

   O tamanho da estrutura intermediária depende do tamanho do XDP original e dos dados unidos ao XDP.

1. Existem limitações relacionadas ao uso de tabelas no meu xdp?

   Resposta: Tabelas complexas causam problemas na renderização.

   * A seção (SubformSet) dentro de uma tabela não é suportada.
   * Linhas de cabeçalho ou rodapé em algumas tabelas são marcadas para repetição. Dividir essas tabelas em várias páginas pode ter alguns problemas.

1. As tabelas acessíveis têm limitações?

   Resposta: Sim, tabelas acessíveis têm as seguintes limitações:

   * Tabelas e subformulários aninhados dentro de uma tabela não são suportados.
   * Os cabeçalhos só são suportados para as colunas da linha superior ou esquerda da tabela. Os cabeçalhos não são compatíveis com elementos de tabelas intermediárias. É possível aplicar cabeçalhos a vários cabeçalhos de linha e coluna, desde que todas as linhas e colunas estejam juntamente com a linha ou a coluna mais à esquerda da tabela.
   * `Rowspan`e  `colspan`de um local aleatório dentro da tabela não é suportado.

   * Não é possível adicionar ou remover dinamicamente instâncias de linhas que contenham elementos com valor de expansão de linha maior que 1.

1. Qual é a ordem de leitura da dica de ferramenta e da legenda para leitores de tela?

   * Quando legenda e dica de ferramenta estão presentes, a única legenda é lida. Se a legenda não estiver disponível, a dica de ferramenta será lida. Também é possível especificar a precedência para a leitura em um XDP usando o designer de formulário
   * Quando você passa o mouse sobre um elemento, a dica de ferramenta é exibida. Se a dica de ferramenta não estiver disponível, o texto de fala será exibido. Se o texto da fala não estiver disponível, o nome do campo será exibido.

1. Quando você passa o mouse sobre um campo, uma dica de ferramenta é exibida. Como desativá-lo?

   Para desativar a dica de ferramenta ao passar o mouse, selecione nenhum no painel de acessibilidade do Designer.

1. No Designer, um usuário pode configurar propriedades de aparência personalizadas de botões de opção e caixas de seleção. Ao renderizar os formulários, os formulários HTML5 levam em consideração essas propriedades de aparência personalizadas?

   Resposta: Formulários HTML5 ignoram as propriedades de aparência personalizadas de botões de opção e caixas de seleção. Os botões de opção e as caixas de seleção são exibidos de acordo com as especificações do navegador subjacente.

1. Quando um Formulário HTML5 é aberto em um navegador compatível, a borda dos campos colocados adjacentemente não é alinhada corretamente ou os subformulários aparecem sobrepostos. Quando o mesmo formulário HTML5 é visualizado no Forms Designer, os campos e o layout não aparecem desalinhados e os subformulários aparecem na posição correta. Como corrigir o problema?

   Quando um subformulário é definido para continuar o conteúdo e ele tem um elemento de borda oculto, a borda dos campos colocados adjacentemente não é alinhada corretamente ou os subformulários aparecem sobrepostos. Para resolver o problema, você pode remover ou comentar os elementos &lt;border> ocultos do XDP correspondente. Por exemplo, o seguinte elemento &lt;border> é marcado como um comentário:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Por que os leitores de tela não funcionam corretamente com o objeto de campo Data/hora?

   Os leitores de tela não suportam campos de data/hora. No entanto, você pode inserir manualmente a data/hora no campo para fazer com que o leitor de tela o leia. Use dica de ferramenta ou texto de leitor de tela para instruir o usuário a selecionar manualmente a data/hora do campo.

1. Os formulários HTML5 são compatíveis com padrões de exibição para campos flutuantes?

   Resposta: Os formulários HTML5 não são compatíveis com padrões de exibição para campos flutuantes.

### Scripts {#scripting}

1. Existem limitações na implementação do JavaScript para HTML Forms?

   Resposta:

   * Há suporte limitado para o script xfa.connectionSet. Para connectionSet, somente a invocação do serviço da Web no lado do servidor é suportada. Para obter informações detalhadas, consulte [Suporte a scripts](/help/forms/using/scripting-support.md).
   * Não há suporte para $record e $data nos scripts do cliente. No entanto, se os scripts forem escritos em um bloco formReady, layoutReady , os scripts ainda funcionarão porque esses eventos são executados no lado do servidor.
   * Os scripts específicos do elemento XFA Draw, como a alteração do texto Draw (ou do texto da Legenda no caso de campos) não são suportados.

1. Existem limitações no uso do formCalc?

   Resposta: Somente um subconjunto dos scripts formCalc está implementado no momento. Para obter informações detalhadas, consulte [Suporte a scripts](/help/forms/using/scripting-support.md).

1. Existe alguma convenção de nomenclatura recomendada e há palavras-chave reservadas para evitar?

   * No AEM Forms Designer, é recomendável não iniciar o nome de um objeto (como um subformulário ou um campo de texto) com um sublinhado (_). Para usar o sublinhado no início do nome, adicione um prefixo depois do sublinhado, _&lt;prefix>&lt;objectname>.
   * Todas as APIs de formulários HTML5 são palavras-chave reservadas. Para APIs/funções personalizadas, use um nome que não seja idêntico a [APIs de formulários HTML5](/help/forms/using/scripting-support.md).

1. Os formulários HTML5 são compatíveis com campos flutuantes?

   Sim, o HTML5 Forms suporta campos flutuantes. Para ativar campos flutuantes, adicione a seguinte propriedade ao perfil de renderização:

   >[!NOTE]
   >
   >Por padrão, os campos não são ativados para flutuação. Você pode usar o Forms Designer para definir a propriedade flutuante dos campos.

   1. Abra o CRXde lite e navegue até o nó `/content/xfaforms/profiles/default` .
   1. Adicione uma propriedade `mfDataDependentFloatingField`do tipo String e defina o valor da propriedade como `true`.
   1. Clique em **Salvar tudo**. Agora os campos flutuantes são ativados para o HTML Forms usando o perfil de renderização atualizado.

      >[!NOTE]
      >
      >Para habilitar campos flutuantes para um formulário específico sem atualizar o perfil de renderização, passe a propriedade mfDataDependentFloatingField=true como um parâmetro de URL.

1. Os formulários HTML5 executam o script de inicialização e o evento pronto para o formulário várias vezes?

   Sim, os scripts de inicialização e os eventos prontos para o formulário são executados várias vezes, pelo menos uma vez no servidor e uma vez no lado do cliente. É sugerido gravar scripts como initialize ou form:ready com base em alguma lógica comercial (formulário ou dados de campo) para que a ação seja executada com base no estado dos dados e idempotente (se os dados forem iguais).

### Criação de XDP {#designing-xdp}

1. Existem palavras-chave reservadas em formulários HTML5?

   Resposta: Todas as APIs de formulários HTML5 são palavras-chave reservadas. Para APIs/funções personalizadas, use um nome que não seja idêntico a [APIs de formulários HTML5](/help/forms/using/scripting-support.md). Além das palavras-chave reservadas, se você usar nomes de objeto que comecem com um sublinhado (_), é recomendável adicionar um prefixo exclusivo após o sublinhado. Adicionar um prefixo ajuda a evitar qualquer possível conflito com as APIs internas dos formulários HTML5. Por exemplo, `_fpField1`
