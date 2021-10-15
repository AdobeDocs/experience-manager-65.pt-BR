---
title: Modelos de fragmentos do conteúdo
description: Saiba como os Modelos de fragmentos de conteúdo servem como base para seu conteúdo headless no AEM e como criar Fragmentos de conteúdo com conteúdo estruturado.
feature: Content Fragments
role: User
exl-id: 6fd1fdb2-d1d3-4f97-b119-ecfddcccec9e
source-git-commit: 924b30680b189ec5061eb0bd664165793a9dbd9c
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 7%

---

# Modelos de fragmentos do conteúdo {#content-fragment-models}

Os Modelos de fragmento de conteúdo no AEM definem a estrutura do conteúdo dos [fragmentos de conteúdo,](/help/assets/content-fragments/content-fragments.md) servindo como base do conteúdo sem cabeçalho.

Para usar os Modelos de fragmento do conteúdo, você pode:

1. [Ativar a funcionalidade do Modelo de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Crie](#creating-a-content-fragment-model) e  [configure](#defining-your-content-fragment-model) os Modelos de fragmento de conteúdo
1. [Ativar os ](#enabling-disabling-a-content-fragment-model) Modelos de fragmento de conteúdo para usar ao criar Fragmentos de conteúdo para usar na criação de Fragmentos de conteúdo
1. [Permita os Modelos de fragmento de conteúdo nas ](#allowing-content-fragment-models-assets-folder) pastas de Ativos necessárias, configurando as  **Políticas**.

## Criação de um modelo de fragmento de conteúdo {#creating-a-content-fragment-model}

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.
1. Navegue até a pasta apropriada para sua [configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Use **Criar** para abrir o assistente.

   >[!CAUTION]
   >
   >Se o [uso de modelos de fragmento de conteúdo não tiver sido ativado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

1. Especifique o **título do modelo**. Você também pode adicionar **Tags**, um **Descrição**, e selecionar **Ativar modelo** para [ativar o modelo](#enabling-disabling-a-content-fragment-model), se necessário.

   ![título e descrição](assets/cfm-models-02.png)

1. Use **Create** para salvar o modelo vazio. Uma mensagem indicará o sucesso da ação, você poderá selecionar **Abrir** para editar imediatamente o modelo ou **Concluído** para retornar ao console.

## Definição do modelo de fragmento de conteúdo {#defining-your-content-fragment-model}

O modelo de fragmento de conteúdo define efetivamente a estrutura dos fragmentos de conteúdo resultantes usando uma seleção de **[Tipos de dados](#data-types)**. Usando o editor de modelo, você pode adicionar instâncias dos tipos de dados e configurá-las para criar os campos necessários:

>[!CAUTION]
>
>A edição de um modelo de fragmento de conteúdo existente pode afetar fragmentos dependentes.

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.

1. Abra o modelo necessário para **Editar**; use a ação rápida ou selecione o modelo e depois a ação na barra de ferramentas.

   Uma vez aberto, o editor de modelo mostra:

   * esquerda: campos já definidos
   * direito: **Tipos de dados** disponíveis para criar campos (e **Propriedades** para uso depois que os campos forem criados)

   >[!NOTE]
   >
   >Quando um campo é **Obrigatório**, o **Rótulo** indicado no painel à esquerda é marcado com um asterisco (*****).

   ![propriedades](assets/cfm-models-03.png)

1. **Para adicionar um campo**

   * Arraste um tipo de dados necessário para o local necessário para um campo:

      ![tipo de dados para campo](assets/cfm-models-04.png)

   * Depois que um campo é adicionado ao modelo, o painel direito mostrará as **Propriedades** que podem ser definidas para esse tipo de dados específico. Aqui, é possível definir o que é necessário para esse campo.

      * Muitas propriedades são autoexplicativas, para obter detalhes adicionais, consulte [Propriedades](#properties).
      * A digitação de um **Rótulo do campo** preencherá automaticamente o **Nome da propriedade** - se estiver vazio, e poderá ser atualizado manualmente posteriormente.

         >[!CAUTION]
         Ao atualizar manualmente um tipo de dados **Nome da propriedade**, observe que os nomes devem conter somente caracteres latinos, dígitos numéricos e sublinhado &quot;_&quot; como caractere especial.
         Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.
      Por exemplo:

      ![propriedades de campo](assets/cfm-models-05.png)


1. **Para remover um campo**

   Selecione o campo desejado e clique/toque no ícone da lixeira. Você receberá uma solicitação para confirmar a ação.

   ![remover](assets/cfm-models-06.png)

1. Adicione todos os campos obrigatórios e defina as propriedades relacionadas, conforme necessário. Por exemplo:

   ![save](assets/cfm-models-07.png)

1. Selecione **Save** para manter a definição.

## Tipos de dados {#data-types}

Uma seleção de tipos de dados está disponível para definir seu modelo:

* **Texto em linha única**
   * Adicione um ou mais campos de uma única linha de texto; o comprimento máximo pode ser definido
* **Texto multilinha**
   * Uma área de texto que pode ser Rich Text, Plain Text ou Markdown
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
   * Referências a outros conteúdos, de qualquer tipo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * Se uma imagem for referenciada, você pode optar por mostrar uma miniatura
* **Referência do fragmento**
   * Faz referência a outros fragmentos de conteúdo; pode ser usado para [criar conteúdo aninhado](#using-references-to-form-nested-content)
   * O tipo de dados pode ser configurado para permitir que os autores de fragmento:
      * Edite o fragmento referenciado diretamente.
      * Crie um novo fragmento de conteúdo, com base no modelo apropriado
* **Objeto JSON**
   * Permite que o autor do fragmento de conteúdo insira a sintaxe JSON nos elementos correspondentes de um fragmento.
      * Para permitir que AEM armazene JSON direto que você tenha copiado/colado de outro serviço.
      * O JSON será transmitido e emitido como JSON no GraphQL.
      * Inclui o realce da sintaxe JSON, o preenchimento automático e o realce de erros no editor de fragmentos de conteúdo.
* **Espaço reservado da guia**
   * Permite a introdução de guias para uso ao editar o conteúdo do Fragmento de conteúdo.
Isso será mostrado como um divisor no editor de modelo, separando seções da lista de tipos de dados de conteúdo. Cada instância representa o início de uma nova guia.
No editor de fragmentos, cada instância aparecerá como uma guia.

      >[!NOTE]
      Esse tipo de dados é usado apenas para formatação e é ignorado pelo esquema GraphQL AEM.

## Propriedades {#properties}

Muitas propriedades são autoexplicativas, para certas propriedades os detalhes adicionais são os seguintes:

>[!CAUTION]
Ao atualizar manualmente o **Nome da propriedade**, observe que os nomes devem conter somente caracteres latinos, dígitos numéricos e sublinhado &quot;_&quot; como caractere especial.
Se os modelos criados em versões anteriores do AEM contiverem caracteres ilegais, remova ou atualize esses caracteres.

* **Renderizar**
comoAs várias opções para realizar/renderizar o campo em um fragmento. Geralmente, isso permite definir se o autor verá uma única instância do campo ou poderá criar várias instâncias.

* **Rótulo**
do campoInserir um 
**O** Rótulo do campo gerará automaticamente um Nome  **de propriedade**, que pode ser atualizado manualmente se necessário.

* ****
A validação ValidationBasic está disponível por mecanismos como a propriedade  **** Required . Alguns tipos de dados têm campos de validação de adição. Consulte [Validação](#validation) para obter mais detalhes.

* No tipo de dados **Texto de várias linhas**, é possível definir o **Tipo padrão** como:

   * **Texto formatado**
   * **Markdown**
   * **Texto sem formatação**

   Se não especificado, o valor padrão **Rich Text** é usado para este campo.

   Alterar o **Tipo padrão** em um modelo de fragmento de conteúdo só terá efeito em um fragmento de conteúdo existente relacionado depois que esse fragmento for aberto no editor e salvo.

* ****
UniqueContent (para o campo específico) deve ser exclusivo em todos os fragmentos de conteúdo criados a partir do modelo atual.

   Isso é usado para garantir que os autores de conteúdo não possam repetir o conteúdo já adicionado em outro fragmento do mesmo modelo.

   Por exemplo, um campo **Texto de linha única** chamado `Country` no Modelo de fragmento de conteúdo não pode ter o valor `Japan` em dois Fragmentos de conteúdo dependentes. Um aviso será emitido quando a segunda instância for tentada.

   >[!NOTE]
   A exclusividade é assegurada por raiz de idioma.

   >[!NOTE]
   As variações podem ter o mesmo valor *exclusivo* que as variações do mesmo fragmento, mas não o mesmo valor que é usado em qualquer variação de outros fragmentos.

* Consulte **[Referência de conteúdo](#content-reference)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

* Consulte **[Referência do fragmento (Fragmentos aninhados)](#fragment-reference-nested-fragments)** para obter mais detalhes sobre esse tipo de dados específico e suas propriedades.

<!--
* **Translatable**
  Checking the **Translatable** checkbox on a field in the Content Fragment Model editor will:

  * Ensure the field's property name is added to the translation configuration, context `/content/dam/<sites-configuration>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.
-->

## Validação {#validation}

Vários tipos de dados agora incluem a possibilidade de definir requisitos de validação para quando o conteúdo é inserido no fragmento resultante:

* **Texto em linha única**
   * Compare com um regex predefinido.
* **Número**
   * Verifique valores específicos.
* **Referência de conteúdo**
   * Teste tipos específicos de conteúdo.
   * Somente ativos de tamanho de arquivo especificado ou menor podem ser referenciados.
   * Somente imagens dentro de um intervalo predefinido de largura e/ou altura (em pixels) podem ser referenciadas.
* **Referência do fragmento**
   * Teste um modelo de fragmento de conteúdo específico.

## Usar referências para formar conteúdo aninhado {#using-references-to-form-nested-content}

Os Fragmentos de conteúdo podem formar conteúdo aninhado, usando um dos seguintes tipos de dados:

* **[Referência de conteúdo](#content-reference)**
   * Fornece uma referência simples a outro conteúdo; de qualquer tipo.
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

* **[Referência de fragmento](#fragment-reference-nested-fragments)**  (fragmentos aninhados)
   * Faz referência a outros fragmentos, dependendo dos modelos específicos especificados.
   * Permite incluir/recuperar dados estruturados.

      >[!NOTE]
      Esse método é de especial interesse em conjunto com [Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Pode ser configurado para uma ou várias referências (no fragmento resultante).

>[!NOTE]
AEM tem proteção de recorrência para:
* Referências de conteúdo
Isso impede que o usuário adicione uma referência ao fragmento atual. Isso pode levar a uma caixa de diálogo vazia do seletor de referência de fragmento.
* Referências de fragmento em GraphQL
Se você criar uma consulta profunda que retorna vários Fragmentos de conteúdo referenciados um pelo outro, ela retornará um valor nulo na primeira ocorrência.


### Referência de conteúdo {#content-reference}

A Referência de conteúdo permite renderizar o conteúdo de outra fonte; por exemplo, imagem ou fragmento de conteúdo.

Além das propriedades padrão, você pode especificar:

* O **Caminho Raiz** para qualquer conteúdo referenciado
* Os tipos de conteúdo que podem ser referenciados
* Limitações para tamanhos de arquivo
* Se uma imagem for referenciada:
   * Mostrar miniatura
   * Sistemas de retenção de imagens em altura e largura

![Referência de conteúdo](assets/cfm-content-reference.png)

### Referência de fragmento (Fragmentos aninhados) {#fragment-reference-nested-fragments}

A Referência do fragmento faz referência a um ou mais fragmentos de conteúdo. Esse recurso de especial interesse ao recuperar conteúdo para uso no aplicativo, pois permite recuperar dados estruturados com várias camadas.

Por exemplo:

* Um modelo que define os detalhes de um funcionário; estes incluem:
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
Isso é de especial interesse em conjunto com [Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Além das propriedades padrão, você pode definir:

* **Renderizar como**:

   * **multicampo**  - o autor do fragmento pode criar várias referências, individuais

   * **referência de fragmento**  - permite que o autor do fragmento selecione uma única referência a um fragmento

* **Modelo**
TipoVários modelos podem ser selecionados. Ao criar o Fragmento de conteúdo, qualquer fragmento referenciado deve ter sido criado usando esses modelos.

* **Caminho raizEspecifica um caminho raiz para qualquer fragmento referenciado.**


* **Permitir criação de fragmentos**

   Isso permitirá que o autor do fragmento crie um novo fragmento com base no modelo apropriado.

   * **fragmentreferencecomposite**  - permite que o autor do fragmento crie um composto, selecionando vários fragmentos

   ![Referência do fragmento](assets/cfm-fragment-reference.png)

>[!NOTE]
Está em vigor um mecanismo de proteção contra as recorrências. Ela proíbe que o usuário selecione o Fragmento de conteúdo atual na Referência de fragmento. Isso pode levar a uma caixa de diálogo vazia do seletor de referência de fragmento.
Também há uma proteção de recorrência para Referências de fragmento em GraphQL. Se você criar uma consulta profunda em dois Fragmentos de conteúdo que fazem referência um ao outro, ela retornará um valor nulo.

## Ativar ou desativar um modelo de fragmento de conteúdo {#enabling-disabling-a-content-fragment-model}

Para ter controle total sobre o uso dos Modelos de fragmento de conteúdo, eles têm um status que pode ser definido.

### Ativar um modelo de fragmento de conteúdo {#enabling-a-content-fragment-model}

Depois que um modelo é criado, ele precisa ser ativado para que ele:

* Está disponível para seleção ao criar um novo Fragmento do conteúdo.
* Pode ser referenciado a partir de um Modelo de fragmento de conteúdo.
* Está disponível para GraphQL; assim, o schema é gerado.

Para ativar um Modelo que esteja sinalizado como:

* **Rascunho** : mw (nunca habilitado).
* **Desativado** : foi especificamente desativado.

Use a opção **Ativar** de:

* A barra de ferramentas superior, quando o Modelo necessário estiver selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Ativar um modelo de rascunho ou desativado](assets/cfm-status-enable.png)

### Desabilitação de um modelo de fragmento de conteúdo {#disabling-a-content-fragment-model}

Um modelo também pode ser desativado para que:

* O modelo não está mais disponível como base para criar *novo* Fragmentos de conteúdo.
* No entanto:
   * O esquema GraphQL continua sendo gerado e ainda pode ser consultado (para evitar impacto na API JSON).
   * Todos os Fragmentos de conteúdo baseados no modelo ainda podem ser consultados e retornados do ponto de extremidade GraphQL.
* O modelo não pode mais ser referenciado, mas as referências existentes são mantidas intocadas e ainda podem ser consultadas e retornadas do ponto de extremidade GraphQL.

Para desativar um Modelo que esteja sinalizado como **Ativado**, use a opção **Desativar** de:

* A barra de ferramentas superior, quando o Modelo necessário estiver selecionado.
* A Ação rápida correspondente (passe o mouse sobre o Modelo necessário).

![Desativar um modelo habilitado](assets/cfm-status-disable.png)

## Permitir modelos de fragmentos de conteúdo na pasta Ativos {#allowing-content-fragment-models-assets-folder}

Para implementar a governança de conteúdo, você pode configurar **Policies** na pasta Assets para controlar quais Modelos de fragmento de conteúdo são permitidos para a criação de Fragmento nessa pasta.

>[!NOTE]
O mecanismo é semelhante a [permitir modelos de página](/help/sites-authoring/templates.md#allowing-a-template-author) para uma página e seus filhos, nas propriedades avançadas de uma página.

Para configurar as **Políticas** para **Modelos permitidos de Fragmento de Conteúdo**:

1. Navegue e abra **Propriedades** para a pasta Ativos necessária.

1. Abra a guia **Policies** , onde você pode configurar:

   * **Herdado de`<folder>`**

      As políticas são automaticamente herdadas ao criar novas pastas secundárias; a política pode ser reconfigurada (e a herança quebrada) se as subpastas precisarem permitir modelos diferentes da pasta pai.

   * **Modelos de fragmento de conteúdo permitidos por caminho**

      Vários modelos podem ser permitidos.

   * **Modelos de fragmento de conteúdo permitidos por tag**

      Vários modelos podem ser permitidos.
   ![Política do modelo de fragmento de conteúdo](assets/cfm-model-policy-assets-folder.png)

1. **** Salve as alterações.

Os Modelos de fragmento de conteúdo permitidos para uma pasta são resolvidos da seguinte maneira:
* O **Policies** para **Modelos de fragmento de conteúdo permitidos**.
* Se estiver vazio, tente determinar a política usando as regras de herança.
* Se a cadeia de herança não fornecer um resultado, verifique a configuração **Cloud Services** dessa pasta (também primeiro diretamente e, em seguida, por herança).
* Se nenhuma das opções acima fornecer resultados, então não há modelos permitidos para essa pasta.

## Exclusão de um modelo de fragmento de conteúdo {#deleting-a-content-fragment-model}

>[!CAUTION]
A exclusão de um modelo de fragmento de conteúdo pode afetar fragmentos dependentes.

Para excluir um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione o modelo, seguido por **Delete** na barra de ferramentas.

   >[!NOTE]
   Se o modelo for referenciado, um aviso será dado. Agir adequadamente.

## Publicação de um modelo de fragmento de conteúdo {#publishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo precisam ser publicados quando/antes de qualquer fragmento de conteúdo dependente ser publicado.

Para publicar um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione o modelo, seguido por **Publish** na barra de ferramentas.
O status publicado será indicado no console.

   >[!NOTE]
   Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

## Desfazer a publicação de um modelo de fragmento de conteúdo {#unpublishing-a-content-fragment-model}

Os modelos de fragmento de conteúdo podem ter a publicação cancelada se não estiverem referenciados por nenhum fragmento.

Para cancelar a publicação de um modelo de fragmento de conteúdo:

1. Navegue até **Ferramentas**, **Ativos** e abra **Modelos de fragmento de conteúdo**.

1. Navegue até a pasta que contém o modelo de fragmento de conteúdo.
1. Selecione o modelo, seguido por **Cancelar publicação** na barra de ferramentas.
O status publicado será indicado no console.

## Modelo de fragmento de conteúdo - Propriedades {#content-fragment-model-properties}

Você pode editar as **Propriedades** de um Modelo de fragmento de conteúdo:

* **Básico**
   * **Título do modelo**
   * **Tags**
   * **Descrição**
   * **Carregar imagem**
