---
title: Desenvolvimento de AEM - diretrizes e práticas recomendadas
seo-title: Desenvolvimento de AEM - diretrizes e práticas recomendadas
description: Diretrizes e práticas recomendadas para o desenvolvimento de AEM
seo-description: Diretrizes e práticas recomendadas para o desenvolvimento de AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---


# Desenvolvimento de AEM - Diretrizes e Práticas recomendadas{#aem-development-guidelines-and-best-practices}

## Diretrizes para o uso de modelos e componentes {#guidelines-for-using-templates-and-components}

AEM componentes e modelos formam um kit de ferramentas muito poderoso. Eles podem ser usados por desenvolvedores para fornecer aos usuários empresariais, editores e administradores do site a funcionalidade de adaptar seus sites às necessidades comerciais em mudança (agilidade de conteúdo) e, ao mesmo tempo, manter o layout uniforme dos sites (proteção da marca).

Um desafio típico para uma pessoa responsável por um site, ou conjunto de sites (por exemplo, em uma filial de uma empresa global), é introduzir um novo tipo de apresentação de conteúdo em seus sites.

Suponhamos que seja necessário adicionar uma página de newslist aos websites, que lista extratos de outros artigos já publicados. A página deve ter o mesmo design e estrutura que o restante do site.

A forma recomendada de abordar este desafio seria:

* Reutilize um modelo existente para criar um novo tipo de página. O modelo define aproximadamente a estrutura da página (elementos de navegação, painéis e assim por diante), que é aprimorada pelo design (CSS, gráficos).
* Use o sistema de parágrafo (parsys/iparsys) nas novas páginas.
* Defina o direito de acesso ao modo Design dos sistemas de parágrafo, para que somente pessoas autorizadas (geralmente o administrador) possam alterá-las.
* Defina os componentes permitidos no sistema de parágrafo fornecido para que os editores possam colocar os componentes necessários na página. Em nosso caso, pode ser um componente de lista, que pode atravessar uma subárvore de páginas e extrair as informações de acordo com regras predefinidas.
* Os editores adicionam e configuram os componentes permitidos, nas páginas pelas quais eles são responsáveis, para fornecer a funcionalidade solicitada (informações) aos negócios.

Isso ilustra como essa abordagem permite que os usuários e administradores do site que contribuem respondam às necessidades dos negócios rapidamente, sem a necessidade do envolvimento das equipes de desenvolvimento. Os métodos alternativos, como a criação de um novo modelo, são geralmente um exercício dispendioso, exigindo um processo de gerenciamento de alterações e envolvimento da equipe de desenvolvimento. Isto torna todo o processo muito mais longo e dispendioso.

Os desenvolvedores de sistemas baseados em AEM devem, por conseguinte, utilizar:

* modelos e controle de acesso para o design do sistema de parágrafo para uniformidade e proteção da marca
* sistema de parágrafo incluindo suas opções de configuração para flexibilidade.

As seguintes regras gerais para os desenvolvedores fazem sentido na maioria dos projetos habituais:

* Mantenha o número de modelos baixo - tão baixo quanto o número de estruturas de página fundamentalmente diferentes nos sites.
* Ofereça flexibilidade e recursos de configuração necessários para seus componentes personalizados.
* Maximize o uso do poder e da flexibilidade AEM sistema de parágrafo - os componentes parsys e iparsys.

### Personalização de componentes e outros elementos {#customizing-components-and-other-elements}

Ao criar seus próprios componentes ou personalizar um componente existente, geralmente é mais fácil (e mais seguro) reutilizar as definições existentes. Os mesmos princípios também se aplicam a outros elementos dentro do AEM, por exemplo, o manipulador de erros.

Isso pode ser feito copiando e sobrepondo a definição existente. Em outras palavras, copiar a definição de `/libs` para `/apps/<your-project>`. Essa nova definição, em `/apps`, pode ser atualizada de acordo com seus requisitos.

>[!NOTE]
>
>Consulte [Usando Sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

Por exemplo:

* [Personalização de um componente](/help/sites-developing/components.md)

   Isso envolveu sobrepor uma definição de componente:

   * Crie uma nova pasta de componentes em `/apps/<website-name>/components/<MyComponent>` copiando um componente existente:

      * Por exemplo, para personalizar a cópia do componente de Texto:

         * de `/libs/foundation/components/text`
         * para `/apps/myProject/components/text`

* [Personalização de páginas mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Esse caso envolve sobreposição de um servlet:

   * No repositório, copie os scripts padrão:

      * de `/libs/sling/servlet/errorhandler/`
      * para `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Você **não deve** alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos).
>
>Para configurações e outras alterações:
>
>1. copie o item em `/libs` para `/apps`
>1. faça quaisquer alterações em `/apps`


## Quando usar Query JCR e quando não usá-los {#when-to-use-jcr-queries-and-when-not-to-use-them}

Os Query JCR são uma ferramenta poderosa quando empregados corretamente. São adequados para:

* query reais do usuário final, como pesquisas de texto completo no conteúdo.
* ocasiões em que o conteúdo estruturado precisa ser encontrado em todo o repositório.

   Nesses casos, verifique se os query só são executados quando absolutamente necessário, por exemplo, na ativação do componente ou na invalidação do cache (em vez de, por exemplo, Etapas do Workflows, Manipuladores de Evento que acionam modificações de conteúdo, Filtros etc).

Os Query JCR nunca devem ser usados para solicitações de renderização pura. Por exemplo, Query JCR não são apropriados para

* renderização da navegação
* criação de uma visão geral dos 10 itens de notícias mais recentes
* mostrar contagens de itens de conteúdo

Para renderizar conteúdo, use o acesso de navegação à árvore de conteúdo em vez de executar um Query JCR.

>[!NOTE]
>
>Se você usar o [Construtor de Query](/help/sites-developing/querybuilder-api.md), usará Query JCR, já que o Construtor de Query gera Query JCR sob o capô.


## Considerações sobre segurança {#security-considerations}

>[!NOTE]
>
>Também vale a pena fazer referência à [lista de verificação de segurança](/help/sites-administering/security-checklist.md).

### Sessões JCR (Repositório) {#jcr-repository-sessions}

Você deve usar a sessão do usuário, não a sessão administrativa. Isso significa que você deve usar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contra script entre sites (XSS) {#protect-against-cross-site-scripting-xss}

Scripts entre sites (XSS) permitem que os invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários maliciosos da Web para ignorar controles de acesso.

AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. A prevenção do XSS é atribuída à prioridade mais alta durante o desenvolvimento e o teste.

Além disso, um firewall de aplicativo da Web, como [mod_security para Apache](https://modsecurity.org), pode fornecer controle central e confiável sobre a segurança do ambiente de implantação e proteger contra ataques de script entre sites não detectados anteriormente.

>[!CAUTION]
>
>O exemplo de código fornecido com AEM pode não proteger contra tais ataques e geralmente depende da filtragem de solicitações por um firewall de aplicativos da Web.

A folha de verificação da API XSS contém informações que você precisa saber para usar a API XSS e tornar um aplicativo AEM mais seguro. Você pode baixá-lo aqui:

A folha de truques XSSAPI.

[Obter arquivo](assets/xss_cheat_sheet_2016.pdf)

### Protegendo a comunicação para informações confidenciais {#securing-communication-for-confidential-information}

Quanto a qualquer pedido de acesso à Internet, certifique-se de que, ao transportar informações confidenciais,

* o tráfego é protegido por SSL
* POST HTTP é usado, se aplicável

Isso se aplica às informações confidenciais do sistema (como configuração ou acesso administrativo), bem como às informações confidenciais dos usuários (como seus detalhes pessoais)

## Tarefas de Desenvolvimento Distintas {#distinct-development-tasks}

### Personalizando páginas de erro {#customizing-error-pages}

As páginas de erro podem ser personalizadas para AEM. Isso é recomendável para que a instância não revele rastreamentos sling em erros internos do servidor.

Consulte [Personalizando páginas de erro mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md) para obter detalhes completos.

### Abrir arquivos no processo Java {#open-files-in-the-java-process}

Como AEM pode acessar um grande número de arquivos, recomenda-se que o número de [arquivos abertos para um processo Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) seja configurado explicitamente para AEM.

Para minimizar esse problema, o desenvolvimento deve garantir que todos os arquivos abertos sejam fechados corretamente assim que possível (significativo).
