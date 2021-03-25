---
title: O componente RemotePage
description: O Componente de página remota é um componente de página personalizado para editar o React SPA remoto no AEM.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# O componente RemotePage {#remote-page-component}

Ao decidir qual nível de integração você gostaria de ter entre seu SPA externo e o AEM, geralmente fica claro que é necessário visualizar e editar o SPA no AEM. O Componente RemotePage é um componente de página personalizado apenas para essa finalidade.

## Visão geral {#overview}

O componente RemotePage obtém todos os ativos necessários do `asset-manifest.json` gerado pelo aplicativo e o usa para renderizar o SPA no AEM.

* A RemotePage permite inserir os scripts e as folhas de estilos de um SPA no corpo de um componente Página AEM.
* Os Componentes do Frente Virtual permitem marcar seções como editáveis AEM Editor de SPA.
* Juntos, um SPA hospedado em um domínio diferente pode ser editado no AEM.

Consulte o artigo [Editar um SPA externo no AEM](spa-edit-external.md) para obter mais detalhes sobre SPA editáveis e externas no AEM.

## Requisitos {#requirements}

* Habilitar CORS no desenvolvimento
* Configurar o URL remoto nas Propriedades da página
* Renderizar a SPA em AEM

## Limitações           {#limitations}

* A implementação atual do componente RemotePage suporta apenas aplicações de Reação Remota.
* O CSS interno definido no arquivo HTML raiz do aplicativo, bem como o CSS em linha no nó DOM raiz, não estarão disponíveis ao fazer a renderização remota no AEM.

## Detalhes técnicos {#technical-details}

Como o resto do projeto de SPA de AEM, o Componente RemotePage é de código aberto. Para obter os detalhes técnicos completos do Componente RemotePage, [consulte o repositório GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
