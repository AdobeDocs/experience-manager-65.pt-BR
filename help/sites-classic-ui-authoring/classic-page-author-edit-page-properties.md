---
title: Edição de propriedades da página
description: As propriedades de uma página podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não, e as informações da live copy estarão disponíveis conforme apropriado.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 20%

---

# Editar as propriedades da página{#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Isso pode variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não, e as informações da live copy estarão disponíveis conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias:

### Básico {#basic}

* **Título**

  O título da página é exibido em vários locais. Por exemplo, a lista de guias **Sites** e as exibições de cartão/lista **Sites**.

  Este campo é obrigatório.

* **Tags**

  Aqui você pode adicionar ou remover tags da página, atualizando a lista na caixa de seleção:

   * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o ícone “x”.
   * Uma tag totalmente nova pode ser inserida digitando o nome em uma caixa de seleção vazia.

     A nova tag será criada quando você pressionar Enter. A nova tag será mostrada em uma caixa, com uma pequena estrela à direita indicando que é uma nova tag.

   * Com a funcionalidade de menu suspenso, é possível selecionar tags existentes.
   * Um x é exibido quando você passa o mouse sobre uma entrada de tag na caixa de seleção; isso pode ser usado para remover essa tag para esta página.

* **Ocultar na Navegação**

  Um switch para indicar se a página está visível ou oculta na navegação da página.

* **Título da página**

  Um título a ser usado na página.

* **Título de navegação**

  Você pode especificar um título separado para usar na navegação (por exemplo, se desejar algo mais conciso). Se estiver vazio, a variável **Título** é usada.

* **Subtítulo**

  Um subtítulo para usar na página.

* **Descrição**

  A descrição da página, a finalidade dela ou qualquer outro detalhe que desejar adicionar.

* **No Prazo**

  A data e a hora em que a página publicada será ativada. Quando publicada, essa página será mantida inativa até o horário especificado.

  Deixe esses campos vazios para páginas que deseja publicar imediatamente (o cenário normal).

* **Tempo de Desativação**

  A hora em que a página publicada será desativada.

  Deixe esses campos vazios novamente para as páginas que deseja publicar imediatamente.

* **URL personalizada**

  Permite inserir um URL personalizado para esta página. Isso permite que você tenha um URL mais curto e expressivo.

  Por exemplo, se a URL personalizada estiver definida como w `elcome` para a página identificada pelo caminho / `v1.0/startpage` para o site h `ttp://example.com,` então h `ttp://example.com/welcome` seria a URL personalizada de h `ttp://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >URLs personalizadas:
  >
  >* deve ser exclusivo, portanto, certifique-se de que o valor ainda não esteja sendo usado por outra página.
  >* não são compatíveis com padrões regex.

* **Redirecionar URL do Vanity**

  Indica se você deseja que a página use a URL personalizada.

### Avançado  {#advanced}

* **Idioma**

  O idioma da página.

* **Redirecionar**

  Indique a página de redirecionamento automático para a página atual.

* **Design**

  Indique o [design](/help/sites-developing/designer.md) a ser usado para esta página.

* **Alias**

  Especifique um alias a ser usado com esta página.

* **Habilitar Grupo de Usuários Fechado**

  Permite (ou desabilita) o uso de [grupos de usuários fechados](/help/sites-administering/cug.md) (CUGs).

* **Página de Logon**

  A página a ser usada para logon.

* **Grupos admitidos**

  Grupos qualificados para fazer logon no CUG.

* **Território**

  Nome do domínio para o CUG.

* **Exportar configuração**

  Especifique uma configuração de exportação.

### Miniatura  {#thumbnail}

* **Miniatura da página**

  Mostra a imagem em miniatura da página. É possível:

   * **Gerar visualização**

     Gera uma visualização da página para usar como miniatura.

   * **Fazer upload de imagem**

     Carregue uma imagem para usar como miniatura.

### Cloud Services {#cloud-services}

* **Cloud Services**

  Defina as propriedades para [serviços em nuvem](/help/sites-developing/extending-cloud-config.md).

### Personalização {#personalization}

* **Personalização**

  Selecione uma [Marca para especificar um escopo de direcionamento](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Permissões   {#permissions}

* **Permissões** (interface otimizada para toque)

  Exiba as [permissões efetivas e adicione novas permissões](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

  Defina as propriedades para uma página do Blueprint no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas no Live Copy.

### Live Copy  {#live-copy}

* **Live Copy**

  Defina as propriedades para uma página de Live Copy no [gerenciamento de vários sites](/help/sites-administering/msm.md). Controla as circunstâncias sob as quais as modificações serão propagadas do Blueprint.

### Estrutura do site  {#site-structure}

* Forneça links para páginas que oferecem funcionalidade em todo o site, como a **Página de Inscrição**, a **Página Offline**, entre outras.

## Editar as propriedades da página {#editing-page-properties-2}

### Editar propriedades de página para uma página específica {#editing-page-properties-for-a-specific-page}

As Propriedades da página definem as várias propriedades da página, como títulos, quando eles são exibidos no site e outros.

1. Abra a página que deseja editar.

1. No sidekick, abra a guia **Página** e selecione **Propriedades da página...**

   Isso abre uma caixa de diálogo com várias guias.

1. Faça as alterações necessárias e clique em **OK** para salvar.
