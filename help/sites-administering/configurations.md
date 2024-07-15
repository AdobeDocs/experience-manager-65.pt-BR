---
title: Configurações e o navegador de configuração
description: Entenda as configurações do AEM e como elas gerenciam as configurações do espaço de trabalho no AEM.
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 4%

---

# Configurações e o navegador de configuração {#configuration-browser}

As configurações do AEM servem para gerenciar configurações no AEM e servem como espaços de trabalho.

## O que é uma configuração? {#what-is-a-configuration}

Uma configuração pode ser considerada a partir de dois pontos de vista diferentes.

* [Um administrador](#configurations-administrator) usa configurações como espaços de trabalho dentro do AEM para definir e gerenciar grupos de configurações.
* [Um desenvolvedor](#configurations-developer) usa o mecanismo de configuração subjacente que implementa configurações para persistir e pesquisar configurações no AEM.

Em resumo: do ponto de vista de um administrador, as configurações são a forma como você cria espaços de trabalho para gerenciar configurações no AEM, enquanto o desenvolvedor deve entender como o AEM usa e gerencia essas configurações no repositório.

Independentemente da sua perspectiva, as configurações atendem a dois objetivos principais no AEM:

* As configurações ativam determinados recursos para determinados grupos de usuários.
* As configurações definem direitos de acesso para esses recursos.

## Configurações como administrador {#configurations-administrator}

O administrador e os autores do AEM podem considerar as configurações como espaços de trabalho. Esses espaços de trabalho podem ser usados para coletar grupos de configurações e seu conteúdo associado para fins organizacionais, implementando direitos de acesso para esses recursos.

Configurações podem ser criadas para vários recursos diferentes dentro do AEM.

* [Configurações na nuvem](/help/sites-administering/configurations.md)
* [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Modelos editáveis](/help/sites-authoring/templates.md)

### Exemplo {#administrator-example}

Por exemplo, um administrador pode criar duas configurações para Modelos editáveis.

* WKND-Geral
* WKND-Magazine

O administrador pode criar modelos de página gerais usando a configuração geral da WKND e, em seguida, modelos específicos para a revista em WKND-Magazine.

O administrador pode então associar o WKND-General a todo o conteúdo do site WKND. No entanto, a configuração WKND-Magazine seria associada somente ao site do periódico.

Ao fazer isso:

* Quando um autor de conteúdo cria uma página para a revista, ele pode escolher entre modelos gerais (WKND-Geral) ou modelos de revista (WKND-Revista).
* Quando um autor de conteúdo cria uma página para outra parte do site que não é a revista, ele só pode escolher entre os modelos gerais (WKND-Geral).

Configurações semelhantes são possíveis não apenas para modelos editáveis, mas também para configurações em nuvem, segmentos do ContextHub e modelos de fragmento de conteúdo.

### Usar o navegador de configuração {#using-configuration-browser}

O Navegador de configuração permite que um administrador crie, gerencie e configure facilmente direitos de acesso a configurações no AEM.

>[!NOTE]
>
>Somente é possível criar configurações usando o Navegador de Configuração se o usuário tiver direitos de `admin`. Direitos de administrador também são necessários para atribuir direitos de acesso à configuração ou para modificar uma configuração de outra forma.

#### Criação de uma configuração {#creating-a-configuration}

É simples criar uma configuração no AEM usando o Navegador de configuração.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Ferramentas** > **Geral** > **Navegador de Configuração**.
1. Clique em **Criar**.
1. Forneça um **Título** e um **Nome** para sua configuração.

   ![Criar configuração](assets/configuration-create.png)

   * O **Título** deve ser descritivo.
   * O **Nome** se tornará o nome do nó no repositório.
      * Ele é gerado automaticamente com base no título e ajustado de acordo com as [convenções de nomenclatura do AEM.](/help/sites-developing/naming-conventions.md)
      * Ele pode ser ajustado, se necessário.
1. Verifique o tipo de configurações que deseja permitir.
   * [Configurações na nuvem](/help/sites-administering/configurations.md)
   * [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Modelos editáveis](/help/sites-authoring/templates.md)
1. Clique em **Criar**.

>[!TIP]
>
>As configurações podem ser aninhadas.

#### Edição de configurações e seus direitos de acesso {#access-rights}

Se você pensar nas configurações como espaços de trabalho, os direitos de acesso poderão ser definidos nessas configurações para impor quem pode ou não acessar esses espaços de trabalho.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Ferramentas** > **Geral** > **Navegador de Configuração**.
1. Selecione a configuração que você deseja modificar e clique em **Propriedades** na barra de ferramentas.
1. Selecione os recursos adicionais que deseja adicionar à configuração.

   >[!NOTE]
   >
   >Não é possível desmarcar um recurso depois que a configuração é criada.

1. Use o botão **Permissões efetivas** para exibir uma matriz de funções e quais permissões elas são concedidas atualmente às configurações.
   ![Janela de permissões efetivas](assets/configuration-effective-permissions.png)
1. Para atribuir novas permissões, digite o nome do usuário ou do grupo no campo **Selecionar usuário ou grupo** da seção **Adicionar novas permissões**.
   * O campo **Selecionar usuário ou grupo** oferece preenchimento automático com base em usuários e funções existentes.
1. Selecione o usuário ou a função apropriada nos resultados de preenchimento automático.
   * É possível selecionar mais de um usuário ou função.
1. Verifique as opções de acesso que os usuários ou funções selecionados devem ter e clique em **Adicionar**.
   ![Adicionar direitos de acesso a uma configuração](assets/configuration-edit.png)
1. Repita as etapas para poder selecionar usuários ou funções e atribuir direitos de acesso adicionais conforme necessário.
1. Selecione **Salvar e fechar** quando terminar.

## Configurações como desenvolvedor {#configurations-developer}

Como desenvolvedor, é importante saber como o AEM as a Cloud Service funciona com configurações e como ele processa a resolução da configuração.

### Separação de configuração e conteúdo {#separation-of-config-and-content}

Embora o [administrador e os usuários possam considerar as configurações como locais de trabalho](#configurations-administrator) para gerenciar diferentes configurações e conteúdo, é importante entender que as configurações e o conteúdo são armazenados e gerenciados separadamente pelo AEM no repositório.

* `/content` é o lar de todo o conteúdo.
* `/conf` é o lar de todas as configurações.

O conteúdo faz referência à sua configuração associada por meio de uma propriedade `cq:conf`. O AEM faz uma pesquisa com base no conteúdo e em sua propriedade `cq:conf` contextual para encontrar a configuração apropriada.

### Exemplo {#developer-example}

Neste exemplo, vamos supor que você tenha algum código de aplicativo interessado nas configurações do DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

O ponto inicial de toda a pesquisa de configuração é um recurso de conteúdo, em algum lugar abaixo de `/content`. Pode ser uma página, um componente dentro de uma página, um ativo ou uma pasta DAM. Este é o conteúdo real para o qual você está procurando a configuração correta que se aplica neste contexto.

Agora, com o objeto `Conf` em mãos, você pode recuperar o item de configuração específico em que está interessado. Nesse caso, é `dam/imageserver`, que é uma coleção de configurações relacionadas a `imageserver`. A chamada `getItem` retorna um `ValueMap`. Em seguida, você lê uma propriedade de cadeia de caracteres `bgkcolor` e fornece um valor padrão de &quot;FFFFFF&quot;, caso a propriedade (ou o item de configuração inteiro) não esteja presente.

Agora vamos observar o conteúdo JCR correspondente:

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

Neste exemplo, você pode assumir uma pasta DAM específica do WKND aqui e uma configuração correspondente. Começando por essa pasta `/content/dam/wknd`, você pode ver que há uma propriedade de cadeia de caracteres chamada `cq:conf` que faz referência à configuração que deve ser aplicada à subárvore. A propriedade é definida no `jcr:content` de uma pasta ou página de ativos. Esses links `conf` são explícitos, portanto, é fácil segui-los apenas observando o conteúdo no CRXDE.

Pulando dentro de `/conf`, você pode seguir a referência e ver que há um nó `/conf/wknd`. Esta é uma configuração. Sua pesquisa é transparente para o código do aplicativo. O código de exemplo nunca tem uma referência dedicada a ele, ele está oculto atrás do objeto `Conf`. A configuração que se aplica é controlada por meio do conteúdo JCR.

Você pode ver que a configuração contém um nó `settings` de nome fixo que contém os itens reais, incluindo o `dam/imageserver` necessário nesse caso. Esse item pode ser considerado um &quot;documento de configurações&quot; e é representado por um `cq:Page`, incluindo um `jcr:content` que contém o conteúdo real.

Finalmente, você pode ver a propriedade `bgkcolor` de que o código de amostra precisa. O `ValueMap` que você recebe de `getItem` é baseado no nó `jcr:content` da página.

### Resolução da configuração {#configuration-resolution}

O exemplo básico acima mostrava uma única configuração. Mas há muitos casos em que você deseja ter configurações diferentes, como uma configuração global padrão, uma diferente para cada marca e talvez uma específica para seus subprojetos.

Para oferecer suporte a isso, a pesquisa de configuração no AEM tem um mecanismo de herança e fallback na seguinte ordem de preferência:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuração específica referenciada de `cq:conf` em algum lugar em `/content`
   * A hierarquia é arbitrária e pode ser projetada exatamente como a estrutura do site, não é o negócio do código do aplicativo saber isso
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>/<parentconfig>`
   * Percorrer pais para configurações de fallback
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>`
   * Percorrer pais para configurações de fallback
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/global`
   * Configurações globais do sistema
   * Padrões globais para sua instalação
   * Definido por uma função `admin`
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/apps`
   * Padrões do aplicativo
   * Corrigido na implantação do aplicativo
   * Somente leitura em tempo de execução
1. `/libs`
   * Padrões de produto para AEM
   * Alterável somente pelo Adobe, acesso ao projeto não permitido
   * Corrigido na implantação do aplicativo
   * Somente leitura em tempo de execução

### Usar configurações {#using-configurations}

As configurações no AEM são baseadas em configurações sensíveis ao contexto do Sling. Os pacotes Sling fornecem uma API de serviço que pode ser usada para obter configurações sensíveis ao contexto. As configurações sensíveis ao contexto são configurações relacionadas a um recurso de conteúdo ou a uma árvore de recursos, como foi [descrito no exemplo anterior.](#developer-example)

Para obter mais detalhes sobre configurações sensíveis ao contexto, exemplos e como usá-las, [consulte a documentação do Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Console da Web do ConfMgr {#confmgr-web-console}

Para fins de depuração e teste, há um console da Web **ConfMgr** em `https://<host>:<port>/system/console/conf`, que pode mostrar configurações para determinado caminho/item.

![ConfMgr](assets/configuration-confmgr.png)

Basta fornecer:

* **Caminho do conteúdo**
* **Item**
* **Usuário**

Para ver quais configurações são resolvidas e receber um código de exemplo que resolva essas configurações, selecione **Resolver**.

### Console da Web de configuração com reconhecimento de contexto {#context-aware-web-console}

Para fins de depuração e teste, há um console da Web **Configuração com Reconhecimento de Contexto** em `https://<host>:<port>/system/console/slingcaconfig`, que permite consultar configurações com reconhecimento de contexto no repositório e exibir suas propriedades.

![Console da Web de Configuração com Reconhecimento de Contexto](assets/configuration-context-aware-console.png)

Basta fornecer:

* **Caminho do conteúdo**
* **Nome da configuração**

Para recuperar os caminhos de contexto associados e as propriedades da configuração selecionada, selecione **Resolver**.
