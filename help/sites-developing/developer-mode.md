---
title: Modo de desenvolvedor
description: O Modo de desenvolvedor abre um painel lateral com várias guias que fornecem ao desenvolvedor informações sobre a página atual.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Modo de desenvolvedor{#developer-mode}

Ao editar páginas no Adobe Experience Manager (AEM), vários [modos](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) estão disponíveis, incluindo o Modo de desenvolvedor. Isso abre um painel lateral com várias guias que fornecem informações sobre a página atual para um desenvolvedor. As três guias são:

* **[Componentes](#components)** para exibir informações sobre estrutura e desempenho.
* **[Testes](#tests)** para executar testes e analisar os resultados.
* **[Erros](#errors)** para ver os problemas ocorridos.

Isso ajuda um desenvolvedor a:

* Descubra: as páginas que são compostas por.
* Depuração: o que está acontecendo, onde e quando, que por sua vez ajuda a resolver problemas.
* Teste: o aplicativo se comporta conforme esperado.

>[!CAUTION]
>
>Modo de desenvolvedor:
>
>* Só está disponível na interface habilitada para toque (ao editar páginas).
>* Não está disponível em dispositivos móveis ou janelas pequenas na área de trabalho (devido a restrições de espaço).
>
>   * Isso ocorre quando a largura é menor que 1024px.
>* Está disponível somente para usuários que são membros do grupo `administrators`.

>[!CAUTION]
>
>O modo de desenvolvedor só está disponível em uma instância de autor padrão que não esteja usando o modo de execução nosamplecontent.
>
>Se necessário, ele pode ser configurado para uso:
>
>* em uma instância do autor usando o modo de execução nosamplecontent
>* uma instância de publicação
>
>Ele deve ser desativado novamente após o uso.

>[!NOTE]
>
>Consulte:
>
>* Artigo da Base de Dados de Conhecimento, [Solução de problemas da interface para toque do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-16935), para obter mais dicas e ferramentas.
>* Sessão do AEM Gems sobre o [Modo de Desenvolvedor do AEM 6.0](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-developer-mode.html?lang=pt-BR).
>

## Abrindo o Modo de Desenvolvedor {#opening-developer-mode}

O modo de desenvolvedor é implementado como um painel lateral para o editor de páginas. Para abrir o painel, selecione **Desenvolvedor** no seletor de modo, na barra de ferramentas do editor de páginas:

![chlimage_1-11](assets/chlimage_1-11.png)

O painel é dividido em duas guias:

* **[Componentes](/help/sites-developing/developer-mode.md#components)** - Mostra uma árvore de componentes, semelhante à [árvore de conteúdo](/help/sites-authoring/author-environment-tools.md#content-tree) para autores

* **[Erros](/help/sites-developing/developer-mode.md#errors)** - Quando ocorrem problemas, os detalhes são mostrados para cada componente.

### Componentes {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

Isso mostra uma árvore de componentes que:

* Descreve a cadeia de componentes e modelos renderizados na página (SLY, JSP e assim por diante). A árvore pode ser expandida para mostrar o contexto dentro da hierarquia.
* Mostra o tempo computacional do lado do servidor para renderizar o componente.
* Permite expandir a árvore e selecionar componentes específicos dentro dela. A seleção fornece acesso aos detalhes do componente; como:

   * Caminho do repositório
   * Links para scripts (acessados no CRXDE Lite)

* Os componentes selecionados (no fluxo de conteúdo, indicados por uma borda azul) serão destacados na árvore de conteúdo (e vice-versa).

Isso pode ajudar a:

* Determine e compare o tempo de renderização por componente.
* Veja e entenda a hierarquia.
* Entenda e melhore o tempo de carregamento da página ao encontrar componentes lentos.

Cada entrada de componente pode mostrar (por exemplo):

![chlimage_1-13](assets/chlimage_1-13.png)

* **Exibir Detalhes**: um link para uma lista que mostra:

   * todos os scripts de componentes usados para renderizar o componente.
   * o caminho do conteúdo do repositório para este componente específico.

  ![chlimage_1-14](assets/chlimage_1-14.png)

* **Editar Script**: um link que:

   * abre o script de componentes no CRXDE Lite.

* A expansão de uma entrada de componente (ponta de seta) também pode mostrar:

   * A hierarquia no componente selecionado.
   * Tempos de renderização para o componente selecionado isolado, quaisquer componentes individuais aninhados dentro dele e o total combinado.

  ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>Alguns links apontam para scripts em `/libs`. No entanto, eles são somente para referência, você **não** deve editar nada em `/libs`, pois as alterações que você fizer podem ser perdidas. Isso ocorre porque essa ramificação pode sofrer alterações sempre que você atualizar ou aplicar um hotfix ou pacote de recursos. Faça as alterações necessárias em `/apps`. Consulte [Sobreposições e substituições](/help/sites-developing/overlays.md).

### Erros {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

Esperamos que a guia **Erros** esteja sempre vazia (como acima), mas quando ocorrerem os problemas os detalhes a seguir são mostrados para cada componente:

* Um aviso se o componente gravar uma entrada no log de erros, juntamente com detalhes do erro e links diretos para o código apropriado no CRXDE Lite.
* Um aviso se o componente abrir uma sessão de administrador.

Por exemplo, em uma situação em que um método indefinido é chamado, o erro resultante é mostrado na guia **Erros**:

![chlimage_1-17](assets/chlimage_1-17.png)

A entrada de componente na árvore da guia Componentes também será marcada com um indicador quando ocorrer um erro.

### Testes {#tests}

>[!CAUTION]
>
>No AEM 6.2, os recursos de teste do modo de Desenvolvedor foram reimplementados como um aplicativo de Ferramentas independente.
>
>Para obter detalhes completos, consulte [Testando sua interface](/help/sites-developing/hobbes.md).
