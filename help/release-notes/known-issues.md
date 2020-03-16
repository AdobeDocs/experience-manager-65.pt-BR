---
title: Problemas conhecidos
description: Notas de versão específicas dos problemas conhecidos com o Adobe Experience Manager 6.5
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 3d607217e3d66998a8463db3f527a626beaca769

---


# Problemas conhecidos {#known-issues}

Esta página apresenta uma lista de problemas conhecidos do Adobe Experience Manager 6.5, lançado em abril de 2019.

[Entre em contato com o suporte](https://helpx.adobe.com/support/experience-manager.html) se precisar de mais informações sobre os problemas conhecidos.

## Plataforma {#platform}

Um problema é reportado onde o CRX-Quickstart e seu conteúdo são excluídos.

Em cada uma dessas ações, verifique se a propriedade &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; nunca é uma string vazia:

1. Chamando &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
2. Atualização para o AEM 6.5.
3. Execução da &quot;migração de conteúdo lento&quot; no AEM 6.5.

Um artigo da [Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) de conhecimento está disponível com mais detalhes e a solução alternativa para esse problema.

## Ativos {#assets}

* **Pesquisar:** A pesquisa não resultará em nenhum retorno se a string de pesquisa contiver espaços à esquerda ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadados de pasta**: depois de adicionar um botão de escolha, os campos ID e Valor não são renderizados como esperado e a funcionalidade de exclusão não funciona. (CQ-4261144)
* Ao renomear um ativo, não é possível usar um espaço em branco no nome do ativo. (CQ-4266403)

## Forms {#forms}

* Quando os formulários do AEM são instalados no sistema operacional do Linux, a assinatura digital com o módulo de segurança de hardware não funciona. (CQ-4266721)
* (AEM Forms on WebSphere only) The **Forms Workflow **> **Task Search** option does not return any result if you search for an **Administrator** with **Username** as the search criteria. (CQ-4266457)

* Os formulários AEM não conseguem converter arquivos .tif e .tiff com compactação JPEG em documentos PDF. (CQ-4265972)
* As opções **Scanner de ativos do AEM Forms** e **Carta para migração de comunicação interativa** não funcionam na página **Migração do AEM Forms**. (CQ-4266572)

* (Somente para JBoss 7) Quando você atualiza de uma versão anterior para o AEM 6.5 Forms e a versão anterior tinha processos (.lca) que criavam e usavam uma cópia do processo padrão de envio ou renderização, o HTML5 Forms usando tais processos (.lca) não executa as ações necessárias. (CQ-4243928)
* Em um formulário adaptável, quando um serviço de modelo de dados do formulário é chamado a partir do editor de regras para atualizar valores dinamicamente do componente de escolha de imagem, os valores do componente de escolha de imagem não são atualizados. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Certifique-se de que os pacotes de tempo de execução redistribuíveis mencionados acima estão instalados antes de iniciar a instalação. (CQ-4265668)

* Quando um formulário adaptável é configurado para atualizar dinamicamente valores de um componente e a instância de publicação que hospeda o formulário é acessada por meio do distribuidor, a funcionalidade para atualizar dinamicamente os valores de um campo para de funcionar. Para solucionar o problema, na instância de publicação, abra o CRXDE, navegue até /libs/fd/af/runtime/clientlibs/guideChartReducer e crie a propriedade listada abaixo. 

   * Nome: allowProxy
   * Tipo: booliano
   * Valor: true
   * Protegido: false
   * Obrigatório: false
   * Vários: false
   * Criado automaticamente: false

A propriedade habilita as bibliotecas de clientes na pasta de tempo de execução para acessar proxies. (CQ-4268679)

