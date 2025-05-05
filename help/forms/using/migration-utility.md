---
title: Migrar ativos e documentos do AEM Forms
description: O utilitário de Migração permite migrar ativos e documentos do Adobe Experience Manager (AEM) Forms AEM do 6.3 Forms AEM ou de versões anteriores para o 6.4 Forms.
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin,User
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 1%

---

# Migrar ativos e documentos do AEM Forms{#migrate-aem-forms-assets-and-documents}

O utilitário de Migração converte os [ativos adaptáveis do Forms](../../forms/using/introduction-forms-authoring.md), as [configurações de nuvem](/help/sites-developing/extending-cloud-config.md) e os [ativos do Gerenciamento de Correspondências](/help/forms/using/cm-overview.md) do formato usado nas versões anteriores para o formato usado no Adobe Experience Manager (AEM) 6.5 Forms. Quando você executa o utilitário de migração, o seguinte é migrado:

* Componentes personalizados para formulários adaptáveis
* Modelos adaptáveis de formulários e gerenciamento de correspondência
* Configurações de nuvem
* Gerenciamento de correspondência e ativos de formulários adaptáveis

>[!NOTE]
>
>Se houver uma atualização fora do local, para ativos do Gerenciamento de correspondências, você poderá executar a migração toda vez que importar os ativos. Para a migração do Gerenciamento de correspondência, é necessário ter o Pacote de compatibilidade do Forms instalado.

## Abordagem da migração {#approach-to-migration}

Você pode [atualizar](../../forms/using/upgrade.md) para a versão mais recente do AEM Forms 6.5 do AEM Forms 6.4, 6.3 ou 6.2, ou fazer uma nova instalação. Dependendo de você ter atualizado sua instalação anterior ou executado uma nova instalação, é necessário executar um dos seguintes procedimentos:

**Se houver uma atualização no local**

Se você tiver executado uma atualização no local, a instância atualizada já terá os ativos e os documentos. No entanto, antes de usar os ativos e documentos, você deve instalar o [pacote de Compatibilidade do AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) (inclui o pacote de Compatibilidade do Gerenciamento de Correspondências)

Em seguida, atualize os ativos e documentos [executando o Utilitário de migração](#runningmigrationutility).

**Se houver uma instalação fora do local**

Se esta for uma instalação fora do local (nova), antes de usar os ativos e documentos, instale o [pacote de Compatibilidade do AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) (inclui o pacote de Compatibilidade do Gerenciamento de Correspondências).

Em seguida, importe o pacote de ativos (zip ou cmp) para a nova configuração e atualize os ativos e documentos [executando o Utilitário de migração](#runningmigrationutility). A Adobe recomenda criar ativos na nova configuração somente após executar o utilitário de migração.

Devido a [alterações relacionadas à compatibilidade com versões anteriores](/help/sites-deploying/backward-compatibility.md), os locais de algumas pastas no repositório crx foram alterados. Exporte e importe manualmente as dependências (bibliotecas e ativos personalizados) da configuração anterior para um novo ambiente.

## Antes de continuar com a migração {#prerequisites}

Para ativos do Gerenciamento de correspondência:

* Para os ativos importados da plataforma anterior, uma propriedade é adicionada: **fd:version=1.0**.
* Desde o AEM 6.1 Forms, os comentários não estão disponíveis imediatamente. Os comentários adicionados anteriormente estão disponíveis nos ativos, mas não ficam visíveis na interface automaticamente. Personalize a propriedade extendedProperties na interface do usuário do AEM Forms para tornar os comentários visíveis.
* Em algumas das versões anteriores, como o LiveCycle ES4, o texto foi editado usando o RichTextEditor da Flex, mas desde o AEM 6.1 Forms, o editor de HTML é usado. Devido a essa renderização e à aparência das fontes, os tamanhos e as margens das fontes podem ser diferentes das versões anteriores na interface do usuário do Autor. No entanto, as letras parecem as mesmas quando renderizadas.
* As listas em módulos de texto foram aprimoradas e agora são renderizadas de forma diferente. Pode haver diferenças visuais. A Adobe recomenda que você renderize e veja as letras nas quais está usando listas em módulos de texto.
* Como os módulos de conteúdo de imagem são convertidos em ativos do DAM e os layouts e fragmentos são adicionados a formulários durante a migração, a propriedade Atualizado por desses módulos muda para administrador.
* O histórico de versões dos ativos não é migrado e não está disponível após a migração. O histórico de versões subsequentes após a migração é mantido.
* O estado Pronto para Publish está obsoleto desde o AEM 6.1 Forms, de modo que todos os ativos no estado Pronto para Publish são alterados para o estado Modificado.
* Como a interface do usuário é atualizada no AEM Forms 6.3, as etapas para executar as personalizações também são diferentes. Refaça a personalização se estiver migrando de uma versão anterior à 6.3.
* Os fragmentos de layout são movidos de `/content/apps/cm/layouts/fragmentlayouts/1001` para `/content/apps/cm/modules/fragmentlayouts`. A referência do dicionário de dados no Assets exibe o caminho do dicionário de dados em vez do nome.
* Os espaços de tabulação usados para alinhamento em módulos de texto devem ser reajustados. Para obter mais informações, consulte [Gerenciamento de correspondência - Usando espaçamento entre guias para organizar o texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* As configurações do compositor de ativos são alteradas para configurações do Gerenciamento de correspondência.
* O Assets é movido para as pastas com nomes como Texto existente e Lista existente.

## Uso do utilitário de Migração {#using-the-migration-utility}

### Execução do utilitário de migração {#runningmigrationutility}

Execute o utilitário de Migração antes de alterar os ativos ou criar ativos. A Adobe recomenda que você não execute o utilitário após fazer qualquer alteração ou criar ativos. Certifique-se de que a interface do usuário do Gerenciamento de correspondência ou do Forms Assets adaptável não esteja aberta enquanto o processo de migração está em execução.

Quando você executa o Utilitário de Migração pela primeira vez, um log é criado com o seguinte caminho e nome: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Este log continua sendo atualizado com as informações de migração do Gerenciamento de correspondência e do Adaptive Forms, como a movimentação de ativos.

>[!NOTE]
>
>Antes de executar o utilitário de migração, verifique se você fez um backup do repositório crx.

1. Em uma sessão do navegador, faça logon na instância do autor do AEM como administrador.

1. Abra o seguinte URL no navegador:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   O navegador exibe quatro opções:

   * Migração de ativos de AEM Forms
   * Migração adaptável de componentes personalizados do Forms
   * Migração adaptável de modelos do Forms
   * Migração das configurações de nuvem de AEM Forms

1. Faça o seguinte para executar a migração:

   * Para migrar **ativos**, selecione Migração do AEM Forms Assets e, na próxima tela, selecione **Iniciar Migração**. Os itens a seguir são migrados:

      * Formulários adaptáveis
      * Fragmentos do documento
      * Temas
      * Cartas
      * Dicionários de dados

   >[!NOTE]
   >
   >Durante a migração de ativos, você pode encontrar mensagens de aviso como &quot;Conflito encontrado para...&quot;. Essas mensagens indicam que as regras para alguns dos componentes em formulários adaptáveis não puderam ser migradas. Por exemplo, se o componente tiver um evento que tenha regras e scripts, se as regras ocorrerem após qualquer script, nenhuma das regras do componente será migrada. Você pode [migrar essas regras abrindo o editor de regras](#migrate-rules) na criação de formulários adaptáveis.

   * Para migrar componentes personalizados de formulários adaptáveis, selecione **Migração de componentes personalizados adaptáveis do Forms** e, na página Migração de componentes personalizados, selecione **Iniciar Migração**. Os itens a seguir são migrados:

      * Componentes personalizados gravados para o Adaptive Forms
      * Sobreposições de componente, se houver.

   * Para migrar modelos de formulário adaptáveis, selecione **Migração de modelo adaptável do Forms** e, na página Migração de componentes personalizados, selecione **Iniciar migração**. Os itens a seguir são migrados:

      * Modelos de formulários adaptáveis criados em `/apps` ou `/conf` usando o Editor de Modelos AEM.

   * Migre os serviços de Configuração da AEM Forms Cloud para usar o novo paradigma de serviço de nuvem com reconhecimento de contexto, que inclui a interface de usuário habilitada para toque (em `/conf`). Ao migrar os serviços de Configuração na nuvem do AEM Forms, os serviços de nuvem no `/etc` são movidos para o `/conf`. Se você não tiver nenhuma personalização dos serviços de nuvem que dependa dos caminhos herdados (`/etc`), o Adobe recomenda executar o utilitário de migração após a atualização para a versão 6.5; use a interface de toque da configuração de nuvem para trabalhar mais. Se você tiver personalizações existentes do Cloud Services, continue usando a interface clássica na instalação atualizada até que as personalizações sejam atualizadas para se alinharem aos caminhos migrados (`/conf`) e execute o utilitário de migração.

   Para migrar os **serviços em nuvem do AEM Forms**, que incluem o seguinte, selecione Migração de Configuração da Nuvem do AEM Forms (a migração de configuração da nuvem é independente do pacote de Compatibilidade do AEMFD). Selecione Migração de configurações da AEM Forms Cloud e, na página Migração de configurações, selecione **Iniciar migração**:

   * Serviços em nuvem do modelo de dados de formulário

      * Caminho do Source: `/etc/cloudservices/fdm`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * Caminho do Source: `/etc/cloudservices/recaptcha`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * Caminho do Source: `/etc/cloudservices/echosign`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/echosign`

   * Serviços em nuvem Typekit

      * Caminho do Source: `/etc/cloudservices/typekit`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/typekit`

   A janela do navegador exibe as seguintes informações à medida que o processo de migração ocorre:

   * Quando os ativos são atualizados: o Assets é atualizado com êxito.
   * Quando a migração for concluída: a migração para ativos foi concluída.

   Quando executado, o utilitário de Migração faz o seguinte:

   * **Adiciona as marcas aos ativos**: adiciona a marca &quot;Gerenciamento de Correspondência: Assets Migrado&quot; / &quot;Forms Adaptável: Assets Migrado&quot;. aos ativos migrados, para que os usuários possam identificar esses ativos. Quando você executa o utilitário de Migração, todos os ativos existentes no sistema são marcados como Migrados.
   * **Gera marcas**: categorias e subcategorias presentes no sistema anterior são criadas como marcas e, em seguida, essas marcas são associadas aos ativos relevantes do Gerenciamento de Correspondências no AEM. Por exemplo, uma Categoria (Declarações) e uma Subcategoria (Declarações) de um modelo de correspondência são geradas como tags.

1. Depois que o Utilitário de migração terminar a execução, prossiga para as [tarefas de manutenção](#housekeepingtasks).

#### Migrar regras usando o editor de regras {#migrate-rules}

Esses componentes podem ser migrados abrindo-os no Editor de regras no editor de Forms adaptável.

* Para migrar regras e scripts (não necessário se estiver atualizando da versão 6.3) em componentes personalizados, selecione Migração de componentes personalizados do Forms adaptável e, na próxima tela, selecione Iniciar migração. Os itens a seguir são migrados:

   * Regras e scripts criados usando o editor de regras (6.1 FP1 e posterior)

   * Scripts criados usando a guia Script na interface do usuário da versão 6.1 e anterior

* Para migrar modelos (não é necessário se estiver atualizando das versões 6.3 e 6.4), selecione Migração de modelo adaptável do Forms e, na próxima tela, selecione Iniciar migração. Os itens a seguir são migrados:

   * Modelos antigos - os modelos de formulários adaptáveis criados em /apps usando o AEM 6.1 Forms ou anterior. Isso inclui os scripts que foram definidos nos componentes do modelo.

   * Novos modelos - Modelos de formulários adaptáveis criados usando o editor de modelo em `/conf`. Isso inclui a migração de regras e scripts criados usando o editor de regras.

### Tarefas de manutenção após executar o utilitário de migração {#housekeepingtasks}

Após executar o utilitário de migração, cuide das seguintes tarefas de manutenção:

1. Verifique se a versão XFA de layouts e layouts de fragmento é a 3.3 ou posterior. Se estiver usando layouts e layouts de fragmento de uma versão mais antiga, pode haver problemas na renderização da correspondência. Para atualizar uma versão de um XFA mais antigo para a versão mais recente, siga estas etapas:

   1. [Baixe o XFA como um arquivo zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) da interface do usuário do Forms.
   1. Extraia o arquivo.
   1. Abra o arquivo XFA na Designer mais recente e salve-o. A versão do XFA é atualizada para a mais recente.
   1. Faça upload do XFA na interface do usuário do Forms.

1. Publish todos os ativos publicados no sistema anterior antes da migração. O utilitário de migração atualiza os ativos somente na instância do Autor e, para atualizar os ativos nas instâncias do Publish, você deve publicar os ativos.

1. No AEM Forms 6.4 e 6.5, alguns dos direitos dos grupos de usuários de formulários são alterados. Se você quiser que qualquer um dos seus usuários possa fazer upload de XDPs e do Adaptive Forms contendo scripts ou usar um editor de código, será necessário adicioná-los ao grupo de usuários avançados de formulários. Da mesma forma, os autores de modelo não podem mais usar o editor de código no Editor de regras. Para que os usuários possam usar um editor de código, adicione-os ao grupo af-template-script-writer. Para obter instruções sobre como adicionar usuários a grupos, consulte [Gerenciando usuários e grupos de usuários](/help/communities/users.md).
