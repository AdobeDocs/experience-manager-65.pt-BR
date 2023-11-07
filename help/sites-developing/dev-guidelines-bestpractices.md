---
title: Desenvolvimento do AEM - diretrizes e práticas recomendadas
description: Diretrizes e práticas recomendadas para o desenvolvimento de AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Desenvolvimento do AEM - diretrizes e práticas recomendadas{#aem-development-guidelines-and-best-practices}

## Diretrizes para o uso de modelos e componentes {#guidelines-for-using-templates-and-components}

Os componentes e modelos do Adobe Experience Manager (AEM) compõem um poderoso kit de ferramentas. Eles podem ser usados pelos desenvolvedores para fornecer aos usuários empresariais, editores e administradores do site a funcionalidade de adaptar seus sites às necessidades comerciais em constante mudança (agilidade do conteúdo). Tudo isso mantendo o layout uniforme dos sites (proteção da marca).

Um desafio típico para uma pessoa responsável por um site, ou conjunto de sites (por exemplo, em uma filial de uma empresa global), é introduzir um novo tipo de apresentação de conteúdo em seus sites.

Suponhamos que seja necessário adicionar uma página de lista de notícias aos sites, que lista extratos de outros artigos já publicados. A página deve ter o mesmo design e estrutura que o restante do site.

A maneira recomendada de abordar esse desafio seria:

* Reutilizar um modelo existente para criar um tipo de página. O modelo define grosseiramente a estrutura da página (elementos de navegação, painéis, etc.), que é ajustada ainda mais pelo seu design (CSS, gráficos).
* Use o sistema de parágrafo (parsys/iparsys) nas novas páginas.
* Defina o direito de acesso ao modo Design dos sistemas de parágrafo, para que somente pessoas autorizadas (geralmente o administrador) possam alterá-las.
* Defina os componentes permitidos no sistema de parágrafo fornecido para que os editores possam colocar os componentes necessários na página. Nesse caso, pode ser um componente de lista, que pode percorrer uma subárvore de páginas e extrair as informações de acordo com regras predefinidas.
* Os editores adicionam e configuram os componentes permitidos nas páginas pelas quais são responsáveis para fornecer a funcionalidade solicitada (informações) à empresa.

Isso ilustra como essa abordagem permite que os usuários e administradores contribuintes do site respondam rapidamente às necessidades comerciais, sem exigir o envolvimento de equipes de desenvolvimento. Métodos alternativos, como a criação de um modelo, geralmente são um exercício dispendioso, exigindo um processo de gerenciamento de alterações e o envolvimento da equipe de desenvolvimento. Isso torna todo o processo mais demorado e caro.

Por conseguinte, os criadores de sistemas baseados no AEM devem utilizar:

* modelos e controle de acesso ao design de sistema de parágrafo para uniformidade e proteção da marca
* sistema de parágrafo, incluindo suas opções de configuração para obter flexibilidade.

As seguintes regras gerais para desenvolvedores fazem sentido nos projetos mais comuns:

* Mantenha o número de modelos baixo - tão baixo quanto o número de estruturas de página fundamentalmente diferentes nos sites.
* Forneça a flexibilidade e os recursos de configuração necessários para seus componentes personalizados.
* Maximize o uso da potência e da flexibilidade do sistema de parágrafo AEM - os componentes parsys e iparsys.

### Personalização de Componentes e Outros Elementos {#customizing-components-and-other-elements}

Ao criar seus próprios componentes ou personalizar um componente existente, geralmente é mais fácil (e mais seguro) reutilizar as definições existentes. Os mesmos princípios também se aplicam a outros elementos dentro do AEM, por exemplo, o manipulador de erros.

Isso pode ser feito copiando e sobrepondo a definição existente. Em outras palavras, copiar a definição de `/libs` para `/apps/<your-project>`. Esta nova definição, em especial `/apps`, podem ser atualizados de acordo com suas necessidades.

>[!NOTE]
>
>Consulte [Uso de sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

Por exemplo:

* [Personalização de um componente](/help/sites-developing/components.md)

  Isso envolvia a sobreposição de uma definição de componente:

   * Criar uma pasta de componentes no `/apps/<website-name>/components/<MyComponent>` copiando um componente existente:

      * Por exemplo, para personalizar a cópia do componente de Texto:

         * de `/libs/foundation/components/text`
         * para `/apps/myProject/components/text`

* [Personalização de páginas mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Esse caso envolve a sobreposição de um servlet:

   * No repositório, copie um ou mais scripts padrão:

      * de `/libs/sling/servlet/errorhandler/`
      * para `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**Não** alterar qualquer item no `/libs` caminho.
>
>O motivo é porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).
>
>Para configuração e outras alterações:
>
>1. copiar o item em `/libs` para `/apps`
>1. fazer alterações em `/apps`

## Quando usar consultas JCR e quando não usá-las {#when-to-use-jcr-queries-and-when-not-to-use-them}

As consultas JCR são uma ferramenta poderosa quando empregadas corretamente. Eles são adequados para:

* consultas reais de usuários finais, como pesquisas de texto completo sobre conteúdo.
* ocasiões em que o conteúdo estruturado deve ser encontrado em todo o repositório.

  Nesses casos, certifique-se de que as consultas só sejam executadas quando necessário. Por exemplo, na ativação de componentes ou na invalidação do cache (em vez de, por exemplo, Etapas de fluxos de trabalho, Manipuladores de eventos que acionam modificações de conteúdo e Filtros).

Nunca use consultas JCR para solicitações de renderização puras. Por exemplo, consultas JCR não são apropriadas para o seguinte:

* navegação de renderização
* criação de uma visão geral &quot;os 10 itens de notícias mais recentes&quot;
* exibição de contagens de itens de conteúdo

Para renderizar conteúdo, use o acesso de navegação à árvore de conteúdo em vez de executar uma consulta JCR.

>[!NOTE]
>
>Se você usar o [Construtor de consulta](/help/sites-developing/querybuilder-api.md), você usa Consultas JCR, já que o Construtor de consultas gera Consultas JCR por baixo dos panos.
>

## Considerações sobre segurança {#security-considerations}

>[!NOTE]
>
>É igualmente útil fazer referência [lista de verificação de segurança](/help/sites-administering/security-checklist.md).

### Sessões JCR (Repositório) {#jcr-repository-sessions}

Use a sessão do usuário, não a sessão administrativa. Isso significa que você deve usar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contra Scripts entre sites (XSS) {#protect-against-cross-site-scripting-xss}

A criação de script entre sites (XSS) permite que invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários mal-intencionados da Web para ignorar controles de acesso.

O AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. É dada a maior prioridade à prevenção de XSS durante o desenvolvimento e o teste.

Além disso, um firewall de aplicativo web, como [mod_security para Apache](https://modsecurity.org)O, oferece controle confiável e central sobre a segurança do ambiente de implantação e proteção contra ataques de script entre sites não detectados anteriormente.

>[!CAUTION]
>
>O código de exemplo fornecido com o AEM pode não proteger contra esses ataques e geralmente depende da filtragem de solicitações por um firewall de aplicativo da Web.

A folha de características da API XSS contém informações que você deve saber para usar a API XSS e tornar um aplicativo AEM mais seguro. Você pode baixá-lo aqui:

A folha de características do XSSAPI.

[Obter arquivo](assets/xss_cheat_sheet_2016.pdf)

### Protegendo a comunicação para informações confidenciais {#securing-communication-for-confidential-information}

Quanto a qualquer aplicativo da Internet, certifique-se de que, ao transportar informações confidenciais

* o tráfego está protegido por SSL
* O POST HTTP é usado se aplicável

Isso se aplica às informações confidenciais para o sistema (como configuração ou acesso administrativo) e às informações confidenciais para seus usuários (como seus detalhes pessoais)

## Tarefas de desenvolvimento distintas {#distinct-development-tasks}

### Personalização de Páginas de Erro {#customizing-error-pages}

As páginas de erro podem ser personalizadas para AEM. Isso é aconselhável para que a instância não revele rastreamentos sling em erros internos do servidor.

Consulte [Personalização de páginas de erro mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md) para obter detalhes completos.

### Abrir arquivos no processo Java™ {#open-files-in-the-java-process}

Como o AEM pode acessar muitos arquivos, é recomendável que o número de [abrir arquivos para um processo Java™](/help/sites-deploying/configuring.md#open-files-in-the-java-process) ser configurados explicitamente para AEM.

Para minimizar esse problema, o desenvolvimento deve garantir que qualquer arquivo aberto seja fechado corretamente quando for possível (de forma significativa).
