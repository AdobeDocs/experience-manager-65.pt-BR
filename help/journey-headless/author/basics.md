---
title: Saiba mais sobre as noções básicas de criação
description: Saiba mais sobre os conceitos e os mecanismos de criação de conteúdo para seu CMS headless usando Fragmentos de conteúdo.
exl-id: 125c4d0b-1572-4dba-823d-cdef2778f275
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 73%

---

# Noções básicas de criação para headless com AEM {#author-headless-basics}

## A história até agora {#story-so-far}

No início da [Jornada do autor de conteúdo headless do AEM](overview.md), a [Introdução](introduction.md) abordou os conceitos básicos e a terminologia relevante para a criação de conteúdo headless.

Este artigo se baseia nessas noções para que você entenda como criar seu próprio conteúdo para o seu projeto headless do AEM.

## Objetivo {#objective}

* **Público-alvo**: iniciante
* **Objetivo**: apresentar as noções básicas da criação de CMS headless:
   * Introdução à criação com o AEMaaCS
   * Introdução aos Fragmentos de conteúdo

## Manuseio básico {#basic-handling}

Antes de lidar com os Fragmentos de conteúdo, veja uma introdução (muito) rápida ao uso do AEM....mas nada substitui a experiência de entrar e tentar usar o sistema.

### Criação e publicação {#author-preview-publish}

Uma instalação do AEM geralmente consiste em pelo menos dois ambientes:

* Autor
* Publicação

Você faz logon e usa o ambiente de criação para gerar o seu conteúdo. Quando estiver pronto, publique seu conteúdo para que ele fique disponível. Para headless, isso seria para outros aplicativos, para páginas da Web, isso seria para os leitores na Web.

Para obter mais detalhes, consulte os Conceitos de criação.

### Fazer logon {#signing-in}

Assim como na maioria dos sistemas, você deve fazer logon. Como autor, você receberá:

* Nome do usuário (conta)
* Senha
* Link para acessar a tela de logon

Sua conta já terá sido configurada com os privilégios necessários. Se você tiver algum problema, a Adobe recomenda que você entre em contato com a equipe interna de suporte ao projeto.

### Navegação {#navigation}

A primeira vez que você efetuar o logon, um pequeno tutorial online destacará alguns dos principais recursos da interface.

Em seguida, você pode usar o Painel de navegação para acessar as áreas-chave do AEM. Para fragmentos de conteúdo, você usará o **Console de ativos**.

O Painel de navegação pode ser aberto selecionando o ícone Adobe no canto superior esquerdo, seguido pelo ícone de bússola pequeno:

![Painel Navegação](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Embora os fragmentos de conteúdo sejam um recurso do AEM **Sites**, elas são encontradas na **Assets** console. Este é um detalhe técnico que não deve afetar você, mas que pode ser útil.

No console, é possível selecionar pastas para navegar até o fragmento de conteúdo ou as navegações estruturais (no cabeçalho) para navegar de volta até a árvore.

![Navegações estruturais](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Ações, Seleção, Exibição {#actions-selecting-viewing}

A variável **Assets** o console tem dedicado **Barras de ferramentas de ação**, e **Ações rápidas** que você pode usar após selecionar um recurso (por exemplo, uma pasta ou fragmento de conteúdo).

As Ações rápidas estão disponíveis para um único recurso, consulte **Basileia** no exemplo abaixo:

![Ações rápidas](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

A barra de ferramentas Ações fornece acesso à gama completa de ações, aplicáveis ao cenário atual. As ações disponíveis podem mudar; por exemplo, dependendo da sua localização ou se você selecionou vários recursos:

![Barra de ferramentas de ação](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Você pode selecionar o formato para exibir seus recursos com o Seletor de exibição:

![Exibir seletor](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

É possível ver informações adicionais sobre itens usando o Seletor de painéis. Isso também dá acesso a ações adicionais.

![Painel esquerdo](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Criação de fragmentos de conteúdo {#authoring-content-fragments}

Então, essa foi uma introdução bem rápida à interface do AEM, mas espero que você tenha tido uma chance de experimentá-la. Agora, chegamos ao seu verdadeiro interesse: Fragmentos de conteúdo para headless.

Teremos que passar pelas coisas do início ao fim, mas sua instância já pode ter pastas e/ou fragmentos criados, e eles podem estar em locais diferentes. Os princípios são os mesmos.

### Organização e navegação {#organizing-and-navigating}

A menos que tenha pouquíssimos Fragmentos de conteúdo, você vai querer organizá-los - para que você (e outros) possam encontrá-los novamente.

#### Criação de pastas {#creating-folder}

Você pode fazer isso criando uma série de pastas no **Arquivos** seção do console Assets. Selecione a opção **Criar** (parte superior direita), seguido por **Pasta**:

![Opção Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Uma caixa de diálogo é aberta, onde você pode inserir os detalhes e confirmar com **Criar**:

![Caixa de diálogo Criar pasta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de caminhos e tags para limitar os Modelos de fragmentos de conteúdo disponíveis na pasta {#tags-paths-for-models-in-folder}

Esta seção é um pouco mais avançada. Na verdade, você não precisa se estiver apenas começando e tentando coisas, mas isso é mais útil quando há muitos fragmentos. Por isso é bom saber sobre ela mesmo que ainda não a utilize.

Seu Arquiteto de conteúdo terá criado todos os Modelos de fragmentos de conteúdo necessários para seu projeto atual e talvez alguns outros projetos também. Para ajudar a simplificar as coisas para você mesmo e para outros autores, você pode limitar a lista de modelos disponíveis para uma pasta específica.

Depois de criar a pasta, você pode abrir suas **Propriedades**. Aqui estão várias guias com informações e detalhes de configuração sobre a pasta. Especificamente para Fragmentos de conteúdo, você pode usar a guia **Políticas** para definir caminhos e/ou tags específicas para a pasta. Isso limita os Modelos de fragmentos do conteúdo disponíveis para uso na pasta, pois significa que eles devem atender a esses critérios antes que possam ser usados para gerar fragmentos nessa pasta.

![Criar propriedades de pasta - Políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Você pode ler mais detalhes em Modelos de fragmentos do conteúdo - Permitir Modelos de fragmentos do conteúdo na pasta de ativos.

Em seguida, navegue por essas pastas para criar e editar os Fragmentos de conteúdo.

#### Por segurança - Configuração dos serviços de pasta na nuvem {#cloud-services-folder}

Por segurança...

Você provavelmente receberá uma pasta inicial em que poderá criar suas pastas. Isso ocorre porque alguns detalhes de configuração devem ser aplicados (geralmente por um Desenvolvedor ou Administrador do Sistema) à pasta raiz. Isso provavelmente não é de seu interesse, mas se necessário, você pode verificar o **Configuração** no **Cloud Service** da pasta **Propriedades**:

![Criar propriedades de pasta - Configuração](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Você pode ler mais em Aplicar a configuração à sua pasta de Ativos.

### Criação de um Fragmento de conteúdo {#creating-fragment}

A criação de um fragmento de conteúdo é muito semelhante - você só usa o **Fragmento do conteúdo** opção em vez disso:

![Opção Criar fragmento de conteúdo](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Desta vez, um assistente é aberto. A primeira etapa é selecionar o Modelo de fragmento de conteúdo no qual o fragmento será baseado:

![Criar fragmento de conteúdo — selecionar modelo](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Depois de continuar com **Próxima** você pode fornecer os detalhes (**Básico** e **Avançado**) para o fragmento:

![Criar fragmento de conteúdo: fornecer um nome](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirmar com **Criar** e você poderá **Abertura** o fragmento no editor.

### Edição de um fragmento {#editing-fragment}

Você pode abrir um fragmento imediatamente após criá-lo ou selecionando-o no console de Ativos.

Quando o editor for aberto pela primeira vez, você verá:

* Uma lista de ícones no lado esquerdo - isso lhe dá acesso a várias áreas de funcionalidade. O editor é aberto na guia **Variações**, em que ocorre a maioria das edições. Você também pode estar interessado nas guias **Anotações** e **Metadados**.

* Um cabeçalho com as informações sobre o fragmento e acesso a várias ações.

* A área de edição principal - isso depende do modelo usado para criar o fragmento.

Como exemplos:

* Um fragmento que apenas requer várias informações, algumas com um tipo específico. Para conteúdo headless, as referências são fundamentais. Você aprenderá sobre isso mais tarde na sua jornada.

  ![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Um fragmento que permite escrever uma longa seção de texto. Aqui há opções adicionais para gerenciar e formatar o texto. Você pode até mesmo abrir os campos de texto individuais em um editor de tela cheia (usando o ícone de tela pequena à direita)

  ![Editor de Fragmentos de conteúdo - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>A documentação específica do projeto pode ser necessária para ajudar os autores com detalhes sobre como preencher alguns campos com êxito.
>
>Consulte Modelos de fragmentos de conteúdo - Tipos de dados e propriedades para detalhes genéricos.

Confirme suas atualizações com **Salvar** ou **Salvar e fechar**.

>[!NOTE]
>
>Para obter mais detalhes, leia Variações - Criação de Fragmentos de conteúdo.

#### Com o que você (provavelmente) não precisa se preocupar {#what-you-probably-do-not-need-to-worry-about}

Essa seção pode parecer um pouco estranha, mas após abrir o Editor de Fragmento de conteúdo e começar a explorar, você verá várias opções que (provavelmente) não se aplicam à sua jornada headless como um Autor de conteúdo. Então, isto é apenas um rápido aviso do que você deve ser capaz de ignorar no contexto headless:

* **Modelos de fragmentos de conteúdo**

  Você verá o nome do Modelo do Fragmento de Conteúdo na parte superior do editor - diretamente sob o nome do fragmento. Este também é um link que leva você ao editor de modelo.
Os Modelos de fragmentos de conteúdo são essenciais para os Fragmentos de conteúdo, pois definem a estrutura usada. No entanto, criá-los e editá-los é (geralmente) responsabilidade de outro perfil, o Arquiteto de conteúdo.

  >[!NOTE]
  >
  >Se quiser saber mais, leia a Jornada do arquiteto de conteúdo do AEM Headless.

* **Conteúdo associado**

  Este é bastante óbvio, pois é uma guia no editor.

  Fragmentos de conteúdo foram disponibilizados no AEM há algumas versões. Originalmente, eles eram disponibilizados para uso “tradicional” durante a criação de páginas....e ainda são usados nesse contexto. Isso pode envolver a associação de ativos (por exemplo, imagens) que, embora não incorporados ao fragmento, precisam estar disponíveis para o autor ao criar uma página.

* **Visualização**

  Esta é outra guia no editor e fornece uma visualização técnica, destinada principalmente aos desenvolvedores.

* **Atualizar referências de página**

  Essa ação está disponível no menu suspenso **...** (reticências). Não é interessante para autores headless, pois se relaciona à criação de página.

### Publicação {#publishing}

<!-- needs more details -->

Após concluir o fragmento, é possível **Publicar** para que esteja disponível para os aplicativos headless.

As ações de publicação estão disponíveis no editor (ou na barra de ferramentas do **Assets** console):

![Editor de fragmento de conteúdo - Meu fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## O que vem a seguir {#whats-next}

Agora que você aprendeu o básico, o próximo passo é [Saiba mais sobre referências](references.md). Isso introduzirá e discutirá as várias referências disponíveis e como criar níveis de estrutura com as Referências de fragmento - uma parte essencial da criação para o headless.

## Recursos adicionais {#additional-resources}

* [Conceitos de criação](/help/sites-authoring/author.md)

* [Manuseio básico](/help/sites-authoring/basic-handling.md) - esta página se baseia principalmente no console **Sites**, mas muitos/a maioria dos recursos também são relevantes para a criação **Fragmentos de conteúdo** no console **Ativos**.

   * [Painel Navegação](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [O Cabeçalho](/help/sites-authoring/basic-handling.md#the-header)

   * [Barra de ferramentas de ação](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [Ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)

   * [Visualização e seleção de recursos](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Seletor de painéis](/help/sites-authoring/basic-handling.md#rail-selector)

* [Trabalho com Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)

   * [Gerenciamento dos Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)

      * [Aplique a configuração à sua pasta de ativos](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Criação de um Fragmento de conteúdo](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variações: criação de Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de conteúdo - Tipos de dados](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de conteúdo: propriedades](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmentos de conteúdo: permitir modelos de fragmento de conteúdo na pasta Ativos](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guias de introdução
   * [Criação de uma pasta de ativos Guia de início rápido do Headless](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Jornada do arquiteto de conteúdo do AEM Headless](/help/journey-headless/architect/overview.md)

* [Jornada de tradução headless do AEM](/help/journey-headless/translation/overview.md)
