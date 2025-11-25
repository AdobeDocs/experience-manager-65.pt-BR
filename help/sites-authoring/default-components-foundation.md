---
title: Componentes de fundação
description: Saiba mais sobre os Componentes de base no Adobe Experience Manager 6.5.
exl-id: 278701f3-3f0c-45f4-90b7-c0e316a7da8a
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '6873'
ht-degree: 4%

---

# Componentes de fundação {#foundation-components}

>[!CAUTION]
>
>A maioria dos componentes básicos agora está obsoleta com o AEM 6.5. Consulte as [notas de versão](/help/release-notes/deprecated-removed-features.md) para obter mais informações.
>
>A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) mais modernos e extensíveis nos projetos AEM. Esses componentes fazem parte do [conteúdo de amostra do We.Retail](/help/sites-developing/we-retail.md) e também podem ser [instalados separadamente e usados para desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html) pelo seu administrador.
>
>Você pode usar o [Conjunto de ferramentas de Modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/) para refatorar seu site baseado em Componentes do Foundation para usar os Componentes principais.

Os componentes básicos foram projetados para uso na criação de conteúdo para uma página da Web padrão. Eles formam um subconjunto dos componentes disponíveis prontos para uso para uma instalação padrão do AEM.

Alguns estão disponíveis imediatamente por meio do navegador de componentes. Vários outros também estão disponíveis usando o [modo de design](/help/sites-authoring/default-components-designmode.md) (se a página for baseada em um modelo estático) ou [editando o modelo](/help/sites-authoring/templates.md) (se a página for baseada em um modelo editável).

O uso de componentes de base é compatível, mas eles foram descontinuados e substituídos por componentes principais que oferecem mais extensibilidade e flexibilidade.

>[!NOTE]
>
>Esta seção discute apenas os componentes disponíveis prontos para uso em uma instalação padrão do AEM.
>
>Dependendo da sua instância, você pode ter componentes personalizados desenvolvidos explicitamente para suas necessidades. Esses componentes personalizados podem até ter o mesmo nome de alguns dos componentes discutidos aqui.

Os componentes estão disponíveis na guia **Componentes** do painel lateral do editor de páginas ao [editar uma página](/help/sites-authoring/editing-content.md).

Você pode selecionar um componente e arrastá-lo até o local desejado na página. A partir daí é possível editá-lo usando:

* [Configurar propriedades](/help/sites-authoring/editing-page-properties.md)
* [Editar conteúdo](/help/sites-authoring/editing-content.md)

* [Editar conteúdo - Modo de tela cheia](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

Os componentes são classificados de acordo com várias categorias chamadas grupos de componentes, incluindo:

* [Geral](#general): inclui componentes básicos, incluindo texto, imagens, tabelas e gráficos.
* [Colunas](#columns): inclui componentes necessários para organizar o layout do conteúdo.
* [Formulário](#formgroup): inclui todos os componentes necessários para criar um formulário.

## Geral {#general}

Os componentes Gerais são os componentes básicos usados para criar conteúdo.

### Item da conta {#account-item}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR).

Você pode definir um link com título e descrição.

![chlimage_1-88](assets/chlimage_1-88.png)

### Imagem adaptativa {#adaptive-image}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=pt-BR).

O componente de base da imagem adaptável gera imagens dimensionadas para caber na janela em que a página da Web é aberta. Para usar o componente, você fornece um recurso de imagem do sistema de arquivos ou do DAM. Quando a página da Web é aberta, o navegador da Web baixa uma cópia da imagem que foi redimensionada para que seja adequada à janela atual.

As seguintes características podem determinar o tamanho da janela:

* Tela do dispositivo: dispositivos móveis normalmente exibem páginas da Web para que se estendam por toda a tela.
* Tamanho da janela do navegador da Web: os usuários de notebooks e desktops podem redimensionar as janelas do navegador da Web.

Por exemplo, o componente gera uma imagem pequena quando a página da Web é aberta em um telefone celular e uma imagem média quando aberta em um tablet. Em um laptop, o componente cria e fornece uma imagem grande quando a página é aberta em um navegador maximizado. Quando o navegador da Web é redimensionado para caber em uma parte da tela, o componente se adapta fornecendo uma imagem menor e atualiza a visualização.

#### Formatos de imagem compatíveis {#supported-image-formats}

Você pode usar arquivos de imagem das seguintes extensões de nome de arquivo com o componente de Imagem adaptável:

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>Arquivos GIF animados não são suportados no AEM para representações adaptáveis.

#### Tamanhos e qualidade das imagens {#images-sizes-and-quality}

A tabela a seguir lista a largura da imagem gerada para a largura de visor especificada. A altura da imagem gerada é calculada para manter uma taxa de proporção constante e nenhum espaço em branco ocorre dentro da borda da imagem. O corte pode ser usado para evitar espaços em branco.

Quando a imagem é uma imagem do JPEG, o tamanho da janela de visualização também pode influenciar a qualidade do JPEG. As seguintes qualidades do JPEG são possíveis:

* Baixo (0,42)
* Medium (0,82)
* Alta (1,00)

| **Intervalo de Largura de Visor (pixels)** | **Largura da Imagem (pixels)** | **Qualidade JPEG** | **Tipo de dispositivo de destino** |
|---|---|---|---|
| largura &lt;= 319 | 320 | baixa |  |
| largura = 320 | 320 | médio | Celular (retrato) |
| 320 &lt; largura &lt; 481 | 480 | médio | Telefone celular (paisagem) |
| 480 &lt; largura &lt; 769 | 476 | alta | Tablet (retrato) |
| 768 &lt; largura &lt; 1025 | 620 | alta | Tablet (paisagem) |
| largura &lt;= 1025 | total (tamanho original) | alta | Desktop |

#### Propriedades {#properties}

A caixa de diálogo permite editar as propriedades da instância do componente de Imagem adaptável, muitas das quais são comuns ao componente de Imagem no qual ele se baseia. As propriedades estão disponíveis em duas guias:

* **Imagem**

   * **Imagem**
Arraste uma imagem do localizador de conteúdo ou clique para abrir uma janela de navegação onde você pode carregar uma imagem. Depois que a imagem for carregada, você poderá recortá-la, girá-la ou excluí-la. Para ampliar e reduzir a imagem, use a barra deslizante abaixo da imagem (acima dos botões OK e Cancelar)

   * **Cortar**
Recortar parte de uma imagem. Arraste a borda para cortar a imagem.

   * **Girar**
Clique em Girar repetidamente até que a imagem seja girada conforme desejado.

   * **Limpar**
Remover a imagem atual.

* **Avançado**

   * **Título**
O componente de Imagem adaptável não usa essa propriedade.

   * **Texto Alternativo**
O texto alternativo a ser usado para a imagem.

   * **Vincular a**
O componente de Imagem adaptável não usa essa propriedade.

   * **Descrição**
O componente de Imagem adaptável não usa essa propriedade.

#### Extensão do componente de imagem adaptável {#extending-the-adaptive-image-component}

Para obter informações sobre como personalizar o componente de Imagem Adaptável, consulte [Noções Básicas sobre o Componente de Imagem Adaptável](/help/sites-developing/responsive.md#using-adaptive-images).

### Carrossel {#carousel}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do Carrossel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=pt-BR).

O componente Carrossel permite exibir imagens associadas a páginas individuais:

* um de cada vez
* por um curto período
* em uma ordem especificada por você
* com um atraso que você especifica

Os controles clicáveis também permitem que o usuário percorra as páginas exibidas em tempo real, sob demanda. A seleção da imagem da página visível atualmente leva você para essa página. Em outras palavras, o Carrossel atua como um controle de navegação.

#### Propriedades {#properties-1}

Essas propriedades estão disponíveis em duas guias:

* **Carrossel**
Aqui você especifica como o carrossel opera:

   * Reproduzir velocidade
O tempo em milissegundos antes do próximo slide é exibido.
   * Tempo de transição
O tempo em milissegundos para a transição entre dois slides.
   * Estilo dos controles
Várias opções estão disponíveis em um menu suspenso; por exemplo, Botões Anterior/Avançar, Comutadores Superior-Direito.

* **Lista**

  Aqui você especifica como as páginas são incluídas no carrossel:

   * **Criar lista usando**
Há várias maneiras de criar uma lista de páginas - Páginas secundárias, Lista fixa, Pesquisa ou Pesquisa avançada (todas descritas abaixo).
Independentemente do método escolhido, as páginas incluídas na lista devem ter, cada uma, uma imagem associada à página. Essa imagem é exibida no Carrossel. Se não houver imagem para uma determinada página nas Propriedades da página, você deve associar uma imagem à página antes de começar. Caso contrário, o Carrossel exibe uma página em branco. Consulte [Editando Propriedades Da Página](/help/sites-authoring/editing-page-properties.md).
Dependendo do item escolhido, um novo painel será exibido:

      * **Opções para Páginas Secundárias**

         * **Página pai**
Especifique um caminho manualmente ou usando o seletor. Deixe em branco para utilizar a página atual como principal.

      * **Opções da Lista Fixa**

         * **Páginas**
Selecione uma lista de páginas. Use `+` para adicionar mais entradas e os botões para cima/baixo para ajustar a ordem.

      * **Opções de Pesquisa**

         * **Iniciar em**
Insira um caminho inicial manualmente ou usando o seletor.

         * **Pesquisar consulta**
Você pode inserir uma consulta de pesquisa de texto simples.

      * **Opções de Pesquisa Avançada**

         * **Notação de predicado do Querybuilder**
Você pode inserir uma consulta de pesquisa usando a notação de predicado do Querybuilder. Por exemplo, você pode digitar &quot;fulltext=Marketing&quot; para que todas as páginas com &quot;Marketing&quot; em seu conteúdo sejam exibidas no Carrossel.
Consulte a [API do QueryBuilder](/help/sites-developing/querybuilder-api.md) para obter uma discussão completa sobre expressões de consulta e mais exemplos.

   * **Solicitar por**
Selecione `jcr:title`, `jcr:created`, `cq:lastModified` ou `cq:template` no menu suspenso.

   * **Limite**
Opcional. O número máximo de itens que você deseja usar no Carrossel.

>[!NOTE]
>
>Você pode criar um componente de carrossel personalizado para o Adobe Experience Manager que exibe ativos digitais no AEM DAM. Consulte [Criação de componentes de Carrossel personalizados para o Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

### Gráfico {#chart}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O componente de Gráfico permite adicionar um gráfico de barras, de linhas ou de pizza. O AEM cria um gráfico com base nos dados fornecidos. Você fornece dados digitando diretamente na guia Dados ou copiando e colando uma planilha.

* **Dados**

   * **Dados do gráfico**
Insira os dados do gráfico usando o formato CSV; o formato de Valores separados por vírgula usa vírgulas (&quot;,&quot;) como separador de campo.

* **Avançado**

   * **Tipo de gráfico**
Selecione entre Gráfico de Pizza, Gráfico de Linhas e Gráfico de Barras.

   * **Texto alternativo**
Exibe texto alternativo em vez do gráfico.

   * **Largura**
A largura do gráfico em pixels.

   * **Altura**
A altura do gráfico em pixels.

A seguir, há um exemplo de dados de gráfico seguido pelo gráfico de Barras resultante:

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
>
>Você pode criar um controle de gráfico AEM personalizado que exibe dados no JCR do AEM. Para obter informações, consulte [Exibindo Dados do Adobe Experience Manager em um Gráfico](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

### Fragmento de conteúdo {#content-fragment}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR).

[Fragmentos de conteúdo](/help/sites-authoring/content-fragments.md) são criados e gerenciados como ativos independentes da página. Em seguida, é possível usar estes fragmentos e suas variações ao criar suas páginas de conteúdo.

### Importador de design {#design-importer}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Este componente permite fazer upload de um arquivo zip que contém um pacote de design.

### Download {#download}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O componente de Download cria um link na página da Web selecionada para baixar um arquivo específico. Você pode arrastar um ativo do Localizador de conteúdo ou carregar um arquivo.

* **Download**

   * **Descrição**
Uma breve descrição é exibida com o link de download.

   * **Arquivo**
O arquivo está disponível para download na página da Web resultante. Arraste um ativo do localizador de conteúdo ou selecione a área para fazer upload do arquivo que deseja disponibilizar para download.

O exemplo a seguir mostra o componente de Download no Geometrixx:

![dc_download_use](assets/dc_download_use.png)

### Externo {#external}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O componente de integração de aplicativos externos (**Externo**) permite que você incorpore aplicativos externos à sua página do AEM usando um iframe.

* **Externo**

   * **Aplicativo de destino**
Especifique o URL do aplicativo Web a ser integrado; por exemplo:

     ```
     https://en.wikipedia.org/wiki/Main_Page
     ```

   * **Passar parâmetros**
Marque a caixa para que os parâmetros sejam passados para o aplicativo quando necessário.

   * **Largura e altura
**Defina o tamanho do iframe

O aplicativo externo está integrado ao sistema de parágrafo da página do AEM; por exemplo, ao usar um aplicativo do Target de `https://en.wikipedia.org/wiki/Main_Page`:

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>Dependendo do caso de uso, outras opções estão disponíveis para integração de aplicativos externos, por exemplo, a [Integração de Portlets](/help/sites-administering/aem-as-portal.md).

### Flash {#flash}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

O componente Flash permite carregar um filme Flash. Você pode arrastar um ativo flash do localizador de conteúdo para o componente ou usar a caixa de diálogo:

* **Flash**

   * **Filme em Flash**

     O arquivo de filme flash. Arraste um ativo do localizador de conteúdo ou clique em para abrir uma janela de navegação.

   * **Tamanho**

     Dimensões em pixels da área de exibição que contém o filme.

* **Imagem alternativa**

  Uma imagem alternativa a ser mostrada

* **Avançado**

   * **Menu de contexto**

     Indica se o menu de contexto deve ser exibido ou oculto.

   * **Modo de janela**

     Como a janela aparece, por exemplo, opaca, transparente ou como uma janela distinta (sólida).

   * **Cor do plano de fundo**

     Uma cor de plano de fundo selecionada no gráfico de cores fornecido.

   * **Versão mínima**

     A versão mínima do Adobe Flash Player necessária para executar o filme. O padrão é 9.0.0.

   * **Atributos**

     Quaisquer outros atributos necessários.

### Imagem {#image}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=pt-BR).

O componente de imagem exibe uma imagem e o texto que a acompanha de acordo com os parâmetros especificados.

É possível carregar uma imagem, editá-la e manipulá-la (por exemplo, cortar, girar, adicionar link/título/texto).

Você pode arrastar e soltar uma imagem do [Navegador Assets](/help/sites-authoring/author-environment-tools.md#assets-browser) diretamente no componente ou em sua [caixa de diálogo de Configuração](/help/sites-authoring/editing-content.md#component-edit-dialog). Você poderá também enviar uma imagem da janela de Configuração; esta janela também controla todas as definições e manipulações da imagem:

![chlimage_1-91](assets/chlimage_1-91.png)

Depois que a imagem for carregada (e não antes), você poderá usar a [edição local](/help/sites-authoring/editing-content.md#edit-content) para recortar/girar a imagem conforme necessário:

![Inserir barra de ferramentas de edição](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>O editor local usa o tamanho original e a proporção da imagem ao editar. Também é possível especificar propriedades de altura e largura. Quaisquer restrições de tamanho e taxa de proporção definidas nas propriedades são aplicadas quando você salva as alterações de edição.
>
>Dependendo da sua instância, restrições mínimas e máximas também podem ser impostas pelo [design da página](/help/sites-developing/designer.md). Essas restrições são desenvolvidas durante a implementação do projeto.

Várias opções adicionais estão disponíveis no modo de edição de tela cheia; por exemplo, map e zoom:

![Modo de edição de tela inteira - mapa e zoom](do-not-localize/chlimage_1-16.png)

>[!NOTE]
>
>O progresso do upload não pode ser monitorado com o Internet Explorer.
>
>Os usuários do Internet Explorer devem carregar a imagem e clicar em **Ok**. Em seguida, reabra a imagem para ver o arquivo carregado na visualização e poder executar modificações (ou seja, recortar).
>
>Consulte a seção [Plataformas certificadas](/help/release-notes/release-notes.md#certifiedplatforms) para obter mais informações sobre os recursos do HTML5 usados pelo AEM.

Quando uma imagem é carregada, você pode configurar o seguinte:

* **Mapa**

  Para mapear uma imagem, selecione Mapear. Você pode especificar como deseja criar o mapa de imagem (retângulo, polígono etc.) e onde a área deve apontar.

* **Cortar**

  Para recortar parte de uma imagem, selecione Cortar. Use o mouse para cortar a imagem.

* **Girar**

  Para girar uma imagem, selecione Girar. Use repetidamente até que a imagem seja girada da maneira desejada.

* **Limpar**

  Remover a imagem atual.

* **Título**

  O título da imagem.

* **Texto Alternativo**

  Um texto alternativo a ser usado ao criar conteúdo acessível.

* **Vincular a**

  Crie um link para ativos ou outras páginas no seu site.

* **Descrição**

  Uma descrição da imagem.

* **Tamanho**

  Define a altura e a largura da imagem.

>[!NOTE]
>
>Algumas opções só estão disponíveis no editor de tela cheia.

A imagem final (com **Título** e **Descrição**) pode ser mostrada como:

![chlimage_1-92](assets/chlimage_1-92.png)

### Contêiner de layout {#layout-container}

Este componente fornece um sistema de parágrafo de grade para que você possa adicionar e posicionar componentes em uma [grade responsiva](/help/sites-authoring/responsive-layout.md). Você pode definir layouts de conteúdo diferentes com base na largura dos dispositivos de destino, incluindo uma variedade de telefones, tablets e área de trabalho.

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
>
>Este componente foi implementado com a [Linguagem de Modelo do HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR).

### Lista {#list}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html).

O componente Lista permite configurar critérios de pesquisa para exibir uma lista:

* **Lista**

   * **Criar lista usando**

     Aqui você especifica onde a lista recupera o conteúdo. Há vários métodos:

   * Dependendo do item escolhido, um novo painel será exibido:

      * **Opções para Páginas Secundárias**

         * **Filhos de** (Página Pai)

           Especifique um caminho manualmente ou usando o seletor. Deixe em branco para utilizar a página atual como principal.

      * **Opções da Lista Fixa**

         * **Páginas**

           Selecione uma lista de páginas. Use + para adicionar mais entradas e os botões para cima/baixo para ajustar a ordem.

      * **Opções de Pesquisa**

         * Começa em

           Insira um caminho inicial manualmente ou usando o seletor.

         * Pesquisar consulta

           Você pode inserir uma consulta de pesquisa de texto simples.

      * **Opções de Pesquisa Avançada**

         * **Notação de predicado do Querybuilder**

           Você pode inserir uma consulta de pesquisa usando a notação de predicado do Querybuilder. Por exemplo, você pode digitar &quot;fulltext=Marketing&quot; para que todas as páginas com &quot;Marketing&quot; em seu conteúdo sejam exibidas no Carrossel.

           Consulte a [API do QueryBuilder](/help/sites-developing/querybuilder-api.md) para obter uma discussão completa sobre expressões de consulta e mais exemplos.

      * **Tags**

        Especifique a **Página pai**, **Marcas/Palavras-chave** e os critérios de correspondência necessários.

   * **Exibir como**

     Como você deseja que os itens sejam listados; inclui Links, Teasers e Notícias.

   * **Solicitar por**

     Se a lista deve ser ordenada e, em caso afirmativo, os critérios a serem usados para a classificação. Você pode inserir um critério ou selecionar um na lista suspensa fornecida.

   * **Limite**

     Especifique o número máximo de itens que deseja exibir na lista.

   * **Habilitar Feed**

     Indica se um feed RSS deve ser ativado para a lista.

   * **Paginar após**

     Aqui você pode especificar o número de itens da lista a serem exibidos de uma vez. Uma lista com mais itens do que o especificado usa a paginação para exibir a lista em várias partes.

O exemplo a seguir mostra um componente **Lista** da maneira que ele pode exibir uma lista de páginas secundárias (o design é controlado pelas definições CSS personalizadas de um design de site).

![dc_list_use](assets/dc_list_use.png)

### Logon {#login}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

Fornece os campos Nome de usuário e Senha.

![chlimage_1-94](assets/chlimage_1-94.png)

Você pode configurar:

* Fazer Logon

   * Rótulo da seção

     Texto de lead-in para os campos de entrada.

   * Rótulo do nome de usuário

     Texto para rotular o campo de nome de usuário.

   * Rótulo da senha

     Texto para rotular o campo de senha.

   * Rótulo do botão de logon

     Texto do botão de logon.

   * Redirecionar para

     Você pode especificar a página do site que deve ser aberta depois que o usuário fizer logon.

* Já está conectado.

   * Continuar a etiqueta do botão

     Texto para indicar que o usuário já está conectado.

### Status do pedido {#order-status}

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

* **Título**

   * **Título**

     Especifique o texto do título que deseja exibir.

   * **Link**

     Especifique a página (produto) para a qual o status do pedido deve ser exibido.

   * **Tipo/Tamanho**

     Selecione a partir da seleção fornecida.

![chlimage_1-95](assets/chlimage_1-95.png)

### Referência {#reference}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=pt-BR).

O componente **Referência** permite referenciar texto de outra página do site do AEM (na instância atual). O conteúdo do parágrafo referenciado aparece como se estivesse na página atual. O conteúdo é atualizado quando o parágrafo de origem é alterado (pode ser necessário atualizar a página).

* **Referência do parágrafo**

   * **Referência**

     Especifique o caminho para a página e o parágrafo que deseja referenciar (inclua o conteúdo).

Para especificar o caminho para um parágrafo, você deve usar o seguinte sufixo no caminho (para a página):

`.../jcr:content/par/<paragraph-ID>`

Por exemplo:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

Além de fazer referência a um parágrafo específico, o caminho também pode ser modificado para especificar um par-system inteiro. Você pode fazer essa referência ao colocar o caminho com o seguinte sufixo:

`/jcr:content/par`

Por exemplo:

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

Após a configuração, o conteúdo é exibido exatamente como na página de origem. O fato de ser uma referência só é visto quando você abre o componente para edição:

![chlimage_1-96](assets/chlimage_1-96.png)

### Pesquisar {#searching}

>[!CAUTION]
>
>Este componente de base está obsoleto. A Adobe recomenda usar o [Componente principal de Pesquisa Rápida](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/quick-search.html).

O componente de Pesquisa adiciona o recurso de pesquisa à página.

Você pode configurar:

* Pesquisar

   * **Tipos de nós**

     Se a pesquisa deve ser restrita a um tipo de nó específico, liste-os aqui; por exemplo, `cq:Page`.

   * **Caminho para pesquisar em**

     Especifique a página raiz da ramificação que deseja pesquisar.

   * **Texto do Botão de Pesquisa**

     O nome exibido no botão de pesquisa real.

   * **Texto de Estatísticas**

     O texto exibido acima dos resultados da pesquisa.

   * **Nenhum texto de resultados**

     Se não houver resultados, o texto inserido aqui será exibido.

   * **Verificar Ortografia do Texto**

     Se alguém inserir um termo semelhante, este texto será exibido antes do termo.
Por exemplo, se você digitar `Geometrixxe`, o sistema exibirá &quot;Você quis dizer? Geometrixx&quot;.

   * **Texto de Páginas Semelhantes**

     O texto que é exibido ao lado de um resultado para páginas semelhantes. Para ver páginas com conteúdo semelhante, clique neste link.

   * **Texto de Pesquisas Relacionadas**

     O texto que aparece ao lado das pesquisas por termos e tópicos relacionados.

   * **Texto de Tendências de Pesquisa**

     O título acima dos termos de pesquisa que um usuário insere.

   * **Rótulo das Páginas de Resultado**

     O texto que aparece na parte inferior desta lista com links para outras páginas de resultados.

   * **Rótulo Anterior**

     O nome que aparece no link para as páginas de pesquisa anteriores.

   * **Próximo Rótulo**

     O nome que aparece no link para as páginas de pesquisa subsequentes.

O exemplo a seguir mostra o componente de Pesquisa após uma pesquisa pela palavra *`geometrixx`* no diretório raiz de uma instalação padrão. Também ilustra a paginação de resultados:

![dc_search_use](assets/dc_search_use.png)

O exemplo a seguir mostra um termo de pesquisa com ortografia incorreta e indisponível:

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Mapa do site {#sitemap}

>[!CAUTION]
>
>Este componente de base está obsoleto. A Adobe recomenda usar os [Componentes principais de Navegação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/navigation.html), [Navegação de Idioma](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/language-navigation.html) e [Navegação estrutural](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/breadcrumb.html).

Uma listagem automática de mapa de site, que (com as configurações padrão) lista todas as páginas (como links ativos) no site atual. Por exemplo, um extrato mostra:

![dc_sitemap_use](assets/dc_sitemap_use.png)

Se necessário, você pode configurar o seguinte:

* **Mapa do site**

   * **Caminho raiz**

     Caminho de onde a listagem deve começar.

### Slideshow {#slideshow}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do Carrossel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html?lang=pt-BR).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

Este componente permite carregar uma série de imagens para serem exibidas como uma apresentação de slides na página. É possível adicionar ou remover imagens e atribuir um título a cada uma. Em Avançado, também é possível especificar o tamanho da área de exibição.

Você pode configurar:

* **Slides**

   * **Novo Slide**

     Você pode especificar uma seleção de slides usando os botões **Adicionar** (e **Remover**).

   * **Título**

     Especifique um título, se necessário. O título é sobreposto no slide apropriado.

* **Avançado**

   * **Tamanho**

     Especifique a largura e a altura em pixels.

O componente de apresentação de slides exibe repetidamente cada um em sequência, por um curto período, antes de passar para o próximo slide:

![dc_slideshow_use](assets/dc_slideshow_use.png)

### Tabela {#table}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html).

>[!NOTE]
>
>O componente de base **Tabela** é baseado no [editor de Rich Text](/help/sites-authoring/rich-text-editor.md), como é o componente de base **[Texto](#text)**.

O componente **Tabela** é pré-configurado para permitir que você construa, preencha e formate uma tabela. Usando a caixa de diálogo, é possível configurar a tabela e criar o conteúdo das seguintes maneiras:

* do zero
* copiar e colar uma planilha ou uma tabela de um editor externo (como Excel, OpenOffice e Notepad).

É possível fazer alterações básicas no conteúdo usando o editor em linha:

![dc_table](assets/dc_table.png)

No modo de tela cheia, é possível configurar o layout da tabela:

![chlimage_1-97](assets/chlimage_1-97.png)

A captura de tela a seguir mostra um exemplo do componente de tabela; o design é determinado pelo CSS específico do site:

![dc_table_use](assets/dc_table_use.png)

### Nuvem de tags {#tag-cloud}

Uma nuvem de tags mostra uma seleção apresentada graficamente das tags aplicadas ao conteúdo em seu site:

![dc_tagclouduse](assets/dc_tagclouduse.png)

Ao configurar o componente do Tag Cloud, você pode especificar:

* **Marcas a Serem Exibidas**

  De onde as tags a serem exibidas são coletadas. Selecione de uma página, uma página com todas as tags secundárias ou todas as tags.

* **Página**

  Selecione a página que será referenciada.

* **Nenhum link nas marcas**

  Se as tags exibidas devem agir como links.

Para obter mais informações sobre como aplicar tags, visite [Usando Tags](/help/sites-authoring/tags.md).

### Texto {#text}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html).

>[!NOTE]
>
>O componente de base **Texto** é baseado no [editor de Rich Text](/help/sites-authoring/rich-text-editor.md), como é o componente de base **Tabela**.

O componente de Texto permite inserir um bloco de texto usando um editor WYSIWYG, com funcionalidade fornecida pelo [editor de Rich Text](/help/sites-authoring/rich-text-editor.md). Uma seleção de ícones permite formatar o texto, incluindo características de fonte, alinhamento, links, listas e recuo.

![chlimage_1-98](assets/chlimage_1-98.png)

Ao abrir a caixa de diálogo **Configurar**, você também pode definir:

* **Espaçador**
* **Estilo do texto**

O texto formatado é mostrado na página. O design real depende do CSS do site:

![dc_text_use](assets/dc_text_use.png)

Para obter informações mais detalhadas sobre o componente de Texto e a funcionalidade fornecida pelo editor de Rich Text, consulte a página [Editor de Rich Text](/help/sites-authoring/rich-text-editor.md).

#### Edição no local {#inplace-editing}

Além do modo de edição de Rich Text baseado em caixas de diálogo, o AEM também fornece a [Edição no local](/help/sites-authoring/editing-content.md), que permite a edição direta do texto conforme ele é exibido no layout da página.

### Texto e imagem {#text-image}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente de Imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=pt-BR) e o [Componente principal de Texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html).

O componente de Texto e imagem adiciona um bloco de texto e uma imagem. Também é possível adicionar e editar texto e imagens separadamente. Consulte os componentes [Texto](#text) e [Imagem](#image) para obter detalhes.

![chlimage_1-99](assets/chlimage_1-99.png)

Você pode configurar:

* **Estilos de Componentes** (**Estilos**)

  Aqui você pode alinhar a imagem à esquerda ou à direita. O padrão é **Esquerda** alinhada, com a imagem à esquerda.

* **Propriedades da Imagem** (**Propriedades Avançadas da Imagem**)

  Permite especificar o seguinte:

   * **Ativos da imagem**

     Carregue a imagem necessária.

   * **Título**

     O título do bloco, mostrado por mouseover.

   * **Texto Alternativo**

     Texto alternativo a ser mostrado se a imagem não puder ser exibida. Se deixado em branco, o título será usado.

   * **Vincular a**

     Especifique um caminho de destino.

   * **Descrição**

     Uma descrição da imagem.

   * **Tamanho**

     Define a altura e a largura da imagem.

O exemplo a seguir mostra um componente de Imagem de texto que exibe a imagem alinhada à esquerda:

![dc_textimage_use](assets/dc_textimage_use.png)

### Título {#title}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Título](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html).

O componente de título pode:

* Exiba o nome da página atual deixando o campo Título em branco.
* Exiba um texto especificado no campo Título.

Você pode configurar:

* **Título**

  Se quiser usar um nome diferente do título da página, insira-o aqui.

* **Link**

  O URI se o título for para operar como um link.

* **Tipo/Tamanho**

  Selecione Pequeno ou Grande na lista suspensa. O pequeno é gerado como uma imagem. Grande é gerado como texto.

O exemplo a seguir mostra um componente **Título** sendo exibido; o design é determinado pelo CSS específico do site.

![dc_title_use](assets/dc_title_use.png)

### Vídeo {#video}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente de Incorporação dos Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

O componente de **Vídeo** permite que você coloque um elemento de vídeo predefinido e pronto para uso em uma página.

Consulte também [Configurar perfis de vídeo](/help/sites-administering/config-video.md#configuringvideoprofiles) para usar com elementos do HTML5.

Depois de colocar uma instância do componente na página, você pode configurar o seguinte:

* Vídeo

   * **Ativo de vídeo**

     Carregue ou solte seu ativo de vídeo.

   * **Tamanho**

     O tamanho nativo do vídeo (largura x altura em pixels) é exibido nas caixas ao lado de Tamanho (veja acima). Insira manualmente as dimensões de largura e altura aqui se desejar substituir as dimensões nativas do vídeo. Selecionar **OK** ignora a caixa de diálogo.

>[!NOTE]
>
>Os formatos compatíveis incluem:
>
>* `.mp4`
>* `Ogg`
>* `FLV` (vídeo em Flash)

## Colunas {#columns}

As colunas são um mecanismo para controlar o layout do conteúdo no AEM. Em uma instalação padrão, são fornecidos componentes para criar duas ou três colunas.

O exemplo a seguir mostra o componente de Duas colunas em uso. É possível usar os espaços reservados para novos componentes:

![dc_columncontrol](assets/dc_columncontroluse.png)

### 2 colunas {#columns-1}

Um componente de Controle de Coluna que assume o padrão de duas colunas iguais.

### 3 colunas {#columns-2}

Um componente de Controle de Coluna que assume três colunas iguais como padrão.

### Controle de coluna {#column-control}

O componente de Controle de coluna permite que os usuários selecionem como desejam dividir o conteúdo do painel principal da página da Web em várias colunas. Os usuários podem selecionar o número de colunas necessárias (de uma lista predefinida) e, em seguida, criar, excluir ou mover o conteúdo em cada uma das colunas.

* **Controle de coluna**

   * **Layout da coluna**

     Selecione o número de colunas que você deseja renderizar. Depois de criada, cada coluna tem seu próprio link para arrastar componentes ou ativos ao adicionar conteúdo.

## Formulário {#form}

>[!CAUTION]
>
>O componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Os componentes de formulário são usados para criar formulários para os visitantes enviarem entrada. Os componentes de formulário e Forms podem ser usados para coletar informações, incluindo feedback do usuário (por exemplo, um questionário de satisfação do cliente) e informações do usuário (por exemplo, registro do usuário).

>[!NOTE]
>
>Consulte a [Ajuda do AEM Forms](/help/forms/using/introduction-aem-forms.md) para obter informações sobre o AEM Forms.

Os Forms são criados a partir de vários componentes diferentes:

* **Formulário**

  O componente de Formulário define o início e o fim de um novo formulário em uma página. Outros componentes podem ser colocados entre esses elementos, como tabelas e downloads.

* **Campos e elementos de formulário**

  Os campos e elementos de formulário podem incluir caixas de texto, botões de opção e imagens. O usuário geralmente conclui uma ação em um campo de formulário, como digitar texto. Consulte elementos de formulário individuais para obter mais informações.

* **Componentes do Perfil**

  Os componentes do perfil estão relacionados aos perfis de visitantes usados para colaboração social e outras áreas em que a personalização do visitante é necessária.

O exemplo a seguir mostra um formulário. Ele é composto pelo componente **Formulário** (início e término), com dois campos **Formulário** **Texto** usados para entrada, um campo **Geral** **Texto** usado para o texto de introdução e um botão **Enviar**.

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>Informações sobre desenvolvimento e personalização de formulários estão disponíveis na [página Desenvolvimento de Forms](/help/sites-developing/developing-forms.md). Essa capacidade inclui adicionar ações, restrições, pré-carregar campos e usar scripts para chamar um serviço para ação, entre outros.

### Configurações comuns aos (muitos) componentes de formulário {#settings-common-to-many-form-components}

Embora cada um dos componentes do formulário tenha uma finalidade diferente, muitos são compostos de opções e parâmetros semelhantes.

Ao configurar qualquer um dos componentes de formulário, as seguintes guias estão disponíveis na caixa de diálogo:

* **Título e texto**

  Aqui você deve especificar as informações básicas, como o título do formulário e qualquer texto que o acompanhe. Quando apropriado, também permite definir outras informações importantes, como se o campo é multisselecionável e se os itens estão disponíveis para seleção.

* **Valores iniciais**

  Permite especificar um valor padrão.

* **Restrições**

  Aqui você pode especificar se um campo é obrigatório e colocar restrições nesse campo (por exemplo, deve ser numérico).

* **Estilo**

  Indica o tamanho e o estilo dos campos.

>[!NOTE]
>
>Os campos que você vê variam significativamente dependendo do componente individual.

Essas guias fornecem os parâmetros necessários. As guias podem depender do tipo de componente individual, mas podem incluir o seguinte:

* **Título e texto**

   * **Nome do elemento**

     Nome do elemento de formulário. Indica onde os dados estão armazenados no repositório.
Este campo é obrigatório e deve conter apenas os seguintes caracteres:

      * caracteres alfanuméricos
      * `_ . / : -`

   * **Título**

     O título exibido com o campo. Se deixado em branco, o título padrão é exibido.

   * **Descrição**

     Permite fornecer informações adicionais ao usuário, se necessário. No formulário, ele é mostrado abaixo do campo, em uma fonte menor do que o título.

   * **Mostrar/Ocultar**

     Determina quando o campo está visível.

* **Valores iniciais**

   * **Valor padrão**

     O valor exibido no campo quando o formulário é aberto. Ou seja, antes que o usuário tenha feito qualquer entrada.

* **Restrições**

   * **Obrigatório**

     As restrições dependem do tipo de componente de formulário, mas fornecem uma ou mais caixas de clique para indicar que este campo é obrigatório, ou determinadas partes deste campo, são obrigatórias.

   * **Mensagem necessária**

     Uma mensagem para informar aos usuários que esse campo é obrigatório. Um campo obrigatório também é sinalizado com um asterisco.

   * **Restrição**

     As restrições disponíveis para seleção dependem do tipo de componente de formulário.

   * **Mensagem de restrição**

     Uma mensagem para informar aos usuários o que é necessário.

* **Estilo**

   * **Tamanho**

     Em linhas e colunas.

   * **Largura**

     Em pixels.

   * **CSS**

### Formulário (componente) {#form-component}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do Contêiner de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html).

O componente de Formulário define o início e o fim de um formulário usando os elementos **Início do Formulário** e **Fim do Formulário**. O início e o fim são sempre emparelhados para garantir que o formulário seja definido corretamente.

![dc_form-1](assets/dc_form-1.png)

Entre o início e o fim de um formulário, é possível adicionar componentes de formulário que definem os campos de entrada reais para usuários.

>[!NOTE]
>
>O componente de formulário, dos Componentes de base, suporta apenas o uso de outros componentes de formulário dos componentes de base (botão, texto, oculto e assim por diante). Não há suporte para o uso de componentes de formulário [core components](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) em um formulário de componente de base (e vice-versa).

#### Início do formulário {#start-of-form}

Esse componente define o início de um novo formulário em uma página. Você pode configurar:

* **Formulário**

   * **Página de Agradecimento**

     A página a ser referenciada para agradecer aos visitantes por fornecer sua entrada. Se deixado em branco, o formulário será exibido novamente após o envio.

   * **Iniciar Fluxo de Trabalho**

     Determina qual fluxo de trabalho será acionado depois que um formulário for enviado.

* **Avançado**

   * **Tipo de ação**

     Um formulário precisa de uma ação. A ação define a operação que é acionada para execução com os dados enviados pelo usuário (semelhante à ação= no HTML). Alguns precisam de uma **Configuração de Ação** correspondente.
Uma seleção de tipos de ação está incluída em uma instalação padrão do AEM:

      * **Solicitação de conta**
      * **Criar conteúdo**
      * **Criar cliente em potencial**
      * **Criar e atualizar a conta**
      * **Serviço de Email: Criar Assinante e adicionar à lista**
      * **Serviço de Email: Enviar email de resposta automática**
      * **Serviço de Email: Cancelar inscrição do usuário na lista**
      * **Editar Comunidade**
      * **Editar Recursos**
      * **Editar Recursos Controlados por Fluxo de Trabalho**
      * **Email**
      * **Detalhes do Pedido Feito**
      * **Atualização de perfil**
      * **Redefinir senha**
      * **Definir senha**
      * **Armazenar conteúdo**

        O tipo de ação padrão.

      * **Armazenar conteúdo com carregamentos**
      * **Enviar Pedido**
      * **Cancelar assinatura do Assinante**
      * **Atualizar Ordem**

   * **Identificador de formulário**

     O identificador do formulário identifica exclusivamente o formulário. Use o identificador de formulário se você tiver vários formulários em uma única página; verifique se eles têm identificadores diferentes.

   * **Carregar Caminho**

     O caminho para as propriedades do nó usadas para carregar valores predefinidos nos campos de formulário.

     Um campo opcional que especifica o caminho para um nó no repositório. Quando esse nó tem propriedades que correspondem aos nomes dos campos, os campos apropriados no formulário são pré-carregados com o valor dessas propriedades. Se não houver correspondência, o campo conterá o valor padrão.

     Usando o **Caminho de Carregamento**, você pode pré-carregar o formulário com valores nos campos obrigatórios. Consulte [Pré-Carregando Valores de Formulário](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **Validação do cliente**

     Indica se a validação do cliente é necessária para este formulário (a validação do servidor *sempre* ocorre). A validação do cliente pode ser obtida com o componente **Forms Captcha**.

   * **Tipo de recurso de validação**

     Define o tipo de recurso de validação de formulário se desejar validar o formulário inteiro (em vez de campos individuais). Se você estiver validando o formulário completo, inclua também um dos seguintes:

      * Um script para validação de cliente:

        `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * Um script para validação no lado do servidor:

        `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`

   * **Configuração de ação**

     As opções disponíveis em **Configuração de Ação** dependem do **Tipo de Ação** selecionado:

      * **Solicitação de conta**

         * **Criar página de conta**

           A página usada ao criar uma conta.

      * **Criar conteúdo**

         * Caminho do conteúdo

           O caminho de conteúdo para qualquer conteúdo que o formulário despeja. Digite um caminho que termine com uma barra `/`. A barra significa que, para cada porta de formulário, um novo nó é criado no local determinado; por exemplo:

           `/forms/feedback/`

         * **Tipo**

           Selecione o tipo necessário.

         * **Formulário**

           Especifique o formulário.

         * **Renderizar com**

           Selecione a opção necessária na lista.

         * **Tipo de recurso**

           Se definido, ele é adicionado a cada comentário como `sling:resourceType`

         * **Exibir seletor**

      * **Criar cliente em potencial**

         * **O lead foi adicionado a esta lista**

           Especifique a lista de clientes potenciais necessária.

      * **Criar e atualizar a conta**

         * **Grupo inicial**

           Grupo ao qual atribuir o novo usuário.

         * **Residência**

           Página a ser exibida após o logon bem-sucedido.

         * **Caminho**

           O caminho (relativo) para onde a nova conta é criada e armazenada.

         * **Exibir Dados...**

           Selecionar esse botão acessa as informações sobre os resultados do formulário no Editor de itens em massa. Aqui, você pode exportar as informações para um arquivo `.tsv` (separado por tabulação) (para uso, por exemplo, em uma planilha do Excel).

      * **Email**

         * **De**

           Insira o endereço de email do qual o email deve vir.

         * **Mailto**

           Insira um ou mais endereços de email para os quais o formulário é enviado.

         * **CC**

           Insira um ou mais endereços de email CC.

         * **CCO**

           Insira um ou mais endereços de email CCO.

         * **Assunto**

           Insira um assunto para o email.

      * **Redefinir senha**

         * **Alterar página de senha**

           A página usada ao alterar a senha.

      * **Armazenar conteúdo**

         * **Caminho do conteúdo**

           O caminho de conteúdo para qualquer conteúdo que o formulário despeja. Digite um caminho que termine com uma barra `/`. A barra significa que, para cada porta de formulário, um novo nó é criado no local determinado; por exemplo:
           `/forms/feedback/`

         * **Exibir Dados...**

           Clique nesse botão para poder acessar as informações sobre os resultados do formulário no Editor de itens em massa. Aqui, é possível exportar as informações para um arquivo .tsv (separado por tabulação) (para uso em uma planilha do Excel, por exemplo).

      * **Armazenar Conteúdo Com Carregamentos**

        Tem as mesmas opções que **Armazenar Conteúdo**.

      * **Cancelar assinatura do Assinante**

         * **O cliente em potencial foi excluído desta lista**

           Especifique a lista de clientes potenciais necessária.

#### Final do formulário {#end-of-form}

Marca o fim do formulário. Você pode configurar o seguinte:

* **Fim do formulário**

   * **Mostrar Botão Enviar**

     Indica se um botão Enviar deve ser mostrado ou não.

   * **Enviar Nome**

     Um identificador se estiver usando vários botões de envio em um formulário.

   * **Enviar Título**

     O nome que aparece no botão, como Enviar ou Enviar.

   * **Mostrar botão de redefinição**

     Marcar a caixa de seleção torna visível o botão Redefinir.

   * **Redefinir título**

     O nome que aparece no botão Redefinir.

   * **Descrição**

     Informações que aparecem abaixo do botão.

### Nome da conta {#account-name}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Texto de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html).

Permite que o usuário insira um nome de conta:

![dc_form_accountname](assets/dc_form_accountname.png)

### Endereço {#address}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Texto de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html).

Permite adicionar um campo de endereço internacional com o seguinte formato:

![dc_form_addressfield](assets/dc_form_addressfield.png)

O componente é configurado para uso imediato, mas você pode alterar a configuração, se necessário. Por exemplo, restrições podem ser adicionadas para os elementos individuais do endereço. Deixar campos vazios significa que as configurações padrão são usadas.

### Captcha {#captcha}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

O componente Captcha requer que o usuário digite uma sequência alfanumérica, conforme exibido na tela. A string é alterada a cada atualização.

![dc_form_captcha](assets/dc_form_captcha.png)

Você pode configurar vários parâmetros para esse componente, incluindo uma mensagem a ser exibida quando a cadeia de caracteres captcha for inválida.

### Grupos de caixa de seleção {#checkbox-group}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Opções de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html).

Uma caixa de seleção permite criar uma lista de uma ou mais caixas de seleção, várias das quais podem ser selecionadas ao mesmo tempo.

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

Você pode especificar vários parâmetros, incluindo um título, uma descrição e um nome de elemento. Usando os botões + e - você pode adicionar ou remover itens e, em seguida, posicioná-los com as setas para cima e para baixo.

>[!NOTE]
>
>Usando o **Caminho de Carregamento de Itens**, você pode pré-carregar a lista de grupos de caixas de seleção com valores.
>
>Consulte [Pré-Carregando Campos de Formulário com Vários Valores](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Detalhes do cartão de crédito {#credit-card-details}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Permite fornecer os campos necessários para inserir detalhes do cartão de crédito. Você pode configurá-lo para especificar os tipos de cartão aceitos e as informações necessárias (por exemplo, código de segurança).

![chlimage_1-100](assets/chlimage_1-100.png)

### Lista suspensa {#dropdown-list}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Opções de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html).

Uma lista suspensa pode ser configurada para fornecer ao usuário um intervalo de valores para seleção:

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

Você pode especificar um título e itens para serem exibidos na lista. Usando os botões + e -, você pode adicionar ou remover os itens da lista e, em seguida, posicioná-los com os botões Para cima e Para baixo. Você pode especificar se os usuários podem selecionar vários itens da lista e quaisquer itens que devem ser selecionados automaticamente na primeira vez que abrirem a lista (valores iniciais).

>[!NOTE]
>
>Usando o **Caminho de Carregamento de Itens**, você pode pré-carregar a lista suspensa com valores.
>
>Consulte [Pré-Carregando Campos de Formulário com Vários Valores](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Upload de arquivo {#file-upload}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O componente de carregamento de arquivo fornece ao usuário um mecanismo para selecionar e carregar um arquivo.

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>Você pode criar um componente de upload personalizado para carregar arquivos em um Sling Servlet. Para obter informações, consulte [Carregando arquivos para o Adobe Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-cloud-service-create-asset-servlet-for-uploading-small-files/td-p/404276).

### Campo oculto {#hidden-field}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal Formulário Oculto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-hidden.html).

Permite criar um campo oculto. Esses campos ocultos podem ser usados para vários propósitos. Por exemplo, quando você deve executar uma ação após enviar o formulário ou quando dados ocultos são necessários no pós-processamento.

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>Você também pode personalizar o formulário para mostrar ou ocultar componentes específicos do formulário de acordo com o valor de outros campos no formulário. Alterar a visibilidade de um campo de formulário é útil quando o campo é necessário somente em condições específicas.
>
>Consulte [Mostrando e ocultando componentes de formulário](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### Botão de imagem {#image-button}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do botão de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html).

Um botão de imagem permite criar um botão com sua própria imagem e texto:

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### Carregamento de imagem {#image-upload}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O componente de upload de imagem fornece ao usuário um mecanismo para selecionar e fazer upload de um arquivo de imagem.

![dc_form_imageupload](assets/dc_form_imageupload.png)

### Campo de link {#link-field}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

O campo link permite que o usuário especifique um URL:

![dc_form_link](assets/dc_form_link.png)

Usado com mais frequência para o formulário de evento do calendário, em que é usado para o campo URL/link de um evento.

### Campo de senha {#password-field}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Permite que o usuário insira sua senha:

![dc_form_password](assets/dc_form_password.png)

### Redefinição de senha {#password-reset}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Esse componente fornece ao usuário dois campos para:

* a entrada de uma senha
* entrada repetida da senha a ser verificada para confirmar se a entrada está correta.

Com as configurações padrão, o componente é exibido da seguinte maneira:

![dc_password_reset](assets/dc_password_reset.png)

### Grupo radial {#radio-group}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Opções de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html).

Um grupo de opções fornece uma lista de uma ou mais caixas de seleção, das quais apenas uma pode ser selecionada em um momento específico.

Você pode especificar o nome do elemento junto com um título e uma descrição. Usando os botões + e - você pode adicionar ou remover itens, posicioná-los com as setas para cima e para baixo e especificar um valor padrão, se necessário:

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>Usando o **Caminho de Carregamento de Itens**, você pode pré-carregar o grupo de opções com valores.
>
>Consulte [Pré-Carregando Campos de Formulário com Vários Valores](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### Botão de enviar {#submit-button}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do botão de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html).

Este componente permite criar um botão de envio, com o texto padrão:

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

Ou com seu próprio texto:

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### Campo de tags {#tags-field}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction).

Este campo permite selecionar tags:

![dc_form_tags_use](assets/dc_form_tags_use.png)

Você pode especificar vários parâmetros, incluindo os namespaces que podem ser usados, usando a guia especializada:

* **Campo de Marca**

   * **Namespaces permitidos**

      * **Geometrixx Outdoors**
      * **Fluxo de trabalho**
      * **Fórum**
      * **Banco de imagens**
      * **Geometrixx Media**
      * **Marcas Padrão**
      * **Marketing**
      * **Propriedades do ativo**
      * **Largura em pixels**
      * **Tamanho do Popup**

### Campo de texto {#text-field}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal de Texto de Formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html).

O campo de texto padrão pode ser configurado para o tamanho necessário e com seu próprio lead na mensagem:

![dc_form_text](assets/dc_form_text.png)

### Botões de envio do fluxo de trabalho {#workflow-submit-button-s}

>[!CAUTION]
>
>Este componente de base está obsoleto. Em vez disso, a Adobe recomenda usar o [Componente principal do botão de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html).

Permite criar um botão Submit para uso em um workflow.

![chlimage_1-101](assets/chlimage_1-101.png)
