---
title: Trabalho com fragmentos de conteúdo
description: Saiba como os Fragmentos de conteúdo no Adobe Experience Manager (AEM) permitem projetar, criar, preparar e usar conteúdo independente da página, ideal para entrega sem interface.
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 6%

---

# Trabalho com fragmentos de conteúdo {#working-with-content-fragments}

Com o Adobe Experience Manager (AEM), os Fragmentos de conteúdo permitem que você crie, crie, prepare e [publique conteúdo independente de página](/help/sites-authoring/content-fragments.md) Eles permitem que você prepare o conteúdo pronto para uso em vários locais/em vários canais, ideal para entrega sem interface.

Fragmentos de conteúdo contêm conteúdo estruturado:

* Elas são baseadas em um [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md), que predefine uma estrutura para o fragmento resultante.
* A estrutura pode variar entre:
   * Básico
      * Por exemplo, um único campo de texto de várias linhas.
      * Pode ser usado para preparar conteúdo direto para uso na criação de página.
   * Complexo
      * Uma combinação de vários campos de tipos de dados variáveis, incluindo texto, número, booleano, dados e tempo, entre outros.
      * Pode ser usado para preparar conteúdo mais estruturado para criação de página ou para entrega em seu aplicativo.
   * Aninhado
      * Os tipos de dados de referência disponíveis permitem aninhar o conteúdo.
      * Tendem a ser usadas para entrega em seu aplicativo.

Os fragmentos de conteúdo também podem ser entregues no formato JSON, usando os recursos de exportação do Modelo do Sling (JSON) AEM componentes principais. Esta forma de delivery:

* permite usar o componente para gerenciar quais elementos de um fragmento fornecer
* permite a entrega em massa, adicionando vários componentes principais do fragmento de conteúdo na página que está sendo usada para a entrega da API

Esta e as seguintes páginas abordam as tarefas de criação, configuração, manutenção e uso dos fragmentos de conteúdo:

* [Ativar a funcionalidade Fragmento de conteúdo para sua instância](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)  - permitindo, criando e definindo seus modelos
* [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)  - crie fragmentos de conteúdo; em seguida, edite, publique e faça referência
* [Variações - Criação do conteúdo do fragmento](/help/assets/content-fragments/content-fragments-variations.md)  - crie o conteúdo do fragmento e crie variações do Principal
* [Marcação](/help/assets/content-fragments/content-fragments-markdown.md)  - uso da sintaxe de marcação para o fragmento
* [Uso de conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md)  - adição do conteúdo associado
* [Metadados - Propriedades do fragmento](/help/assets/content-fragments/content-fragments-metadata.md)  - visualização e edição das propriedades do fragmento
* Use os [Fragmentos de conteúdo, juntamente com GraphQL, para fornecer conteúdo](/help/assets/content-fragments/content-fragments-graphql.md) para uso em seus aplicativos. Para ajudar nisso, você pode visualizar [saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Essas páginas podem ser lidas junto com:
>
>* [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
>* [Personalização e extensão de fragmentos de conteúdo](/help/sites-developing/customizing-content-fragments.md)
>* [Fragmentos de conteúdo configuram componentes para renderização](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [Suporte a Fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/assets-api-content-fragments.md)
>* [AEM API GraphQL para uso com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md)


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
* Crie conteúdo aninhado para refletir a complexidade de seus dados.

Esses fragmentos de conteúdo podem ser montados para proporcionar experiências em uma variedade de canais.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)** são recursos diferentes no AEM:
>* **Os** Fragmentos de conteúdo são conteúdo editorial, que pode ser usado para acessar dados estruturados, incluindo textos, números e datas, entre outros. São conteúdo puro, com definição e estrutura, mas sem design visual e/ou layout adicionais.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.

>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte também [Entendendo fragmentos de conteúdo e fragmentos de experiência em AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments).

>[!NOTE]
>
>Antes do AEM 6.3, os Fragmentos de conteúdo eram criados com o uso de modelos em vez de modelos. Os modelos não estão mais disponíveis para criar novos fragmentos, mas os fragmentos criados com esse modelo ainda são compatíveis.

## Fragmentos de conteúdo e serviços de conteúdo {#content-fragments-and-content-services}

Os Serviços de conteúdo AEM foram projetados para generalizar a descrição e a entrega de conteúdo de/para AEM além de um foco nas páginas da Web.

Eles fornecem a entrega de conteúdo para canais que não são páginas da Web tradicionais AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos móveis nativos
* outros canais e pontos de contato externos ao AEM

O delivery é feito no formato JSON usando o Exportador JSON.

AEM Fragmentos de conteúdo podem ser usados para descrever e gerenciar conteúdo estruturado. O conteúdo estruturado é definido em modelos que podem conter vários tipos de conteúdo; incluindo texto, dados numéricos, booleano, data e hora e muito mais.

Juntamente com os recursos de exportação JSON de AEM componentes principais, esse conteúdo estruturado pode ser usado para fornecer conteúdo AEM a canais diferentes de páginas AEM.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM também suporta a tradução do conteúdo do fragmento.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## Tipo de conteúdo {#content-type}

Os fragmentos de conteúdo são:

* Armazenado como **Assets**:

   * Os fragmentos de conteúdo (e suas variações) podem ser criados e mantidos no console **Assets**.
   * Criado e editado no Editor de fragmento de conteúdo.

* Usado no [editor de página por meio do componente do Fragmento de conteúdo](/help/sites-authoring/content-fragments.md) (componente de referência):

   * O componente **Fragmento de conteúdo** está disponível para os autores da página. Ele permite referenciar e fornecer o fragmento de conteúdo necessário no formato HTML ou JSON.

* Acessível usando a [AEM API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md).

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

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### Partes constituintes de um fragmento de conteúdo {#constituent-parts-of-a-content-fragment}

Os ativos do fragmento de conteúdo são compostos das seguintes partes (direta ou indiretamente):

* **Elementos do fragmento**

   * Os elementos estão correlacionados aos campos de dados que contêm conteúdo.
   * Use um modelo de conteúdo para criar o fragmento de conteúdo. Os elementos (campos) especificados no modelo definem a estrutura do fragmento. Esses elementos (campos) podem ser de uma variedade de tipos de dados.

* **Parágrafos de fragmento**

   * Blocos de texto, muitas vezes de várias linhas, que são delimitados como entidades individuais.

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
      >Os ativos podem ser (inadvertidamente) removidos de um fragmento ao alternar para o formato Texto simples.

      >[!NOTE]
      >
      >Os ativos também podem ser adicionados como [conteúdo adicional (intermediário)](/help/sites-authoring/content-fragments.md#using-associated-content) ao usar um fragmento em uma página; usando Conteúdo associado ou ativos no navegador Ativos.

* **Conteúdo associado**

   * Esse é um conteúdo externo a um fragmento, mas com relevância editorial para ele. Geralmente, imagens, vídeos ou outros fragmentos.
   * Os ativos individuais dentro da coleção estão disponíveis para serem usados com o fragmento no editor de páginas, quando ele é adicionado a uma página. Isso significa que elas são opcionais, dependendo dos requisitos do canal específico.
   * Os ativos estão [associados a fragmentos por meio de coleções](/help/assets/content-fragments/content-fragments-assoc-content.md); as coleções associadas permitem que o autor decida quais ativos usar ao criar a página.

      * As coleções podem ser associadas a fragmentos como conteúdo padrão ou por autores durante a criação do fragmento.
      * [As ](/help/assets/manage-collections.md) Coleções de ativos (DAM) são a base para o conteúdo associado dos fragmentos.
   * Opcionalmente, também é possível adicionar o fragmento a uma coleção para auxiliar no rastreamento.

* **Metadados de fragmento**

   * Use os [esquemas de metadados de ativos](/help/assets/metadata-schemas.md).
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
   * Pode ser definido durante a criação do fragmento.
   * Armazenado no fragmento, para ajudar a evitar a dispersão de cópias de conteúdo.
   * As variações podem ser [sincronizadas](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) com Principal se o conteúdo Principal tiver sido atualizado.
   * Pode ser [Summarizado](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rapidamente o texto para um comprimento predefinido.
   * Disponível na guia [Variations](/help/assets/content-fragments/content-fragments-variations.md) do editor de fragmentos.

### Conteúdo intermediário ao criar a página com fragmentos de conteúdo {#in-between-content-when-page-authoring-with-content-fragments}

Conteúdo intermediário:

* Está disponível para uso no Editor de páginas ao trabalhar com Fragmentos de conteúdo.
* É [conteúdo adicional adicionado dentro do fluxo de um fragmento](/help/sites-authoring/content-fragments.md#adding-in-between-content) depois de ter sido usado/referenciado em uma página.
* Está disponível para uso no [Editor de página ao trabalhar com Fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
* O conteúdo intermediário pode ser adicionado a qualquer fragmento, onde há apenas um elemento visível.
* O conteúdo associado pode ser usado, assim como os ativos e/ou componentes do navegador apropriado.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Não é armazenado no fragmento de conteúdo.

### Necessário por fragmentos {#required-by-fragments}

Para criar fragmentos de conteúdo, você precisa:

* **Modelo de conteúdo**

   * [estão ativados usando o Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * São [criados usando Ferramentas](/help/assets/content-fragments/content-fragments-models.md).
   * Necessário para [criar um fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define a estrutura de um fragmento (título, elementos de conteúdo, definições de tag).
   * As definições do modelo de conteúdo exigem um título e um elemento de dados; tudo o resto é opcional.
   * O modelo pode definir o conteúdo padrão, se aplicável.
   * Os autores não podem alterar a estrutura definida ao criar o conteúdo do fragmento.
   * As alterações feitas em um modelo após a criação de fragmentos de conteúdo dependentes podem afetar esses fragmentos de conteúdo.

Para usar os Fragmentos de conteúdo para criação de página, também é necessário:

* **Componente do fragmento de conteúdo**

   * Instrumental para entregar o fragmento no formato HTML e/ou JSON.
   * Necessário para [fazer referência ao fragmento em uma página](/help/sites-authoring/content-fragments.md).
   * Responsável pela disposição e entrega de um fragmento; ou seja, canais.
   * Os fragmentos precisam de um ou mais componentes dedicados para definir o layout e fornecer alguns ou todos os elementos/variações e conteúdo associado.
   * Arrastar um fragmento para uma página na criação associará automaticamente o componente necessário.

## Exemplo de uso {#example-usage}

Um fragmento, com seus elementos e variações, pode ser usado para criar conteúdo coerente para vários canais. Ao projetar o fragmento, é necessário considerar o que será usado em qualquer lugar.
