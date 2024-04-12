---
title: Introdução à tradução do AEM headless
description: Saiba como organizar seu conteúdo headless e como funcionam as ferramentas de tradução do AEM.
exl-id: 764f78a7-1d3d-4406-85b1-b80dffae2350
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 85%

---

# Introdução à Tradução do AEM Headless {#getting-started}

Saiba como organizar seu conteúdo headless e como funcionam as ferramentas de tradução do AEM.

## A história até agora {#story-so-far}

No documento anterior da jornada de tradução do AEM headless, [Saiba mais sobre o conteúdo headless e como traduzir no AEM](learn-about.md), você aprendeu a teoria básica do que seria um CMS headless e agora você deve:

* Entender os conceitos básicos de entrega de conteúdo headless.
* Estar familiarizado com como o AEM dá suporte a headless e tradução.

Este artigo se baseia nesses fundamentos para que você entenda como o AEM armazena e gerencia conteúdo headless e como você pode usar as ferramentas de tradução do AEM para traduzir esse conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como começar a traduzir conteúdo headless no AEM. Depois de ler esse documento, você deverá:

* Compreender a importância da estrutura de conteúdo para a tradução.
* Entenda como o AEM armazena conteúdo headless.
* Se familiarizar com as ferramentas de tradução do AEM.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar a traduzir o conteúdo do AEM headless.

### Conhecimento {#knowledge}

* Experiência em tradução de conteúdo em um CMS
* Experiência no uso de recursos básicos de um CMS em larga escala
* Possuir um conhecimento prático no manuseio básico do AEM
* Noções básicas do serviço de tradução que você está usando
* Ter uma compreensão básica do conteúdo que você está traduzindo

>[!TIP]
>
>Se você não estiver familiarizado com o uso de um CMS em larga escala como o AEM, considere revisar a documentação de [Manuseio básico](/help/sites-authoring/basic-handling.md) antes de continuar. A documentação de Manuseio básico não faz parte da jornada, portanto, retorne a esta página quando terminar.

### Ferramentas {#tools}

* Acesso à sandbox para testes de tradução do conteúdo
* Credenciais para se conectar ao serviço de tradução de sua preferência
* Ser membro do grupo `projects-administrators` no AEM

## Estrutura é fundamental {#content-structure}

O conteúdo do AEM, seja ele headless ou páginas da web tradicionais, é orientado por sua estrutura. O AEM impõe poucos requisitos à estrutura de conteúdo, mas uma consideração cuidadosa da hierarquia de conteúdo como parte do planejamento do projeto pode tornar a tradução muito mais simples.

>[!TIP]
>
>Planeje a tradução logo no início do projeto headless. Trabalhe em conjunto com o gerente do projeto e os arquitetos de conteúdo antecipadamente.
>
>Pode ser necessário um gerente de projetos de internacionalização como uma pessoa separada, cuja responsabilidade é definir qual conteúdo deve ser traduzido e qual não, além de qual conteúdo traduzido poderá ser modificado pelos produtores de conteúdo regionais ou locais.

## Como o AEM armazena conteúdo headless {#headless-content-in-aem}

Para o especialista em tradução, não é importante entender em detalhes como o AEM gerencia conteúdo headless. Entretanto, familiarizar-se com os conceitos e a terminologia básicos será útil, pois você poderá usar as ferramentas de tradução do AEM mais tarde. Principalmente, você precisa entender seu próprio conteúdo e como ele é estruturado para traduzi-lo efetivamente.

### Modelos de conteúdo {#content-models}

Para que o conteúdo headless seja entregue de forma consistente em canais, regiões e idiomas, o conteúdo deve ser altamente estruturado. O AEM usa Modelos de conteúdo para aplicar essa estrutura. Pense nos Modelos de conteúdo como um tipo de modelo ou padrão para criar conteúdo headless. Como cada projeto tem suas próprias necessidades, cada projeto define seus próprios Modelos de fragmento de conteúdo. O AEM não possui requisitos ou estrutura fixos para esses modelos.

O arquiteto de conteúdo funciona no início do projeto para definir essa estrutura. Como especialista em tradução, você deve trabalhar em conjunto com o arquiteto de conteúdo para entender e organizar o conteúdo.

>[!NOTE]
>
>É de responsabilidade do arquiteto de conteúdo definir os Modelos de conteúdo. O especialista em tradução deve estar familiarizado apenas com a estrutura, conforme descrito nas etapas a seguir.

Como os Modelos de conteúdo definem a estrutura do seu conteúdo, é necessário saber quais campos de seus modelos devem ser traduzidos. Geralmente, você trabalha com o arquiteto de conteúdo para definir isso. Para navegar pelos campos de seus modelos de conteúdo, siga as etapas abaixo.

1. Navegue até **Ferramentas** > **Assets** > **Modelos de fragmentos do conteúdo**.
1. Os Modelos de fragmentos de conteúdo geralmente são armazenados em uma estrutura de pastas. Clique na pasta do projeto.
1. Os modelos estão listados. Clique no modelo para ver os detalhes.
   ![Modelos de fragmentos do conteúdo](assets/content-fragment-models.png)
1. O **Editor do modelo de fragmento de conteúdo** abre.
   1. A coluna esquerda contém os campos do modelo. Essa coluna nos interessa.
   1. A coluna direita contém os campos que podem ser adicionados ao modelo. Essa coluna pode ser ignorada.
      ![Editor de modelos de fragmentos do conteúdo](assets/content-fragment-model-editor.png)
1. Clique em um dos campos do modelo. O AEM o marca e os detalhes desse campo são mostrados na coluna direita.
   ![Detalhe do Editor de modelo de fragmento de conteúdo](assets/content-fragment-model-editor-detail.png)

Anote o campo **Nome da propriedade** para todos os campos que devem ser traduzidos. Essas informações serão necessárias posteriormente na jornada. Esses **Nome da propriedade** s são necessários para informar ao AEM quais campos do seu conteúdo devem ser traduzidos.

>[!TIP]
>
>Geralmente, o arquiteto de conteúdo fornece ao especialista em tradução a **Nome da propriedade** s de todos os campos necessários para tradução. Esses nomes de campos são necessários para uma versão posterior da jornada. As etapas anteriores são fornecidas para a compreensão do especialista em tradução.

### Fragmentos de conteúdo {#content-fragments}

Os Modelos de conteúdo são usados pelos autores de conteúdo para criar o conteúdo headless real. Os autores de conteúdo selecionam em qual modelo basear seu conteúdo e, em seguida, criam fragmentos de conteúdo. Fragmentos de conteúdo são instâncias dos modelos e representam o conteúdo real que deve ser entregue de forma headless.

Se os Modelos de conteúdo são os padrões do conteúdo, os Fragmentos de conteúdo são o conteúdo real baseado nesses padrões. Os Fragmentos de conteúdo representam o conteúdo que deve ser traduzido.

Os Fragmentos de conteúdo são gerenciados como ativos no AEM como parte do Gerenciamento de ativos digitais (DAM). Isso é importante, pois todos estão localizados no caminho `/content/dam`.

## Estrutura de conteúdo recomendada {#recommended-structure}

Conforme recomendado anteriormente, trabalhe com seu arquiteto de conteúdo para determinar a estrutura de conteúdo apropriada para seu próprio projeto. No entanto, a seguinte estrutura é comprovada, simples e intuitiva, além de ser bastante eficaz.

Defina uma pasta base para o seu projeto em `/content/dam`.

```text
/content/dam/<your-project>
```

O idioma em que o conteúdo é criado é chamado de raiz de idioma. No nosso exemplo, é o inglês e deve estar dentro deste caminho.

```text
/content/dam/<your-project>/en
```

Todo o conteúdo do projeto que pode precisar ser localizado deve ser colocado na raiz de idioma.

```text
/content/dam/<your-project>/en/<your-project-content>
```

As traduções devem ser criadas como pastas irmãs ao lado da raiz de idioma, com o nome da pasta representando o código ISO-2 do idioma. Por exemplo, o alemão teria o seguinte caminho.

```text
/content/dam/<your-project>/de
```

>[!NOTE]
>
>O arquiteto de conteúdo geralmente é responsável pela criação dessas pastas de idioma. Se não forem criadas, o AEM não será capaz de criar trabalhos de tradução posteriormente.

A estrutura final pode ficar parecida com a seguinte.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

Você deve anotar o caminho específico do conteúdo, pois ele será necessário posteriormente para configurar a tradução.

>[!NOTE]
>
>Geralmente, é responsabilidade do arquiteto de conteúdo definir a estrutura do conteúdo, mas ele pode colaborar com o especialista em tradução.
>
>Ela é detalhada aqui para oferecer completude.

## Ferramentas de tradução do AEM {#translation-tools}

Agora que você entendeu o que são Fragmentos de conteúdo e a importância da estrutura do conteúdo, podemos ver como traduzir esse conteúdo. As ferramentas de tradução do AEM são bastante poderosas, mas são simples de entender em nível superior.

* **Conector de tradução** - O conector é o vínculo entre o AEM e o serviço de tradução usado.
* **Regras de tradução** - As regras definem qual conteúdo localizado em caminhos específicos deve ser traduzido.
* **Projetos de tradução** - Os projetos de tradução reúnem conteúdo que deve ser tratado como um único esforço de tradução e acompanha o progresso da tradução, interagindo com o conector para transmitir o conteúdo a ser traduzido e recebê-lo de volta do serviço de tradução.

Geralmente, você só configura o conector para a instância e as regras uma vez por projeto headless. Então, você usa projetos de tradução para traduzir seu conteúdo e manter suas traduções atualizadas continuamente.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de tradução headless, você deve:

* Compreender a importância da estrutura de conteúdo para a tradução.
* Entenda como o AEM armazena conteúdo headless.
* Se familiarizar com as ferramentas de tradução do AEM.

Desenvolva esse conhecimento e continue sua jornada de tradução AEM headless revisando o documento a seguir [Configurar a integração da tradução](configure-connector.md) onde você aprenderá a conectar o AEM a um serviço de tradução.|

## Recursos adicionais {#additional-resources}

Embora seja recomendável que você passe para a próxima parte da jornada de tradução headless revisando o documento [Configurar o conector de tradução](configure-connector.md), veja a seguir alguns recursos opcionais adicionais que fazem uma análise mais profunda de alguns conceitos mencionados neste documento, mas não são necessários para continuar na jornada headless.

* [Manuseio básico do AEM](/help/sites-authoring/basic-handling.md) - Conheça as noções básicas da interface de usuário do AEM para navegar e executar tarefas essenciais confortavelmente, como encontrar seu conteúdo.
* [Identificação do conteúdo a ser traduzido](/help/sites-administering/tc-rules.md) - Saiba como as regras de tradução identificam o conteúdo que precisa ser traduzido.
* [Configuração da estrutura de integração de tradução](/help/sites-administering/tc-tic.md) - Saiba como configurar a Estrutura de integração de tradução para integrar-se a serviços de tradução de terceiros.
* [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md) - Saiba como criar e gerenciar projetos de tradução automática e humana no AEM.
* Um [Introdução ao AEM as a Headless CMS](/help/sites-developing/headless/introduction.md)
* A variável [Portal do desenvolvedor de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutorials para headless no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR)
