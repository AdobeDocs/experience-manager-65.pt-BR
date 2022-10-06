---
title: Editar as propriedades da página
seo-title: Editing Page Properties
description: Defina as propriedades desejadas para uma página
seo-description: Define the required properties for a page
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: 9946bfd3c2701a37d13e6eb6b4c19562ef77d24c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 88%

---

# Editar as propriedades da página{#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Eles podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias.

### Básico {#basic}

* **Título**

   O título da página é exibido em vários locais. Por exemplo, a lista da guia **Sites** e as visualizações de cartão/lista dos **Sites**.

   Este é um campo obrigatório.

* **Tags**

   Aqui você pode adicionar ou remover as tags da página, atualizando a lista na caixa de seleção:

   * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o x.
   * Uma tag totalmente nova pode ser inserida, digitando o nome em uma caixa de seleção vazia.

      * A nova tag será criada ao apertar a tecla enter.
      * A nova tag será então exibida com uma pequena estrela à direita, indicando que é uma nova tag.
   * Com a funcionalidade suspensa, você pode selecionar a partir das tags existentes.
   * Um x será exibido ao passar o mouse em cima de uma entrada de tag na caixa de seleção, que pode ser usado para remover a tag desta página.

   Para obter mais informações sobre tags, acesse [Usar tags](/help/sites-authoring/tags.md).

* **Ocultar na navegação**

   Indica se a página está visível ou oculta na navegação de página do site resultante.

* **Marcas**

   Aplique uma identidade de marca consistente em todas as páginas, anexando uma descrição da marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior do [Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)

   * **Substituir** - marque essa opção para definir a descrição da marca nesta página.
      * O valor será herdado por qualquer página secundária, a menos que também tenha definidos seus valores para **Substituir**.
   * **Substituir valor** - o texto da descrição da marca a ser anexado ao título da página.
      * O valor é anexado ao título da página após um caractere de barra vertical, como &quot;Cycling Tuscany | Sempre pronto para a WKND&quot;
* **Título da página**

   Um título para ser usado na página. Normalmente usado pelos componentes do título. Caso esteja vazio, o **Título** será usado.

* **Titulo da Navegação**

   Você pode especificar um título separado para uso na navegação (por exemplo, caso deseje algo mais conciso). Caso esteja vazio, o **Título** será usado.

* **Legenda**

   Um subtítulo para usar na página.

* **Descrição**

   A sua descrição da página, finalidade ou qualquer outro detalhe que desejar adicionar.

* **Hora de ligar**

   A data e a hora em que a página publicada será ativada. Caso seja publicada, esta página será mantida inativa até o tempo especificado.

   Deixe estes campos vazios para as páginas que deseja publicar imediatamente (o cenário normal).

* **Hora de desligar**

   A hora em que a página publicada será desativada.

   Novamente, deixe esses campos em branco para ação imediata.

* **URL personalizada**

   Permite que você insira uma vanity URL para esta página, o que pode permitir que você tenha um URL menor e/ou mais expressivo.

   Por exemplo, se o URL personalizado estiver definido como `welcome`para a página identificada pelo caminho `/v1.0/startpage`para o site `http://example.com,` then `http://example.com/welcome`será a URL personalizada de `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URLs personalizadas:
   >
   >* Deve ser exclusiva, dessa forma, é necessário tomar cuidado para que o valor não seja utilizado por outra página.
   >* Não é compatível com padrões do regex.
   >* Não deve ser definido como uma página existente.


   Você também precisa configurar o Dispatcher para habilitar o acesso a URLs personalizadas. Consulte [Ativando o acesso a URLs personalizadas](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) para obter mais detalhes.

* **Redirecionar URL personalizada**

   Indica se você deseja que a página use a URL personalizada.

### Avançado  {#advanced}

* **Idioma**

   O idioma da página.

* **Raiz do idioma**

   Deve ser marcado se a página for a raiz de uma cópia de idioma.

* **Redirecionar**

   Indique a página de redirecionamento automático.

* **Design**

   Indique o [design](/help/sites-developing/designer.md) a ser usado para esta página.

* **Alias**

   Especifique um alias a ser usado com esta página.

   * Por exemplo: se você definir um pseudônimo de `private` para a página `/content/wknd/us/en/magazine/members-only`, essa página poderá ser acessada por meio de `/content/wknd/us/en/magazine/private`
   * A criação de um pseudônimo define a propriedade de `sling:alias` no nó da página, que afeta apenas o recurso, não o caminho do repositório.
   * As páginas acessadas por pseudônimos no editor não podem ser publicadas. As [Opções de publicação](/help/sites-authoring/publishing-pages.md) no editor só estão disponíveis para páginas acessadas por meio de seus caminhos de fato.
   * Para obter mais detalhes, consulte [Nomes de página localizados em SEO e Práticas recomendadas de gerenciamento de URL](/help/managing/seo-and-url-management.md#localized-page-names).

* **Herdado de &lt;*path*>**

   Indica se a página é herdada. e de onde.

* **Configuração na nuvem**

   O caminho para a configuração.

* **Modelos permitidos**

   [Defina a lista de modelos que estará disponível](/help/sites-authoring/templates.md#allowingatemplate) dentro desta sub-ramificação.

* **Habilitar** (Requisito de autenticação)

   Habilite (ou desabilite) o uso de autenticação para acessar a página.

   >[!NOTE]
   >
   >Os grupos de usuários fechados para a página são definidos na guia **[Permissões](/help/sites-authoring/editing-page-properties.md#permissions)**.

   >[!CAUTION]
   >
   >O **[Permissões](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permite a edição de configurações CUG com base na presença do `granite:AuthenticationRequired` mistura. Se as permissões de página forem configuradas usando configurações obsoletas de CUG, com base na presença de `cq:cugEnabled` , uma mensagem de aviso será exibida em **Requisito de autenticação** e a opção não será editável, nem a variável [Permissões](/help/sites-authoring/editing-page-properties.md#permissions) ser editável.
   >
   >
   >Nesse caso, as permissões de CUG devem ser editadas na [interface do usuário clássica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Página de logon**

   A página para ser usada para logon.

* **Exportar configuração**

   Especifique uma configuração de exportação.

### Miniatura  {#thumbnail}

Exibe a imagem de miniatura da página. É possível:

* **Gerar pré-visualização**

   Gere uma visualização da página para usar como miniatura.

* **Fazer upload de imagem**

   Carregue uma imagem para usar como miniatura.

* **Selecionar imagem**

   Selecione um ativo existente para usar como miniatura.

* **Reverter**

   Esta opção fica disponível após você ter feito uma alteração na miniatura. Se você não quiser manter sua alteração, poderá reverter essa alteração antes de salvar.

### Redes sociais {#social-media}

* **Compartilhamento em rede social**

   Define as opções de compartilhamento disponíveis na página. Expõe as opções disponíveis para o [Componente de compartilhamento principal](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **Permitir o compartilhamento de usuário para Facebook**
   * **Permitir o compartilhamento de usuário para Pinterest**
   * **Variação preferida de XF**
Define a variação do fragmento de experiência usada para gerar metadados para a página

### Cloud Services {#cloud-services}

* **Cloud Services**

   Defina as propriedades para os [serviços em nuvem](/help/sites-developing/extending-cloud-config.md).

### Personalização {#personalization}

* **Configurações do ContextHub**

   Selecione [Configuração do ContextHub](/help/sites-developing/ch-configuring.md) e [ Caminho de segmentos](/help/sites-administering/segmentation.md).

* **Configuração de direcionamento**

   Selecione uma [Marca para especificar um escopo de direcionamento](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >Para selecionar essa opção, é necessário que a conta de usuário esteja no `Target Adminstrators`grupo.

### Permissões  {#permissions}

* **Permissões**

   Nesta guia, você pode:

   * [Adicionar permissões](/help/sites-administering/user-group-ac-admin.md)
   * [Editar grupo de usuários fechado](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Exibir as [permissões efetivas](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >O **Permissões** permite a edição de configurações CUG com base na presença do `granite:AuthenticationRequired` mistura. Se as permissões de página forem configuradas usando configurações obsoletas de CUG, com base na presença de `cq:cugEnabled` , uma mensagem de aviso será exibida e as permissões de CUG não serão editáveis, assim como o Requisito de autenticação na [Avançado](/help/sites-authoring/editing-page-properties.md#advanced) poderá ser editada.
   >
   >
   >Nesse caso, as permissões de CUG devem ser editadas na [interface do usuário clássica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >O guia Permissões não permite a criação de grupos vazios de CUG, que podem ser úteis como uma maneira simples de negar o acesso para cada usuário. Para fazer isso, use o CRX Explorer. Consulte o documento [Administração de usuários, grupos e direitos de acesso](/help/sites-administering/user-group-ac-admin.md) para obter mais informações.

### Blueprint {#blueprint}

* **Blueprint**

   Defina as propriedades para uma página do Blueprint no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas no Live Copy.

### Live Copy  {#live-copy}

* **Live Copy**

   Defina as propriedades para uma página de Live Copy no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas do Blueprint.

### Estrutura do site  {#site-structure}

* Forneça links para páginas que oferecem funcionalidade em todo o site, como a **Página de inscrição**, a **Página offline**, entre outras.

## Editar as propriedades da página {#editing-page-properties-1}

É possível definir as propriedades de página:

* No console **Sites**:

   * [Criação de uma nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page) (um subconjunto das propriedades)

   * Ao clicar ou tocar em **Propriedades**

      * Para uma página única
      * Para várias páginas (apenas um subconjunto das propriedades está disponível para edição em massa)

* No editor de páginas:

   * Ao usar **Informações da página** (em seguida, **Abrir propriedades**)

### No console Sites - Página única {#from-the-sites-console-single-page}

Ao clicar ou tocar em **Propriedades** para definir as propriedades da página:

1. Usando o console **Sites**, navegue até o local da página no qual deseja visualizar e editar as propriedades.

1. Selecione a opção **Propriedades da exibição** para a página desejada usando uma das seguintes opções:

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-authoring/basic-handling.md#selectionmode)

   As propriedades da página serão exibidas usando as guias adequadas.

1. Exiba ou edite as propriedades conforme necessário.

1. Em seguida, clique em **Salvar** para salvar as atualizações, e em **Fechar** para retornar ao console.

### Ao editar uma página {#when-editing-a-page}

Ao editar uma página, você pode usar as **Informações da página** para definir as propriedades da página:

1. Abra a página na qual deseja editar as propriedades.

1. Selecione o ícone **Informações da página** para abrir o menu de seleção:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Selecionar **Abrir propriedades** e uma caixa de diálogo será aberta permitindo que você edite as propriedades, escolhidas através da guia apropriada. Os seguintes botões também estão disponíveis à direita da barra de ferramentas:

   * **Cancelar**
   * **Salvar e fechar**

1. Use o botão **Salvar e fechar** para salvar as alterações.

### No console Sites - Várias páginas {#from-the-sites-console-multiple-pages}

No console **Sites**, é possível selecionar várias páginas e usar **Propriedades de exibição** para exibir e/ou editar as propriedades da página. Isso é conhecido como edição em massa das propriedades da página.

>[!NOTE]
>
>A edição em massa de propriedades também está disponível no Assets. É muito semelhante, mas difere em alguns pontos. Consulte [Editar propriedades de vários ativos](/help/assets/metadata.md) para obter detalhes.
>
>Também existe o [Editor de itens em massa](/help/sites-administering/bulk-editor.md), que permite que você pesquise o conteúdo de várias páginas usando o GQL (Google Query Language) e, em seguida, editar o conteúdo diretamente no editor de itens em massa antes de salvar as alterações para as páginas de origem.

É possível selecionar várias páginas para a edição de itens em massa através de diversos métodos, incluindo:

* Ao navegar no console **Sites**
* Após usar a opção **Pesquisar** para localizar um conjunto de páginas

![epp-01](assets/epp-01.png)

Após selecionar as páginas e, em seguida, clicar ou tocar na opção **Propriedades**, as propriedades em massa serão mostradas:

![epp-02](assets/epp-02.png)

Só é possível fazer a edição de itens em massa nas páginas que:

* Compartilham o mesmo tipo de recurso
* Não fazem parte de uma live copy

   * Uma mensagem será mostrada quando as propriedades forem abertas, se qualquer página estiver em uma live copy.

Depois de entrar na edição de itens em massa é possível:

* **Exibir**

   Ao exibir as Propriedades da página de várias páginas é possível visualizar:

   * Uma lista das páginas impactadas

      * Você pode selecionar/desmarcar conforme necessário
   * Guias

      * As propriedades são ordenadas em guias, como ao exibir as propriedades para uma página única.
   * Um subconjunto de propriedades

      * As propriedades que estão disponíveis em todas as páginas selecionadas e tenham sido explicitamente definidas como disponíveis para a edição de itens em massa estão visíveis.
      * Se você reduzir a seleção de página para uma página, em seguida, todas as propriedades ficarão visíveis.
   * Propriedades comuns com um valor comum

      * Apenas as propriedades com um valor comum são mostradas no modo de Exibição.
      * Quando o campo tem vários valores (por exemplo, Tags), eles só serão exibidos quando *todos* forem comuns. Se apenas alguns forem comuns, eles só serão exibidos durante a edição.

   Quando não existirem propriedades com um valor comum, uma mensagem será exibida.

* **Editar**

   Ao editar as Propriedades da página em várias páginas:

   * Você pode atualizar os valores nos campos disponíveis.

      * Os novos valores serão aplicados a todas as páginas selecionadas ao escolher **Concluído**.
      * Quando o campo tem vários valores (por exemplo, Tags), você pode acrescentar um novo valor ou remover um valor comum.
   * Os campos que são comuns, mas têm valores diferentes em várias páginas, serão indicados com um valor especial; como o texto `<Mixed Entries>`. Para evitar a perda de dados, alguns cuidados devem ser tomados ao editar os campos.


>[!NOTE]
>
>O componente da página pode ser configurado para especificar os campos disponíveis para edição de itens em massa. Consulte [Configurar sua página para a edição de itens em massa das propriedades da página](/help/sites-developing/bulk-editing.md).
