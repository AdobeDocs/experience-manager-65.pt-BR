---
title: Trabalho com fragmentos de conteúdo
seo-title: Trabalho com fragmentos de conteúdo
description: Saiba como os Fragmentos de conteúdo permitem projetar, criar, preparar e usar conteúdo independente da página.
seo-description: Saiba como os Fragmentos de conteúdo permitem projetar, criar, preparar e usar conteúdo independente da página.
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
feature: Fragmentos de conteúdo
role: Profissional de negócios, Administrador
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 7%

---


# Trabalho com fragmentos de conteúdo{#working-with-content-fragments}

Os Fragmentos de conteúdo do Adobe Experience Manager (AEM) permitem que você crie, crie, prepare e [publique conteúdo independente da página](/help/sites-authoring/content-fragments.md). Eles permitem que você prepare conteúdo pronto para uso em vários locais/em vários canais.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo do Sling (JSON) AEM componentes principais. Esta forma de delivery:

* permite usar o componente para gerenciar quais elementos de um fragmento fornecer
* permite a entrega em massa, adicionando vários componentes principais do fragmento de conteúdo na página que está sendo usada para a entrega da API

Esta e as seguintes páginas abordam as tarefas de criação, configuração e manutenção dos fragmentos de conteúdo:

* [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)  - crie fragmentos de conteúdo; em seguida, edite, publique e faça referência
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)  - permitindo, criando e definindo seus modelos
* [Variações - Criação do conteúdo do fragmento](/help/assets/content-fragments/content-fragments-variations.md)  - crie o conteúdo do fragmento e crie variações do Principal
* [Marcação](/help/assets/content-fragments/content-fragments-markdown.md)  - uso da sintaxe de marcação para o fragmento
* [Uso de conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md)  - adição do conteúdo associado
* [Metadados - Propriedades do fragmento](/help/assets/content-fragments/content-fragments-metadata.md)  - visualização e edição das propriedades do fragmento

>[!NOTE]
>
>Essas páginas devem ser lidas junto com [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).

O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo de delivery, como:

* Canal físico; por exemplo, desktop, móvel.
* Forma de entrega num canal físico; por exemplo, a &quot;página de detalhes do produto&quot;, &quot;página de categoria do produto&quot; para desktop, ou &quot;web móvel&quot;, &quot;aplicativo móvel&quot; para dispositivos móveis.

No entanto, você (provavelmente) não deseja usar exatamente o mesmo conteúdo para todos os canais; é necessário otimizar o conteúdo de acordo com o canal específico.

Fragmentos de conteúdo permitem:

* Considere como atingir públicos-alvo com eficiência em todos os canais.
* Crie e gerencie conteúdo editorial neutro ao canal.
* Crie pools de conteúdo para um intervalo de canais.
* Desenvolva variações de conteúdo para canais específicos.
* Adicione imagens ao texto inserindo ativos (fragmentos de mídia mista).

Esses fragmentos de conteúdo podem ser montados para proporcionar experiências em uma variedade de canais.

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os Serviços de conteúdo AEM foram projetados para generalizar a descrição e a entrega de conteúdo de/para AEM além de um foco nas páginas da Web.

Eles fornecem a entrega de conteúdo para canais que não são páginas da Web tradicionais AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos móveis nativos
* outros canais e pontos de contato externos ao AEM

O delivery é feito no formato JSON.

AEM Fragmentos de conteúdo podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter vários tipos de conteúdo; incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Juntamente com os recursos de exportação JSON de AEM componentes principais, esse conteúdo estruturado pode ser usado para fornecer conteúdo AEM a canais diferentes de páginas AEM.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)** são recursos diferentes no AEM:
>* **Fragmentos de conteúdo** são conteúdos editoriais, principalmente texto e imagens relacionadas. Eles são puro conteúdo, sem design e layout.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.

>
>
Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte também [Entendendo fragmentos de conteúdo e fragmentos de experiência em AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html).

>[!CAUTION]
>
>Os fragmentos de conteúdo não estão disponíveis na interface clássica.
>
>O componente Fragmento do conteúdo pode ser visualizado no sidekick da interface clássica, mas outras funcionalidades não estão disponíveis.

>[!NOTE]
>
>AEM também suporta a tradução do conteúdo do fragmento. Consulte [Criação de projetos de tradução para fragmentos de conteúdo](/help/assets/creating-translation-projects-for-content-fragments.md) para obter mais informações.

## Tipos de fragmento de conteúdo {#types-of-content-fragment}

Os fragmentos de conteúdo podem ser:

* Fragmentos simples
Elas não têm estrutura predefinida. Eles contêm apenas texto e imagens.
Elas são baseadas no modelo de Fragmento simples .

* Fragmentos que contêm conteúdo estruturado
Elas são baseadas em um [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md), que predefine uma estrutura para o fragmento resultante.
Eles também podem ser usados para realizar serviços de conteúdo usando o Exportador JSON.

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Armazenado como **Assets**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos no console **Assets**.
   * Criado e editado no Editor de fragmento de conteúdo.

* Usado no [editor de página por meio do componente do Fragmento de conteúdo](/help/sites-authoring/content-fragments.md) (componente de referência):

   * O componente **Fragmento de conteúdo** está disponível para os autores da página. Ele permite referenciar e fornecer o fragmento de conteúdo necessário no formato HTML ou JSON.

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* São sem layout ou design (alguma formatação de texto é possível no modo Rich Text).
* Conter uma ou mais partes [componentes](#constituent-parts-of-a-content-fragment).
* Pode [conter ou ser conectado a imagens](#fragments-with-visual-assets).
* Pode usar [conteúdo intermediário](#in-between-content-when-page-authoring-with-content-fragments) quando referenciado em uma página.

* São independentes do mecanismo de delivery (ou seja, página, canal).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para dar aos autores mais controle do conteúdo, as imagens podem ser adicionadas e/ou integradas a um fragmento de conteúdo.

Os ativos podem ser usados com um fragmento de conteúdo de várias maneiras; cada um com a sua própria vantagem:

* **Inserir** ativo em um fragmento (fragmentos de mídia mista)

   * São parte integrante do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Defina a posição do ativo.
   * Consulte [Inserir ativos em seu fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) no Editor de fragmentos para obter mais informações.

   >[!NOTE]
   >
   >Os ativos visuais inseridos no próprio fragmento de conteúdo são anexados ao parágrafo anterior. Quando o fragmento é adicionado a uma página, esses ativos são movidos em relação a esse parágrafo quando o conteúdo intermediário é adicionado.

* **Conteúdo associado**

   * Estão conectadas a um fragmento; mas não é uma parte fixa do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Permite alguma flexibilidade para posicionamento.
   * São facilmente disponíveis para uso (como conteúdo intermediário) ao usar o fragmento em uma página.
   * Consulte [Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obter mais informações.

* Ativos disponíveis no **navegador Ativos** do editor de página

   * Permitir flexibilidade total para a seleção de um ativo.
   * Permite alguma flexibilidade para posicionamento.
   * Não fornece o conceito de aprovação para um fragmento específico.
   * Consulte [Navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser) para obter mais informações.

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Para fragmentos com conteúdo estruturado, use um modelo de conteúdo para criar o fragmento de conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de uma variedade de tipos de dados.
   * Para fragmentos simples:

      * O conteúdo é mantido em um (ou mais) campo(s) de texto de várias linhas ou elemento(s).
      * Os elementos são definidos no modelo do fragmento (não pode ser definido ao criar o fragmento, consulte [Modelos de fragmento de conteúdo](/help/sites-developing/content-fragment-templates.md)).

* **Parágrafos de fragmento**

   * Blocos de texto, que são:

      * separados por espaços verticais (retorno de carro)
      * em elementos de texto de várias linhas; em fragmentos simples ou estruturados
   * Nos modos [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Marcação](/help/assets/content-fragments/content-fragments-variations.md#markdown), um parágrafo pode ser formatado como um cabeçalho, nesse caso ele e o parágrafo a seguir pertencem como uma unidade.

   * Ative o controle de conteúdo durante a criação da página.


* **Ativos inseridos em um fragmento (Fragmentos de mídia mista)**

   * Ativos (imagens) inseridos no fragmento real e usados como conteúdo interno de um fragmento.
   * São incorporados ao sistema de parágrafo do fragmento.
   * Pode ser formatado quando o fragmento [é usado/referenciado em uma página](/help/sites-authoring/content-fragments.md).
   * Só pode ser adicionado, excluído ou movido para dentro de um fragmento usando o editor de fragmentos. Essas ações não podem ser feitas no editor de páginas.
   * Só podem ser adicionados, excluídos ou movidos dentro de um fragmento usando o formato [Rich Text no editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Só podem ser adicionados a elementos de texto de várias linhas (qualquer tipo de fragmento).
   * São anexadas ao texto anterior (parágrafo).

   >[!CAUTION]
   >
   >Pode ser (inadvertidamente) removido de um fragmento ao alternar para o formato Texto simples.

   >[!NOTE]
   >
   >Os ativos também podem ser adicionados como [conteúdo adicional (intermediário)](/help/sites-authoring/content-fragments.md#using-associated-content) ao usar um fragmento em uma página; usando Conteúdo associado ou ativos no navegador Ativos.

* **Conteúdo associado**

   * Esse é um conteúdo externo a um fragmento, mas com relevância editorial para ele. Geralmente, imagens, vídeos ou outros fragmentos.
   * Os ativos individuais dentro da coleção estão disponíveis para serem usados com o fragmento no editor de páginas, quando ele é adicionado a uma página. Isso significa que elas são opcionais, dependendo dos requisitos do canal específico.
   * Os ativos estão [associados a fragmentos por meio de coleções](/help/assets/content-fragments/content-fragments-assoc-content.md); as coleções associadas permitem que o autor decida quais ativos usar ao criar a página.

      * As coleções podem ser associadas a fragmentos por meio de modelos, como conteúdo padrão ou por autores durante a criação do fragmento.
      * [As ](/help/assets/manage-collections.md) Coleções de ativos (DAM) são a base para o conteúdo associado dos fragmentos.
   * Opcionalmente, também é possível adicionar o fragmento a uma coleção para auxiliar no rastreamento.


* **Metadados de fragmento**

   * Use os [esquemas de metadados de ativos](/help/assets/metadata.md).
   * Tags podem ser criadas quando você:

      * Criar e criar o fragmento
      * Ou posterior:

         * Ao visualizar/editar o fragmento **Propriedades** do console
         * Ao editar o **Metadados** quando estiver no editor de fragmentos

   >[!CAUTION]
   >
   >Os perfis de processamento de metadados não se aplicam aos Fragmentos de conteúdo.

* **Mestre**

   * Parte integral do fragmento

      * Cada fragmento de conteúdo tem uma instância de Principal.
      * Principal não pode ser excluído.
   * Principal pode ser acessado no editor de fragmentos em **[Variations](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Principal não é uma variação enquanto tal, mas a base de todas as variações.


* **Variações**

   * Representações de texto de fragmento específicas para fins editoriais; podem estar relacionadas a canais, mas não são obrigatórias, também podem ser para modificações locais ad hoc.
   * São criadas como cópias de **Principal**, mas podem ser editadas conforme necessário; geralmente há sobreposição de conteúdo entre as próprias variações.
   * Pode ser definido durante a criação do fragmento ou predefinido nos modelos de fragmento.
   * Armazenado no fragmento, para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [sincronizadas](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) com Principal se o conteúdo Principal tiver sido atualizado.
   * Pode ser [Summarizado](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rapidamente o texto para um comprimento predefinido.
   * Disponível na guia [Variations](/help/assets/content-fragments/content-fragments-variations.md) do editor de fragmentos.

### Conteúdo intermediário ao criar a página com fragmentos de conteúdo {#in-between-content-when-page-authoring-with-content-fragments}

Conteúdo intermediário:

* Está disponível para uso no [Editor de página ao trabalhar com Fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
* É [conteúdo adicional adicionado dentro do fluxo de um fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) depois de ter sido usado/referenciado em uma página.
* O conteúdo intermediário pode ser adicionado a qualquer fragmento, onde há apenas um elemento visível.
* O conteúdo associado pode ser usado, assim como os ativos e/ou componentes do navegador apropriado.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Não é armazenado no fragmento de conteúdo.

### Necessário por Fragmentos {#required-by-fragments}

Para criar, editar e usar fragmentos de conteúdo, também é necessário:

* **Modelo de conteúdo**

   * Estão [ativadas e depois criadas com Ferramentas](/help/assets/content-fragments/content-fragments-models.md).
   * Necessário para [criar um fragmento estruturado](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições de modelos de conteúdo exigem um título e um elemento de dados; tudo o resto é opcional. O modelo define um escopo mínimo do fragmento e do conteúdo padrão, se aplicável. Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento.

* **Modelo do fragmento**

   * Necessário para [criar um fragmento simples](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Geralmente [desenvolvido durante a implementação do projeto](/help/sites-developing/content-fragment-templates.md); não pode ser criado durante a criação.
   * Define as propriedades básicas de um fragmento simples (título, número de elementos de texto, definições de tags).
   * As definições de modelo exigem um título e um elemento de texto; tudo o resto é opcional. O modelo define um escopo mínimo do fragmento e do conteúdo padrão, se aplicável. Posteriormente, os autores podem estender um fragmento além do que é definido no modelo.

* **Componente do fragmento de conteúdo**

   * Instrumental para entregar o fragmento no formato HTML e/ou JSON.
   * Necessário para [fazer referência ao fragmento em uma página](/help/sites-authoring/content-fragments.md).
   * Responsável pela disposição e entrega de um fragmento; ou seja, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associará automaticamente o componente necessário.

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que será usado em qualquer lugar.

### Amostra We.Retail {#we-retail-sample}

Um fragmento de amostra pode ser visto em:

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
