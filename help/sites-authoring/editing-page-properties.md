---
title: Editar as propriedades da página
description: Defina as propriedades necessárias para uma página no Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
mini-toc-levels: 2
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 37%

---


# Editar as propriedades da página{#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Isso pode variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não, e as informações da live copy ficam disponíveis conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias.

### Básico {#basic}

#### Título e tags {#tile}

* **Título** - O título da página é exibido em vários locais
   * Por exemplo, a lista de guias **Sites** e as exibições de cartão/lista **Sites**.
   * Este campo é obrigatório.
* **Marcas** - Aqui é possível adicionar ou remover marcas da página, atualizando a lista na caixa de seleção.
   * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o ícone “x”.
   * Uma nova tag pode ser inserida digitando o nome em uma caixa de seleção vazia.
      * A nova tag é criada ao pressionar Enter.
      * A nova tag é mostrada com uma pequena estrela à direita, indicando que é uma nova tag.
   * Com o menu suspenso, é possível selecionar entre tags existentes.
   * Um “x” é exibido ao passar o mouse sobre uma entrada de tag na caixa de seleção, e esse ícone pode ser usado para remover a tag desta página.
   * Para obter mais informações sobre marcas, consulte [Usando Marcas.](/help/sites-authoring/tags.md)
* **Ocultar na Navegação** - Indica se a página está visível ou oculta na navegação de página do site resultante

#### Identidade visual {#branding}

Aplique uma identidade de marca consistente em todas as páginas, anexando uma descrição da marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior do [Componentes principais.](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction)

* **Sobrepor**: marque essa opção para definir a descrição da marca nesta página.
   * O valor é herdado por todas as páginas filhas, a menos que elas também tenham seus valores de **Sobreposição** definidos.
* **Substituir valor** - O texto da descrição da marca a ser anexado ao título da página
   * O valor é anexado ao título da página após um caractere de barra vertical, como `Cycling Tuscany | Always ready for the WKND`

#### Mais títulos e descrições {#more}

* **Título da página** - Um título a ser usado na página
   * Normalmente usado por componentes de título
   * Se estiver vazio, a variável **Título** é usada.
* **Título de Navegação** - Você pode especificar um título separado para usar na navegação (por exemplo, se desejar algo mais conciso).
   * Se estiver vazio, a variável **Título** é usada.
* **Subtítulo** - Uma subtítulo para usar na página
* **Descrição** - Sua descrição da página, a finalidade dela ou qualquer outro detalhe que desejar adicionar

#### Horário ligado/desligado {#on-time}

O horário de ativação/desativação de uma página é uma maneira conveniente de ocultar temporariamente um conteúdo já publicado. O conteúdo permanece na instância de publicação quando está desativado. Desativar uma página não cancela a publicação do conteúdo.

* **Momento da ativação**: a data e a hora em que a página publicada ficará visível (renderizada) no ambiente de publicação. A página deve estar publicada, seja manualmente ou por replicação automática pré-configurada.

   * Se já [publicada](/help/sites-authoring/publishing-pages.md), esta página estará disponível na instância de publicação, mas permanecerá inativa (oculta) até a renderização no horário especificado.
   * Se não for publicada e [estiver configurada para replicação automática](/help/sites-deploying/replication.md), a página será publicada automaticamente e, em seguida, renderizada no horário especificado.
   * Se não for publicada e não estiver configurada para replicação automática, a página não será publicada automaticamente. Um 404 é exibido quando é feita uma tentativa de acessar a página.

* **Momento da desativação**: semelhante e frequentemente usado em combinação com o **Momento da ativação**, define o momento em que a página publicada fica oculta no ambiente de publicação.

Deixe esses campos (**Momento da ativação** e **Momento da desativação**) vazios para páginas que deseja publicar e que estão disponíveis imediatamente e no ambiente de publicação até que sejam desativadas (o cenário normal).

>[!NOTE]
>Se o **Momento da ativação** ou **Momento da desativação** estiverem no passado e a replicação automática estiver configurada, então a ação relevante será acionada imediatamente.

>[!TIP]
>
>Os tempos de ativação/desativação lidam estritamente com o conteúdo já publicado (manualmente ou por replicação automática). Por esse motivo, fluxos de trabalho de publicação, como aqueles para aprovação de conteúdo, não são acionados por horários de ativação/desativação e horários de ativação/desativação não afetam o status de publicação da página. Por esse motivo, os horários de ativação/desativação são mais apropriados para mostrar/ocultar temporariamente um conteúdo já aprovado e publicado.
>
>Se quiser publicar conteúdo novo com todos os fluxos de trabalho associados ou remover totalmente (cancelar a publicação do conteúdo) do site, considere [gerenciar sua publicação.](/help/sites-authoring/publishing-pages.md#manage-publication)

#### URL personalizado {#vanity-url}

Insira um URL personalizado para esta página, o que pode permitir que você tenha um URL mais curto e/ou mais expressivo.

Por exemplo, se a URL personalizada estiver definida como `welcome` para a página identificada pelo caminho `/v1.0/startpage` para o site `http://example.com,`, `http://example.com/welcome` será a URL personalizada de `http://example.com/content/v1.0/startpage`

>[!CAUTION]
>
>URLs personalizados:
>
>* Deve ser única.
>* Não é compatível com padrões de regex.
>* Não deve ser definido como uma página existente.

Configure o Dispatcher para habilitar o acesso a URLs personalizados. Consulte [Habilitando o acesso a URLs personalizados](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#enabling-access-to-vanity-urls-vanity-urls) para obter mais detalhes.

* **Adicionar** - Toque ou clique para adicionar uma URL personalizada.
* **Remover** - Toque ou clique para remover uma URL personalizada.
  **Redirecionar URL personalizado** - Indica se você deseja que a página use a URL personalizado ou redirecione para a URL real da página

### Avançado {#advanced}

#### Configurações {#settings}

* **Idioma** - o idioma da página
* **Raiz de idioma** - deve ser marcado se a página for a raiz de uma cópia no idioma de destino
* **Redirecionar** - indica a página de redirecionamento automático para a página atual. 
* **Design** - Indica o [design](/help/sites-developing/designer.md) a ser usado para esta página.
* **Pseudônimo** - especifica um pseudônimo para ser usado com esta página
   * Por exemplo: se você definir um pseudônimo de `private` para a página `/content/wknd/us/en/magazine/members-only`, essa página poderá ser acessada por meio de `/content/wknd/us/en/magazine/private`
   * A criação de um pseudônimo define a propriedade de `sling:alias` no nó da página, que afeta apenas o recurso, não o caminho do repositório.
   * Páginas acessadas por pseudônimos no editor não podem ser publicadas. As [Opções de publicação](/help/sites-authoring/publishing-pages.md) no editor só estão disponíveis para páginas acessadas por meio de seus caminhos de fato.
   * Para obter mais detalhes, consulte [Nomes de página localizados em SEO e Práticas recomendadas de gerenciamento de URL](/help/managing/seo-and-url-management.md#localized-page-names).

#### Configuração {#configuration}

* **Herdado de &lt;*caminho*>** - Habilitar/desabilitar a herança da **Configuração da Nuvem** para a página
* **Configuração na nuvem** - o caminho para a configuração

#### Configurações do modelo {#templates}

* **Modelos permitidos**: [define a lista de modelos que estão disponíveis](/help/sites-authoring/templates.md#allowingatemplate) dentro desta sub-ramificação

#### Requisitos de autenticação {#authentication}

* **Habilitar** - Habilita (ou desabilita) o uso de autenticação para que você possa acessar a página
* **Página de logon** - a página a ser usada para logon

>[!NOTE]
>
>Os grupos de usuários fechados para a página são definidos na guia **[Permissões](/help/sites-authoring/editing-page-properties.md#permissions)**.

>[!CAUTION]
>
>A guia **[Permissões](#permissions)** permite editar configurações CUG com base na presença do mixin `granite:AuthenticationRequired`. Se as permissões de página forem configuradas usando configurações CUG obsoletas, com base na presença da propriedade `cq:cugEnabled`, uma mensagem de aviso será mostrada em **Requisito de autenticação** e a opção não será editável, nem as [Permissões](/help/sites-authoring/editing-page-properties.md#permissions) serão editáveis.
>
>
>Nesse caso, as permissões CUG devem ser editadas na [interface clássica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

#### Exportar {#export}

* **Configuração** - Especifica uma configuração de exportação

#### SEO {#seo}

* **URL canônica** - Usada para substituir a URL canônica da página
   * Se deixado em branco, o URL da página será o URL canônico.
* **Marcas de robôs** - Use a lista suspensa para selecionar as marcas de robôs e controlar o comportamento dos rastreadores do mecanismo de pesquisa
   * Algumas opções são conflitantes entre si, nesse caso, a opção mais permissiva tem precedência.
* **Gerar Mapa do Site** - Quando selecionado, um `sitemap.xml` é gerado para esta página e seus descendentes.

### Imagens {#images}

#### Imagem em destaque {#featured-image}

Esta seção é usada para selecionar e configurar a imagem a ser apresentada. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

* **Imagem** - Você pode **Escolher** um ativo ou procurar um arquivo para carregar e, em seguida, **Editar** ou **Limpar** a imagem selecionada.
* **Texto Alternativo** - Texto usado para representar o significado e/ou a função da imagem, comumente usado por leitores de tela
* **Herdar - Valor retirado do ativo DAM** - Quando marcado, o texto alternativo é preenchido com o valor dos `dc:description`metadados no DAM.

#### Miniatura  {#thumbnail}

Esta seção é usada para selecionar e configurar a miniatura da imagem para a página. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

* **Gerar visualização** - Gera uma visualização da página que você deseja usar como miniatura
* **Carregar Imagem** - Carrega uma imagem que você deseja usar como miniatura
* **Selecionar imagem** - Seleciona um Ativo existente que você deseja usar como miniatura
* **Reverter** - Esta opção fica disponível após você ter alterado a miniatura. Se você não quiser manter a alteração, poderá revertê-la antes de salvar.

### Cloud Services {#cloud-services}

* **Configurações do Cloud Service** - Define qual configuração é usada para os serviços em nuvem na página
* **Herdado de** - Para Live Copies e Cópias de idioma, as configurações de nuvem são herdadas por padrão do Blueprint.
   * Desmarcar para substituir a herança

### Personalização {#personalization}

#### Configurações do ContextHub {#contexthub}

* **Herdado de** - As configurações do ContextHub são herdadas por padrão da página pai.
   * Desmarque para substituir a herança.
* **Caminho do ContextHub** - Seleciona a [Configuração do ContextHub](/help/sites-developing/ch-configuring.md)
* **Caminho dos segmentos** - Seleciona o [Caminho dos segmentos](/help/sites-administering/segmentation.md).

#### Configuração de direcionamento {#targeting}

Selecione uma [Marca para especificar um escopo para Direcionamento.](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>Para selecionar essa opção, é necessário que a conta de usuário esteja no `Target Adminstrators`grupo.

### Permissões  {#permissions}

Use a guia **Permissões** para definir quais usuários, grupos ou [grupos de usuários fechados (CUGs)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=pt-BR) podem acessar e/ou modificar a página.

* [Adicionar permissões](/help/sites-administering/user-group-ac-admin.md)
* [Editar grupo de usuários fechado](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
* Exibir as [Permissões ativas](/help/sites-administering/user-group-ac-admin.md)

>[!CAUTION]
>
>A guia **Permissões** permite editar configurações CUG com base na presença do mixin `granite:AuthenticationRequired`. Se as permissões de página forem configuradas usando configurações CUG obsoletas, com base na presença da propriedade `cq:cugEnabled`, uma mensagem de aviso será exibida e as permissões CUG não serão editáveis, nem o Requisito de Autenticação na guia [Avançado](/help/sites-authoring/editing-page-properties.md#advanced) será editável.
>
>
>Nesse caso, as permissões CUG devem ser editadas na [interface clássica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

>[!NOTE]
>
>A guia Permissões não permite a criação de grupos CUG vazios, o que pode ser útil como uma maneira simples de negar acesso a todos os usuários. Para fazer isso, o CRX Explorer deve ser usado. Consulte o documento [Administração de Usuários, Grupos e Direitos de Acesso](/help/sites-administering/user-group-ac-admin.md) para obter mais informações.

### Blueprint {#blueprint}

Essa guia só fica visível para páginas que servem como blueprints. Os blueprints servem como base para as Live Copies que fazem parte do [Gerenciamento de vários sites.](/help/sites-administering/msm.md)

* **Implantação** - Inicia uma implantação do conteúdo do blueprint nas Live Copies
* **Visão geral da Live Copy** - abre uma janela para navegar pela estrutura da página da Live Copy
* **Live Copies atuais** - Uma lista de páginas baseadas na (ou seja, são Live Copies da) página de blueprint selecionada
* **Configuração de implantação** - Define a configuração de implantação da página

### Live Copy {#live-copy}

Essa guia só fica visível para páginas configuradas como Live Copies. Assim como em [blueprints,](#blueprint) Live Copies fazem parte do [Gerenciamento de Vários Sites.](/help/sites-administering/msm.md)

* **Sincronizar** - Sincroniza o Live Copy com o blueprint, mantendo as modificações locais
* **Redefinir** - Redefine o Live Copy para o estado de blueprint, removendo as modificações locais
* **Suspender** - Suspende modificações adicionais de implantação na Live Copy
* **Desanexar** - Desanexa a Live Copy do blueprint

#### Origem {#source}

* Exibe o caminho do blueprint para esta Live Copy

#### Status {#status}

* Lista o status atual da Live Copy da página

#### Configuração {#live-copy-config}

* **Herança da Live Copy** - Se marcada, a configuração da Live Copy terá efeito em todas as páginas secundárias.
* **Herdar configurações de implantação da principal** - Se marcado, a configuração de implantação é herdada da página principal.
* **Escolher configuração de implantação**: define as circunstâncias em que as modificações são propagadas a partir do Blueprint e só estão disponíveis quando **Herdar configurações de implantação da página principal** não está selecionado
* **Lista de caminhos excluídos**

## Editar as propriedades da página {#editing-page-properties-1}

É possível definir as propriedades de página:

* No console **Sites**:

   * [Criando uma página](/help/sites-authoring/managing-pages.md#creating-a-new-page) (um subconjunto das propriedades)

   * Ao clicar ou tocar em **Propriedades**

      * Para uma única página
      * Para várias páginas (somente um subconjunto das propriedades está disponível para edição em massa)

* No editor de páginas:

   * Ao usar **Informações da página** (em seguida, **Abrir propriedades**)

### No console Sites - Página única {#from-the-sites-console-single-page}

Ao clicar ou tocar em **Propriedades** para definir as propriedades da página:

1. Usando o console **Sites**, navegue até o local da página no qual deseja visualizar e editar as propriedades.

1. Selecione a opção **Propriedades da exibição** para a página desejada usando uma das seguintes opções:

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-authoring/basic-handling.md#selectionmode)

   As propriedades da página são exibidas usando as guias adequadas.

1. Exiba ou edite as propriedades conforme necessário.

1. Em seguida, use **Salvar** para salvar suas atualizações, seguido por **Fechar** para que você possa retornar ao console.

### Ao editar uma página {#when-editing-a-page}

Ao editar uma página, você pode usar **Informações da página** para definir as propriedades da página:

1. Abra a página na qual deseja editar as propriedades.

1. Selecione o ícone **Informações da página** para abrir o menu de seleção:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Selecione **Abrir propriedades** e uma caixa de diálogo será aberta, permitindo que você edite as propriedades, classificadas pela guia apropriada. Os seguintes botões também estão disponíveis à direita da barra de ferramentas:

   * **Cancelar**
   * **Salvar e fechar**

1. Use o botão **Salvar e fechar** para salvar as alterações.

### No console Sites - Várias páginas {#from-the-sites-console-multiple-pages}

No console **Sites**, é possível selecionar várias páginas e usar **Propriedades de Exibição** para exibir e/ou editar as propriedades da página. Isso é conhecido como edição em massa das propriedades da página.

>[!NOTE]
>
>A edição em massa de propriedades também está disponível no Assets. É semelhante, mas difere em alguns pontos. Consulte [Editando Propriedades de Várias Assets](/help/assets/metadata.md) para obter detalhes.
>
>Há também o [Editor de itens em massa](/help/sites-administering/bulk-editor.md). Esse editor permite que você pesquise o conteúdo de várias páginas usando o GQL (Google Query Language) e, em seguida, edite o conteúdo diretamente usando o Editor de itens em massa antes de salvar as alterações nas páginas de origem.

Você pode selecionar várias páginas para a edição em massa por meio de vários métodos, incluindo:

* Ao navegar pelos consoles dos **Sites**
* Depois de usar a função **Pesquisar** para localizar um conjunto de páginas

![epp-01](assets/epp-01.png)

Após selecionar as páginas e clicar ou tocar na **opção Propriedades**, as propriedades em massa serão exibidas:

![epp-02](assets/epp-02.png)

Só é possível editar em massa as páginas que:

* Compartilham o mesmo tipo de recurso
* Não fazem parte de uma live copy

   * Se alguma das páginas estiver em uma live copy, uma mensagem será exibida quando as propriedades forem abertas.

Depois de entrar na Edição em massa, você pode fazer o seguinte:

* **Exibir**

  Ao visualizar Propriedades de página para várias páginas, você pode ver o seguinte:

   * Uma lista das páginas afetadas

      * Você pode marcar/desmarcar se necessário

   * Guias

      * Assim como ao visualizar propriedades de uma única página, as propriedades são ordenadas em guias.

   * Um subconjunto de propriedades

      * As propriedades que estão disponíveis em todas as páginas selecionadas e tenham sido explicitamente definidas como disponíveis para a edição de itens em massa estão visíveis.
      * Se você reduzir a seleção de página para uma página, em seguida, todas as propriedades ficarão visíveis.

   * Propriedades comuns com um valor comum

      * Apenas as propriedades com um valor comum são mostradas no modo de Exibição.
      * Quando o campo tem vários valores (por exemplo, Marcas), eles só são exibidos quando *todos* são comuns. Se apenas alguns forem comuns, eles só serão exibidos durante a edição.

  Quando não existirem propriedades com um valor comum, uma mensagem será exibida.

* **Editar**

  Ao editar as Propriedades da página para várias páginas:

   * Você pode atualizar os valores nos campos disponíveis.

      * Os novos valores são aplicados a todas as páginas selecionadas ao clicar em **Concluído**.
      * Quando o campo tem vários valores (por exemplo, Tags), você pode anexar um novo valor ou remover um valor comum.

   * Os campos que são comuns, mas têm valores diferentes em várias páginas, são indicados com um valor especial, como o texto `<Mixed Entries>`.

>[!NOTE]
>
>O componente da página pode ser configurado para especificar os campos disponíveis para edição de itens em massa. Consulte [Configurar sua página para a edição de itens em massa das propriedades da página](/help/sites-developing/bulk-editing.md).
