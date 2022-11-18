---
title: Modelos de fragmentos do conteúdo
description: Saiba como os Modelos de fragmentos de conteúdo servem como base para seu conteúdo headless no AEM e como criar Fragmentos de conteúdo com conteúdo estruturado.
feature: Content Fragments
role: User
exl-id: 6fd1fdb2-d1d3-4f97-b119-ecfddcccec9e
source-git-commit: 6b9eb1a6df7cc4a8afab1c83d93d8a53bd94f6f5
workflow-type: tm+mt
source-wordcount: '2332'
ht-degree: 95%

---

# Modelos de fragmentos do conteúdo {#content-fragment-models}

Modelos de fragmentos do conteúdo no AEM definem a estrutura do conteúdo para o [fragmentos de conteúdo,](/help/assets/content-fragments/content-fragments.md) servir como base do seu conteúdo sem periféricos.

Para usar modelos de fragmento de conteúdo, você pode:

1. [Ativar a funcionalidade de modelo de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Criar](#creating-a-content-fragment-model) e [configurar](#defining-your-content-fragment-model) os modelos de fragmento de conteúdo
1. [Ativar os modelos de fragmento de conteúdo](#enabling-disabling-a-content-fragment-model) para uso ao criar Fragmentos de conteúdo
1. [Autorizar os modelos de fragmento de conteúdo nas pastas de ativos necessárias](#allowing-content-fragment-models-assets-folder) ao configurar as **Políticas**.

## Criação de um modelo de fragmento de conteúdo {#creating-a-content-fragment-model}

1. Navegar para **Ferramentas**, **Ativos**, depois abra **Modelos de fragmentos do conteúdo**.
1. Navegue até a pasta apropriada para sua [configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Use **Criar** para abrir o assistente.

   >[!CAUTION]
   >
   >Se o [uso de modelos de fragmento de conteúdo não foi habilitado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

1. Especifique o **título do modelo**. Você também pode adicionar **Tags**, uma **Descrição** e selecionar **Ativar modelo** para [ativar o modelo](#enabling-disabling-a-content-fragment-model) se necessário.

   ![título e descrição](assets/cfm-models-02.png)

1. Use **Criar** para salvar o modelo vazio. Uma mensagem indicará o sucesso da ação. Você poderá selecionar **Abrir** para editar imediatamente o modelo, ou **Concluído** para retornar ao console.

## Definição do modelo de fragmento de conteúdo {#defining-your-content-fragment-model}

O modelo de fragmento de conteúdo define efetivamente a estrutura dos fragmentos de conteúdo resultantes usando uma seleção de **[Tipos de dados](#data-types)**. Usando o editor do modelo, é possível adicionar instâncias dos tipos de dados e configurá-las para criar os campos necessários:

>[!CAUTION]
>
>A edição de um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes.

1. Navegar para **Ferramentas**, **Ativos**, depois abra **Modelos de fragmentos do conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.

1. Abra o modelo necessário para **Edição**; use a ação rápida ou selecione o modelo e depois a ação na barra de ferramentas.

   Uma vez aberto, o editor de modelo mostra:

   * à esquerda: campos já definidos
   * à direita: **Tipos de dados** disponíveis para criar campos (e **Propriedades** para uso depois que os campos forem criados)

   >[!NOTE]
   >
   >Quando um campo é **Obrigatório**, o **Rótulo** indicado no painel à esquerda é marcado com um asterisco (**&#42;**).

   ![propriedades](assets/cfm-models-03.png)

1. **Para adicionar um campo**

   * Arraste um tipo de dados necessário para o local exigido de um campo:

      ![tipo de dados do campo](assets/cfm-models-04.png)

   * Depois que um campo é adicionado ao modelo, o painel direito mostrará as **Propriedades** que podem ser definidas para esse tipo de dados específico. Aqui é possível definir o que é necessário para esse campo.

      * Muitas propriedades são autoexplicativas. Para obter mais detalhes, consulte [Propriedades](#properties).
      * Digitar um **Rótulo de campo** preencherá automaticamente o **Nome da propriedade** se estiver vazio, e pode ser atualizado manualmente posteriormente.

         >[!CAUTION]
         >
         >Ao atualizar manualmente a propriedade **Nome da propriedade** de um tipo de dados, observe que os nomes devem conter somente caracteres latinos (A-Z, a-z), dígitos numéricos (0-9) e o underline (“_”) como caractere especial.
         >
         >Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.
      Por exemplo:

      ![propriedades de campo](assets/cfm-models-05.png)


1. **Para remover um campo**

   Selecione o campo desejado e clique/toque no ícone da lixeira. Você receberá uma solicitação para confirmar a ação.

   ![remover](assets/cfm-models-06.png)

1. Adicione todos os campos obrigatórios e defina as propriedades relacionadas, conforme necessário. Por exemplo:

   ![save](assets/cfm-models-07.png)

1. Selecione **Salvar** para salvar a definição.

## Tipos de dados {#data-types}

Uma variedade de tipos de dados está disponível para a definição do seu modelo:

* **Texto em linha única**
   * Adicionar um ou mais campos de uma única linha de texto; o comprimento máximo pode ser definido
* **Texto multilinha**
   * Uma área de texto que pode ser Rich Text, texto sem formatação ou Markdown
* **Número**
   * Adicionar um ou mais campos numéricos
* **Booleano**
   * Adicionar uma caixa de seleção booleana
* **Data e hora**
   * Adicionar uma data e/ou hora
* **Enumeração**
   * Adicionar um conjunto de caixas de seleção, botões de opção ou campos suspensos
* **Tags**
   * Permite que os autores de fragmentos acessem e selecionem áreas de tags
* **Referência de conteúdo**
   * Faz referência a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * Se uma imagem for referenciada, você pode optar por mostrar uma miniatura
* **Referência do fragmento**
   * Faz referência a outros fragmentos de conteúdo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * O tipo de dados pode ser configurado para permitir que os autores de fragmento:
      * Editem o fragmento referenciado diretamente.
      * Criem um novo fragmento de conteúdo, com base no modelo apropriado
* **Objeto JSON**
   * Permite que o autor do fragmento de conteúdo insira a sintaxe JSON nos elementos correspondentes de um fragmento.
      * Para permitir que o AEM armazene o JSON direto que você tenha copiado/colado de outro serviço.
      * O JSON será transmitido e emitido como JSON no GraphQL.
      * Inclui o realce da sintaxe JSON, o preenchimento automático e o realce de erros no editor de fragmentos de conteúdo.
* **Espaço reservado da guia**
   * Permite a introdução de guias para uso ao editar o conteúdo do fragmento de conteúdo.
Isso será mostrado como um divisor no editor de modelo, separando seções da lista de tipos de dados de conteúdo. Cada instância representa o início de uma nova guia.
No editor de fragmentos, cada instância será exibida como uma guia.

      >[!NOTE]
      >
      >Esse tipo de dados é usado apenas para formatação e é ignorado pelo esquema GraphQL do AEM.

## Propriedades {#properties}

Muitas propriedades são autoexplicativas. Para certas propriedades, os detalhes adicionais são os seguintes:


* **Nome da Propriedade**

   Ao atualizar manualmente essa propriedade para um tipo de dados, observe que os nomes **devem** conter *somente* caracteres latinos (A-Z, a-z), dígitos numéricos (0-9) e o underline (“_”) como caractere especial.

   >[!CAUTION]
   >
   >Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.

* **Renderizar como**
As várias opções para realizar/renderizar o campo em um fragmento. Geralmente, isso permite definir se o autor verá uma única instância do campo ou se poderá criar várias instâncias.

* **Rótulo de campo**
Inserir um 
**rótulo de campo** gerará automaticamente um **nome de propriedade**, que pode ser atualizado manualmente se necessário.

* **Validação**
A validação básica está disponível por meio de mecanismos como a propriedade **Obrigatório**. Alguns tipos de dados têm campos de validação de adição. Consulte [Validação](#validation) para obter mais detalhes.

* No tipo de dados **Texto multilinha**, é possível definir o **Tipo padrão** como:

   * **Rich Text**
   * **Markdown**
   * **Texto sem formatação**

   Se não for especificado, o valor padrão **Rich Text** é usado para esse campo.

   Alterar o **Tipo padrão** em um modelo de fragmento de conteúdo só terá efeito em um fragmento de conteúdo existente relacionado depois que esse fragmento for aberto no editor e salvo.

* **Exclusivo**
O conteúdo (para o campo específico) deve ser exclusivo em todos os fragmentos de conteúdo criados a partir do modelo atual.

   Isso é usado para garantir que os autores de conteúdo não possam repetir o conteúdo já adicionado em outro fragmento do mesmo modelo.

   Por exemplo, um campo **Texto de linha única** chamado de `Country` no modelo de fragmento de conteúdo não pode ter o valor `Japan` em dois fragmentos de conteúdo dependentes. Um aviso será emitido na tentativa da segunda instância.

   >[!NOTE]
   >
   >A exclusividade é assegurada por raiz de idioma.

   >[!NOTE]
   >
   >As variações podem ter o mesmo valor *exclusivo* como variações do mesmo fragmento, mas não o mesmo valor usado em qualquer variação de outros fragmentos.

* Consulte **[Referência de conteúdo](#content-reference)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

* Consulte **[Referência de fragmento (fragmentos aninhados)](#fragment-reference-nested-fragments)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

<!--
* **Translatable**
  Checking the **Translatable** checkbox on a field in the Content Fragment Model editor will:

  * Ensure the field's property name is added to the translation configuration, context `/content/dam/<sites-configuration>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.
-->

## Validação {#validation}

Vários tipos de dados agora incluem a possibilidade de definir requisitos de validação para quando o conteúdo é inserido no fragmento resultante:

* **Texto em linha única**
   * Comparar com uma expressão regular predefinida.
* **Número**
   * Verificar valores específicos.
* **Referência de conteúdo**
   * Testar tipos específicos de conteúdo.
   * Somente ativos de tamanho de arquivo especificado ou menores podem ser referenciados.
   * Somente imagens dentro de um intervalo predefinido de largura e/ou altura (em pixels) podem ser referenciadas.
* **Referência do fragmento**
   * Testar um modelo de fragmento de conteúdo específico.

## Usar referências para formar conteúdo aninhado {#using-references-to-form-nested-content}

Os fragmentos de conteúdo podem formar conteúdo aninhado, usando um dos seguintes tipos de dados:

* **[Referência de conteúdo](#content-reference)**
   * Fornece uma referência simples a outro conteúdo, de qualquer tipo.
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

* **[Referência de fragmento](#fragment-reference-nested-fragments)** (fragmentos aninhados)
   * Faz referência a outros fragmentos, dependendo dos modelos especificados.
   * Permite incluir/recuperar dados estruturados.

      >[!NOTE]
      >
      >Este método é especialmente interessante quando utilizado em conjunto com a [Entrega de conteúdo headless usando fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

>[!NOTE]
>
>O AEM tem proteção de recorrência para:
>
>* Referências do conteúdo
   >  Isso impede que o usuário adicione uma referência ao fragmento atual. Isso pode resultar em uma caixa de diálogo vazia do seletor de referência de fragmento.
>
>* Referências de fragmento no GraphQL
   >  Se você criar uma consulta profunda que retorna vários fragmentos de conteúdo referenciados uns pelos outros, ele retornará um valor nulo na primeira ocorrência.


### Referência de conteúdo {#content-reference}

A referência de conteúdo permite renderizar o conteúdo de outra fonte; por exemplo, imagem ou fragmento de conteúdo.

Além das propriedades padrão, é possível especificar:

* O **Caminho raiz** para qualquer conteúdo referenciado
* Os tipos de conteúdo que podem ser referenciados
* Limitações para tamanhos de arquivo
* Se uma imagem for referenciada:
   * Mostrar miniatura
   * Restrições de altura e largura da imagem

![Referência de conteúdo](assets/cfm-content-reference.png)

### Referência de fragmento (fragmentos aninhados) {#fragment-reference-nested-fragments}

A referência do fragmento faz referência a um ou mais fragmentos de conteúdo. Esse recurso é especialmente interessante ao recuperar conteúdo para uso no aplicativo, pois permite recuperar dados estruturados com várias camadas.

Por exemplo:

* Um modelo que define os detalhes de um funcionário. Isso inclui:
   * Uma referência ao modelo que define o empregador (empresa)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>Isso é especialmente interessante em conjunto com a [Entrega de conteúdo headless usando fragmentos de conteúdo com o GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Além das propriedades padrão, você pode definir:

* **Renderizar como**:

   * **multifield** — o autor do fragmento pode criar várias referências individuais

   * **fragmentreference** — permite que o autor do fragmento selecione uma única referência a um fragmento

* **Tipo de modelo**
Vários modelos podem ser selecionados. Ao criar o fragmento de conteúdo, qualquer fragmento referenciado deve ter sido criado usando esses modelos.

* **Caminho raiz**
Especifica um caminho raiz para qualquer fragmento referenciado.

* **Permitir criação de fragmentos**

   Isso permitirá que o autor do fragmento crie um novo fragmento com base no modelo apropriado.

   * **fragmentreferencecomposite** — permite que o autor do fragmento crie uma composição ao selecionar vários fragmentos

   ![Referência do fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>Um mecanismo de proteção contra recorrências está em vigor. Ele proíbe que o usuário selecione o fragmento de conteúdo atual na referência do fragmento. Isso pode resultar em uma caixa de diálogo vazia do seletor de referência de fragmento.
>
>Também há uma proteção de recorrência para referências de fragmento em GraphQL. Se você criar uma consulta profunda em dois fragmentos de conteúdo que fazem referência um ao outro, ela retornará um valor nulo.

## Ativar ou desativar um modelo de fragmento de conteúdo {#enabling-disabling-a-content-fragment-model}

Para ter controle total sobre o uso dos modelos de fragmento de conteúdo, eles têm um status que pode ser definido.

### Ativar um modelo de fragmento de conteúdo {#enabling-a-content-fragment-model}

Depois que um modelo é criado, ele precisa ser ativado para:

* Estar disponível para seleção ao criar um novo fragmento de conteúdo.
* Poder ser referenciado a partir de um modelo de fragmento de conteúdo.
* Estar disponível no GraphQL; assim, o esquema é gerado.

Para ativar um modelo que esteja sinalizado como:

* **Rascunho**: novo (nunca ativado).
* **Desativado**: foi especificamente desativado.

Você usa a opção **Ativar** a partir:

* Da barra de ferramentas superior, quando o modelo necessário estiver selecionado.
* Da ação rápida correspondente (passa o mouse sobre o modelo necessário).

![Ativar um rascunho ou modelo desativado](assets/cfm-status-enable.png)

### Desativar um modelo de fragmento de conteúdo {#disabling-a-content-fragment-model}

Um modelo também pode ser desativado para que:

* O modelo não fique mais disponível como base para a criação de *novos* fragmentos de conteúdo.
* No entanto:
   * O esquema de GraphQL continua sendo gerado e ainda pode ser consultado (para evitar impacto na API JSON).
   * Quaisquer fragmentos de conteúdo baseados no modelo ainda podem ser consultados e retornados a partir do ponto de acesso do GraphQL.
* O modelo não pode mais ser referenciado, mas as referências existentes são mantidas e ainda podem ser consultadas e retornadas a partir do ponto de acesso do GraphQL.

Para desativar um Modelo que esteja sinalizado como **Ativado**, você usa a opção **Desativar**:

* Da barra de ferramentas superior, quando o modelo necessário estiver selecionado.
* Da ação rápida correspondente (passa o mouse sobre o modelo necessário).

![Desativar um modelo ativado](assets/cfm-status-disable.png)

## Permitir modelos de fragmentos de conteúdo na pasta de ativos {#allowing-content-fragment-models-assets-folder}

Para implementar a governança de conteúdo, você pode configurar **Políticas** na pasta de ativos para controlar quais modelos de fragmento de conteúdo são permitidos na criação de fragmentos dessa pasta.

>[!NOTE]
>
>O mecanismo é semelhante ao de [permitir modelos de página](/help/sites-authoring/templates.md#allowing-a-template-author) para uma página e suas derivadas nas suas propriedades avançadas.

Para configurar as **políticas** para **modelos de fragmento de conteúdo permitidos**:

1. Navegue e abra as **Propriedades** da pasta de ativos necessária.

1. Abra a guia **Políticas**, onde é possível configurar:

   * **Herdado de`<folder>`**

      As políticas são automaticamente herdadas ao criar novas pastas derivadas; a política pode ser reconfigurada (e a herança quebrada) se as subpastas precisarem permitir modelos diferentes da pasta principal.

   * **Modelos de fragmento de conteúdo permitidos por caminho**

      Vários modelos podem ser permitidos.

   * **Modelos de fragmento de conteúdo permitidos por tag**

      Vários modelos podem ser permitidos.
   ![Política do modelo de fragmento de conteúdo](assets/cfm-model-policy-assets-folder.png)

1. **Salve** quaisquer alterações.

Os modelos de fragmento de conteúdo permitidos para uma pasta são resolvidos da seguinte maneira:
* As **políticas** para **modelos de fragmento do conteúdo permitidos**.
* Se estiver vazia, tente determinar a política usando as regras de herança.
* Se a cadeia de herança não fornecer um resultado, verifique a configuração de **Cloud Services** dessa pasta (diretamente e, em seguida, por herança).
* Se nenhuma das opções acima fornecer resultados, então não há modelos permitidos para essa pasta.

## Exclusão de um modelo de fragmento de conteúdo {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>A exclusão de um modelo de fragmento de conteúdo pode afetar fragmentos dependentes.

Para excluir um modelo de fragmento de conteúdo:

1. Navegar para **Ferramentas**, **Ativos**, depois abra **Modelos de fragmentos do conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione seu modelo e, em seguida, **Excluir** na barra de ferramentas.

   >[!NOTE]
   >
   >Se o modelo for referenciado, um aviso será exibido. Tome as medidas apropriadas.

## Publicação de um modelo de fragmento de conteúdo {#publishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo precisam ser publicados quando/antes de qualquer fragmento de conteúdo dependente ser publicado.

Para publicar um modelo de fragmento de conteúdo:

1. Navegar para **Ferramentas**, **Ativos**, depois abra **Modelos de fragmentos do conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione seu modelo e, em seguida, **Publicar** na barra de ferramentas.
O status publicado será exibido no console.

   >[!NOTE]
   >
   >Se você publicar um fragmento de conteúdo cujo modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado junto com o fragmento.

## Desfazer a publicação de um modelo de fragmento de conteúdo {#unpublishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo podem ter sua publicação desfeita se não forem referenciados por nenhum fragmento.

Para desfazer a publicação de um modelo de fragmento de conteúdo:

1. Navegar para **Ferramentas**, **Ativos**, depois abra **Modelos de fragmentos do conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione seu modelo e, em seguida, **Desfazer publicação** na barra de ferramentas.
O status publicado será exibido no console.

## Modelo do fragmento de conteúdo — Propriedades {#content-fragment-model-properties}

É possível editar as **Propriedades** de um modelo do fragmento de conteúdo:

* **Básico**
   * **Título do modelo**
   * **Tags**
   * **Descrição**
   * **Fazer upload de imagem**
