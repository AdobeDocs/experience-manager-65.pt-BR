---
title: Migrar ativos e documentos da AEM Forms
seo-title: Migrar ativos e documentos da AEM Forms
description: O utilitário de Migração permite que você Migre ativos e documentos da AEM Forms do AEM 6.3 Forms ou de versões anteriores para o AEM 6.4 Forms.
seo-description: O utilitário de Migração permite que você Migre ativos e documentos da AEM Forms do AEM 6.3 Forms ou de versões anteriores para o AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 2%

---


# Migrar ativos e documentos da AEM Forms{#migrate-aem-forms-assets-and-documents}

O utilitário de Migração converte os ativos [](../../forms/using/introduction-forms-authoring.md)Adaptive Forms, as configurações [de](/help/sites-developing/extending-cloud-config.md)nuvem e os ativos [do Gerenciamento de](/help/forms/using/cm-overview.md) correspondência do formato usado nas versões anteriores para o formato usado no Forms AEM 6.5. Quando você executa o utilitário de migração, os seguintes itens são migrados:

* Componentes personalizados para formulários adaptáveis
* Modelos de gerenciamento de correspondência e formulários adaptativos
* Configurações da nuvem
* Gerenciamento de correspondência e ativos de formulários adaptáveis

>[!NOTE]
>
>Em caso de atualização fora do local, no caso de ativos do Gerenciamento de correspondência, você pode executar a migração toda vez que importar os ativos. Para a migração do Gerenciamento de correspondência, é necessário ter o Pacote de compatibilidade Forms instalado.

## Abordagem da migração {#approach-to-migration}

Você pode [atualizar](../../forms/using/upgrade.md) para a versão mais recente do AEM Forms 6.5 do AEM Forms 6.4, 6.3 ou 6.2 ou executar uma instalação de limpeza. Se você atualizou a instalação anterior ou executou uma instalação de limpeza, é necessário:

**Em caso de atualização no local**

Se você tiver realizado uma atualização no local, a instância atualizada já terá os ativos e os documentos. No entanto, antes de poder usar os ativos e documentos, será necessário instalar o pacote [Compatibilidade do](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEMFD (inclui o pacote Compatibilidade do Correspondence Management)

Em seguida, é necessário atualizar os ativos e documentos [executando o utilitário](#runningmigrationutility)de Migração.

**Em caso de instalação fora do local**

Se for uma instalação fora de lugar (nova), antes de poder usar os ativos e documentos, será necessário instalar o pacote [Compatibilidade do](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEMFD (inclui o pacote Compatibilidade do Correspondence Management).

Em seguida, é necessário importar o pacote de ativos (zip ou cmp) na nova configuração e atualizar os ativos e documentos [executando o utilitário](#runningmigrationutility)de Migração. A Adobe recomenda criar novos ativos na nova configuração somente depois de executar o utilitário de migração.

Devido a alterações [anteriores relacionadas](/help/sites-deploying/backward-compatibility.md) à compatibilidade, os locais de algumas pastas no repositório crx são alterados. Exporte e importe manualmente dependências (bibliotecas e ativos personalizados) da configuração anterior para o ambiente novo.

## Leia antes de continuar com a migração {#prerequisites}

Para os ativos de Gestão de Correspondência:

* Para os ativos importados da plataforma anterior, uma propriedade é adicionada: **fd:version=1.0**.
* Desde o AEM 6.1 Forms, os comentários não estão disponíveis na caixa. Os comentários adicionados anteriormente estão disponíveis nos ativos, mas não são visíveis automaticamente na interface. É necessário personalizar a propriedade ExtendedProperties na interface do usuário do AEM Forms para tornar os comentários visíveis.
* Em algumas das versões anteriores, como o LiveCycle ES4, o texto foi editado usando o Flex RichTextEditor, mas desde AEM 6.1 Forms, o editor HTML é usado. Devido a essa renderização e aparência das fontes, os tamanhos de fonte e as margens de fonte podem ser diferentes das versões anteriores na interface do usuário do Autor. No entanto, as letras têm a mesma aparência quando renderizadas.
* As listas nos módulos de texto são aprimoradas e agora são renderizadas de forma diferente. Podem existir diferenças visuais. Recomendamos que você renderize e veja as letras nas quais está usando o lista nos módulos de texto.
* Como os módulos de conteúdo de imagem são convertidos em ativos DAM e os layouts e fragmentos são adicionados aos formulários durante a migração, a propriedade Atualizado por para esses módulos muda para admin.
* O histórico de versão dos ativos não é migrado e não está disponível após a migração. O histórico de versão subsequente após a migração é mantido.
* O estado Pronto para publicar está obsoleto desde o AEM 6.1 Forms, portanto todos os ativos no estado Pronto para publicar são alterados para o estado Modificado.
* Como a interface do usuário é atualizada no AEM Forms 6.3, as etapas para executar as personalizações também são diferentes. É necessário refazer a personalização se você estiver migrando de uma versão anterior à 6.3.
* Os Fragmentos de layout mudam de /content/apps/cm/layouts/fragmentlayouts/1001 para /content/apps/cm/modules/fragmentlayouts. A referência do Dicionário de dados em ativos exibe o caminho do Dicionário de dados em vez do nome.
* Quaisquer espaços de tabulação usados para alinhamento em módulos de texto precisam ser reajustados. Para obter mais informações, consulte Gerenciamento de [correspondência - Uso do espaçamento entre guias para organizar o texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* As configurações do compositor de ativos mudam para as configurações do Gerenciamento de correspondência.
* Os ativos são movidos em pastas com nomes como Texto existente e Lista existente.

## Uso do utilitário de migração {#using-the-migration-utility}

### Execução do utilitário de migração {#runningmigrationutility}

Execute o utilitário de Migração antes de fazer alterações nos ativos ou criar ativos. Recomendamos que você não execute o utilitário depois de fazer alterações ou criar ativos. Certifique-se de que a interface do usuário do Gerenciamento de correspondência ou dos Ativos adaptáveis Forms não esteja aberta enquanto o processo de migração estiver em execução.

Quando você executa o Utilitário de migração pela primeira vez, um log é criado com o seguinte caminho e nome: \[aem-installation-diretory]\cq-quickstart\logs\aem-forms-migration.log. Este registro continua sendo atualizado com as informações de gerenciamento de correspondência e migração adaptativa do Forms, como a movimentação de ativos.

>[!NOTE]
>
>Antes de executar o utilitário de migração, certifique-se de ter realizado um backup do repositório do crx.

1. Em uma sessão do navegador, faça logon AEM instância do autor como um Administrador.

1. Abra o seguinte URL no navegador:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   O navegador exibe quatro opções:

   * Migração de ativos de AEM Forms
   * Migração adaptável de componentes personalizados Forms
   * Migração de modelos adaptáveis Forms
   * Migração das configurações de nuvem de AEM Forms

1. Faça o seguinte para executar a migração:

   * Para migrar **ativos**, toque em Migração de ativos AEM Forms e, na tela seguinte, toque em Migração **de** Start. Os itens a seguir são migrados:

      * Formulários adaptáveis
      * Fragmentos de documento
      * Temas
      * Cartas
      * Dicionários de dados

   >[!NOTE]
   >
   >Durante a migração de ativos, você pode encontrar mensagens de aviso como &quot;Conflito encontrado para...&quot;. Essas mensagens indicam que as regras para alguns componentes em formulários adaptáveis não puderam ser migradas. Por exemplo, se o componente tiver um evento com regras e scripts, se as regras ocorrerem após qualquer script, nenhuma das regras do componente será migrada. No entanto, essas regras podem ser migradas abrindo o editor de regras na criação de formulários adaptáveis.
   >
   >
   >Esses componentes podem ser migrados abrindo-os no Editor de regras no editor Adaptive Forms.
   >
   >
   >
   >    * Para migrar regras e scripts (não necessário se a atualização for feita a partir da versão 6.3) em componentes personalizados, toque em Migração de componentes personalizados da Forms adaptáveis e, na tela seguinte, toque em Migração de Start. Os itens a seguir são migrados:    >
      >
      >
      >        

      * Regras e scripts criados usando o editor de regras (6.1 FP1 e posterior)
      >        * Scripts criados usando a guia Script na interface do usuário da versão 6.1 e anterior
   >
   >
   >    * Para migrar modelos (não é necessário se a atualização for feita da versão 6.3 e 6.4), toque em Migração de modelo Forms adaptável e, na tela seguinte, toque em Migração de Start. Os itens a seguir são migrados:

      >
      >
      >
      >        


      * Modelos antigos - os modelos de formulários adaptáveis criados em /apps usando AEM 6.1 Forms ou anterior. Isso inclui os scripts que foram definidos nos componentes do modelo.
      >        * Novos modelos - Modelos de formulários adaptáveis criados usando o editor de modelos em /conf. Isso inclui a migração de regras e scripts criados usando o editor de regras.


   * Para migrar de componentes personalizados de forma adaptável, toque em Migração **de componentes personalizados** adaptáveis Forms e, na página Migração de componentes personalizados, toque em Migração **de** Start. Os itens a seguir são migrados:

      * Componentes personalizados criados para o Adaptive Forms
      * Sobreposições de componentes, se houver.
   * Para migrar modelos de formulário adaptáveis, toque em Migração **de modelo Forms adaptável e, na página Migração de componentes personalizados, toque em Migração** de **** Start. Os itens a seguir são migrados:

      * Modelos de formulário adaptáveis criados em /apps ou /conf usando AEM Editor de modelos.
   * Migre os serviços de Configuração da AEM Forms Cloud para aproveitar o novo paradigma de serviço em nuvem sensível ao contexto, que inclui a interface habilitada para toque (em /conf). Quando você migra os serviços de Configuração da AEM Forms Cloud, os serviços em nuvem em /etc são movidos para /conf. Se você não tiver personalizações de serviços em nuvem que dependam dos caminhos herdados (/etc), é recomendável executar o utilitário de migração logo após a atualização para a versão 6.5 e usar a configuração em nuvem Touch UI para qualquer trabalho adicional. Se você tiver personalizações de serviços em nuvem, continue usando a interface clássica na configuração atualizada até que as personalizações sejam atualizadas para alinhar-se aos caminhos migrados (/conf) e execute o utilitário de migração.

   Para migrar os serviços **em nuvem da** AEM Forms, que incluem o seguinte, toque em Migração de configuração da AEM Forms Cloud (a migração de configuração em nuvem é independente do pacote de compatibilidade da AEMFD), toque em Migração de configurações da AEM Forms Cloud e, na página Migração de configuração, toque em Migração **de** Start:

   * Serviços em nuvem do Form Data Model

      * Caminho de origem: /etc/cloudservices/fdm
      * Caminho do público alvo: /conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * Caminho de origem: /etc/cloudservices/recaptcha
      * Caminho do público alvo: /conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * Caminho de origem: /etc/cloudservices/echosign
      * Caminho do público alvo: /conf/global/settings/cloudconfigs/echosign
   * Serviços em nuvem Typekit

      * Caminho de origem: /etc/cloudservices/typekit
      * Caminho do público alvo: /conf/global/settings/cloudconfigs/typekit

   A janela do navegador exibe o seguinte à medida que o processo de migração ocorre:

   * Quando os ativos são atualizados: Ativos atualizados com êxito.
   * Quando a migração estiver concluída: Migração de ativos concluída.

   Quando executado, o utilitário de Migração faz o seguinte:

   * **Adiciona as tags aos ativos**: Adiciona a tag &quot;Gerenciamento de correspondência: Migração de ativos&quot; / &quot;Forms adaptável: Ativos migrados&quot;. para os ativos migrados, para que os usuários possam identificar os ativos migrados. Quando você executa o utilitário de Migração, todos os ativos existentes no sistema são marcados como Migrados.
   * **Gera tags**: Categorias e subcategorias presentes no sistema anterior são criadas como tags e, em seguida, essas tags são associadas aos ativos relevantes do Gerenciamento de correspondência no AEM. Por exemplo, uma Categoria (Reivindicações) e uma Subcategoria (Reivindicações) de um modelo de carta são geradas como tags.

















1. Depois que o utilitário de migração terminar de ser executado, vá para as tarefas [de](#housekeepingtasks)manutenção.

### Tarefas para uso doméstico após executar o utilitário de migração {#housekeepingtasks}

Após executar o utilitário de migração, tome cuidado com as seguintes tarefas de manutenção: [](../../forms/using/import-export-forms-templates.md)

1. Certifique-se de que a versão XFA de layouts e layouts de fragmento seja 3.3 ou posterior. Se você estiver usando layouts e layouts de fragmento de uma versão mais antiga, pode haver problemas na renderização da carta. Para atualizar a versão de um XFA mais antigo para a versão mais recente, conclua as seguintes etapas:

   1. [Baixe o XFA como um arquivo](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) zip da interface do usuário do Forms.
   1. Extraia o arquivo.
   1. Abra o arquivo XFA no Designer mais recente e salve-o. A versão do XFA é atualizada para a mais recente.
   1. Carregue o XFA na interface do usuário do Forms.

1. Publique todos os ativos que foram publicados no sistema anterior antes da migração. O utilitário de migração atualiza os ativos somente na instância do autor e para atualizar os ativos nas instâncias de publicação que você precisa para publicar os ativos.
1. No AEM Forms 6.4 e 6.5, alguns dos direitos dos grupos de usuários dos formulários são alterados. Se você quiser que qualquer um de seus usuários seja capaz de carregar XDPs e Forms adaptável que contêm scripts ou usar o editor de códigos, é necessário adicioná-los ao grupo de usuários avançados para formulários. Da mesma forma, os autores de modelo não podem mais usar o editor de código no Editor de regras. Para que os usuários possam usar o editor de código, adicione-os ao grupo af-template-script-writer. Para obter instruções sobre como adicionar usuários a grupos, consulte [Gerenciamento de usuários e grupos](/help/communities/users.md)de usuários.

