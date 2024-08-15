---
title: Verificações pós-atualização e solução de problemas
description: Saiba como solucionar problemas que podem ocorrer após uma atualização.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 0%

---

# Verificações pós-atualização e solução de problemas{#post-upgrade-checks-and-troubleshooting}

## Verificações pós-atualização {#post-upgrade-checks}

Após a [Atualização no Local](/help/sites-deploying/in-place-upgrade.md), as atividades a seguir devem ser executadas para finalizar a atualização. Pressupõe-se que o AEM tenha sido iniciado com o jar 6.5 e que a base de código atualizada tenha sido implantada.

* [Verificar logs para o sucesso da atualização](#main-pars-header-290365562)

* [Verificar pacotes OSGi](#main-pars-header-1637350649)

* [Verificar versão do Oak](#main-pars-header-1293049773)

* [Inspect, a pasta PreUpgradeBackup](#main-pars-header-988995987)

* [Validação inicial das páginas](#main-pars-header-20827371)
* [Aplicar Service Packs do AEM](#main-pars-header-215142387)

* [Migrar recursos do AEM](#main-pars-header-1434457709)

* [Verificar configurações de manutenção programada](#main-pars-header-1552730183)

* [Habilitar agentes de replicação](#main-pars-header-823243751)

* [Habilitar os trabalhos agendados personalizados](#main-pars-header-244535083)

* [Executar plano de teste](#main-pars-header-1167972233)

### Verificar logs para Êxito na Atualização {#verify-logs-for-upgrade-success}

**atualizar.log**

Anteriormente, a inspeção do estado pós-atualização da instância exigia uma inspeção cuidadosa de vários arquivos de log, partes do repositório e a barra inicial. Gerar um relatório pós-atualização pode ajudar a detectar atualizações com defeito antes de entrar em funcionamento.

O principal objetivo desse recurso é reduzir a necessidade de interpretação manual ou lógica de análise complexa entre vários endpoints necessários para qualificar o sucesso de uma atualização. A solução tem como objetivo fornecer informações inequívocas para que os sistemas de automação externos reajam ao sucesso ou à falha identificada de uma atualização.

Mais especificamente, garante que:

* As falhas de atualização detectadas pela estrutura de atualização são centralizadas em um único relatório de atualização;
* O relatório de atualização inclui indicadores sobre a intervenção manual necessária.

Para acomodar isso, foram feitas alterações na maneira como os logs são gerados no arquivo `upgrade.log`.

Este é um exemplo de relatório que não mostra erros durante a atualização:

![1487887443006](assets/1487887443006.png)

Este é um exemplo de relatório que mostra um pacote que não foi instalado durante o processo de atualização:

![1487887532730](assets/1487887532730.png)

**log.erro**

O error.log deve ser cuidadosamente revisado durante e após a inicialização do AEM usando o jar da versão de destino. Quaisquer avisos ou erros devem ser revisados. Em geral, é melhor procurar problemas no início do log. Os erros que ocorrem posteriormente no log podem ser, na verdade, efeitos colaterais de uma causa raiz que é chamada no início do arquivo. Se ocorrerem erros e avisos repetidos, consulte abaixo para [Analisar problemas com a Atualização](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificar pacotes OSGi {#verify-osgi-bundles}

Navegue até o console OSGi `/system/console/bundles` e verifique se algum pacote não foi iniciado. Se algum pacote estiver em um estado instalado, consulte `error.log` para determinar o problema raiz.

### Verificar versão do Oak {#verify-oak-version}

Após a atualização, você deve ver que a versão do Oak foi atualizada para **1.10.2**. Para verificar a versão do Oak, navegue até o console OSGi e verifique a versão associada aos pacotes do Oak: Oak Core, Oak Commons, Oak Segment Tar.

### Pasta PreUpgradeBackup do Inspect {#inspect-preupgradebackup-folder}

Durante a atualização, o AEM tenta fazer backup das personalizações e armazená-las abaixo de `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Para exibir esta pasta no CRXDE Lite, talvez seja necessário [habilitar temporariamente o CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

A pasta com o carimbo de data/hora deve ter uma propriedade chamada `mergeStatus` com o valor `COMPLETED`. A pasta **a processar** deve estar vazia e o nó **substituído** indica quais nós foram substituídos durante a atualização. O conteúdo abaixo do nó restante indica conteúdo que não pôde ser mesclado com segurança durante a atualização. Se a implementação depender de qualquer um dos nós secundários (e ainda não instalados pelo pacote de código atualizado), eles precisarão ser mesclados manualmente.

Desative o CRXDE Lite após este exercício se estiver em um ambiente de Preparo ou Produção.

### Validação inicial das páginas {#initial-validation-of-pages}

Executar uma validação inicial em várias páginas no AEM. Se estiver atualizando um ambiente de Autor, abra a página Inicial e a página de Boas-vindas ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Em ambos os ambientes, Autor e Publish, abra algumas páginas de aplicativo e teste de fumaça que eles renderizam corretamente. Se algum problema ocorrer, consulte `error.log` para solucionar.

### Aplicar Service Packs do AEM {#apply-aem-service-packs}

Aplique quaisquer Service Packs AEM 6.5 relevantes caso eles tenham sido lançados.

### Migrar recursos do AEM {#migrate-aem-features}

Vários recursos no AEM exigem etapas adicionais após a atualização. Uma lista completa desses recursos e etapas para migrá-los no AEM 6.5 pode ser encontrada na página [Atualizando código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md).

### Verificar configurações de manutenção programada {#verify-scheduled-maintenance-configurations}

#### Habilitar coleta de lixo do armazenamento de dados {#enable-data-store-garbage-collection}

Se estiver usando um Armazenamento de dados de arquivo, verifique se a tarefa Coleta de lixo do armazenamento de dados está ativada e adicionada à lista de Manutenção semanal. As instruções estão descritas em [Limpeza de revisão](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Isso não é recomendado para instalações de armazenamento de dados personalizado S3 ou ao usar um armazenamento de dados compartilhado.

#### Ativar limpeza de revisão online {#enable-online-revision-cleanup}

Se estiver usando MongoMK ou o novo formato de segmento TarMK, verifique se a tarefa Revision Clean Up está ativada e adicionada à lista Daily Maintenance (Manutenção diária). As instruções estão descritas em [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md).

### Executar plano de teste {#execute-test-plan}

Execute o plano de teste detalhado conforme definido [Atualizando Código e Personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) na seção **Procedimento de Teste**.

### Habilitar agentes de replicação {#enable-replication-agents}

Depois que o ambiente de publicação for totalmente atualizado e validado, ative os agentes de replicação no Ambiente de autor. Verifique se os agentes podem se conectar às respectivas instâncias do Publish. Consulte U [Atualizar Procedimento](/help/sites-deploying/upgrade-procedure.md) para obter mais detalhes sobre a ordem dos eventos.

### Habilitar os trabalhos agendados personalizados {#enable-custom-scheduled-jobs}

Todos os trabalhos agendados como parte da base de código podem ser ativados neste ponto.

## Análise De Problemas Com A Atualização {#analyzing-issues-with-upgrade}

Esta seção contém alguns cenários de problemas que podem ocorrer durante o procedimento de atualização para AEM 6.3.

Esses cenários devem ajudar a rastrear a causa raiz de problemas relacionados à atualização e devem ajudar a identificar problemas específicos do projeto ou do produto.

### Falha na migração do repositório  {#repository-migration-failing-}

A migração de dados do CRX2 para o Oak deve ser viável para qualquer cenário que comece com Instâncias do Source com base no CQ 5.4. Siga exatamente as instruções de atualização neste documento, que incluem a preparação do `repository.xml`, verificando se nenhum autenticador personalizado foi iniciado via JAAS e se a instância foi verificada em busca de inconsistências antes de iniciar a migração.

Se a migração ainda falhar, você poderá descobrir qual é a causa raiz inspecionando o `upgrade.log`. Se o problema ainda não for conhecido, relate-o ao Suporte ao Cliente.

### A Atualização Não Foi Executada {#the-upgrade-did-not-run}

Antes de iniciar as etapas de preparação, execute primeiro a instância **source** com o comando Java™ -jar aem-quickstart.jar. Isso é necessário para garantir que o arquivo quickstart.properties seja gerado corretamente. Se estiver ausente, a atualização não funcionará. Como alternativa, você pode verificar se o arquivo está presente procurando em `crx-quickstart/conf` na pasta de instalação da instância de origem. Além disso, ao iniciar o AEM para iniciar a atualização, ele deve ser executado com o comando Java™ -jar aem-quickstart.jar. A inicialização a partir de um script de inicialização não iniciará o AEM no modo de atualização.

### Falha ao atualizar pacotes e pacotes  {#packages-and-bundles-fail-to-update-}

Se os pacotes não forem instalados durante a atualização, os pacotes que eles contêm também não serão atualizados. Essa categoria de problemas é causada por uma configuração incorreta do armazenamento de dados. Eles também aparecerão como mensagens de **ERRO** e **AVISO** no error.log. Como na maioria desses casos o logon padrão pode falhar, você pode usar o CRXDE diretamente para inspecionar e encontrar os problemas de configuração.

### Alguns pacotes de AEM não estão mudando para o estado ativo {#some-aem-bundles-are-not-switching-to-the-active-state}

Se houver pacotes não inicializando, verifique se há dependências não satisfeitas.

Caso esse problema esteja presente, mas se baseie em uma instalação de pacote com falha que resultou na não atualização de pacotes, eles serão considerados incompatíveis para a nova versão. Para obter mais informações sobre como solucionar problemas, consulte **Falha ao atualizar pacotes e pacotes** acima.

Também é recomendável comparar a lista de pacotes de uma instância atualizada do AEM 6.5 com a atualizada para detectar os pacotes que não foram atualizados. Isso fornecerá um escopo mais próximo do que procurar no `error.log`.

### Pacotes personalizados não estão alternando para o estado ativo {#custom-bundles-not-switching-to-the-active-state}

Caso seus pacotes personalizados não estejam alternando para o estado ativo, é provável que haja um código que não esteja importando a API de alteração. Isso levará, na maioria das vezes, a dependências insatisfeitas.

A API removida deve ser marcada como obsoleta em uma das versões anteriores. Você pode encontrar instruções sobre uma migração direta do seu código neste aviso de desativação. O Adobe visa o controle de versão semântico sempre que possível, para que as versões possam indicar alterações de quebra.

Também é melhor verificar se a alteração que causou o problema foi necessária e, caso contrário, revertê-la. Verifique também se o aumento da versão da exportação de pacotes foi aumentado mais do que o necessário, após o controle de versão semântico rigoroso.

### Interface de plataforma defeituosa {#malfunctioning-platform-ui}

Se houver determinada funcionalidade da interface do usuário que não esteja funcionando corretamente após a atualização, verifique primeiro se há sobreposições personalizadas da interface. Algumas estruturas podem ter sido alteradas e a sobreposição pode precisar de uma atualização ou está obsoleta.

Em seguida, verifique se há erros do JavaScript que possam ser rastreados até extensões adicionadas personalizadas que estejam vinculadas às bibliotecas do cliente. O mesmo pode se aplicar ao CSS personalizado que pode estar causando problemas no layout do AEM.

Por fim, verifique se há erros de configuração com os quais o JavaScript talvez não possa lidar. Geralmente, isso ocorre com extensões desativadas incorretamente.

### Componentes personalizados com defeito, Modelos ou Extensões de UI {#malfunctioning-custom-components-templates-or-ui-extensions}

Normalmente, as causas básicas desses problemas são as mesmas dos pacotes que não são iniciados ou dos pacotes que não estão sendo instalados, com a única diferença de que os problemas começam a ocorrer ao usar os componentes pela primeira vez.

A maneira de lidar com um código personalizado incorreto é primeiro executar testes de fumaça para identificar a causa. Depois de encontrá-lo, consulte as recomendações nesta seção [link] do artigo para saber como corrigi-lo.

### Personalizações ausentes em /etc {#missing-customizations-under-etc}

`/apps` e `/libs` são bem tratados pela atualização, mas as alterações em `/etc` podem precisar ser restauradas manualmente de `/var/upgrade/PreUpgradeBackup` após a atualização. Verifique neste local se há conteúdo que precise ser mesclado manualmente.

### Analisando error.log e upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Na maioria das situações, os registros precisam ser consultados para que os erros localizem a causa de um problema. No entanto, com as atualizações, também é necessário monitorar problemas de dependência, pois os pacotes antigos podem não ser atualizados corretamente.

A melhor maneira de fazer isso é remover o error.log, removendo todas as mensagens que provavelmente não estão relacionadas ao problema que você está enfrentando. Você pode fazer isso por meio de uma ferramenta como o grep, usando:

```shell
grep -v UnrelatedErrorString
```

Algumas mensagens de erro podem não ser explicativas imediatamente. Nesse caso, observar o contexto em que eles ocorrem também pode ajudar a entender onde o erro foi criado. É possível separar o erro usando:

* `grep -B` para adicionar linhas antes do erro;

ou

* `grep -A` para adicionar linhas após.

Em alguns casos, mensagens de AVISO também podem ser encontradas, pois pode haver casos válidos que levam a esse estado e o aplicativo nem sempre pode decidir se esse é um erro real. Consulte também estas mensagens.

### Contato com o suporte da Adobe {#contacting-adobe-support}

Se você seguiu as instruções desta página e ainda está vendo problemas, entre em contato com o Suporte da Adobe. Para fornecer o máximo possível de informações ao engenheiro de suporte que trabalha no seu caso, inclua o arquivo upgrade.log da sua atualização.
