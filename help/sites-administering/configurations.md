---
title: Configurações e o navegador de configuração
description: Entenda AEM configurações e como elas gerenciam as configurações de espaço de trabalho em AEM.
translation-type: tm+mt
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Configurações e o navegador de configuração {#configuration-browser}

AEM configurações servem para gerenciar configurações em AEM e servir como espaços de trabalho.

## O que é uma configuração? {#what-is-a-configuration}

Uma configuração pode ser considerada de dois pontos de vista diferentes.

* [Um administrador](#configurations-administrator) usa configurações como espaços de trabalho no AEM para definir e gerenciar grupos de configurações.
* [Um desenvolvedor](#configurations-developer) usa o mecanismo de configuração subjacente que implementa configurações para persistir e procurar configurações no AEM.

Em resumo: do ponto de visualização de um administrador, as configurações são a forma como você cria espaços de trabalho para gerenciar as configurações no AEM, enquanto o desenvolvedor deve entender como o AEM usa e gerencia essas configurações no repositório.

Independentemente da sua perspectiva, as configurações servem dois objetivos principais em AEM:

* As configurações permitem determinados recursos para determinados grupos de usuários.
* As configurações definem direitos de acesso para esses recursos.

## Configurações como administrador {#configurations-administrator}

O administrador do AEM e os autores podem considerar configurações como espaços de trabalho. Esses espaços de trabalho podem ser usados para reunir grupos de configurações, bem como seu conteúdo associado para fins organizacionais, implementando direitos de acesso para esses recursos.

As configurações podem ser criadas para vários recursos diferentes dentro do AEM.

* [Configurações da nuvem](/help/sites-administering/configurations.md)
* [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Modelos editáveis](/help/sites-authoring/templates.md)

### Exemplo {#administrator-example}

Por exemplo, um administrador pode criar duas configurações para Modelos editáveis.

* WKND-Geral
* WKND-Magazine

O administrador pode então criar modelos de página gerais usando a configuração WKND-General e, em seguida, modelos específicos para a revista em WKND-Magazine.

O administrador pode então associar o WKND-Geral a todo o conteúdo do site WKND. No entanto, a configuração da WKND-Magazine seria associada apenas ao site da revista.

Fazendo isso:

* Quando um autor de conteúdo cria uma nova página para a revista, o autor pode escolher entre modelos gerais (WKND-General) ou modelos de revista (WKND-Magazine).
* Quando um autor de conteúdo cria uma nova página para outra parte do site que não seja a revista, o autor só pode escolher entre os modelos gerais (WKND-General).

Configurações semelhantes são possíveis não apenas para modelos editáveis, mas também para configurações em nuvem, segmentos do ContextHub e modelos de fragmento de conteúdo.

### Usando o navegador de configuração {#using-configuration-browser}

O Navegador de configuração permite que um administrador crie, gerencie e configure facilmente os direitos de acesso às configurações no AEM.

>[!NOTE]
>
>Só é possível criar configurações usando o Navegador de configuração se o usuário tiver `admin` direitos. `admin` os direitos também são necessários para atribuir direitos de acesso à configuração ou modificar uma configuração de outra forma.

#### Criando uma configuração {#creating-a-configuration}

É muito simples criar uma nova configuração no AEM usando o Navegador de configuração.

1. Faça logon no AEM como um Cloud Service e, no menu principal, selecione **Ferramentas** -> **Geral** -> Navegador **de** configuração.
1. Toque ou clique em **Criar**.
1. Forneça um **Título** e um **Nome** para sua configuração.

   ![Criar configuração](assets/configuration-create.png)

   * O **Título** deve ser descritivo.
   * O **Nome** se tornará o nome do nó no repositório.
      * Será gerado automaticamente com base no título e ajustado de acordo com as convenções de nomenclatura [AEM.](/help/sites-developing/naming-conventions.md)
      * Pode ser ajustado, se necessário.
1. Verifique o tipo de configurações que deseja permitir.
   * [Configurações da nuvem](/help/sites-administering/configurations.md)
   * [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Modelos editáveis](/help/sites-authoring/templates.md)
1. Toque ou clique em **Criar**.

>[!TIP]
>
>As configurações podem ser aninhadas.

#### Edição de configurações e seus direitos de acesso {#access-rights}

Se você considerar configurações como espaços de trabalho, os direitos de acesso podem ser definidos nessas configurações para impor quem pode ou não acessar esses espaços de trabalho.

1. Faça logon no AEM como um Cloud Service e, no menu principal, selecione **Ferramentas** -> **Geral** -> Navegador **de** configuração.
1. Selecione a configuração que deseja modificar e toque ou clique em **Propriedades** na barra de ferramentas.
1. Selecione os recursos adicionais que deseja adicionar à configuração
   >[!NOTE]
   >
   >Não é possível desmarcar um recurso depois que a configuração é criada.
1. Use o botão Permissões **** eficazes para visualização de uma matriz de funções e quais permissões são concedidas atualmente às configurações.
   ![Janela de permissões efetivas](assets/configuration-effective-permissions.png)
1. Para atribuir novas permissões, digite o nome do usuário ou grupo no campo **Selecionar usuário ou grupo** na seção **Adicionar novas permissões** .
   * O campo **Selecionar usuário ou grupo** oferta a conclusão automática com base em usuários e funções existentes.
1. Selecione o usuário ou função apropriado nos resultados de preenchimento automático.
   * Você pode selecionar mais de um usuário ou função.
1. Verifique as opções de acesso que os usuários ou funções selecionados devem ter e clique em **Adicionar**.
   ![Adicionar direitos de acesso a uma configuração](assets/configuration-edit.png)
1. Repita as etapas para selecionar usuários ou funções e atribuir direitos de acesso adicionais, conforme necessário.
1. Toque ou clique em **Salvar e fechar** ao terminar.

## Configurações como desenvolvedor {#configurations-developer}

Como desenvolvedor, é importante saber como o AEM como Cloud Service funciona com configurações e como ele processa a resolução da configuração.

### Separação de configuração e conteúdo {#separation-of-config-and-content}

Embora o [administrador e os usuários possam considerar as configurações como locais](#configurations-administrator) de trabalho para gerenciar diferentes configurações e conteúdo, é importante entender que as configurações e o conteúdo são armazenados e gerenciados separadamente por AEM no repositório.

* `/content` é o lar de todo o conteúdo.
* `/conf` é o local de todas as configurações.

O conteúdo faz referência à configuração associada por meio de uma `cq:conf` propriedade. AEM realiza uma pesquisa com base no conteúdo e é uma `cq:conf` propriedade contextual localizar a configuração apropriada.

### Exemplo {#developer-example}

Neste exemplo, vamos supor que você tenha algum código de aplicativo que esteja interessado nas configurações de DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

O ponto de partida de toda a pesquisa de configuração é um recurso de conteúdo, geralmente em algum lugar em `/content`. Pode ser uma página, um componente dentro de uma página, um ativo ou uma pasta DAM. Este é o conteúdo real para o qual procuramos a configuração correta que se aplica neste contexto.

Agora com o `Conf` objeto em mãos, podemos recuperar o item de configuração específico em que estamos interessados. Nesse caso, é `dam/imageserver`, que é uma coleção de configurações relacionadas ao `imageserver`. A `getItem` chamada retorna um `ValueMap`. Em seguida, lemos uma propriedade de `bgkcolor` string e fornecemos um valor padrão de &quot;FFFFF&quot; caso a propriedade (ou o item de configuração inteiro) não esteja presente.

Agora vamos ver o conteúdo do JCR correspondente:

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

Neste exemplo, assumimos uma pasta DAM específica do WKND aqui e uma configuração correspondente. A partir dessa pasta `/content/dam/wknd`, veremos que há uma propriedade de string chamada `cq:conf` que faz referência à configuração que deve ser aplicada à subárvore. A propriedade geralmente será definida na pasta `jcr:content` de um ativo ou página. Esses `conf` links são explícitos, portanto, é fácil segui-los observando apenas o conteúdo no CRXDE.

Pulando dentro `/conf`, nós seguimos a referência e vemos que há um `/conf/wknd` nó. Esta é uma configuração. Observe que sua pesquisa é completamente transparente para o código do aplicativo. O código de exemplo nunca tem uma referência dedicada a ele, está oculto atrás do `Conf` objeto. A configuração que se aplica é completamente controlada pelo conteúdo do JCR.

Vemos que a configuração contém um `settings` nó com nome fixo que contém os itens reais, incluindo o `dam/imageserver` necessário no nosso caso. Tal item pode ser considerado como um &quot;documento de configurações&quot; e geralmente é representado por um `cq:Page` incluindo um `jcr:content` contendo o conteúdo real.

Finalmente, vemos a propriedade `bgkcolor` que nosso código de amostra precisa. A `ValueMap` partir da qual retornamos `getItem` é baseada no `jcr:content` nó da página.

### Resolução de configuração {#configuration-resolution}

O exemplo básico acima mostrava uma única configuração. Mas há muitos casos em que você deseja ter configurações diferentes, como uma configuração global padrão, uma configuração diferente para cada marca e talvez uma específica para seus subprojetos.

Para suportar isso, a pesquisa de configuração no AEM tem o mecanismo de herança e fallback na seguinte ordem de preferência:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuração específica mencionada de `cq:conf` algum lugar em `/content`
   * A hierarquia é arbitrária e pode ser projetada exatamente como a estrutura do site, não é da competência do código do aplicativo saber isso
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>/<parentconfig>`
   * Pais transversais para configurações de fallback
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>`
   * Pais transversais para configurações de fallback
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/conf/global`
   * Configurações globais do sistema
   * Geralmente, os padrões globais para sua instalação
   * Definido por uma `admin` função
   * Alterável no tempo de execução por usuários com privilégios de configuração
1. `/apps`
   * Padrões do aplicativo
   * Corrigido com a implantação do aplicativo
   * Somente leitura em tempo de execução
1. `/libs`
   * Padrões de produtos AEM
   * Somente alterável por Adobe, o acesso ao projeto não é permitido
   * Corrigido com a implantação do aplicativo
   * Somente leitura em tempo de execução

### Usando configurações {#using-configurations}

As configurações no AEM são baseadas em Configurações Sling sensíveis ao contexto. Os pacotes Sling fornecem uma API de serviço que pode ser usada para obter configurações sensíveis ao contexto. Configurações sensíveis ao contexto são configurações relacionadas a um recurso de conteúdo ou a uma árvore de recursos, conforme [descrito no exemplo anterior.](#developer-example)

Para obter mais detalhes sobre Configurações sensíveis ao contexto, exemplos e como usá-las, [consulte a documentação Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web Console {#confmgr-web-console}

Para fins de depuração e teste, há um console da Web do **ConfMgr** em `https://<host>:<port>/system/console/conf`, que pode mostrar configurações para um determinado caminho/item.

![ConfMgr](assets/configuration-confmgr.png)

Simplesmente forneça:

* **Caminho do conteúdo**
* **Item**
* **Usuário**

Clique em **Resolver** para ver quais configurações foram resolvidas e receba um código de amostra que resolverá essas configurações.

### Console Web de configuração sensível ao contexto {#context-aware-web-console}

Para fins de depuração e teste, há um console da Web de Configuração **sensível ao** contexto em `https://<host>:<port>/system/console/slingcaconfig`, que permite consultar configurações sensíveis ao contexto no repositório e exibir suas propriedades.

![Console da Web de configuração sensível ao contexto](assets/configuration-context-aware-console.png)

Simplesmente forneça:

* **Caminho do conteúdo**
* **Nome da configuração**

Clique em **Resolver** para recuperar os caminhos de contexto e as propriedades associadas para a configuração selecionada.
