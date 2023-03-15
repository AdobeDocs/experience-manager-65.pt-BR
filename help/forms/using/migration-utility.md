---
title: Migrar ativos e documentos do AEM Forms
seo-title: Migrate AEM Forms assets and documents
description: O Utilitário de migração permite migrar ativos e documentos do AEM Forms do AEM 6.3 Forms ou de versões anteriores para o AEM 6.4 Forms.
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# Migrar ativos e documentos do AEM Forms{#migrate-aem-forms-assets-and-documents}

O utilitário de Migração converte o [Ativos adaptáveis do Forms](../../forms/using/introduction-forms-authoring.md), [configurações de nuvem](/help/sites-developing/extending-cloud-config.md)e [Ativos de gerenciamento de correspondência](/help/forms/using/cm-overview.md) do formato usado nas versões anteriores ao formato usado no AEM 6.5 Forms. Quando você executa o utilitário de migração, as seguintes etapas são migradas:

* Componentes personalizados para formulários adaptáveis
* Formulários adaptáveis e modelos de gerenciamento de correspondência
* Configurações da nuvem
* Gerenciamento de correspondência e ativos de formulários adaptáveis

>[!NOTE]
>
>No caso de atualização fora do local, no caso de ativos de Gerenciamento de correspondência, é possível executar a migração toda vez que importar os ativos. Para a migração do Gerenciamento de correspondência, é necessário ter o Pacote de compatibilidade do Forms instalado.

## Abordagem da migração {#approach-to-migration}

Você pode [atualizar](../../forms/using/upgrade.md) para a versão mais recente do AEM Forms 6.5 do AEM Forms 6.4, 6.3 ou 6.2 ou execute uma nova instalação. Dependendo de você ter atualizado sua instalação anterior ou executado uma nova instalação, é necessário executar um dos seguintes procedimentos:

**No caso de atualização no local**

Se você tiver realizado uma atualização no local, a instância atualizada já terá os ativos e documentos. No entanto, antes de usar os ativos e documentos, será necessário instalar o [Pacote de compatibilidade AEMFD](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) (inclui o pacote de Compatibilidade do Correspondence Management)

Em seguida, é necessário atualizar os ativos e documentos por [executando o utilitário Migração](#runningmigrationutility).

**Em caso de instalação fora do local**

Se for uma instalação fora do local (nova), antes de poder usar os ativos e documentos, será necessário instalar [Pacote de compatibilidade AEMFD](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) (inclui o pacote Compatibilidade do gerenciamento de correspondência).

Em seguida, é necessário importar o pacote de ativos (zip ou cmp) na nova configuração e, em seguida, atualizar os ativos e documentos por [executando o utilitário Migração](#runningmigrationutility). O Adobe recomenda criar novos ativos na nova configuração somente após a execução do utilitário de migração.

Devido a [compatibilidade com versões anteriores](/help/sites-deploying/backward-compatibility.md) alterações, os locais de algumas pastas no repositório crx são alterados. Exportar e importar dependências manualmente (bibliotecas e ativos personalizados) da configuração anterior para um novo ambiente.

## Leia antes de continuar com a migração {#prerequisites}

Para ativos de Gerenciamento de correspondência:

* Para os ativos importados da plataforma anterior, uma propriedade é adicionada: **fd:version=1.0**.
* Desde o AEM 6.1 Forms, os comentários não estão disponíveis para uso imediato. Os comentários adicionados anteriormente estão disponíveis nos ativos, mas não ficam visíveis na interface automaticamente. É necessário personalizar a propriedade ExtendedProperties na interface do usuário do AEM Forms para tornar os comentários visíveis.
* Em algumas versões anteriores, como o LiveCycle ES4, o texto foi editado usando o Flex RichTextEditor, mas desde AEM 6.1 Forms, o editor do HTML é usado. Devido a essa renderização e aparência das fontes, os tamanhos das fontes e as margens das fontes podem ser diferentes das versões anteriores na interface do usuário Autor. No entanto, as letras têm a mesma aparência ao serem renderizadas.
* As listas nos módulos de texto são aprimoradas e agora são renderizadas de forma diferente. Pode haver diferenças visuais. Recomendamos que você renderize e veja as letras em que está usando listas em módulos de texto.
* Como os módulos de conteúdo de imagem são convertidos em ativos do DAM e os layouts e fragmentos são adicionados aos formulários durante a migração, a propriedade Atualizado por para esses módulos muda para administrador.
* O histórico de versões dos ativos não é migrado e não está disponível após a migração. O histórico de versões subsequente após a migração é mantido.
* O estado Pronto para publicar está obsoleto desde o AEM 6.1 Forms, portanto, todos os ativos no estado Pronto para publicar são alterados para o estado Modificado.
* Como a interface do usuário é atualizada no AEM Forms 6.3, as etapas para executar as personalizações também são diferentes. Você precisa refazer a personalização se estiver migrando de uma versão anterior à 6.3.
* Os fragmentos de layout mudam de /content/apps/cm/layouts/fragmentlayouts/1001 para /content/apps/cm/modules/fragmentlayouts/1001. A referência do Dicionário de dados em ativos exibe o caminho do Dicionário de dados em vez de seu nome.
* Quaisquer espaços de tabulação usados para alinhamento em módulos de texto precisam ser reajustados. Para obter mais informações, consulte [Gerenciamento de correspondência - Uso do espaçamento entre guias para organizar o texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* As configurações do compositor de ativos são alteradas nas configurações de Gerenciamento de correspondência.
* Os ativos são movidos em pastas com nomes como Texto existente e Lista existente.

## Uso do utilitário de Migração {#using-the-migration-utility}

### Execução do utilitário de migração {#runningmigrationutility}

Execute o Migration Utility antes de fazer alterações nos ativos ou criar ativos. Recomendamos que você não execute o utilitário após fazer qualquer alteração ou criar ativos. Certifique-se de que a interface do usuário do Correspondence Management ou do Adaptive Forms Assets não esteja aberta enquanto o processo de migração estiver em execução.

Ao executar o Utilitário de migração pela primeira vez, um log é criado com o seguinte caminho e nome: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Esse log continua sendo atualizado com informações de gerenciamento de correspondência e migração do Adaptive Forms, como movimentação de ativos.

>[!NOTE]
>
>Antes de executar o utilitário de migração, certifique-se de ter feito um backup do seu repositório crx.

1. Em uma sessão do navegador, faça logon AEM instância do autor como Administrador.

1. Abra o seguinte URL no navegador:

   https://[*hostname*]:[*porta*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   O navegador exibe quatro opções:

   * Migração de ativos de AEM Forms
   * Migração de componentes personalizados adaptáveis do Forms
   * Migração de modelos adaptáveis do Forms
   * Migração das configurações de nuvem de AEM Forms

1. Faça o seguinte para executar a migração:

   * Para migrar **ativos**, toque em Migração de ativos do AEM Forms e, na próxima tela, toque em **Iniciar migração**. Os itens a seguir são migrados:

      * Formulários adaptáveis
      * Fragmentos de documento
      * Temas
      * Cartas
      * Dicionários de dados

   >[!NOTE]
   >
   >Durante a migração de ativos, é possível encontrar mensagens de aviso, como &quot;Conflito encontrado para...&quot;. Essas mensagens indicam que as regras para alguns componentes em formulários adaptáveis não puderam ser migradas. Por exemplo, se o componente tiver um evento que tenha regras e scripts, se as regras ocorrerem após qualquer script, nenhuma das regras do componente será migrada. Você pode [migrar essas regras abrindo o editor de regras](#migrate-rules) na criação de formulários adaptáveis.

   * Para migrar componentes personalizados de formulário adaptáveis, toque em **Migração de componentes personalizados adaptáveis do Forms** e, na página Migração de componentes personalizados, toque em **Iniciar migração**. Os itens a seguir são migrados:

      * Componentes personalizados criados para o Adaptive Forms
      * Sobreposições de componentes, se houver.
   * Para migrar modelos de formulário adaptáveis, toque em **Migração de modelo adaptável do Forms** e, na página Migração de componentes personalizados, toque em **Iniciar migração**. Os itens a seguir são migrados:

      * Modelos de formulário adaptável criados em `/apps` ou `/conf` usando AEM Editor de modelo.
   * Migrar os serviços de configuração da AEM Forms Cloud para aproveitar o novo paradigma do serviço de nuvem sensível ao contexto, que inclui a interface habilitada para toque (em `/conf`). Ao migrar os serviços de Configuração da AEM Forms Cloud, os serviços em nuvem em `/etc` são movidas para `/conf`. Se você não tiver personalizações de serviços de nuvem que dependem dos caminhos herdados (`/etc`), é recomendável executar o utilitário de migração logo após a atualização para o 6.5 e usar a interface do usuário de toque de configuração de nuvem para qualquer trabalho adicional. Se você já tiver personalizações de serviços de nuvem, continue usando a interface clássica na configuração atualizada até que as personalizações sejam atualizadas para se alinharem aos caminhos migrados (`/conf`) e, em seguida, execute o utilitário de migração.

   Para migrar **Serviços em nuvem da AEM Forms**, que incluem o seguinte, toque em Migração de configuração da AEM Forms Cloud (a migração de configuração da nuvem não depende do pacote de compatibilidade do AEMFD), toque em Migração de configurações da nuvem da AEM Forms e, em seguida, na página Migração de configuração , toque em **Iniciar migração**:

   * Serviços em nuvem do Modelo de dados de formulário

      * Caminho de origem: `/etc/cloudservices/fdm`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/fdm`
   * Recaptcha

      * Caminho de origem: `/etc/cloudservices/recaptcha`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * Caminho de origem: `/etc/cloudservices/echosign`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/echosign`
   * Serviços em nuvem Typekit

      * Caminho de origem: `/etc/cloudservices/typekit`
      * Caminho de destino: `/conf/global/settings/cloudconfigs/typekit`

   A janela do navegador exibe o seguinte à medida que o processo de migração ocorre:

   * Quando os ativos são atualizados: Ativos atualizados com êxito.
   * Quando a migração for concluída: Migração de ativos concluída.

   Quando executado, o utilitário de Migração faz o seguinte:

   * **Adiciona as tags aos ativos**: Adiciona a tag &quot;Gerenciamento de correspondência : Ativos migrados&quot; / &quot;Forms adaptável : Ativos migrados&quot;. para os ativos migrados, para que os usuários possam identificar os ativos migrados. Ao executar o utilitário de Migração, todos os ativos existentes no sistema são marcados como Migrado.
   * **Gera tags**: As categorias e subcategorias presentes no sistema anterior são criadas como tags e, em seguida, essas tags são associadas aos ativos relevantes do Gerenciamento de correspondência no AEM. Por exemplo, uma Categoria (Reivindicações) e uma Subcategoria (Reivindicações) de um modelo de carta são geradas como tags.










1. Depois que o utilitário de migração terminar de ser executado, continue com a [tarefas domésticas](#housekeepingtasks).

#### Migrar regras usando o editor de regras {#migrate-rules}

Esses componentes podem ser migrados abrindo-os no Editor de regras no editor adaptável do Forms.

* Para migrar regras e scripts (não é necessário se estiver atualizando da versão 6.3) em componentes personalizados, toque em Migração de componentes personalizados do Adaptive Forms e, na próxima tela, toque em Iniciar migração. Os itens a seguir são migrados:

   * Regras e scripts criados com o editor de regras (6.1 FP1 e posterior)

   * Scripts criados usando a guia Script na interface do usuário da versão 6.1 e anterior

* Para migrar modelos (não é necessário se estiver atualizando da versão 6.3 e 6.4), toque em Migração de modelo do Adaptive Forms e, na próxima tela, toque em Iniciar migração. Os itens a seguir são migrados:

   * Modelos antigos - os modelos de formulários adaptáveis criados em /apps usando o AEM 6.1 Forms ou anterior. Isso inclui os scripts que foram definidos nos componentes do modelo.

   * Novos modelos - Modelos de formulários adaptáveis criados usando o editor de modelos em /conf. Isso inclui a migração de regras e scripts criados com o editor de regras.

### Tarefas da família após executar o utilitário de migração {#housekeepingtasks}

Depois de executar o utilitário de Migração, siga as seguintes tarefas de manutenção:

1. Certifique-se de que a versão XFA dos layouts e dos layouts de fragmento seja a 3.3 ou posterior. Se você estiver usando layouts e layouts de fragmento de uma versão mais antiga, poderá haver problemas na renderização da carta. Para atualizar a versão de um XFA mais antigo para a versão mais recente, execute as seguintes etapas:

   1. [Baixe o XFA como um arquivo zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) na interface do usuário do Forms.
   1. Extraia o arquivo.
   1. Abra o arquivo XFA no Designer mais recente e salve-o. A versão do XFA é atualizada para a mais recente.
   1. Faça upload do XFA na interface do usuário do Forms.

1. Publique todos os ativos que foram publicados no sistema anterior antes da migração. O utilitário de migração atualiza os ativos somente na instância do autor e para atualizar os ativos na (s) instância (s) de publicação, é necessário publicar os ativos.

1. No AEM Forms 6.4 e 6.5, alguns dos direitos dos grupos de usuários de formulários são alterados. Se você quiser que qualquer um dos seus usuários possa fazer upload de XDPs e Adaptive Forms contendo scripts ou usar o editor de código, será necessário adicioná-los ao grupo de usuários avançados de formulários. Da mesma forma, os autores de modelo não podem mais usar o editor de código no Editor de regras. Para que os usuários possam usar o editor de código, adicione-os ao grupo af-template-script-writer. Para obter instruções sobre como adicionar usuários a grupos, consulte [Gerenciar usuários e grupos de usuários](/help/communities/users.md).
