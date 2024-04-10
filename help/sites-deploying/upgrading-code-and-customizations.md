---
title: Atualização de código e personalizações
description: Saiba mais sobre como atualizar código e personalizações no AEM.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 0%

---

# Atualização de código e personalizações{#upgrading-code-and-customizations}

Ao planejar uma atualização, as seguintes áreas de uma implementação devem ser investigadas e abordadas.

* [Atualizar a base de código](#upgrade-code-base)
* [Alinhar com a estrutura do repositório 6.5](#align-repository-structure)
* [Personalizações do AEM](#aem-customizations)
* [Procedimento de teste](#testing-procedure)

## Visão geral {#overview}

1. **Detector de padrões** - Execute o Detector de padrões conforme descrito no planejamento de atualização e detalhado em [esta página](/help/sites-deploying/pattern-detector.md). Você recebe um relatório de detector de padrão que contém mais detalhes sobre as áreas que devem ser abordadas, além das APIs/pacotes indisponíveis na versão Target do AEM. O relatório Detecção de padrões fornece uma indicação de quaisquer incompatibilidades no código. Se não houver nenhum, sua implantação já será compatível com a versão 6.5. Você ainda pode optar por fazer um novo desenvolvimento para usar a funcionalidade 6.5, mas não é necessário apenas para manter a compatibilidade. Se houver incompatibilidades relatadas, você poderá escolher executar no modo de compatibilidade e adiar o desenvolvimento para obter novos recursos ou compatibilidade com o 6.5. Ou você pode decidir fazer o desenvolvimento após a atualização e ir para a etapa 2. Consulte [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.

1. **Desenvolva a base de código para 6.5 **- Crie uma ramificação ou repositório dedicado para a base de código para a versão do Target. Use as informações da Compatibilidade de pré-atualização para planejar as áreas do código a serem atualizadas.
1. **Compilar com 6.5 Uber jar **- Atualize os POMs de base de código para apontar para 6.5 uber jar e compilar o código com ele.
1. **Atualizar personalizações do AEM*** - *Quaisquer personalizações ou extensões do AEM devem ser atualizadas/validadas para funcionar no 6.5 e adicionadas à base de código do 6.5. Inclui interface de pesquisa do Forms, personalizações de ativos, tudo usando /mnt/overlay

1. **Implantar no ambiente 6.5** - Uma instância limpa do AEM 6.5 (Autor + Publicação) deve ser colocada em um ambiente Dev/QA. A base de código atualizada e uma amostra representativa de conteúdo (da produção atual) devem ser implantadas.
1. **Validação de controle de qualidade e correção de erros** - O controle de qualidade deve validar o aplicativo nas instâncias Autor e Publicar do 6.5. Quaisquer bugs encontrados devem ser corrigidos e confirmados na base de código 6.5. Repita o Dev-Cycle conforme necessário até que todos os bugs sejam corrigidos.

Antes de continuar com uma atualização, você deve ter uma base de código de aplicativo estável que foi testada minuciosamente em relação à versão alvo do AEM. Com base em observações feitas em testes, pode haver maneiras de otimizar o código personalizado. Por exemplo, pode incluir a refatoração do código para evitar o percorrer o repositório, a indexação personalizada para otimizar a pesquisa ou o uso de nós desordenados no JCR, entre outros.

Além de atualizar opcionalmente sua base de código e as personalizações para funcionar com a nova versão do AEM, o 6.5 também ajuda a gerenciar suas personalizações com mais eficiência com o recurso Compatibilidade com versões anteriores, conforme descrito na seção [esta página](/help/sites-deploying/backward-compatibility.md).

Como mencionado acima e mostrado no diagrama abaixo, executar o [Detector de padrões](/help/sites-deploying/pattern-detector.md) a primeira etapa pode ajudá-lo a avaliar a complexidade geral da atualização. Ele também pode ajudá-lo a decidir se você deseja executar no modo de compatibilidade ou atualizar suas personalizações para usar todos os novos recursos do AEM 6.5. Consulte a [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Atualizar a base de código {#upgrade-code-base}

### Criar uma ramificação dedicada para o código 6.5 no controle de versão {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todos os códigos e configurações necessários para a implementação do AEM devem ser gerenciados usando alguma forma de controle de versão. Uma ramificação dedicada no controle de versão deve ser criada para gerenciar todas as alterações necessárias para a base de código na versão de destino do AEM. O teste iterativo da base de código em relação à versão de destino do AEM e correções de bugs subsequentes é gerenciado nessa ramificação.

### Atualizar a versão AEM Uber Jar {#update-the-aem-uber-jar-version}

O jar AEM Uber inclui todas as APIs AEM como uma única dependência no do projeto Maven `pom.xml`. É sempre uma prática recomendada incluir o Uber Jar como uma única dependência em vez de incluir dependências individuais da API do AEM. Ao atualizar a base de código, altere a versão do Uber Jar para apontar para a versão de destino do AEM. Se seu projeto foi desenvolvido em uma versão de AEM antes da existência do Uber Jar, remova todas as dependências individuais da API AEM. Substitua-os por uma única inclusão do Uber Jar para a versão de destino do AEM. Recompile a base de código em relação à nova versão do Uber Jar. Atualize quaisquer APIs ou métodos obsoletos para que sejam compatíveis com a versão de destino do AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Eliminar o uso do Resolvedor de recursos administrativos {#phase-out-use-of-administrative-resource-resolver}

O uso de uma sessão administrativa por meio de `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` O era predominante em bases de código antes do AEM 6.0. Esses métodos foram descontinuados por motivos de segurança, pois fornecem um nível de acesso muito amplo. [Em versões futuras do Sling, esses métodos serão removidos](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). É altamente recomendável refatorar qualquer código para usar os Usuários de serviço. Mais informações sobre Usuários de Serviço e [como eliminar as sessões administrativas pode ser encontrado aqui](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Consultas e índices Oak {#queries-and-oak-indexes}

Qualquer uso de queries na base de código deve ser totalmente testado como parte da atualização da base de código. Para clientes que estão atualizando do Jackrabbit 2 (versões do AEM anteriores à 6.0), esse teste é especialmente importante, pois o Oak não indexa o conteúdo automaticamente e os índices personalizados devem ser criados. Se estiver atualizando de uma versão AEM 6.x, as definições de índice Oak prontas para uso podem ter sido alteradas e podem afetar as consultas existentes.

As seguintes ferramentas estão disponíveis para analisar e inspecionar o desempenho da consulta:

* [Ferramentas de índice do AEM](/help/sites-deploying/queries-and-indexing.md)

* [Ferramentas de Diagnóstico de Operações - Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Criação da interface clássica {#classic-ui-authoring}

A criação da interface clássica ainda está disponível no AEM 6.5, mas está sendo descontinuada. Mais informações podem ser encontradas [aqui](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Se seu aplicativo estiver sendo executado no ambiente de autor da interface clássica, é recomendável atualizar para AEM 6.5 e continuar usando a interface clássica. A migração para a interface para toque pode ser planejada como um projeto separado a ser concluído em vários ciclos de desenvolvimento. Para usar a interface clássica no AEM 6.5, várias configurações de OSGi devem ser enviadas para a base de código. Mais detalhes sobre como fazer a configuração podem ser encontrados [aqui](/help/sites-administering/enable-classic-ui.md).

## Alinhar com a estrutura do repositório 6.5 {#align-repository-structure}

Para facilitar as atualizações e garantir que as configurações não sejam substituídas durante uma atualização, o repositório é reestruturado na versão 6.4 para separar o conteúdo da configuração.

Portanto, várias configurações devem ser movidas para não residirem mais em `/etc` como no passado. Para analisar todo o conjunto de problemas de reestruturação de repositórios que devem ser revisados e acomodados na atualização para o AEM 6.4, consulte [Reestruturação do repositório no AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizações do AEM  {#aem-customizations}

Todas as personalizações no ambiente de criação do AEM na versão de origem do AEM devem ser identificadas. Depois de identificadas, é recomendável que cada personalização seja armazenada no controle de versão ou que seja feito um backup mínimo como parte de um pacote de conteúdo. Todas as personalizações devem ser implantadas e validadas em um ambiente de controle de qualidade ou preparo que execute a versão de destino do AEM antes de uma atualização de produção.

### Sobreposições em geral {#overlays-in-general}

É uma prática comum estender a funcionalidade do AEM imediatamente, sobrepondo nós e/ou arquivos em /libs com nós adicionais em /apps. Essas sobreposições devem ser rastreadas no controle de versão e testadas em relação à versão de destino do AEM. Se um arquivo (como JS, JSP, HTL) estiver sobreposto, a Adobe recomenda que você deixe um comentário sobre qual funcionalidade foi aumentada para facilitar o teste de regressão na versão de destino do AEM. Mais informações sobre sobreposições em geral podem ser encontradas [aqui](/help/sites-developing/overlays.md). As instruções para sobreposições específicas de AEM podem ser encontradas abaixo.

### Atualização do Forms de pesquisa personalizada {#upgrading-custom-search-forms}

Os Aspectos de pesquisa personalizados exigem alguns ajustes manuais após a atualização para funcionarem corretamente. Para obter mais detalhes, consulte [Atualização do Forms de pesquisa personalizada](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizações da interface do usuário do Assets {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimento é necessário apenas para atualizações de versões anteriores ao AEM 6.2.

As instâncias que personalizaram implantações de ativos devem ser preparadas para a atualização. Essa ação é necessária para garantir que todo o conteúdo personalizado seja compatível com a nova estrutura de nó 6.4.

Você pode preparar personalizações para a interface do usuário do Assets fazendo o seguinte:

1. Na instância que está sendo atualizada, abra o CRXDE Lite em *https://server:port/crx/de/index.jsp*

1. Vá para o seguinte nó:

   * `/apps/dam/content`

1. Renomeie o nó de conteúdo para **content_backup** clicando com o botão direito do mouse no painel do explorer no lado esquerdo da janela e escolhendo **Renomear**.

1. Depois que o nó for renomeado, crie um nó chamado conteúdo em `/apps/dam` nomeado **conteúdo** e defina seu tipo de nó como **sling:Folder**.

1. Mover todos os nós filhos de **content_backup** ao nó de conteúdo recém-criado, clicando com o botão direito do mouse em cada nó secundário no painel do explorador e selecionando **Mover**.

1. Exclua o **content_backup** nó.

1. Os nós atualizados abaixo de `/apps/dam` com o tipo de nó correto de `sling:Folder` O ideal é que seja salvo no controle de versão e implantado com a base de código ou, no mínimo, armazenado em backup como um pacote de conteúdo.

### Gerando IDs de ativo para ativos existentes {#generating-asset-ids-for-existing-assets}

Para gerar IDs de ativos para ativos existentes, atualize os ativos ao atualizar a instância do AEM para executar o AEM 6.5. Esta etapa é necessária para habilitar a variável [Recurso do Assets Insights](/help/assets/asset-insights.md). Para obter mais detalhes, consulte [Adicionar código incorporado](/help/assets/use-page-tracker.md#add-embed-code).

Para atualizar ativos, configure o pacote Associar IDs de ativos no console JMX. Dependendo do número de ativos no repositório, `migrateAllAssets` pode levar muito tempo. Os testes internos da Adobe estimam aproximadamente uma hora para 125.000 ativos na TarMK.

![1487758945977](assets/1487758945977.png)

Se você precisar de IDs de ativo para um subconjunto de ativos inteiros, use o `migrateAssetsAtPath` API.

Para todos os outros fins, use o `migrateAllAssets()` API.

### Personalizações do script do InDesign {#indesign-script-customizations}

O Adobe recomenda colocar scripts personalizados em `/apps/settings/dam/indesign/scripts` localização. Mais informações sobre as personalizações do Script do InDesign podem ser encontradas [aqui](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperando configurações do ContextHub {#recovering-contexthub-configurations}

As configurações do ContextHub são afetadas por uma atualização. As instruções sobre como recuperar configurações existentes do ContextHub podem ser encontradas [aqui](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizações do fluxo de trabalho {#workflow-customizations}

É uma prática comum editar workflows prontos para adicionar ou remover funcionalidades desnecessárias. Um fluxo de trabalho comum personalizado é o [!UICONTROL Ativo de atualização DAM] fluxo de trabalho. Todos os workflows necessários para uma implementação personalizada devem ser submetidos a backup e armazenados no controle de versão, pois podem ser substituídos durante uma atualização.

### Modelos editáveis {#editable-templates}

>[!NOTE]
>
>Este procedimento é necessário somente para atualizações de Sites que usam Modelos editáveis do AEM 6.2

A estrutura dos modelos Editáveis foi alterada entre o AEM 6.2 e 6.3. Se você estiver atualizando do 6.2 ou anterior, e se o conteúdo do site for criado usando modelos editáveis, será necessário usar o [Ferramenta de limpeza de nós responsivos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). A ferramenta deve ser executada **após** uma atualização para limpar o conteúdo. Execute-o nos níveis Autor e Publicar.

### Alterações na implementação de CUG {#cug-implementation-changes}

A implementação de Grupos de usuários fechados mudou significativamente para lidar com as limitações de desempenho e escalabilidade em versões anteriores do AEM. A versão anterior do CUG foi descontinuada no 6.3 e a nova implementação é compatível somente com a interface para toque. Se você estiver atualizando do 6.2 ou anterior, as instruções para migrar para a nova implementação CUG podem ser encontradas [aqui](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedimento de teste {#testing-procedure}

Um plano de teste abrangente deve ser preparado para testar as atualizações. O teste da base de código e do aplicativo atualizados deve ser feito primeiro em ambientes inferiores. Quaisquer bugs encontrados devem ser corrigidos de forma iterativa até que a base de código seja estável, somente então os ambientes de nível superior devem ser atualizados.

### Testando o procedimento de atualização {#testing-the-upgrade-procedure}

O procedimento de atualização, conforme descrito aqui, deve ser testado em ambientes de desenvolvimento e controle de qualidade, conforme documentado no seu manual de execução personalizado (consulte [Planejando sua atualização](/help/sites-deploying/upgrade-planning.md)). O procedimento de atualização deve ser repetido até que todas as etapas sejam documentadas no livro de execução de atualização e o processo de atualização seja tranquilo.

### Áreas de teste de implementação  {#implementation-test-areas-}

Abaixo estão áreas críticas de qualquer implementação de AEM que devem ser cobertas pelo seu plano de teste depois que o ambiente for atualizado e a base de código atualizada for implantada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de teste funcional</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Sites publicados</td>
   <td>Teste da implementação do AEM e do código associado no nível de publicação<br /> por meio do Dispatcher. Deve incluir critérios para atualizações de página e<br /> invalidação de cache.</td>
  </tr>
  <tr>
   <td>Criação  </td>
   <td>Teste da implementação do AEM e do código associado no nível do Autor. Deve incluir página, criação de componentes e caixas de diálogo.</td>
  </tr>
  <tr>
   <td>Integrações com as soluções Experience Cloud</td>
   <td>Validação de integrações com produtos como Analytics, DTM e Target.</td>
  </tr>
  <tr>
   <td>Integrações com sistemas de terceiros</td>
   <td>Valide todas as integrações de terceiros nos níveis do Autor e de Publicação.</td>
  </tr>
  <tr>
   <td>Autenticação, segurança e permissões</td>
   <td>Todos os mecanismos de autenticação, como LDAP/SAML, devem ser validados.<br /> As permissões e os grupos devem ser testados em Autor e Publicação<br /> níveis.</td>
  </tr>
  <tr>
   <td>Consultas</td>
   <td>Índices e consultas personalizados devem ser testados junto com o desempenho da consulta.</td>
  </tr>
  <tr>
   <td>Personalizações da interface do usuário</td>
   <td>Quaisquer extensões ou personalizações da interface do usuário do AEM no ambiente de criação.</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td>Fluxos de trabalho e funcionalidade personalizados e/ou prontos para uso.</td>
  </tr>
  <tr>
   <td>Teste de desempenho</td>
   <td>O teste de carga deve ser executado nos níveis de Autor e Publicação que simulam cenários do mundo real.</td>
  </tr>
 </tbody>
</table>

### Documentar o plano de teste e os resultados {#document-test-plan-and-results}

Deve ser criado um plano de teste que abranja as áreas de teste de implementação acima. Geralmente, faz sentido separar o plano de teste por Listas de tarefas Autor e Publicar. Esse plano de teste deve ser executado em ambientes de Desenvolvimento, Controle de qualidade e Preparo antes da atualização dos ambientes de Produção. Os resultados dos testes e as métricas de desempenho devem ser capturados em ambientes inferiores para fornecer comparação ao atualizar ambientes de Preparo e Produção.
