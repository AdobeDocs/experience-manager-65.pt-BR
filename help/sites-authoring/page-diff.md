---
title: 'Diferencial de páginas  '
seo-title: 'Diferencial de páginas  '
description: O recurso de diferencial de página permite a comparação lado a lado conveniente de duas páginas com suas diferenças realçadas.
seo-description: O recurso de diferencial de página permite a comparação lado a lado conveniente de duas páginas com suas diferenças realçadas.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
translation-type: tm+mt
source-git-commit: eb9a4792f4d64f98805919f00bb62193a6a7dafc
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 99%

---


# Diferencial de páginas  {#page-diff}

## Introdução {#introduction}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja poder comparar facilmente a página atual lado a lado com outra versão.

O recurso de diferencial de página permite a comparação lado a lado conveniente de duas páginas com suas diferenças realçadas.

>[!TIP]
>
>Consulte [Desenvolvimento e diff de página](/help/sites-developing/pagediff.md#operation-details) para obter mais detalhes técnicos sobre este recurso.

## Uso {#use}

O diferencial lado a lado pode comparar o seguinte:

* [Versões](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) - versão anterior de uma página com seu estado atual
* [](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page)Live Copies - Live Copy com blueprint
* [Lançamentos](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) - lançamento com sua origem
* [](/help/sites-administering/tc-manage.md#comparing-language-copies)Cópias de idioma - uma página antes e depois da (nova) tradução

Consulte os respectivos tópicos sobre como iniciar o diferencial nesses contextos.

### Apresentação das diferenças   {#presentation-of-differences}

Independentemente do conteúdo que está sendo comparado, a apresentação das diferenças permanece a mesma.

* O conteúdo selecionado quando você iniciou o diferencial é exibido à esquerda (o ponto de entrada do diferencial).
* O conteúdo comparativo é exibido à direita (com base no qual o conteúdo selecionado é comparado).

Por exemplo, ao comparar versões, a versão atual é exibida à esquerda e a versão anterior é exibida à direita.

A origem de ambas as páginas é exibida claramente na barra de cabeçalho na parte superior da janela do navegador.

![chlimage_1-109](assets/chlimage_1-109.png)

O diferencial detecta alterações no componente e no nível do HTML. Itens que foram alterados são destacados com cores diferentes.

**Alterações de componentes**

* Verde claro - Componente adicionado
* Rosa - Componente removido
* Azul - Componente alterado
* Azul - Componente movido

Observe que as cores alteradas e movidas são as mesmas.

**Alterações no HTML**

* Verde escuro - HTML adicionado
* Vermelho - HTML removido

>[!NOTE]
>
>Ao comparar cópias de idiomas, o realce é desativado, pois, em uma tradução, tudo muda, e não seria benéfico realçar.

### Tela cheia e ao sair   {#fullscreen-and-exiting}

Para se concentrar em um conteúdo específico, você pode clicar no ícone de tela inteira para qualquer &quot;lado&quot; da comparação lado a lado, ampliando o conteúdo até o tamanho da janela do navegador.

![](do-not-localize/chlimage_1-18.png)

O lado selecionado preencherá a janela inteira, mas a barra permanecerá no topo, permitindo que você alterne entre as duas páginas.

![chlimage_1-110](assets/chlimage_1-110.png)

Você também pode optar por fechar a visualização em tela cheia clicando no ícone Saída da tela cheia.

![](do-not-localize/chlimage_1-19.png)

Você pode sair do diferencial lado a lado a qualquer momento clicando no botão Fechar do cabeçalho.

## Limitações   {#limitations}

Existem algumas situações em que o recurso de diferencial de páginas pode não detectar uma diferença conforme o esperado.

* Ao diferenciar versões e lançamentos, o recurso de diferencial não leva em consideração os componentes dinâmicos, como navegação estrutural, menus, listas de produtos ou logotipos (componentes que dependem da estrutura do site para renderizar seu conteúdo).
* Para versões, o diferencial não recria a política de controle de acesso e as relações de live copy.
* Se for feita alguma alteração em uma imagem, como modificar os atributos alt, title ou src, ela será destacada em azul como alterada. No entanto, em alguns casos, a imagem tem uma representação Base64 do atributo src e, mesmo que as duas imagens tenham a mesma aparência, elas serão marcadas pelo recurso de diferencial como diferentes por causa dos diferentes atributos src.
* O recurso de diferencial é incapaz de detectar a rotação da imagem.
* Se uma página for movida, você não poderá mais executar um diff com versões feitas antes do movimento.

   * Se você tiver problemas com um diff, verifique a [Linha do tempo](/help/sites-authoring/basic-handling.md#timeline) da página para ver se a página foi movida.

>[!NOTE]
>
>Versões não podem ser comparadas entre si. Somente a versão atual pode ser comparada com outras versões da página. A versão atual é sempre a versão realçada com alterações.

>[!NOTE]
>
>Para obter mais detalhes sobre a operação do mecanismo diff da página, bem como limitações que podem afetar o diff da página, consulte a [documentação do desenvolvedor](/help/sites-developing/pagediff.md) desse recurso.
