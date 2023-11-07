---
title: O componente RemotePage
description: O componente RemotePage é um componente de página personalizado para editar o SPA React remoto dentro do AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---

# O componente RemotePage {#remote-page-component}

Ao decidir qual nível de integração você gostaria de ter entre seu SPA externo e AEM, geralmente fica claro que você precisa ser capaz de visualizar e editar o SPA dentro do AEM. O componente RemotePage é um componente de página personalizado apenas para esta finalidade.

## Visão geral {#overview}

O componente RemotePage busca todos os ativos necessários do aplicativo gerado `asset-manifest.json` e usa isso para renderizar o SPA dentro do AEM.

* A RemotePage permite inserir os scripts e folhas de estilos de um SPA no corpo de um componente AEM Page.
* Os Componentes de front-end virtuais permitem marcar seções como editáveis no Editor de SPA AEM.
* Juntos, um SPA hospedado em um domínio diferente pode se tornar editável no AEM.

Consulte o artigo [Edição de um AEM externo no SPA](spa-edit-external.md) para obter mais detalhes sobre SPA externo editável no AEM.

## Requisitos {#requirements}

* Ativar o CORS em desenvolvimento
* Configurar o URL remoto nas Propriedades da página
* Renderizar o AEM no SPA
* O aplicativo da Web deve usar um manifesto de ativo de pacote como um dos seguintes e expor um arquivo asset-manifest.json na raiz do domínio que lista, em uma propriedade de pontos de entrada, todos os arquivos CSS e JS que devem ser carregados:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![Pontos de entrada](assets/asset-manifest-entrypoints.png)

* O aplicativo deve ser capaz de inicializar em um `<div id="root"></div>` abaixo do elemento body. Se uma marcação diferente for esperada para o aplicativo instanciar, ela deverá ser ajustada de acordo nos scripts HTL do componente proxy que tem um `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitações {#limitations}

* O componente RemotePage espera que a implementação forneça um manifesto de ativo como o [encontrado aqui.](https://github.com/shellscape/webpack-manifest-plugin) No entanto, o componente RemotePage só foi testado para funcionar com a estrutura React (e o Next.js por meio do componente remote-page-next) e, portanto, não oferece suporte ao carregamento remoto de aplicativos de outras estruturas, como o Angular.
* O CSS interno definido no arquivo de HTML raiz do aplicativo e o CSS em linha no nó DOM raiz não estarão disponíveis ao fazer renderização remota no AEM.

## Detalhes técnicos {#technical-details}

AEM Como o restante do projeto SPA, o componente RemotePage é de código aberto. Para obter todos os detalhes técnicos do componente RemotePage, [consulte o repositório do GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
