---
title: Diagnósticos do ContextHub
description: O ContextHub fornece uma página de diagnóstico onde você pode ter uma visão geral da estrutura do ContextHub
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# Diagnósticos do ContextHub {#contexthub-diagnostics}

O ContextHub fornece uma página de diagnósticos na qual você pode ter uma visão geral da estrutura do ContextHub. Para abrir a página, vá para a página `contexthub.diagnostics.html` da instância do autor do AEM, por exemplo:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

A página Diagnóstico do ContextHub fornece informações sobre os armazenamentos e módulos de interface do usuário criados, as pastas da biblioteca do cliente carregadas e os links para páginas úteis.

>[!NOTE]
>
>Para que as informações de diagnóstico sejam retornadas, o modo de depuração deve estar ativado; caso contrário, a página de diagnósticos ficará em branco. Consulte [este documento](ch-configuring.md#debugging-contexthub) para obter detalhes sobre como habilitar o modo de depuração.

>[!NOTE]
>
>Para configurações do ContextHub ainda localizadas em seus caminhos herdados, o local da página de diagnóstico é `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Lojas {#stores}

A seção Lojas lista todos os armazenamentos do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** O [tipo de armazenamento](/help/sites-developing/ch-samplestores.md) no qual o armazenamento se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** o caminho do nó de repositório onde o tipo de repositório está definido.
* **clientlibs:** as categorias das bibliotecas de clientes carregadas que implementam o tipo de armazenamento.

## Módulos {#modules}

A seção Módulos lista todos os módulos de interface do usuário do ContextHub que foram configurados. Cada item na lista consiste nas seguintes informações:

* **Título:** O [tipo de Módulo de Interface do Usuário](/help/sites-developing/ch-samplemodules.md) no qual o módulo de interface do usuário se baseia.
* **caminho:** O caminho para o nó do repositório que contém a configuração.
* **resourceType:** o caminho do nó do repositório onde o tipo de módulo da interface do usuário é definido.
* **clientlibs:** as categorias das bibliotecas de clientes carregadas que implementam o tipo de módulo da interface do usuário.

## Clientlibs {#clientlibs}

A seção Clientlibs lista todas as pastas da biblioteca do cliente que o ContextHub carregou. As bibliotecas de clientes são categorizadas:

* **kernel.js:** Bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** bibliotecas de clientes que implementam os tipos de módulo de interface e interface do usuário do ContextHub.
* **style.css:** arquivos CSS que são carregados das bibliotecas do cliente.

## URLs {#urls}

A seção URLs contém links para recursos do ContextHub:

* **Editor de configuração:** abre a [página Configuração do ContextHub](ch-configuring.md), onde você pode configurar lojas, modos de interface do usuário e módulos de interface do usuário.

* **Configuração de módulos do ContextHub:** Abre o arquivo /etc/cloudsettings/default/contexthub.config.kernel.js, que contém a representação do objeto JavaScript das configurações de armazenamento do ContextHub.
* **Configuração da interface do usuário do ContextHub:** Abre o arquivo /etc/cloudsettings/default/contexthub.config.ui.js, que contém a representação do objeto JavaScript das configurações de modo da interface do usuário do ContextHub.
* **kernel.js:** abre o arquivo /etc/cloudsettings/default/contexthub.kernel.js, que contém o código-fonte das bibliotecas de clientes que implementam a estrutura do ContextHub, o mecanismo de segmento e os tipos de armazenamento.
* **ui.js:** abre o arquivo /etc/cloudsettings/default/contexthub.ui.js, que contém o código-fonte das bibliotecas de clientes que implementam os tipos de módulo da interface do usuário e da interface do usuário do ContextHub.
* **style.css:** Abre o arquivo /etc/cloudsettings/default/contexthub.styles.css, que contém os estilos CSS para a interface do usuário do ContextHub e os módulos de interface do usuário.
