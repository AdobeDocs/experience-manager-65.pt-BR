---
title: Trabalho com fragmentos de conteúdo
description: Saiba como os Fragmentos de conteúdo no Adobe Experience Manager (AEM) permitem projetar, criar, preparar e usar conteúdo independente da página, ideal para entrega sem interface.
feature: Content Fragments
role: User
exl-id: 0ee883c5-0cea-46b7-a759-600b8ea3bc3e
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 93%

---

# Trabalho com fragmentos de conteúdo {#working-with-content-fragments}

Com o Adobe Experience Manager (AEM), os Fragmentos de conteúdo permitem projetar, criar, preparar e [publicar conteúdo independente da página](/help/sites-authoring/content-fragments.md) Eles permitem que você prepare conteúdo pronto para uso em vários locais/em vários canais, ideal para entrega sem interface.

Os fragmentos de conteúdo contêm conteúdo estruturado:

* Eles se baseiam em um [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md), que predefine uma estrutura para o fragmento resultante.
* A estrutura pode variar entre:
   * Básico
      * Por exemplo, um único campo de texto de várias linhas.
      * Pode ser usado para preparar conteúdo direto para uso na criação de páginas.
   * Complexo
      * Uma combinação de vários campos de tipos de dados variáveis, incluindo texto, número, booleano, data e hora, entre outros.
      * Pode ser usado para preparar conteúdo mais estruturado para a criação de páginas ou para entrega em seu aplicativo.
   * Aninhado
      * Os tipos de dados de referência disponíveis permitem aninhar o conteúdo.
      * Tendem a ser usados para entrega em seu aplicativo.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo Sling (JSON) dos componentes principais do AEM. Esta forma de entrega:

* permite usar o componente para gerenciar quais elementos de um fragmento fornecer
* permite a entrega em massa, adicionando vários componentes principais do fragmento de conteúdo na página que está sendo usada para a entrega da API

Esta e as seguintes páginas abordam as tarefas de criação, configuração, manutenção e uso dos fragmentos de conteúdo:

* [Ativar a funcionalidade de fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md) — ativar, criar e definir modelos
* [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md) — crie fragmentos de conteúdo; em seguida, edite, publique e faça referência
* [Variações - Criação do conteúdo dos fragmentos](/help/assets/content-fragments/content-fragments-variations.md) — crie o conteúdo do fragmento e variações do Principal
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) — uso da sintaxe de marcação para o fragmento
* [Uso de conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) — adição de conteúdo associado
* [Metadados - Propriedades do fragmento](/help/assets/content-fragments/content-fragments-metadata.md) — visualização e edição das propriedades do fragmento
* Use [Fragmentos de conteúdo, juntamente com GraphQL, para fornecer conteúdo](/help/assets/content-fragments/content-fragments-graphql.md) para uso em seus aplicativos. Para ajudar nisso, você pode visualizar [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Essas páginas podem ser lidas em conjunto com:
>
>* [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
>* [Personalização e extensão de fragmentos de conteúdo](/help/sites-developing/customizing-content-fragments.md)
>* [Fragmentos de conteúdo configuram componentes para renderização](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [Compatibilidade com os Fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/assets-api-content-fragments.md)
>* [API GraphQL do AEM para uso com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md)


O número de canais de comunicação aumenta anualmente. Normalmente, os canais se referem ao mecanismo de entrega, como:

* Canal físico; por exemplo, desktop, dispositivo móvel.
* Forma de entrega em um canal físico; por exemplo, “página de detalhes do produto”, “página de categoria do produto” para desktop ou “web para publicação de conteúdo para dispositivos móveis”, “aplicativo para dispositivos móveis” para dispositivos móveis.

No entanto, você (provavelmente) não deseja usar exatamente o mesmo conteúdo para todos os canais; é necessário otimizar o conteúdo de acordo com o canal específico.

Com os Fragmentos de conteúdo é possível:

* Considerar como atingir públicos-alvo com eficiência em todos os canais.
* Criar e gerenciar conteúdo editorial neutro para o canal.
* Criar grupos de conteúdo para um intervalo de canais.
* Desenvolver variações de conteúdo para canais específicos.
* Adicionar imagens ao texto inserindo ativos (fragmentos de mídia mista).
* Criar conteúdo aninhado para refletir a complexidade dos seus dados.

Esses fragmentos de conteúdo podem ser reunidos para proporcionar experiências em uma variedade de canais.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)** são recursos diferentes no AEM:
>* **Fragmentos de conteúdo** são conteúdos editoriais que podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros. Eles são conteúdo puro, com definição e estrutura, mas sem designs visuais e/ou layouts adicionais.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte também [Entender sobre os fragmentos de conteúdo e fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

>[!NOTE]
>
>Antes do AEM 6.3, os Fragmentos de conteúdo eram criados com o uso de modelos em vez de modelos. Os modelos não estão mais disponíveis para criar novos fragmentos, mas os fragmentos criados com esse modelo ainda são compatíveis.

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os Serviços de conteúdo do AEM foram criados para generalizar a descrição e a entrega de conteúdo de e para o AEM para além do foco em páginas da Web.

Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos nativos para dispositivos móveis
* outros canais e pontos de contato externos ao AEM

A entrega é feita no formato JSON usando o Exportador JSON.

Os fragmentos de conteúdo do AEM podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter vários tipos de conteúdo; incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Juntamente com os recursos de exportação em JSON dos componentes principais do AEM, esse conteúdo estruturado pode ser usado para fornecer conteúdo do AEM a outros canais além das páginas do AEM.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>O AEM também permite a tradução do conteúdo do fragmento.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Armazenados como **Ativos**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos a partir do **Ativos** console.
   * Criados e editados no Editor de fragmento de conteúdo.

* Usados no [editor de páginas por meio do componente Fragmento de conteúdo](/help/sites-authoring/content-fragments.md) (componente de referência):

   * O componente **Fragmento de conteúdo** está disponível para autores de página. Ele permite referenciar e entregar o fragmento de conteúdo necessário nos formatos HTML ou JSON.

* Acessíveis por meio da [API GraphQL do AEM](/help/assets/content-fragments/graphql-api-content-fragments.md).

Fragmentos de conteúdo são uma estrutura de conteúdo que:

* Não possuem layout ou design (alguma formatação de texto é possível no modo Rich Text).
* Contêm uma ou mais [partes constituintes](#constituent-parts-of-a-content-fragment).
* Podem [conter ou estar conectados a imagens](#fragments-with-visual-assets).
* Podem usar [conteúdo intermediário](#in-between-content-when-page-authoring-with-content-fragments) quando referenciados em uma página.

* São independentes do mecanismo de entrega (ou seja, a página ou canal).

### Fragmentos com ativos visuais {#fragments-with-visual-assets}

Para conceder mais controle do conteúdo aos autores, as imagens podem ser adicionadas e/ou integradas a um fragmento de conteúdo.

Os ativos podem ser usados com um fragmento de conteúdo de várias maneiras; cada uma com as suas próprias vantagens:

* **Inserir ativo** em um fragmento (fragmentos de mídia mista)

   * São uma parte integral do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Definem a posição do ativo.
   * Consulte [Inserir ativos no fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) no Editor de fragmentos para obter mais informações.

   >[!NOTE]
   >
   >Os ativos visuais inseridos no fragmento de conteúdo propriamente dito são anexados ao parágrafo anterior no fragmento. Quando o fragmento é adicionado a uma página, esses ativos são movidos em relação a esse parágrafo quando o conteúdo intermediário é adicionado.

* **Conteúdo associado**

   * Estão conectados a um fragmento; mas não a uma parte fixa do fragmento (consulte [Partes constituintes de um fragmento de conteúdo](#constituent-parts-of-a-content-fragment)).
   * Permitem alguma flexibilidade para o posicionamento.
   * Estão facilmente disponíveis para uso (como conteúdo intermediário) ao usar o fragmento em uma página.
   * Consulte o [Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obter mais informações.

* Ativos disponíveis no **navegador de Ativos** do editor de página

   * Permitem flexibilidade total para a seleção de um ativo.
   * Permitem alguma flexibilidade para o posicionamento.
   * Não fornecem o conceito de aprovação para um fragmento específico.

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Usa-se um modelo de conteúdo para criar o fragmento de conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de uma variedade de tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, geralmente multilinha, que são delimitados como entidades individuais.

   * Nos modos [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), um parágrafo pode ser formatado como um cabeçalho. Nesse caso, ele e o parágrafo a seguir pertencem como uma unidade.

   * Ativam o controle de conteúdo durante a criação da página.

* **Ativos inseridos em um fragmento (fragmentos de mídia mista)**

   * Ativos (imagens) inseridos no fragmento real e usados como conteúdo interno de um fragmento.
   * São incorporados ao sistema de parágrafo do fragmento.
   * Podem ser formatados quando o [fragmento é usado/referenciado em uma página](/help/sites-authoring/content-fragments.md).
   * Só podem ser adicionados, excluídos ou movidos dentro de um fragmento usando o editor de fragmentos. Essas ações não podem ser realizadas no editor de páginas.
   * Só podem ser adicionados, excluídos ou movidos dentro de um fragmento usando o [formato Rich Text no editor de fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Só podem ser adicionados a elementos de texto multilinha (qualquer tipo de fragmento).
   * São anexados ao texto anterior (parágrafo).

      >[!CAUTION]
      >
      >Os ativos podem ser (inadvertidamente) removidos de um fragmento ao alternar para o formato de Texto sem formatação.

      >[!NOTE]
      >
      >Os ativos também podem ser adicionados como [conteúdo adicional (intermediário)](/help/sites-authoring/content-fragments.md#using-associated-content) ao usar um fragmento em uma página; usando o conteúdo associado ou ativos do navegador de ativos.

* **Conteúdo associado**

   * Esse é um conteúdo externo a um fragmento, mas com relevância editorial. Em geral, imagens, vídeos ou outros fragmentos.
   * Os ativos individuais contidos na coleção estão disponíveis para serem usados com o fragmento no editor de páginas, quando ele é adicionado a uma página. Isso significa que elas são opcionais, dependendo dos requisitos do canal específico.
   * Os ativos são [associados aos fragmentos por meio de coleções](/help/assets/content-fragments/content-fragments-assoc-content.md); as coleções associadas permitem que o autor decida quais ativos usar ao criar a página.

      * As coleções podem ser associadas aos fragmentos como conteúdo padrão ou por autores durante a criação do fragmento.
      * As [coleções de ativos (DAM)](/help/assets/manage-collections.md) são a base para o conteúdo associado de fragmentos.
   * Opcionalmente, também é possível adicionar o próprio fragmento a uma coleção para auxiliar no rastreamento.

* **Metadados de fragmento**

   * Usa os [esquemas de metadados de ativos](/help/assets/metadata-schemas.md).
   * Tags podem ser criadas quando você:

      * Cria o fragmento
      * Ou posteriormente:

         * Ao visualizar/editar as **Propriedades** do fragmento no console
         * Ao editar os **Metadados** no editor de fragmento

   >[!CAUTION]
   >
   >Os perfis de processamento de metadados não se aplicam aos fragmentos de conteúdo.

* **Principal**

   * Uma parte integral do fragmento

      * Cada fragmento de conteúdo tem uma instância Principal.
      * O Principal não pode ser excluído.
   * O Principal pode ser acessado no editor de fragmentos, em **[Variações](/help/assets/content-fragments/content-fragments-variations.md)**.
   * O Principal não é uma variação em si, mas a base de todas as variações.


* **Variações**

   * Representações de texto de fragmento específicas para fins editoriais; podem estar relacionadas a canais, mas não é obrigatório. Também podem ser para modificações locais ad hoc.
   * São criadas como cópias do **Principal**, mas podem ser editadas conforme necessário; geralmente há sobreposição de conteúdo entre as próprias variações.
   * Podem ser definidas durante a criação do fragmento.
   * São armazenadas no fragmento para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [sincronizadas](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) com o Principal se o conteúdo do Principal tiver sido atualizado.
   * Podem ser [resumidas](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rapidamente o texto em um comprimento predefinido.
   * Disponíveis na guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) do editor de fragmentos.

### Conteúdo intermediário ao criar páginas com fragmentos de conteúdo {#in-between-content-when-page-authoring-with-content-fragments}

Conteúdo intermediário:

* Está disponível para uso no Editor de páginas ao trabalhar com Fragmentos de conteúdo.
* É o [conteúdo adicional acrescentado no fluxo de um fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) depois de ter sido usado/referenciado em uma página.
* Está disponível para uso no [Editor de páginas ao trabalhar com Fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
* O conteúdo intermediário pode ser adicionado a qualquer fragmento onde há apenas um elemento visível.
* O conteúdo associado pode ser usado, assim como os ativos e/ou componentes do navegador apropriado.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Não é armazenado no fragmento de conteúdo.

### Exigido por fragmentos {#required-by-fragments}

Para criar fragmentos de conteúdo, você precisa:

* **Modelo de conteúdo**

   * É [ativado usando o Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * É [criado usando Ferramentas](/help/assets/content-fragments/content-fragments-models.md).
   * Obrigatório para [criar um fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições do modelo de conteúdo exigem um título e um elemento de dados; todo o resto é opcional.
   * O modelo pode definir o conteúdo padrão, se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento.
   * As alterações feitas em um modelo após a criação de fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

Para usar os Fragmentos de conteúdo para a criação de páginas, também é necessário:

* **Componente Fragmento de Conteúdo**

   * Fundamental para entregar o fragmento no formato HTML e/ou JSON.
   * Obrigatório para [fazer referência ao fragmento em uma página](/help/sites-authoring/content-fragments.md).
   * Responsável pela disposição e entrega de um fragmento; ou seja, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associará automaticamente o componente necessário.

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que e onde será usado.
