---
title: Diagnóstico do ContextHub
seo-title: Diagnóstico do ContextHub
description: O ContextHub fornece uma página de diagnósticos na qual você pode ver uma visão geral da estrutura do ContextHub
seo-description: O ContextHub fornece uma página de diagnósticos na qual você pode ver uma visão geral da estrutura do ContextHub
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Diagnóstico do ContextHub {#contexthub-diagnostics}

O ContextHub fornece uma página de diagnósticos na qual você pode ver uma visão geral da estrutura do ContextHub. Para abrir a página, vá para a `contexthub.diagnostics.html` página da instância do autor AEM, por exemplo:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

A página Diagnóstico do ContextHub fornece informações sobre os armazenamentos e os módulos de interface do usuário que foram criados, as pastas da biblioteca do cliente que foram carregadas e os links para páginas úteis.

>[!NOTE]
>
>Para que as informações de diagnóstico sejam retornadas, o modo de depuração deve estar ativado, caso contrário, a página de diagnósticos ficará em branco. Consulte [este documento](ch-configuring.md#debugging-contexthub) para obter detalhes sobre como ativar o modo de depuração.

>[!NOTE]
>
>Para configurações do ContextHub ainda localizadas sob seus caminhos herdados, o local da página de diagnósticos é `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Lojas {#stores}

A seção Lojas lista todos os armazenamentos do ContextHub que foram configurados. Cada item da lista consiste nas seguintes informações:

* **Título:** O tipo [de](/help/sites-developing/ch-samplestores.md) loja em que a loja se baseia.
* **caminho:** O caminho para o nó do repositório que armazena a configuração.
* **resourceType:** O caminho do nó do repositório no qual o tipo de armazenamento é definido.
* **clientlibs:** As categorias das bibliotecas clientes carregadas que implementam o tipo de armazenamento.

## Módulos {#modules}

A seção Módulos lista todos os módulos de interface do usuário do ContextHub que foram configurados. Cada item da lista consiste nas seguintes informações:

* **Título:** O tipo [de módulo de](/help/sites-developing/ch-samplemodules.md) interface em que o módulo de interface do usuário se baseia.
* **caminho:** O caminho para o nó do repositório que armazena a configuração.
* **resourceType:** O caminho do nó do repositório no qual o tipo de módulo da interface do usuário é definido.
* **clientlibs:** As categorias das bibliotecas clientes que são carregadas que implementam o tipo de módulo da interface do usuário.

## Clientlibs {#clientlibs}

A seção Clientlibs lista todas as pastas da biblioteca do cliente que o ContextHub carregou. As bibliotecas do cliente são categorizadas:

* **kernel.js:** Bibliotecas clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** Bibliotecas do cliente que implementam os tipos de módulos de interface do usuário e interface do ContextHub.
* **style.css:** Arquivos CSS carregados das bibliotecas do cliente.

## URLs {#urls}

A seção URLs contém links para os recursos do ContextHub:

* **Editor de configuração:** Abre a página [Configuração do](ch-configuring.md) ContextHub, onde é possível configurar armazenamentos, modos de interface do usuário e módulos de interface do usuário.

* **Configuração dos módulos do ContextHub:** Abre o arquivo /etc/cloudsettings/default/contexthub.config.kernel.js, que contém a representação de objeto Javascript das configurações de armazenamento do ContextHub.
* **Configuração da interface do usuário do ContextHub:** Abre o arquivo /etc/cloudsettings/default/contexthub.config.ui.js, que contém a representação de objeto Javascript das configurações do modo de interface do usuário do ContextHub.
* **kernel.js:** Abre o arquivo /etc/cloudsettings/default/contexthub.kernel.js, que contém o código fonte das bibliotecas do cliente que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** Abre o arquivo /etc/cloudsettings/default/contexthub.ui.js, que contém o código-fonte das bibliotecas do cliente que implementam os tipos de módulos de interface do usuário e interface do ContextHub.
* **style.css:** Abre o arquivo /etc/cloudsettings/default/contexthub.styles.css, que contém os estilos CSS para os módulos de interface do usuário e da interface do usuário do ContextHub.