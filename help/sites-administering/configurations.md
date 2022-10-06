---
title: Configurações e o navegador de configuração
description: Entenda AEM configurações e como elas gerenciam as configurações do espaço de trabalho em AEM.
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 6%

---

# Configurações e o navegador de configuração {#configuration-browser}

AEM configurações servem para gerenciar configurações no AEM e servir como espaços de trabalho.

## O que é uma configuração? {#what-is-a-configuration}

Uma configuração pode ser considerada a partir de dois pontos de vista diferentes.

* [Um administrador](#configurations-administrator) O usa configurações como espaços de trabalho no AEM para definir e gerenciar grupos de configurações.
* [Um desenvolvedor](#configurations-developer) O usa o mecanismo de configuração subjacente que implementa configurações para persistir e buscar configurações no AEM.

Em resumo: do ponto de vista do administrador, as configurações são a forma como você cria espaços de trabalho para gerenciar as configurações no AEM, enquanto o desenvolvedor deve entender como o AEM usa e gerencia essas configurações no repositório.

Independentemente da sua perspectiva, as configurações atendem a dois objetivos principais no AEM:

* As configurações permitem determinados recursos para determinados grupos de usuários.
* As configurações definem direitos de acesso para esses recursos.

## Configurações como administrador {#configurations-administrator}

O administrador do AEM e os autores podem considerar as configurações como espaços de trabalho. Esses espaços de trabalho podem ser usados para coletar grupos de configurações, bem como seu conteúdo associado para fins organizacionais, implementando direitos de acesso para esses recursos.

As configurações podem ser criadas para vários recursos diferentes no AEM.

* [Configurações da nuvem](/help/sites-administering/configurations.md)
* [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Modelos editáveis](/help/sites-authoring/templates.md)

### Exemplo {#administrator-example}

Por exemplo, um administrador pode criar duas configurações para Modelos editáveis.

* WKND-Geral
* WKND-Magazine

O administrador pode então criar modelos de página gerais usando a configuração WKND-General e, em seguida, modelos específicos para a revista em WKND-Magazine.

O administrador pode então associar o WKND-General a todo o conteúdo do site WKND. No entanto, a configuração da WKND-Magazine seria associada apenas ao site de revistas.

Ao fazer isso:

* Quando um autor de conteúdo cria uma nova página para a revista, o autor pode escolher entre modelos gerais (WKND-General) ou modelos de revista (WKND-Magazine).
* Quando um autor de conteúdo cria uma nova página para outra parte do site que não é a revista, o autor só pode escolher entre os modelos gerais (WKND-General).

Configurações semelhantes são possíveis não apenas para Modelos editáveis, mas também para Configurações de nuvem, Segmentos do ContextHub e Modelos de fragmento de conteúdo.

### Usar o navegador de configuração {#using-configuration-browser}

O Navegador de configuração permite que um administrador crie, gerencie e configure facilmente os direitos de acesso às configurações no AEM.

>[!NOTE]
>
>Só é possível criar configurações usando o Navegador de configuração se o usuário tiver `admin` direitos. `admin` direitos também são necessários para atribuir direitos de acesso à configuração ou modificar uma configuração de outra forma.

#### Criação de uma configuração {#creating-a-configuration}

É muito simples criar uma nova configuração no AEM usando o Navegador de configuração.

1. Efetue login AEM as a Cloud Service e, no menu principal, selecione **Ferramentas** -> **Geral** -> **Navegador de configuração**.
1. Toque ou clique em **Criar**.
1. Forneça um **Título** e um **Nome** para sua configuração.

   ![Criar configuração](assets/configuration-create.png)

   * O **Título** deve ser descritivo.
   * O **Nome** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado de acordo com as [convenções de nomenclatura do AEM.](/help/sites-developing/naming-conventions.md)
      * Ele pode ser ajustado, se necessário.
1. Verifique o tipo de configurações que deseja permitir.
   * [Configurações da nuvem](/help/sites-administering/configurations.md)
   * [Segmentos do Context Hub](/help/sites-administering/segmentation.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Modelos editáveis](/help/sites-authoring/templates.md)
1. Toque ou clique em **Criar**.

>[!TIP]
>
>As configurações podem ser aninhadas.

#### Editar configurações e seus direitos de acesso {#access-rights}

Se você pensar em configurações como espaços de trabalho, os direitos de acesso poderão ser definidos nessas configurações para impor quem pode ou não acessar esses espaços de trabalho.

1. Efetue login AEM as a Cloud Service e, no menu principal, selecione **Ferramentas** -> **Geral** -> **Navegador de configuração**.
1. Selecione a configuração que deseja modificar e toque ou clique em **Propriedades** na barra de ferramentas.
1. Selecione os recursos adicionais que deseja adicionar à configuração
   >[!NOTE]
   >
   >Não é possível desmarcar um recurso depois que a configuração é criada.
1. Use o **Permissões efetivas** para exibir uma matriz de funções e quais permissões são concedidas às configurações no momento.
   ![Janela de permissões efetivas](assets/configuration-effective-permissions.png)
1. Para atribuir novas permissões, insira o nome do usuário ou grupo na função **Selecionar usuário ou grupo** no campo **Adicionar novas permissões** seção.
   * O  **Selecionar usuário ou grupo** O campo oferece o preenchimento automático com base em usuários e funções existentes.
1. Selecione o usuário ou a função apropriada nos resultados de preenchimento automático.
   * Você pode selecionar mais de um usuário ou função.
1. Verifique as opções de acesso que os usuários ou funções selecionados devem ter e clique em **Adicionar**.
   ![Adicionar direitos de acesso a uma configuração](assets/configuration-edit.png)
1. Repita as etapas para selecionar usuários ou funções e atribuir direitos de acesso adicionais conforme necessário.
1. Toque ou clique **Salvar e fechar** quando terminar.

## Configurações como um desenvolvedor {#configurations-developer}

Como desenvolvedor, é importante saber como o AEM as a Cloud Service funciona com configurações e como ele processa a resolução da configuração.

### Separação de configuração e conteúdo {#separation-of-config-and-content}

Embora a variável [administradores e usuários podem considerar configurações como locais de trabalho](#configurations-administrator) para gerenciar configurações e conteúdo diferentes, é importante entender que as configurações e o conteúdo são armazenados e gerenciados separadamente pelo AEM no repositório.

* `/content` O é o local de todo o conteúdo.
* `/conf` O é o local de todas as configurações.

O conteúdo faz referência à configuração associada por meio de uma `cq:conf` propriedade. AEM realiza uma pesquisa com base no conteúdo e é contextual `cq:conf` para encontrar a configuração apropriada.

### Exemplo {#developer-example}

Neste exemplo, suponhamos que você tenha algum código de aplicativo interessado nas configurações do DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

O ponto de partida de toda a pesquisa de configuração é um recurso de conteúdo, geralmente em algum lugar em `/content`. Pode ser uma página, um componente dentro de uma página, um ativo ou uma pasta DAM. Este é o conteúdo real para o qual estamos procurando a configuração correta que se aplica neste contexto.

Agora com o `Conf` em mãos, podemos recuperar o item de configuração específico em que estamos interessados. Nesse caso, é `dam/imageserver`, que é uma coleção de configurações relacionadas ao `imageserver`. O `getItem` chamada retorna um `ValueMap`. Então, lemos um `bgkcolor` propriedade string e forneça um valor padrão de &quot;FFFFF&quot; caso a propriedade (ou o item de configuração inteiro) não esteja presente.

Agora vamos analisar o conteúdo do JCR correspondente:

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

Neste exemplo, assumimos uma pasta DAM específica do WKND aqui e uma configuração correspondente. Iniciando nessa pasta `/content/dam/wknd`, veremos que há uma propriedade de string chamada `cq:conf` que faz referência à configuração que deve ser aplicada à subárvore. A propriedade geralmente será definida no `jcr:content` de uma pasta ou página de ativos. Esses `conf` os links são explícitos, portanto, é fácil segui-los observando apenas o conteúdo no CRXDE.

Pulando para dentro `/conf`, seguimos a referência e vemos que há uma `/conf/wknd` nó . Esta é uma configuração. Observe que sua pesquisa é totalmente transparente para o código do aplicativo. O código de exemplo nunca tem uma referência dedicada, está oculto atrás do `Conf` objeto. Qual configuração se aplica é totalmente controlada pelo conteúdo do JCR.

Vemos que a configuração contém um nome fixo `settings` nó que contém os itens reais, incluindo o `dam/imageserver` precisamos no nosso caso. Tal item pode ser considerado como um &quot;documento de configurações&quot; e geralmente é representado por um `cq:Page` incluindo um `jcr:content` mantendo o conteúdo real.

Finalmente, vemos a propriedade `bgkcolor` que nosso código de amostra precisa. O `ValueMap` voltamos de `getItem` é baseado no `jcr:content` nó .

### Resolução de Configuração {#configuration-resolution}

O exemplo básico acima mostrou uma única configuração. Mas há muitos casos em que você deseja ter configurações diferentes, como uma configuração global padrão, uma diferente para cada marca e talvez uma específica para seus subprojetos.

Para dar suporte a isso, a pesquisa de configuração no AEM tem o mecanismo de herança e fallback na seguinte ordem de preferência:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuração específica referenciada de `cq:conf` em algum lugar em `/content`
   * A hierarquia é arbitrária e pode ser projetada da mesma forma que a estrutura do site, não é da empresa do código de aplicativo saber isso
   * Alterável em tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>/<parentconfig>`
   * Pais transversais para configurações de fallback
   * Alterável em tempo de execução por usuários com privilégios de configuração
1. `/conf/<siteconfig>`
   * Pais transversais para configurações de fallback
   * Alterável em tempo de execução por usuários com privilégios de configuração
1. `/conf/global`
   * Configurações globais do sistema
   * Geralmente, os padrões globais para sua instalação
   * Definido por um `admin` função
   * Alterável em tempo de execução por usuários com privilégios de configuração
1. `/apps`
   * Padrões do aplicativo
   * Corrigido com a implantação do aplicativo
   * Somente leitura no tempo de execução
1. `/libs`
   * Padrões de produto AEM
   * Somente alterável pelo Adobe, o acesso ao projeto não é permitido
   * Corrigido com a implantação do aplicativo
   * Somente leitura no tempo de execução

### Uso de configurações {#using-configurations}

As configurações em AEM são baseadas em configurações sensíveis ao contexto do Sling. Os pacotes do Sling fornecem uma API de serviço que pode ser usada para obter configurações sensíveis ao contexto. As configurações sensíveis ao contexto são configurações relacionadas a um recurso de conteúdo ou a uma árvore de recursos como estava [descrito no exemplo anterior.](#developer-example)

Para obter mais detalhes sobre configurações sensíveis ao contexto, exemplos e como usá-las, [consulte a documentação do Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Console da Web do ConfMgr {#confmgr-web-console}

Para fins de depuração e teste, há um **ConfMgr** console da Web em `https://<host>:<port>/system/console/conf`, que pode mostrar configurações para um determinado caminho/item.

![ConfMgr](assets/configuration-confmgr.png)

Basta fornecer:

* **Caminho do conteúdo**
* **Item**
* **Usuário**

Clique em **Resolver** para ver quais configurações são resolvidas e receber o código de amostra que resolverá essas configurações.

### Console da Web de configuração sensível ao contexto {#context-aware-web-console}

Para fins de depuração e teste, há um **Configuração sensível ao contexto** console da Web em `https://<host>:<port>/system/console/slingcaconfig`, que permite consultar configurações sensíveis ao contexto no repositório e exibir suas propriedades.

![Console da Web de configuração sensível ao contexto](assets/configuration-context-aware-console.png)

Basta fornecer:

* **Caminho do conteúdo**
* **Nome da configuração**

Clique em **Resolver** para recuperar os caminhos de contexto e as propriedades associadas para a configuração selecionada.
