---
title: Verificação e solução de problemas da pós-atualização
seo-title: Verificação e solução de problemas da pós-atualização
description: Saiba como solucionar problemas que podem aparecer após uma atualização.
seo-description: Saiba como solucionar problemas que podem aparecer após uma atualização.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
feature: Atualização
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---


# Pós-atualização e solução de problemas{#post-upgrade-checks-and-troubleshooting}

## Controles de pós-atualização {#post-upgrade-checks}

Após a [Atualização no local](/help/sites-deploying/in-place-upgrade.md) as seguintes atividades devem ser executadas para finalizar a atualização. Pressupõe-se que AEM tenha sido iniciado com o jar 6.5 e que a base de código atualizada tenha sido implantada.

* [Verificar logs para o sucesso da atualização](#main-pars-header-290365562)

* [Verificar pacotes OSGi](#main-pars-header-1637350649)

* [Verificar Versão do Oak](#main-pars-header-1293049773)

* [Inspect da pasta PreUpgradeBackup](#main-pars-header-988995987)

* [Validação inicial de páginas](#main-pars-header-20827371)
* [Aplicar AEM Service Packs](#main-pars-header-215142387)

* [Migrar recursos AEM](#main-pars-header-1434457709)

* [Verificar configurações de manutenção programadas](#main-pars-header-1552730183)

* [Ativar Agentes de Replicação](#main-pars-header-823243751)

* [Habilitar trabalhos agendados personalizados](#main-pars-header-244535083)

* [Executar plano de teste](#main-pars-header-1167972233)

### Verifique os logs para o sucesso da atualização {#verify-logs-for-upgrade-success}

**upgrade.log**

Anteriormente, inspecionar o estado pós-atualização da sua instância exigia uma inspeção cuidadosa de vários arquivos de log, partes do repositório e a barra de lançamento. Gerar um relatório pós-atualização pode ajudar a detectar atualizações com defeito antes de entrar em funcionamento.

A principal finalidade desse recurso é reduzir a necessidade de interpretação manual ou lógica de análise complexa em vários endpoints necessários para qualificar o sucesso de uma atualização. A solução tem como objetivo fornecer informações inequívocas para que os sistemas externos de automação reajam ao sucesso ou à falha identificada de uma atualização.

Mais especificamente, garante que:

* As falhas de atualização detectadas pela estrutura de atualização podem ser centralizadas em um único relatório de atualização;
* O relatório de atualização inclui indicadores sobre a intervenção manual necessária.

Para acomodar isso, as alterações foram feitas na maneira como os logs são gerados no arquivo `upgrade.log` .

Este é um exemplo de relatório que não mostra erros durante a atualização:

![148788743006](assets/1487887443006.png)

Este é um exemplo de relatório que mostra um pacote que não foi instalado durante o processo de atualização:

![1487887532730](assets/1487887532730.png)

**error.log**

O error.log deve ser cuidadosamente revisado durante e após a inicialização do AEM usando o jar da versão de destino. Quaisquer avisos ou erros devem ser revisados. Em geral, é melhor procurar problemas no início do log. Os erros que ocorrem posteriormente no log podem ser efeitos colaterais de uma causa raiz que é chamada precocemente no arquivo . Se ocorrerem erros e avisos repetidos, veja abaixo [Analisando Problemas com o Upgrade](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificar pacotes OSGi {#verify-osgi-bundles}

Navegue até o console OSGi `/system/console/bundles` e verifique se algum pacote não foi iniciado. Se algum pacote estiver em um estado instalado, consulte o `error.log` para determinar o problema raiz.

### Verifique a versão do Oak {#verify-oak-version}

Após a atualização, você deve ver que a versão do Oak foi atualizada para **1.10.2**. Para verificar a versão do Oak, navegue até o console OSGi e olhe a versão associada aos pacotes Oak: Oak Core, Oak Commons, Oak Segment Tar.

### Pasta Inspect PreUpgradeBackup {#inspect-preupgradebackup-folder}

Durante a atualização, o AEM tentará fazer backup das personalizações e armazená-las abaixo de `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Para visualizar essa pasta no CRXDE Lite, talvez seja necessário [ativar temporariamente o CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

A pasta com o carimbo de data e hora deve ter uma propriedade chamada `mergeStatus` com um valor `COMPLETED`. A pasta **to-process** deve estar vazia e o nó **overwrite** indica quais nós foram substituídos durante a atualização. O conteúdo abaixo do nó **esquerdos** indica o conteúdo que não pôde ser mesclado com segurança durante a atualização. Se sua implementação depender de qualquer um dos nós secundários (e ainda não estiver instalada pelo seu pacote de códigos atualizado), eles precisarão ser mesclados manualmente.

Desative o CRXDE Lite após este exercício se estiver em um ambiente de Preparo ou Produção.

### Validação inicial das páginas {#initial-validation-of-pages}

Execute uma validação inicial em relação a várias páginas no AEM. Se estiver atualizando um ambiente de Autor, abra a página Iniciar e a página de Boas-vindas ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Nos ambientes Autor e Publicação, abra algumas páginas do aplicativo e teste de fumaça que sejam renderizados corretamente. Se algum problema ocorrer, consulte o `error.log` para solucionar o problema.

### Aplicar AEM Service Packs {#apply-aem-service-packs}

Aplique todos os Service Packs relevantes do AEM 6.5, se tiverem sido lançados.

### Migrar recursos AEM {#migrate-aem-features}

Vários recursos no AEM exigem etapas adicionais após a atualização. Uma lista completa desses recursos e etapas para migrá-los no AEM 6.5 pode ser encontrada na página [Upgrade Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md).

### Verificar as configurações de manutenção programadas {#verify-scheduled-maintenance-configurations}

#### Habilitar coleta de lixo do armazenamento de dados {#enable-data-store-garbage-collection}

Se estiver usando um Armazenamento de dados de arquivo, verifique se a tarefa Coleta de lixo do armazenamento de dados está habilitada e adicionada à lista Manutenção semanal . As instruções são descritas [aqui](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Isso não é recomendado para instalações personalizadas de armazenamento de dados S3 ou ao usar um armazenamento de dados compartilhado.

#### Ativar Limpeza de Revisão Online {#enable-online-revision-cleanup}

Se estiver usando o MongoMK ou o novo formato de segmento TarMK, certifique-se de que a tarefa Revisão de limpeza esteja habilitada e adicionada à lista Manutenção diária. Instruções descritas [aqui](/help/sites-deploying/revision-cleanup.md).

### Executar plano de teste {#execute-test-plan}

Execute o plano de teste detalhado em função da definição [Upgrade Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md) na seção **Test Procedure**.

### Ativar Agentes de Replicação {#enable-replication-agents}

Depois que o ambiente de publicação tiver sido totalmente atualizado e validado, ative os agentes de replicação no Ambiente do autor. Verifique se os agentes podem se conectar às respectivas instâncias de Publicação. Consulte U [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md) para obter mais detalhes sobre a ordem dos eventos.

### Habilitar tarefas agendadas personalizadas {#enable-custom-scheduled-jobs}

Quaisquer tarefas programadas como parte da base de código podem ser ativadas neste ponto.

## Analisando Problemas Com A Atualização {#analyzing-issues-with-upgrade}

Esta seção contém alguns cenários de problema que podem ser enfrentados ao longo do procedimento de atualização para o AEM 6.3.

Esses cenários devem ajudar a rastrear a causa raiz dos problemas relacionados à atualização e devem ajudar a identificar problemas específicos do projeto ou produto.

### Falha na migração do repositório {#repository-migration-failing-}

A migração de dados do CRX2 para o Oak deve ser viável para qualquer cenário que comece com Instâncias de Origem com base no CQ 5.4. Certifique-se de seguir exatamente as instruções de atualização neste documento, que incluem a preparação do `repository.xml`, certificando-se de que nenhum autenticador personalizado personalizado seja iniciado via JAAS e de que a instância tenha sido verificada em busca de inconsistências antes de iniciar a migração.

Se a migração ainda falhar, você poderá descobrir qual é a causa raiz inspecionando o `upgrade.log`. Se o problema ainda não for conhecido, informe-o ao Suporte ao cliente.

### A atualização não foi executada {#the-upgrade-did-not-run}

Antes de iniciar as etapas de preparação, execute a instância **source** primeiro executando-a com o comando java -jar aem-quickstart.jar. Isso é necessário para garantir que o arquivo quickstart.properties seja gerado corretamente. Se estiver faltando, a atualização não funcionará. Como alternativa, você pode verificar se o arquivo está presente procurando em `crx-quickstart/conf` na pasta de instalação da instância de origem. Além disso, ao iniciar o AEM para iniciar a atualização, ele deve ser executado com o comando java -jar aem-quickstart.jar. A inicialização a partir de um script de início não iniciará AEM no modo de atualização.

### Pacotes e pacotes falham ao atualizar {#packages-and-bundles-fail-to-update-}

Caso ocorra falha na instalação dos pacotes durante a atualização, os pacotes que eles contêm também não serão atualizados. Normalmente, essa categoria de problemas é causada por erros de configuração do armazenamento de dados. Eles também serão exibidos como mensagens **ERROR** e **AVISO** no error.log. Como na maioria desses casos o logon padrão pode falhar, você pode usar o CRXDE diretamente para inspecionar e encontrar os problemas de configuração.

### Alguns pacotes de AEM não estão alternando para o estado ativo {#some-aem-bundles-are-not-switching-to-the-active-state}

No caso de pacotes que não estão sendo iniciados, você deve verificar se há dependências insatisfeitas.

Caso esse problema esteja presente, mas se baseie em uma instalação de pacote com falha que levou à não atualização dos pacotes, eles serão considerados incompatíveis para a nova versão. Para obter mais informações sobre como solucionar problemas, consulte **Pacotes e Pacotes Falham em Atualizar** acima.

Também é recomendável comparar a lista de pacotes de uma nova instância do AEM 6.5 com a atualizada para detectar os pacotes que não foram atualizados. Isso fornecerá um escopo mais próximo do que pesquisar no `error.log`.

### Pacotes personalizados que não estão alternando para o estado ativo {#custom-bundles-not-switching-to-the-active-state}

Caso seus pacotes personalizados não estejam alternando para o estado ativo, é provável que haja um código que não esteja importando a API de alteração. Isso frequentemente levará a dependências insatisfeitas.

A API que foi removida deve ser marcada como obsoleta em uma das versões anteriores. Você pode encontrar instruções sobre a migração direta do seu código neste aviso de descontinuação. O Adobe visa o controle de versão semântico sempre que possível, para que as versões possam indicar alterações de quebra.

Também é melhor verificar se a mudança que causou o problema foi absolutamente necessária e revertê-la, caso não seja. Verifique também se o aumento da versão da exportação do pacote foi aumentado mais do que o necessário, após o controle de versão semântico restrito.

### Interface de usuário da plataforma com funcionamento incorreto {#malfunctioning-platform-ui}

No caso de determinadas funcionalidades da interface do usuário que não estão funcionando corretamente após a atualização, verifique primeiro se há sobreposições personalizadas da interface. Algumas estruturas podem ter mudado e a sobreposição pode precisar de uma atualização ou é obsoleta.

Em seguida, verifique se há erros de Javascript que podem ser rastreados até extensões personalizadas adicionadas que estão conectadas às bibliotecas do cliente. O mesmo pode ser aplicado para CSS personalizado que pode estar causando problemas no layout de AEM.

Finalmente, verifique se há configuração incorreta que o Javascript talvez não consiga lidar. Isso geralmente ocorre com extensões desativadas incorretamente.

### Componentes personalizados com mau funcionamento, modelos ou extensões de interface do usuário {#malfunctioning-custom-components-templates-or-ui-extensions}

Na maioria dos casos, as causas raiz desses problemas são as mesmas dos pacotes que não foram iniciados ou dos pacotes que não estão sendo instalados com a única diferença de que os problemas começam a ocorrer ao usar os componentes pela primeira vez.

A maneira de lidar com códigos personalizados incorretos é primeiro realizar testes de fumaça para identificar a causa. Depois de encontrá-lo, examine as recomendações nesta seção [link] do artigo para descobrir maneiras de corrigi-las.

### Personalizações ausentes em /etc {#missing-customizations-under-etc}

`/apps` e  `/libs` são bem manipuladas pela atualização, mas as alterações em  `/etc` podem precisar ser restauradas manualmente a partir de  `/var/upgrade/PreUpgradeBackup` após a atualização. Certifique-se de verificar este local para qualquer conteúdo que precise ser mesclado manualmente.

### Analisando o error.log e o upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Na maioria das situações, os registros precisam ser consultados quanto a erros, para encontrar a causa de um problema. No entanto, no caso de atualizações, também é necessário monitorar os problemas de dependência, pois os pacotes antigos podem não ser atualizados corretamente.

A melhor maneira de fazer isso é eliminar o error.log, removendo todas as mensagens que devem não estar relacionadas ao problema que você está enfrentando. Você pode fazer isso por meio de uma ferramenta como grep, usando:

```shell
grep -v UnrelatedErrorString
```

Algumas mensagens de erro podem não ser explicativas imediatamente. Nesse caso, observar o contexto em que ocorre também pode ajudar a entender onde o erro foi criado. Você pode separar o erro usando:

* `grep -B` para adicionar linhas antes do erro;

ou

* `grep -A` para adicionar linhas depois de.

Em alguns casos, também é possível encontrar erros nas mensagens AVISO, pois pode haver casos válidos que levam a esse estado e o aplicativo nem sempre pode decidir se esse é um erro real. Consulte essas mensagens também.

### Entrar em contato com o suporte do Adobe {#contacting-adobe-support}

Se você tiver passado pelos conselhos nesta página e ainda estiver vendo problemas, entre em contato com o Suporte do Adobe. Para fornecer o máximo possível de informações ao engenheiro de suporte que trabalha no seu caso, inclua o arquivo upgrade.log da sua atualização.
