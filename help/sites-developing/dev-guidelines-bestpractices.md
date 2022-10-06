---
title: Desenvolvimento de AEM - Diretrizes e práticas recomendadas
seo-title: AEM Development - Guidelines and Best Practices
description: Diretrizes e práticas recomendadas para desenvolver o AEM
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Desenvolvimento de AEM - Diretrizes e práticas recomendadas{#aem-development-guidelines-and-best-practices}

## Diretrizes para usar modelos e componentes {#guidelines-for-using-templates-and-components}

AEM componentes e modelos formam um kit de ferramentas muito potente. Eles podem ser usados pelos desenvolvedores para fornecer aos usuários empresariais do site, editores e administradores a funcionalidade de adaptar seus sites às necessidades comerciais em constante mudança (agilidade do conteúdo), além de manter o layout uniforme dos sites (proteção da marca).

Um desafio típico para uma pessoa responsável por um site, ou conjunto de sites (por exemplo, em uma filial de uma empresa global), é introduzir um novo tipo de apresentação de conteúdo em seus sites.

Suponhamos que seja necessário adicionar uma página de listagem aos sites, que lista extratos de outros artigos já publicados. A página deve ter o mesmo design e estrutura que o resto do site.

A forma recomendada de abordar esse desafio seria:

* Reutilize um modelo existente para criar um novo tipo de página. O modelo define a estrutura da página (elementos de navegação, painéis e assim por diante), que é aprimorada ainda mais por seu design (CSS, gráficos).
* Use o sistema de parágrafo (parsys/iparsys) nas novas páginas.
* Defina o direito de acesso ao modo Design dos sistemas de parágrafo, de modo que somente pessoas autorizadas (geralmente o administrador) possam alterá-las.
* Defina os componentes permitidos no sistema de parágrafo específico para que os editores possam colocar os componentes necessários na página. Em nosso caso, pode ser um componente de lista, que pode atravessar uma subárvore de páginas e extrair as informações de acordo com regras predefinidas.
* Os editores adicionam e configuram os componentes permitidos, nas páginas pelas quais são responsáveis, para fornecer a funcionalidade solicitada (informações) aos negócios.

Isso ilustra como essa abordagem capacita os usuários e administradores contribuidores do site a responder às necessidades dos negócios rapidamente, sem exigir o envolvimento de equipes de desenvolvimento. Métodos alternativos, como a criação de um novo modelo, geralmente é um exercício dispendioso, que requer um processo de gerenciamento de alterações e o envolvimento da equipe de desenvolvimento. Isso torna todo o processo muito mais longo e dispendioso.

Os desenvolvedores de sistemas baseados em AEM devem, portanto, utilizar:

* modelos e controle de acesso ao design do sistema de parágrafo para uniformidade e proteção da marca
* sistema de parágrafo, incluindo suas opções de configuração para flexibilidade.

As seguintes regras gerais para desenvolvedores fazem sentido na maioria dos projetos usuais:

* Mantenha o número de modelos baixo - tão baixo quanto o número de estruturas de página fundamentalmente diferentes nos sites.
* Forneça a flexibilidade e os recursos de configuração necessários para seus componentes personalizados.
* Maximize o uso do poder e da flexibilidade AEM sistema de parágrafo - os componentes parsys e iparsys.

### Personalização de componentes e outros elementos {#customizing-components-and-other-elements}

Ao criar seus próprios componentes ou personalizar um componente existente, geralmente é mais fácil (e seguro) reutilizar as definições existentes. Os mesmos princípios também se aplicam a outros elementos dentro do AEM, por exemplo, o manipulador de erros.

Isso pode ser feito copiando e sobrepondo a definição existente. Em outras palavras, copiar a definição de `/libs` para `/apps/<your-project>`. Essa nova definição, em `/apps`, pode ser atualizado de acordo com suas necessidades.

>[!NOTE]
>
>Consulte [Uso de sobreposições](/help/sites-developing/overlays.md) para obter mais detalhes.

Por exemplo:

* [Personalização de um componente](/help/sites-developing/components.md)

   Isso envolvia a sobreposição de uma definição de componente:

   * Crie uma nova pasta de componentes em `/apps/<website-name>/components/<MyComponent>` copiando um componente existente:

      * Por exemplo, para personalizar a cópia do componente de Texto:

         * de `/libs/foundation/components/text`
         * para `/apps/myProject/components/text`

* [Personalização de páginas mostradas pelo Manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   Esse caso envolve a sobreposição de um servlet:

   * No repositório, copie os scripts padrão:

      * de `/libs/sling/servlet/errorhandler/`
      * para `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Você **não deve** altere qualquer coisa na `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>Para configuração e outras alterações:
>
>1. copiar o item em `/libs` para `/apps`
>1. fazer qualquer alteração no `/apps`


## Quando usar os queries JCR e quando não usá-los {#when-to-use-jcr-queries-and-when-not-to-use-them}

Consultas de JCR são uma ferramenta poderosa quando empregadas corretamente. São adequados para:

* consultas reais de usuários finais, como pesquisas de texto completo no conteúdo.
* ocasiões em que o conteúdo estruturado precisa ser encontrado em todo o repositório.

   Nesses casos, verifique se as consultas só são executadas quando absolutamente necessário, por exemplo, na ativação de componentes ou na invalidação do cache (em vez de, por exemplo, Etapas de fluxos de trabalho, Manipuladores de evento que acionam modificações de conteúdo, Filtros etc).

Consultas JCR nunca devem ser usadas para solicitações de renderização pura. Por exemplo, Consultas de JCR não são apropriadas para

* renderização da navegação
* criação de uma visão geral dos &quot;10 itens de notícias mais recentes&quot;
* mostrar contagens de itens de conteúdo

Para renderizar o conteúdo, use o acesso de navegação à árvore de conteúdo em vez de executar uma Consulta JCR.

>[!NOTE]
>
>Se você usar a variável [Query Builder](/help/sites-developing/querybuilder-api.md), use Consultas JCR, já que o Construtor de consultas gera Consultas JCR no capô.

## Considerações de segurança {#security-considerations}

>[!NOTE]
>
>Também vale a pena fazer referência ao [lista de verificação de segurança](/help/sites-administering/security-checklist.md).

### Sessões JCR (Repositório) {#jcr-repository-sessions}

Você deve usar a sessão do usuário, não a sessão administrativa. Isso significa que você deve usar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contra script entre sites (XSS) {#protect-against-cross-site-scripting-xss}

O cross-site scripting (XSS) permite que invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários maliciosos da Web para ignorar controles de acesso.

AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. A prevenção do XSS recebe a prioridade mais alta durante o desenvolvimento e o teste.

Além disso, um firewall de aplicativo Web, como [mod_security para Apache](https://modsecurity.org)O pode fornecer controle central e confiável sobre a segurança do ambiente de implantação e proteção contra ataques de script entre sites não detectados anteriormente.

>[!CAUTION]
>
>O código de exemplo fornecido com o AEM pode não se proteger contra tais ataques e geralmente depende da filtragem de solicitações por um firewall de aplicativo da Web.

O gabarito da API XSS contém informações que você precisa saber para usar a API XSS e tornar um aplicativo AEM mais seguro. Você pode baixá-lo aqui:

O gabarito XSSAPI.

[Obter arquivo](assets/xss_cheat_sheet_2016.pdf)

### Proteção da comunicação de informações confidenciais {#securing-communication-for-confidential-information}

Quanto a qualquer pedido na Internet, certifique-se de que, ao transportar informações confidenciais

* o tráfego é protegido por SSL
* HTTP POST, se aplicável

Isso se aplica a informações confidenciais do sistema (como configuração ou acesso administrativo), bem como informações confidenciais para seus usuários (como seus detalhes pessoais)

## Tarefas de desenvolvimento distintas {#distinct-development-tasks}

### Personalização de páginas de erro {#customizing-error-pages}

Páginas de erro podem ser personalizadas para AEM. Isso é aconselhável para que a instância não revele rastreamentos sling em erros internos do servidor.

Consulte [Personalização de páginas de erro mostradas pelo manipulador de erros](/help/sites-developing/customizing-errorhandler-pages.md) para obter detalhes completos.

### Abrir arquivos no processo Java {#open-files-in-the-java-process}

Como AEM pode acessar um grande número de arquivos, é recomendável que o número de [abrir arquivos para um processo Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) ser explicitamente configurado para AEM.

Para minimizar esse problema, o desenvolvimento deve garantir que qualquer arquivo aberto seja fechado corretamente assim que possível (significativo).
