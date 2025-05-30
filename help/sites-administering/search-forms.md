---
title: Configuração de formulários de pesquisa
description: Saiba como usar o Search Forms para personalizar a seleção de predicados de pesquisa usados nos painéis de pesquisa disponíveis nos consoles AEM e painéis do ambiente de criação.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 7%

---


# Configuração de formulários de pesquisa{#configuring-search-forms}

Use a **Forms de Pesquisa** para personalizar a seleção de predicados de pesquisa usados nos painéis de pesquisa disponíveis em vários consoles AEM e/ou painéis do ambiente de criação. A personalização desses painéis torna a funcionalidade de pesquisa versátil, de acordo com suas necessidades específicas.

Um [intervalo do predicado](#predicates-and-their-settings)s está disponível e pronto para uso. Você pode adicionar vários predicados, incluindo (entre outros) o predicado Propriedade, para pesquisar ativos que correspondam a uma única propriedade especificada por você. Ou, no predicado Opções, para pesquisar ativos que correspondem a um ou mais valores especificados para uma propriedade específica.

Você pode [configurar os formulários de pesquisa](#configuring-your-search-forms) usados em vários consoles e no navegador de ativos (ao editar páginas). As [caixas de diálogo para configurar estes formulários](#configuring-your-search-forms) podem ser acessadas via:

* **Ferramentas**

   * **Geral**

      * **Pesquisar Forms**

Ao acessar esse console pela primeira vez, você pode ver que todas as configurações têm um símbolo de cadeado. Isso indica que a configuração apropriada é a configuração padrão (pronta para uso) e não pode ser excluída. Após personalizar a configuração, o bloqueio desaparecerá, a menos que você [exclua sua configuração personalizada](#deleting-a-configuration-to-reinstate-the-default). Nesse caso, o padrão (e o indicador de cadeado) é restabelecido.

![Janela de formulários de pesquisa](assets/chlimage_1-374.png)

## Configurações {#configurations}

As configurações padrão disponíveis são:

* **Editor de páginas (Pesquisa de documentos):**

  Essa configuração define as opções disponíveis ao pesquisar por um documento no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de imagens):**

  Essa configuração define as opções disponíveis ao pesquisar imagens no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de manuscrito):**

  Essa configuração define as opções disponíveis ao pesquisar manuscritos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de páginas):**

  Essa configuração define as opções disponíveis ao pesquisar páginas no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de parágrafos):**

  Essa configuração define as opções disponíveis ao pesquisar parágrafos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de produto):**

  Essa configuração define as opções disponíveis ao pesquisar produtos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Dynamic Media Classic [pesquisa anterior do Scene7])**:

  Essa configuração define as opções disponíveis ao pesquisar recursos do Scene7 no navegador de ativos (ao editar uma página).

* **Painel de Pesquisa do Administrador de Sites**:

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao usar o painel de pesquisa do console Sites.

* **Editor de páginas (Pesquisa de vídeos):**

  Essa configuração define as opções disponíveis ao pesquisar vídeos no navegador de ativos (ao editar uma página).

* **Painel de Pesquisa do Administrador do Assets:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao usar o console Assets.

* **Painel de Pesquisa do Administrador de Catálogos:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar um catálogo de comércio.

* **Painel de Pesquisa do Administrador de Pedidos:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar pedidos de comércio.

* **Painel de Pesquisa do Administrador de Coleções de Produtos:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar coleções de produtos comerciais.

* **Painel de Pesquisa do Administrador de Produtos:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar produtos comerciais.

* **Painel de Pesquisa do Administrador de Projetos:**

  Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar projetos.

## Predicados e suas configurações {#predicates-and-their-settings}

### Predicados {#predicates}

Os seguintes predicados estão disponíveis, dependendo da configuração:

<table>
 <tbody>
  <tr>
   <th>Predicado</th>
   <th>Propósito</th>
   <th>Configurações</th>
  </tr>
  <tr>
   <td>Analytics </td>
   <td>Pesquise/filtre recursos no navegador do Sites ao mostrar dados alimentados por análise. Os filtros de pesquisa do Analytics são carregados para corresponder às colunas de análise personalizadas mapeadas.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Última modificação do ativo </td>
   <td>Data em que o ativo foi modificado pela última vez.<br /> </td>
   <td>Um predicado personalizado, com base no Predicado de data.</td>
  </tr>
  <tr>
   <td>Componentes </td>
   <td>Permite que um autor pesquise/filtre por páginas com um componente específico. Por exemplo, uma galeria de imagens.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Profundidade da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data </td>
   <td>Pesquisa deslizante de ativos com base em uma propriedade de data.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de datas </td>
   <td>Pesquise ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, você pode especificar datas de início e término.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Texto do intervalo (de)*</li>
     <li>Texto do intervalo (até)*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da expiração </td>
   <td>Pesquisar ativos com base no status de expiração.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamanho do arquivo </td>
   <td>Pesquise ativos com base em seu tamanho.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro oculto</td>
   <td>Um filtro na propriedade e no valor, não visível para o usuário.</td>
   <td>
    <ul>
     <li>Nome de propriedade</li>
     <li>Valor de propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opções </td>
   <td><p>As opções são nós de conteúdo criados pelo usuário.</p> <p>Consulte <a href="#addinganoptionspredicate">Adicionando um Predicado de Opções</a> para obter mais informações.</p> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Caminho JSON</li>
     <li>Nome da propriedade*</li>
     <li>Seleção única</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriedade de opções </td>
   <td>Pesquise em uma propriedade da opção.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho do nó de opções<br /> </li>
     <li>Seleção única</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da página </td>
   <td>Pesquisar páginas de acordo com seu status.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade de publicação</li>
     <li>Nome de propriedade do LiveCopy</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Caminho </td>
   <td>Pesquise ativos localizados em um caminho específico.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Adicionar caminho de pesquisa</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriedade </td>
   <td>Pesquisar em uma propriedade especificada.</td>
   <td>nenhum</td>
  </tr>
  <tr>
   <td>Publicar status </td>
   <td>Pesquisar ativos com base no status de publicação</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo </td>
   <td>Pesquisar recursos que estão dentro de um intervalo especificado. No painel Pesquisar, é possível especificar valores mínimos e máximos para o intervalo.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome de propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opções de intervalo </td>
   <td>Um predicado de pesquisa específico para o Assets e o mesmo que o Predicado de controle deslizante comum. O ainda está disponível devido a problemas de compatibilidade com versões anteriores.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Avaliação </td>
   <td>Pesquise ativos de acordo com sua classificação.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data relativa </td>
   <td>Pesquisar ativos com base na data relativa de sua criação<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Data relativa</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo do controle deslizante </td>
   <td>Um predicado de pesquisa comum que estende o predicado de intervalo com o recurso de controle deslizante. O valor da propriedade pesquisada deve estar entre os limites do controle deslizante.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Pesquise ativos com base em tags. Você pode configurar a propriedade Caminho para preencher várias tags na lista Tags.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tags </td>
   <td>Pesquisar com base em tags.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Os predicados de pesquisa comuns são definidos em:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* Os predicados de pesquisa relacionados somente ao siteadmin (interface clássica) estão localizados em:
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * Eles estão obsoletos e só estão disponíveis para compatibilidade com versões anteriores.
>
>Essas informações são somente para referência. Não alterar `/libs`.

### Configurações de predicado {#predicate-settings}

Dependendo do predicado, uma seleção de configurações está disponível para configuração:

* **Rótulo do campo**

  O rótulo que aparece como o cabeçalho recolhível ou como o rótulo do campo do predicado.

* **Descrição**

  Detalhes descritivos do usuário.

* **Espaço reservado**

  Texto vazio ou o marcador de posição do predicado, caso nenhum texto de filtragem seja inserido.

* **Nome da Propriedade**

  A propriedade a ser pesquisada. Ele usa um caminho relativo e os curingas `*/*/*` especificam a profundidade da propriedade em relação ao nó `jcr:content` (cada asterisco representa um nível de nó).

  Se você deseja pesquisar apenas em um nó filho de primeiro nível do recurso que tem a propriedade `x` no nó `jcr:content`, use `*/jcr:content/x`

* **Profundidade da propriedade**

  A profundidade máxima para pesquisar essa propriedade nos recursos. Assim, uma pesquisa nessa propriedade pode ser executada em um recurso e em filhos recursivos até que o nível dos filhos seja igual à profundidade especificada.

* **Valor da propriedade**

  O valor da propriedade como uma cadeia absoluta ou linguagem de expressão; por exemplo, `cq:Page` ou

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto do Intervalo**

  O rótulo do campo de intervalo no predicado **Intervalo de datas**.

* **Caminho da opção**

  O usuário pode selecionar o caminho usando o Navegador de caminho na guia de configuração do predicado. Após selecionar **+**, o ícone é usado para adicionar a seleção à lista de opções válidas (em seguida, o ícone **-** a ser removido, se necessário).

  As opções são nós de conteúdo criados pelo usuário, com a seguinte estrutura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Caminho do nó de opções**
Efetivamente igual ao **Caminho de opções**, somente isso está no campo de predicado comum, o outro é específico para ativos.

* **Seleção única**
Se marcadas, as opções são renderizadas como caixas de seleção que permitem apenas uma única seleção. Se for marcada por engano, uma caixa de seleção pode ser desmarcada.

* **Nomes de propriedades do Publish e da Live Copy**
Os rótulos das caixas de seleção Publicar e Live Copy para o predicado específico do Sites.

* O &ast; nos rótulos de campo na guia **Configurações** significa que os campos são obrigatórios e, se deixado em branco, uma mensagem de erro será exibida.

## Configuração do Forms de pesquisa {#configuring-your-search-forms}

### Criação/abertura de uma configuração personalizada {#creating-opening-a-customized-configuration}

1. Navegue até **Ferramentas** >> **Geral** >> **Pesquisar Forms**.

1. Selecione a configuração que deseja personalizar.
1. Use o ícone **Editar** para abrir a configuração para atualização.
1. Se for feita uma nova personalização, você provavelmente vai [adicionar novos campos de predicado e definir as configurações](#add-edit-a-predicate-field-and-define-field-settings) conforme necessário. Se houver uma personalização, você poderá selecionar um campo existente e [atualizar as configurações](#add-edit-a-predicate-field-and-define-field-settings).
1. Selecione **Concluído** para salvar a configuração.

   >[!NOTE]
   >
   >As configurações personalizadas são armazenadas (conforme apropriado) em:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Adicionar/editar um campo de predicado e definir configurações de campo {#add-edit-a-predicate-field-and-define-field-settings}

É possível adicionar ou editar campos e definir/atualizar suas configurações:

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Se quiser adicionar um campo, abra a guia **Selecionar predicado** e arraste o predicado necessário para o local desejado. Por exemplo, o **Predicado do intervalo de datas**:

   ![Editando um formulário de pesquisa](assets/chlimage_1-375.png)

1. Dependendo se:

   * Você está adicionando um campo:

     Depois de adicionar o predicado, a guia **Configurações** é aberta e mostra as propriedades que podem ser definidas.

   * Você deseja atualizar um predicado existente:

     Selecione o campo de predicado (à direita) e abra a guia **Configurações**.

   Por exemplo, as configurações para o **Predicado do intervalo de datas**:

   ![Propriedades do Predicado do Intervalo de Datas](assets/chlimage_1-376.png)

1. Faça as alterações necessárias e confirme com **Concluído**.

### Pré-visualização da configuração de pesquisa {#previewing-the-search-configuration}

1. Selecione o ícone Visualizar:

   ![Visualizar formulários de pesquisa](do-not-localize/chlimage_1-31.png)

1. Isso exibe os formulários de pesquisa conforme são mostrados (totalmente expandidos) na coluna Pesquisa do console apropriado.

   ![Visualizando o formulário de pesquisa](assets/chlimage_1-377.png)

1. **Feche** a visualização para que você possa retornar e concluir a configuração.

### Exclusão de um campo de predicado {#deleting-a-predicate-field}

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Selecione o campo de predicado (à direita), abra a guia **Configurações** e selecione o ícone **Excluir** (canto inferior esquerdo).

   ![Ícone Excluir](do-not-localize/chlimage_1-32.png)

1. Uma caixa de diálogo solicita a confirmação da ação de exclusão.

1. Confirme esta e todas as outras alterações com **Concluído**.

### Excluir uma configuração (para restaurar o padrão) {#deleting-a-configuration-to-reinstate-the-default}

Depois de personalizar uma configuração, isso substituirá os padrões. Você pode restaurar a configuração padrão excluindo sua configuração personalizada.

>[!NOTE]
>
>Não é possível excluir nenhuma das configurações padrão.

A exclusão de uma configuração personalizada é feita no console:

1. Selecione a configuração necessária (por exemplo, **Editor de páginas (pesquisa de parágrafos)**) e o ícone **Excluir** na barra de ferramentas:

   ![Excluindo um formulário](assets/chlimage_1-378.png)

1. A configuração personalizada é excluída e o padrão é restabelecido (isso é indicado pela reaparição do símbolo de cadeado no console).

### Adição de predicados de opções {#adding-options-predicates}

Os predicados de opção (Opções, Propriedade de opções) permitem configurar um item a ser pesquisado. Eles são usados para pesquisar algo diretamente na página; por exemplo, uma propriedade no nó da página.

O exemplo a seguir (para pesquisar de acordo com o modelo usado para criar uma página) ilustra as etapas envolvidas:

1. Crie o nó que define a propriedade na qual será pesquisada.

   Você precisa de um nó raiz que contenha definições das opções individuais para estar disponível ao usuário.

   Os nós das opções individuais precisam das propriedades:

   * `jcr:title` - o rótulo de campo a ser exibido no painel de pesquisa
   * `value` - o valor da propriedade a ser pesquisada

   ![Adicionando opções no CRXDE](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >***não*** altere nada no caminho `/libs`.
   >
   >Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >1. Recrie o item necessário, como ele existe em `/libs`, em `/apps`. Nesse caso, de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Fazer alterações em `/apps.`

1. Abra o console **Forms de Pesquisa** e selecione a configuração que deseja atualizar. Por exemplo, **Painel de pesquisa do administrador de sites**.

   Em seguida, clique no ícone **Editar formulários de pesquisa**.

1. Dependendo da configuração, adicione uma **Propriedade de opções** ou **Propriedade de opções** à configuração.
1. Atualize os campos, especialmente:

   * **Nome da Propriedade**

     Específica a propriedade do nó a ser pesquisada nos nós de destino. Por exemplo:

     `jcr:content/cq:template`

   * **Caminho do nó de opção**

     Selecione o caminho para onde as opções são mantidas. Por exemplo:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Adicionando caminho de propriedade](assets/chlimage_1-380.png)

1. Selecione **Concluído** para salvar sua configuração.
1. Navegue até o console apropriado (neste exemplo, **Sites**) e abra o painel **Pesquisar**. Os formulários de pesquisa recém-definidos, juntamente com as várias opções, ficam visíveis. Selecione a opção necessária para ver os resultados da pesquisa:

   ![Os resultados finais](assets/chlimage_1-381.png)

## Permissões de usuário {#user-permissions}

A tabela a seguir lista as permissões necessárias para executar ações de edição, exclusão e visualização em formulários de pesquisa.

<table>
 <tbody>
  <tr>
   <td><strong>Ação</strong></td>
   <td><strong>Permissões</strong></td>
  </tr>
  <tr>
   <td>Editar </td>
   <td>Permissões de Leitura e Gravação no nó <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td>Permissões de Leitura, Gravação e Exclusão no nó <code>/apps</code></td>
  </tr>
  <tr>
   <td>Visualização</td>
   <td>Permissões de leitura, gravação e exclusão no nó <code>/var/dam/content</code>.<br /> permissões de Leitura e Gravação no nó <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
