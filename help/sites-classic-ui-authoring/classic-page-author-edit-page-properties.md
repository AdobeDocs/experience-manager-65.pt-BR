---
title: Editar as propriedades da página
seo-title: Editar as propriedades da página
description: As propriedades de uma página podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.
seo-description: As propriedades de uma página podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Editar as propriedades da página{#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Eles podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por meio de várias guias:

### Básico {#basic}

* **Título**

   O título da página é exibido em vários locais. Por exemplo, a lista da guia **Sites** e as visualizações de cartão/lista dos **Sites**.

   Este é um campo obrigatório.

* **Tags**

   Aqui você pode adicionar ou remover as tags da página, atualizando a lista na caixa de seleção:

   * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o x.
   * Uma tag totalmente nova pode ser inserida, digitando o nome em uma caixa de seleção vazia.

      A nova tag será realmente criada ao apertar a tecla enter. A nova tag será então exibida em uma caixa com uma pequena estrela à direita, indicando que é uma nova tag.

   * Com a funcionalidade suspensa, você pode selecionar a partir das tags existentes.
   * Um x será exibido ao passar o mouse em cima de uma entrada de tag na caixa de seleção; isso pode ser usado para remover a tag desta página.

* **Ocultar na navegação**

   Um interruptor para indicar se a página é exibida ou ocultada na navegação da página.

* **Título da página**

   Um título para ser usado na página.

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

   Deixe novamente estes campos vazios para as páginas que desejar publicar imediatamente.

* **URL personalizada**

   Permite inserir uma URL personalizada para esta página. Permite que você tenha uma URL mais curta e mais expressiva.

   For example, if the Vanity URL is set to w `elcome`to the page identified by the path / `v1.0/startpage`for the website h `ttp://example.com,` then h `ttp://example.com/welcome`would be the vanity URL of h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URLs personalizadas:
   >
   >* deve ser exclusiva, dessa forma, é necessário tomar cuidado para que o valor não seja utilizado por outra página.
   >* não é compatível com padrões do regex.


* **Redirecionar URL personalizada**

   Indica se você deseja que a página use a URL personalizada.

### Avançado {#advanced}

* **Idioma**

   O idioma da página.

* **Redirecionar**

   Indique a página de redirecionamento automático.

* **Design**

   Indique o [design](/help/sites-developing/designer.md) a ser usado para esta página.

* **Alias**

   Especifique um alias a ser usado com esta página.

* **Ativar grupo de usuários fechado**

   Ativa (ou desativa) o uso de [grupos de usuários fechados](/help/sites-administering/cug.md) (CUGs, Closed user groups).

* **Página de logon**

   A página para ser usada para logon.

* **Grupos aceitos**

   Grupos elegíveis para o logon no CUG.

* **Território**

   Nome do território para o CUG.

* **Exportar configuração**

   Especifique uma configuração de exportação.

### Miniatura {#thumbnail}

* **Miniatura da página**

   Exibe a imagem de miniatura da página. É possível:

   * **Gerar pré-visualização**

      Gere uma visualização da página para usar como miniatura.

   * **Carregar imagem**

      Carregue uma imagem para usar como miniatura.

### Serviços em nuvem {#cloud-services}

* **Serviços em nuvem**

   Defina as propriedades para os [serviços em nuvem](/help/sites-developing/extending-cloud-config.md).

### Personalização {#personalization}

* **Personalização**

   Selecione uma [Marca para especificar um escopo para a segmentação](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Permissões {#permissions}

* **Permissões** (interface otimizada para toque)

   Exiba as [permissões efetivas e adicione novas permissões](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Defina as propriedades para uma página do Blueprint no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas no Live-copy.

### Live Copy {#live-copy}

* **Live Copy**

   Defina as propriedades para uma página de Live Copy no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas do Blueprint.

### Estrutura do site {#site-structure}

* Forneça links para páginas que oferecem funcionalidade em todo o site, como a **Página de inscrição**, a **Página offline**, entre outras.

## Editar as propriedades da página {#editing-page-properties-2}

### Edição das Propriedades de página para uma página específica {#editing-page-properties-for-a-specific-page}

As propriedades da página definem as várias propriedades da página, como títulos, quando aparecem no site e outros.

1. Abra a página que deseja editar.

1. No sidekick, abra a guia **Página** em seguida, selecione **Propriedades da página...**

   Isso abre uma janela com várias abas.

1. Faça as alterações necessárias e clique em **OK** para salvar.

