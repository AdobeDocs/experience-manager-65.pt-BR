---
title: Modo de desenvolvedor
seo-title: Developer Mode
description: O modo Desenvolvedor abre um painel lateral com várias guias que fornecem a um desenvolvedor informações sobre a página atual
seo-description: Developer mode opens a side panel with several tabs that provide a developer with infomation about the current page
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# Modo de desenvolvedor{#developer-mode}

Ao editar páginas em AEM, vários [modos](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) estão disponíveis, incluindo o modo Desenvolvedor . Isso abre um painel lateral com várias guias que fornecem ao desenvolvedor informações sobre a página atual. As três guias são:

* **[Componentes](#components)** para exibir informações sobre estrutura e desempenho.
* **[Testes](#tests)** para executar testes e analisar os resultados.
* **[Erros](#errors)** para ver qualquer problema que esteja ocorrendo.

Isso ajuda um desenvolvedor a:

* Discover: quais páginas são compostas.
* Depuração: o que está acontecendo onde e quando, o que por sua vez ajuda a resolver os problemas.
* Teste: O aplicativo se comporta conforme esperado.

>[!CAUTION]
>
>Modo de desenvolvedor:
>
>* Está disponível somente na interface habilitada para toque (ao editar páginas).
>* Não está disponível em dispositivos móveis ou janelas pequenas no desktop (devido a restrições de espaço).
   >
   >   * Isso ocorre quando a largura é inferior a 1024px.
>* Está disponível somente para usuários que são membros do `administrators` grupo.


>[!CAUTION]
>
>O modo Desenvolvedor só está disponível em uma instância de autor padrão que não está usando o modo de execução nosamplecontent.
>
>Se necessário, ele pode ser configurado para uso:
>
>* em uma instância do autor usando nosamplecontent run-mode
>* uma instância de publicação
>
>Deve ser desativado novamente após a utilização.

>[!NOTE]
>
>Consulte o:
>
>* Artigo da Base de conhecimento, [Solução de problemas AEM TouchUI](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obter mais dicas e ferramentas.
>* Sessão AEM Gems sobre [Modo de desenvolvedor do AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).
>


## Abrir o Modo de Desenvolvedor {#opening-developer-mode}

O modo Desenvolvedor é implementado como um painel lateral para o editor de páginas. Para abrir o painel, selecione **Desenvolvedor** no seletor de modo na barra de ferramentas do editor de páginas:

![chlimage_1-11](assets/chlimage_1-11.png)

O painel é dividido em duas guias:

* **[Componentes](/help/sites-developing/developer-mode.md#components)** - Mostra uma árvore de componentes, semelhante à [árvore de conteúdo](/help/sites-authoring/author-environment-tools.md#content-tree) para autores

* **[Erros](/help/sites-developing/developer-mode.md#errors)** - Quando ocorrem problemas, os detalhes são mostrados para cada componente.

### Componentes {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

Isso mostra uma árvore de componentes que:

* Descreve a cadeia de componentes e modelos renderizados na página (SLY, JSP, etc.). A árvore pode ser expandida para mostrar o contexto na hierarquia.
* Mostra o tempo computacional do lado do servidor necessário para renderizar o componente.
* Permite expandir a árvore e selecionar componentes específicos dentro da árvore. A seleção fornece acesso aos detalhes do componente; como:

   * Caminho do repositório
   * Links para scripts (acessados no CRXDE Lite)

* Os componentes selecionados (no fluxo de conteúdo, indicado por uma borda azul) serão realçados na árvore de conteúdo (e vice-versa).

Isso pode ajudar a:

* Determine e compare o tempo de renderização por componente.
* Consulte e entenda a hierarquia.
* Entenda e melhore o tempo de carregamento da página ao encontrar componentes lentos.

Cada entrada de componente pode mostrar (por exemplo):

![chlimage_1-13](assets/chlimage_1-13.png)

* **Exibir detalhes**: um link para uma lista que mostra:

   * todos os scripts de componente usados para renderizar o componente.
   * o caminho do conteúdo do repositório para esse componente específico.

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **Editar script**: um link que:

   * abre o script de componente no CRXDE Lite.

* Expandir uma entrada de componente (cabeça de seta) também pode mostrar:

   * A hierarquia no componente selecionado.
   * Tempos de renderização do componente selecionado de forma isolada, quaisquer componentes individuais aninhados dentro dele e o total combinado.

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>Alguns links apontam para scripts em `/libs`. No entanto, esses são apenas para referência, você **não deve** edite qualquer item em `/libs`, como qualquer alteração feita, pode ser perdida. Isso se deve ao fato de que essa ramificação está sujeita a alterações sempre que você atualiza ou aplica um hotfix/pacote de recursos. Quaisquer alterações necessárias devem ser feitas em `/apps`, consulte [Sobreposições e substituições](/help/sites-developing/overlays.md).

### Erros {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

Espero que a variável **Erros** sempre estará vazia (como acima), mas quando ocorrerem problemas, os seguintes detalhes serão mostrados para cada componente:

* Um aviso se o componente gravar uma entrada no log de erros, juntamente com detalhes do erro e links diretos para o código apropriado no CRXDE Lite.
* Um aviso se o componente abrir uma sessão de administrador.

Por exemplo, em uma situação em que um método indefinido é chamado, o erro resultante será mostrado na função **Erros** guia :

![chlimage_1-17](assets/chlimage_1-17.png)

A entrada de componente na árvore da guia Componentes também será marcada com um indicador quando ocorrer um erro.

### Testes {#tests}

>[!CAUTION]
>
>No AEM 6.2, os recursos de teste do modo Desenvolvedor foram reimplementados como um aplicativo de Ferramentas independente.
>
>Para obter detalhes completos, consulte [Testar sua interface do usuário](/help/sites-developing/hobbes.md).
