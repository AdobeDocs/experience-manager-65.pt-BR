---
title: Configuração de formulários de pesquisa
description: Saiba como configurar o Search Forms.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f82391d7-e30d-48d2-8f66-88fcae3dfb5f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 12%

---

# Configuração de formulários de pesquisa{#configuring-search-forms}

Use **Pesquisar Forms** para personalizar a seleção de predicados de pesquisa usados nos painéis de pesquisa disponíveis em vários consoles e/ou painéis de AEM do ambiente do autor. Personalizar esses painéis torna a funcionalidade de pesquisa versátil de acordo com suas necessidades específicas.

A [gama de predicados](#predicates-and-their-settings)s estão disponíveis prontamente. Você pode adicionar vários predicados, incluindo (entre outros) o predicado Propriedade para procurar ativos que correspondam a uma única propriedade especificada por você, ou o predicado Opções para pesquisar ativos que correspondam a um ou mais valores especificados para uma propriedade específica.

Você pode [configurar os formulários de pesquisa](#configuring-your-search-forms) usado em vários consoles e no navegador de ativos (ao editar páginas). O [caixas de diálogo para configurar esses formulários](#configuring-your-search-forms) pode ser acessado via:

* **Ferramentas**

   * **Geral**

      * **Formulários de pesquisa**

Ao acessar esse console pela primeira vez, você pode ver que todas as configurações têm um símbolo de cadeado. Isso indica que a configuração apropriada é a configuração padrão (pronta para uso) e não pode ser excluída. Depois de personalizar a configuração, o bloqueio desaparecerá, a menos que você [excluir sua configuração personalizada](#deleting-a-configuration-to-reinstate-the-default), nesse caso, o padrão (e o indicador de cadeado) será reinstalado.

![chlimage_1-374](assets/chlimage_1-374.png)

## Configurações {#configurations}

As configurações padrão disponíveis são:

* **Editor de páginas (Pesquisa de documentos):**

   Essa configuração define as opções disponíveis ao pesquisar por documento no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de imagens):**

   Essa configuração define as opções disponíveis ao pesquisar por imagens no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de manuscrito):**

   Essa configuração define as opções disponíveis ao pesquisar por manuscritos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de páginas):**

   Essa configuração define as opções disponíveis ao pesquisar por páginas no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de parágrafos):**

   Essa configuração define as opções disponíveis ao pesquisar por parágrafos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Pesquisa de produto):**

   Essa configuração define as opções disponíveis ao procurar produtos no navegador de ativos (ao editar uma página).

* **Editor de páginas (Dynamic Media Classic) [anteriormente Scene7] search)**:

   Essa configuração define as opções disponíveis ao pesquisar recursos do Scene7 no navegador de ativos (ao editar uma página).

* **Trilho de pesquisa do administrador de sites**:

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao usar o painel de pesquisa do console Sites .

* **Editor de página (Pesquisa de vídeos):**

   Essa configuração define as opções disponíveis ao procurar vídeos no navegador de ativos (ao editar uma página).

* **Trilho de pesquisa do administrador de ativos:**

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao usar o console Ativos .

* **Painel de pesquisa do administrador de catálogos:**

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar um catálogo de comércio.

* **Painel de pesquisa do administrador de pedidos:**

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar pedidos de comércio.

* **Painel de pesquisa do administrador das coleções do produto:**

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar coleções de produtos de comércio.

* **Painel de pesquisa do administrador de produtos:**

   Essa configuração define as opções de pesquisa disponíveis para o usuário ao pesquisar produtos de comércio.

* **Trilho de pesquisa do administrador de projetos:**

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
   <td>Pesquise/filtre recursos no navegador Sites ao mostrar dados fornecidos pelo Analytics. Os filtros de pesquisa do Analytics são carregados para corresponder às colunas de análise personalizadas mapeadas.</td>
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
   <td>Permite que um autor pesquise/filtre por páginas que têm um componente específico nele. Por exemplo, uma galeria de imagens.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Profundidade da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data </td>
   <td>Pesquisa de ativos com base em controle deslizante com base em uma propriedade de data.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de datas </td>
   <td>Pesquise ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar , é possível especificar datas de Início e Término.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
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
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamanho do arquivo </td>
   <td>Pesquisar ativos com base em seu tamanho.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro oculto</td>
   <td>Um filtro na propriedade e no valor , não visível para o usuário.</td>
   <td>
    <ul>
     <li>Nome da Propriedade</li>
     <li>Valor da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opções </td>
   <td><p>As opções são nós de conteúdo criados pelo usuário.</p> <p>Consulte <a href="#addinganoptionspredicate">Adicionar um predicado de opções</a> para obter mais informações.</p> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Caminho JSON</li>
     <li>Nome da Propriedade*</li>
     <li>Única seleção</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opções Propriedade </td>
   <td>Pesquise em uma propriedade da opção .</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho do nó de opções<br /> </li>
     <li>Única seleção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da página </td>
   <td>Pesquise páginas de acordo com seu status.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade de publicação</li>
     <li>Nome de propriedade do LiveCopy</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Caminho  </td>
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
   <td>Pesquise em uma propriedade especificada.</td>
   <td>nenhum</td>
  </tr>
  <tr>
   <td>Publicar status </td>
   <td>Pesquisar ativos com base em seu status de publicação</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo </td>
   <td>Pesquise os recursos que estão dentro de um intervalo especificado. No painel Pesquisar , é possível especificar valores mínimos e máximos para o intervalo.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opções de intervalo </td>
   <td>Um predicado de pesquisa específico para Ativos e o mesmo Predicado de controle deslizante comum. Ainda está disponível devido a problemas de compatibilidade com versões anteriores.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Classificação </td>
   <td>Pesquisar ativos de acordo com sua classificação.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
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
     <li>Nome da Propriedade*</li>
     <li>Data relativa</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo do controle deslizante </td>
   <td>Um predicado de pesquisa comum que estende o predicado de intervalo com o recurso do controle deslizante. O valor da propriedade pesquisada deve estar entre os limites do controle deslizante.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Pesquisar ativos com base em tags. Você pode configurar a propriedade Caminho para preencher várias tags na lista Tags.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
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
     <li>Nome da Propriedade*</li>
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
   >   * Eles estão obsoletos e disponíveis apenas para compatibilidade com versões anteriores.
>
>Essas informações são apenas para referência, você não deve fazer alterações em `/libs`.

### Configurações do predicado {#predicate-settings}

Dependendo do predicado, uma seleção de configurações está disponível para configuração:

* **Rótulo do campo**

   O rótulo que aparecerá como o cabeçalho que pode ser recolhido ou como o rótulo de campo do predicado.

* **Descrição**

   Detalhes descritivos do usuário.

* **Espaço reservado**

   Texto vazio ou o espaço reservado do predicado caso nenhum texto de filtragem seja inserido.

* **Nome da Propriedade**

   A propriedade a ser pesquisada. Ele usa um caminho relativo e curingas `*/*/*` especifique a profundidade da propriedade em relação à variável `jcr:content` (cada asterisco representa um nível de nó).

   Se quiser pesquisar apenas em um nó filho de primeiro nível do recurso que tenha o `x` na `jcr:content` uso do nó `*/jcr:content/x`

* **Profundidade da propriedade**

   A profundidade máxima para procurar essa propriedade nos recursos. Portanto, uma pesquisa nessa propriedade pode ser executada em um recurso e em filhos recursivos até que o nível dos filhos seja igual à profundidade especificada.

* **Valor da propriedade**

   O valor da propriedade como uma string absoluta ou como uma linguagem de expressão; por exemplo, `cq:Page` ou

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto do intervalo**

   O rótulo do campo de intervalo na variável **Intervalo de datas** predicado.

* **Caminho de opção**

   O usuário pode selecionar o caminho usando o Navegador de caminhos na guia de configuração do predicado. Depois de selecionar o **+** é usado para adicionar a seleção à lista de opções válidas (em seguida, o ícone **-** ícone para remover, se necessário).

   As opções são nós de conteúdo criados pelo usuário, com a seguinte estrutura:

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Caminho do nó Opções**
Efetivamente, o mesmo que o 
**Caminho das opções**, somente se estiver no campo predicado comum, o outro é específico para ativos.

* **Seleção única**
Se marcada, as opções são renderizadas como caixas de seleção que permitem somente uma seleção. Se estiver selecionado incorretamente, uma caixa de seleção pode ser desmarcada.

* **Publicar e Live Copy Nome(s) de Propriedade**
Os rótulos das caixas de seleção publicar e live copy para o predicado específico Sites.

* O &amp;último; nos rótulos de campo na **Configurações** guia significa que os campos são obrigatórios e, se deixado em branco, uma mensagem de erro será exibida

## Configurar sua Forms de pesquisa {#configuring-your-search-forms}

### Criando/Abrindo uma Configuração Personalizada {#creating-opening-a-customized-configuration}

1. Navegar para **Ferramentas**, **Geral**, **Pesquisar Forms**.

1. Selecione a configuração que deseja personalizar.
1. Use o **Editar** ícone para abrir a configuração para atualização.
1. Se uma nova personalização você provavelmente desejará [adicionar novos campos de predicado e definir as configurações](#add-edit-a-predicate-field-and-define-field-settings) conforme necessário. Se houver uma personalização, você poderá selecionar um campo existente e [atualizar as configurações](#add-edit-a-predicate-field-and-define-field-settings).
1. Selecionar **Concluído** para salvar a configuração.

   >[!NOTE]
   >
   >As configurações personalizadas são armazenadas (conforme o caso) em:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Adicionar/editar um campo predicado e definir configurações de campo {#add-edit-a-predicate-field-and-define-field-settings}

Você pode adicionar ou editar campos e definir/atualizar suas configurações:

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Se quiser adicionar um novo campo, abra o **Selecionar predicado** e arraste o predicado necessário para o local desejado. Por exemplo, a variável **Predicado de intervalo de datas**:

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. Dependendo de:

   * Você está adicionando um novo campo:

      Após adicionar o predicado **Configurações** será aberta e mostrará as propriedades que podem ser definidas.

   * Você deseja atualizar um predicado existente:

      Selecione o campo predicado (à direita) e abra o **Configurações** guia .
   Por exemplo, as configurações da variável **Predicado de intervalo de datas**:

   ![chlimage_1-376](assets/chlimage_1-376.png)

1. Faça as alterações necessárias e confirme com **Concluído**.

### Visualização da configuração de pesquisa {#previewing-the-search-configuration}

1. Selecione o ícone Preview :

   ![](do-not-localize/chlimage_1-31.png)

1. Isso exibirá os formulários de pesquisa da forma que serão exibidos (totalmente expandidos) na coluna Pesquisar do console apropriado.

   ![chlimage_1-377](assets/chlimage_1-377.png)

1. **Fechar** a pré-visualização para retornar e concluir a configuração.

### Excluindo um campo de predicado {#deleting-a-predicate-field}

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Selecione o campo predicado (à direita) e abra o **Configurações** e selecione a **Excluir** ícone (canto inferior esquerdo).

   ![](do-not-localize/chlimage_1-32.png)

1. Uma caixa de diálogo solicitará a confirmação da ação de exclusão.

1. Confirme esta e quaisquer outras alterações com **Concluído**.

### Excluindo uma configuração (para restabelecer o padrão) {#deleting-a-configuration-to-reinstate-the-default}

Após personalizar uma configuração, os padrões serão substituídos. Você pode restabelecer a configuração padrão excluindo a configuração personalizada.

>[!NOTE]
>
>Não é possível excluir nenhuma das configurações padrão.

A exclusão de uma configuração personalizada é feita no console:

1. Selecione a configuração necessária (por exemplo, **Editor de páginas (pesquisa de parágrafos)**) e depois a variável **Excluir** na barra de ferramentas:

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. A configuração personalizada será excluída e o padrão reinstalado (isso é indicado pelo reaparecimento do símbolo de cadeado no console).

### Adicionar predicados de opções {#adding-options-predicates}

Os predicados de opção (Opções, Propriedade de opções) permitem configurar um item a ser pesquisado. Normalmente, eles são usados para procurar algo diretamente abaixo da página; por exemplo, uma propriedade no nó da página.

O exemplo a seguir (para pesquisar de acordo com o modelo usado para criar uma página) ilustra as etapas envolvidas:

1. Crie o nó que define a propriedade a ser pesquisada.

   Você precisará de um nó raiz contendo definições das opções individuais para estar disponível para o usuário.

   Os nós das opções individuais precisam das propriedades:

   * `jcr:title` - o rótulo do campo a ser exibido no painel de pesquisa
   * `value` - o valor da propriedade a ser pesquisada

   ![chlimage_1-379](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >Você ***must*** não altere nada no `/libs` caminho.
   >
   >Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >1. Recrie o item necessário, como ele existe em `/libs`, sob `/apps`. Nesse caso, de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Faça quaisquer alterações no `/apps.`


1. Abra o **Pesquisar Forms** e selecione a configuração que deseja atualizar. Por exemplo, **Painel de pesquisa do administrador de sites**.

   Em seguida, clique/toque no botão **Editar formulários de pesquisa** ícone .

1. Dependendo da configuração, adicione uma **Opções** ou **Propriedade Opções** à configuração.
1. Atualizar os campos, em particular:

   * **Nome da Propriedade**

      Específico da propriedade do nó a ser pesquisado nos nós de destino. Por exemplo:

      `jcr:content/cq:template`

   * **Caminho do nó da opção**

      Selecione o caminho onde suas opções são mantidas. Por exemplo:

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![chlimage_1-380](assets/chlimage_1-380.png)

1. Selecionar **Concluído** para salvar sua configuração.
1. Navegue até o console apropriado (neste exemplo, **Sites**) e abra o **Pesquisar** trilho. Os formulários de pesquisa recém-definidos, juntamente com as várias opções, estarão visíveis. Selecione a opção necessária para ver os resultados da pesquisa:

   ![chlimage_1-381](assets/chlimage_1-381.png)

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
   <td>Permissões de leitura e gravação no <code>/apps </code>nó .</td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td>Permissões de Leitura, Gravação e Exclusão no <code>/apps</code> nó</td>
  </tr>
  <tr>
   <td>Visualizar</td>
   <td>Permissões de Leitura, Gravação e Exclusão no <code>/var/dam/content</code> nó .<br /> Permissões de leitura e gravação no <code>/apps</code> nó .</td>
  </tr>
 </tbody>
</table>
