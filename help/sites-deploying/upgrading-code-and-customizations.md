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
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 0%

---

# Atualização de código e personalizações{#upgrading-code-and-customizations}

Ao planejar uma atualização, as seguintes áreas de uma implementação devem ser investigadas e abordadas.

* [Atualizar a base de código](#upgrade-code-base)
* [Alinhar com a estrutura do repositório 6.5](#align-repository-structure)
* [Personalizações do AEM](#aem-customizations)
* [Procedimento de teste](#testing-procedure)

## Visão geral {#overview}

1. **Detector de Padrões** - Execute o Detector de Padrões conforme descrito no planejamento de atualização e detalhado na página [Avaliação da Complexidade de Atualização com o Detector de Padrões](/help/sites-deploying/pattern-detector.md). Você recebe um relatório de detector de padrão que contém mais detalhes sobre as áreas que devem ser abordadas, além das APIs/pacotes indisponíveis na versão Target do AEM. O relatório Detecção de padrões fornece uma indicação de quaisquer incompatibilidades no código. Se não houver nenhum, sua implantação já será compatível com a versão 6.5. Você ainda pode optar por fazer um novo desenvolvimento para usar a funcionalidade 6.5, mas não é necessário apenas para manter a compatibilidade. Se houver incompatibilidades relatadas, você poderá escolher executar no modo de compatibilidade e adiar o desenvolvimento para obter novos recursos ou compatibilidade com o 6.5. Ou você pode decidir fazer o desenvolvimento após a atualização e ir para a etapa 2. Consulte [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.

1. **Desenvolva a base de código para 6.5 &#x200B;**- Crie uma ramificação ou repositório dedicado para a base de código para a versão do Target. Use as informações da Compatibilidade de pré-atualização para planejar as áreas do código a serem atualizadas.
1. **Compilar com 6.5 Uber jar &#x200B;**- Atualize os POMs de base de código para apontar para 6.5 uber jar e compilar o código com ele.
1. **Atualizar personalizações do AEM*** - *Todas as personalizações ou extensões do AEM devem ser atualizadas/validadas para funcionar no 6.5 e adicionadas à base de código do 6.5. Inclui UI Search Forms, Personalizações do Assets, tudo usando /mnt/overlay

1. **Implantar no 6.5 Ambiente** - Uma instância limpa do AEM 6.5 (Autor + Publish) deve ser colocada em um ambiente Dev/QA. A base de código atualizada e uma amostra representativa de conteúdo (da produção atual) devem ser implantadas.
1. **Validação de controle de qualidade e correção de erros** - o controle de qualidade deve validar o aplicativo nas instâncias do Autor e do Publish do 6.5. Quaisquer bugs encontrados devem ser corrigidos e confirmados na base de código 6.5. Repita o Dev-Cycle conforme necessário até que todos os bugs sejam corrigidos.

Antes de continuar com uma atualização, você deve ter uma base de código de aplicativo estável que foi testada minuciosamente em relação à versão alvo do AEM. Com base em observações feitas em testes, pode haver maneiras de otimizar o código personalizado. Por exemplo, pode incluir a refatoração do código para evitar o percorrer o repositório, a indexação personalizada para otimizar a pesquisa ou o uso de nós desordenados no JCR, entre outros.

Além de atualizar opcionalmente sua base de código e as personalizações para funcionar com a nova versão do AEM, o 6.5 também ajuda a gerenciar suas personalizações com mais eficiência com o recurso Compatibilidade com versões anteriores, conforme descrito em [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md).

Conforme mencionado acima e mostrado no diagrama abaixo, executar o [Detector de padrões](/help/sites-deploying/pattern-detector.md) na primeira etapa pode ajudar a avaliar a complexidade geral da atualização. Ele também pode ajudá-lo a decidir se você deseja executar no modo de compatibilidade ou atualizar suas personalizações para usar todos os novos recursos do AEM 6.5. Consulte a página [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.
[![opção_cortada](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Atualizar a base de código {#upgrade-code-base}

### Criar uma Ramificação Dedicada para o Código 6.5 no Controle de Versão {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todos os códigos e configurações necessários para a implementação do AEM devem ser gerenciados usando alguma forma de controle de versão. Uma ramificação dedicada no controle de versão deve ser criada para gerenciar todas as alterações necessárias para a base de código na versão de destino do AEM. O teste iterativo da base de código em relação à versão de destino do AEM e correções de bugs subsequentes é gerenciado nessa ramificação.

### Atualizar a versão AEM Uber Jar {#update-the-aem-uber-jar-version}

O jar AEM Uber inclui todas as APIs AEM como uma única dependência no `pom.xml` do seu projeto Maven. É sempre uma prática recomendada incluir o Uber Jar como uma única dependência em vez de incluir dependências individuais da API do AEM. Ao atualizar a base de código, altere a versão do Uber Jar para apontar para a versão de destino do AEM. Se seu projeto foi desenvolvido em uma versão de AEM antes da existência do Uber Jar, remova todas as dependências individuais da API AEM. Substitua-os por uma única inclusão do Uber Jar para a versão de destino do AEM. Recompile a base de código em relação à nova versão do Uber Jar. Atualize quaisquer APIs ou métodos obsoletos para que sejam compatíveis com a versão de destino do AEM.

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

O uso de uma sessão administrativa através de `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` foi predominante em bases de código antes do AEM 6.0. Esses métodos foram descontinuados por motivos de segurança, pois fornecem um nível de acesso muito amplo. [Em versões futuras do Sling, esses métodos serão removidos](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). É altamente recomendável refatorar qualquer código para usar os Usuários de serviço. Para obter informações sobre Usuários de Serviço e como encerrar as sessões administrativas, consulte [Usuários de Serviço no Adobe Experience Manager (AEM)](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Consultas e índices Oak {#queries-and-oak-indexes}

Qualquer uso de queries na base de código deve ser totalmente testado como parte da atualização da base de código. Para clientes que estão atualizando do Jackrabbit 2 (versões do AEM anteriores à 6.0), esse teste é especialmente importante, pois o Oak não indexa o conteúdo automaticamente e os índices personalizados devem ser criados. Se estiver atualizando de uma versão AEM 6.x, as definições de índice Oak prontas para uso podem ter sido alteradas e podem afetar as consultas existentes.

As seguintes ferramentas estão disponíveis para analisar e inspecionar o desempenho da consulta:

* [Ferramentas de índice do AEM](/help/sites-deploying/queries-and-indexing.md)

* [Ferramentas de Diagnóstico de Operações - Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Criação da interface clássica {#classic-ui-authoring}

A criação da interface clássica ainda está disponível no AEM 6.5, mas está sendo descontinuada. Consulte [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release) para obter mais informações. Se seu aplicativo estiver sendo executado no ambiente de autor da interface clássica, é recomendável atualizar para AEM 6.5 e continuar usando a interface clássica. A migração para a interface para toque pode ser planejada como um projeto separado a ser concluído em vários ciclos de desenvolvimento. Para usar a interface clássica no AEM 6.5, várias configurações de OSGi devem ser enviadas para a base de código. Mais detalhes sobre como fazer a configuração podem ser encontrados em [Habilitando o Acesso à Interface Clássica](/help/sites-administering/enable-classic-ui.md).

## Alinhar com a estrutura do repositório 6.5 {#align-repository-structure}

Para facilitar as atualizações e garantir que as configurações não sejam substituídas durante uma atualização, o repositório é reestruturado na versão 6.4 para separar o conteúdo da configuração.

Portanto, várias configurações devem ser movidas para não residirem mais em `/etc`, como acontecia no passado. Para analisar o conjunto completo de problemas de reestruturação de repositório que devem ser revisados e acomodados no AEM 6.4 atualizado, consulte [Reestruturação de repositório no AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizações do AEM  {#aem-customizations}

Todas as personalizações no ambiente de criação do AEM na versão de origem do AEM devem ser identificadas. Depois de identificadas, é recomendável que cada personalização seja armazenada no controle de versão ou que seja feito um backup mínimo como parte de um pacote de conteúdo. Todas as personalizações devem ser implantadas e validadas em um ambiente de controle de qualidade ou preparo que execute a versão de destino do AEM antes de uma atualização de produção.

### Sobreposições em geral {#overlays-in-general}

É uma prática comum estender a funcionalidade do AEM imediatamente, sobrepondo nós e/ou arquivos em /libs com nós adicionais em /apps. Essas sobreposições devem ser rastreadas no controle de versão e testadas em relação à versão de destino do AEM. Se um arquivo (como JS, JSP, HTL) estiver sobreposto, a Adobe recomenda que você deixe um comentário sobre qual funcionalidade foi aumentada para facilitar o teste de regressão na versão de destino do AEM. Consulte [Sobreposições](/help/sites-developing/overlays.md) para obter informações genéricas. As instruções para sobreposições específicas de AEM podem ser encontradas abaixo.

### Atualização do Forms de pesquisa personalizada {#upgrading-custom-search-forms}

Os Aspectos de pesquisa personalizados exigem alguns ajustes manuais após a atualização para funcionarem corretamente. Para obter mais detalhes, consulte [Atualizando Forms de Pesquisa Personalizada](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizações da interface do usuário do Assets {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimento é necessário apenas para atualizações de versões anteriores ao AEM 6.2.

As instâncias que personalizaram implantações do Assets devem ser preparadas para a atualização. Essa ação é necessária para garantir que todo o conteúdo personalizado seja compatível com a nova estrutura de nó 6.4.

Você pode preparar personalizações para a interface do usuário do Assets fazendo o seguinte:

1. Na instância que está sendo atualizada, abra o CRXDE Lite em *https://server:port/crx/de/index.jsp*

1. Vá para o seguinte nó:

   * `/apps/dam/content`

1. Renomeie o nó de conteúdo como **content_backup** clicando com o botão direito do mouse no painel do explorador no lado esquerdo da janela e escolhendo **Renomear**.

1. Depois que o nó for renomeado, crie um nó chamado conteúdo em `/apps/dam` chamado **conteúdo** e defina seu tipo de nó como **sling:Folder**.

1. Mova todos os nós filhos de **content_backup** para o nó de conteúdo recém-criado clicando com o botão direito do mouse em cada nó filho no painel do explorador e selecionando **Mover**.

1. Exclua o nó **content_backup**.

1. Idealmente, os nós atualizados abaixo de `/apps/dam` com o tipo de nó correto de `sling:Folder` devem ser salvos no controle de versão e implantados com a base de código ou, no mínimo, ser incluídos no backup como um pacote de conteúdo.

### Gerar IDs de ativos para Assets existentes {#generating-asset-ids-for-existing-assets}

Para gerar IDs de ativos para ativos existentes, atualize os ativos ao atualizar a instância do AEM para executar o AEM 6.5. Esta etapa é necessária para habilitar o [recurso do Assets Insights](/help/assets/asset-insights.md). Para obter mais detalhes, consulte [Adicionar código incorporado](/help/assets/use-page-tracker.md#add-embed-code).

Para atualizar ativos, configure o pacote Associar IDs de ativos no console JMX. Dependendo do número de ativos no repositório, `migrateAllAssets` pode demorar. Os testes internos da Adobe estimam aproximadamente uma hora para 125.000 ativos na TarMK.

![1487758945977](assets/1487758945977.png)

Se você precisar de IDs de ativos para um subconjunto de todos os seus ativos, use a API `migrateAssetsAtPath`.

Para todos os outros fins, use a API `migrateAllAssets()`.

### Personalizações do script do InDesign {#indesign-script-customizations}

A Adobe recomenda colocar scripts personalizados no local `/apps/settings/dam/indesign/scripts`. Mais informações sobre as personalizações do Script do InDesign podem ser encontradas em [Integrar o Adobe Experience Manager Assets com o Adobe InDesign Server](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperando configurações do ContextHub {#recovering-contexthub-configurations}

As configurações do ContextHub são afetadas por uma atualização. Consulte [Configurando o ContextHub](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading) para obter instruções sobre como recuperar configurações existentes do ContextHub.

### Personalizações do fluxo de trabalho {#workflow-customizations}

É uma prática comum editar workflows prontos para adicionar ou remover funcionalidades desnecessárias. Um fluxo de trabalho comum personalizado é o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM]. Todos os workflows necessários para uma implementação personalizada devem ser submetidos a backup e armazenados no controle de versão, pois podem ser substituídos durante uma atualização.

### Modelos editáveis {#editable-templates}

>[!NOTE]
>
>Este procedimento é necessário somente para atualizações de Sites que usam Modelos editáveis do AEM 6.2

A estrutura dos modelos Editáveis foi alterada entre o AEM 6.2 e 6.3. Se você estiver atualizando a partir da versão 6.2 ou anterior, e se o conteúdo do site for criado com modelos editáveis, você deverá usar a [Ferramenta de Limpeza de Nós Responsivos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). A ferramenta deve executar **após** uma atualização para limpar o conteúdo. Execute-o nos níveis do Author e do Publish.

### Alterações na implementação de CUG {#cug-implementation-changes}

A implementação de Grupos de usuários fechados mudou significativamente para lidar com as limitações de desempenho e escalabilidade em versões anteriores do AEM. A versão anterior do CUG foi descontinuada no 6.3 e a nova implementação é compatível somente com a interface para toque.

## Procedimento de teste {#testing-procedure}

Um plano de teste abrangente deve ser preparado para testar as atualizações. O teste da base de código e do aplicativo atualizados deve ser feito primeiro em ambientes inferiores. Quaisquer bugs encontrados devem ser corrigidos de forma iterativa até que a base de código seja estável, somente então os ambientes de nível superior devem ser atualizados.

### Testando o procedimento de atualização {#testing-the-upgrade-procedure}

O procedimento de atualização descrito aqui deve ser testado em ambientes de Desenvolvimento e Controle de Qualidade, conforme documentado no seu manual de execução personalizado (consulte [Planejando sua atualização](/help/sites-deploying/upgrade-planning.md)). O procedimento de atualização deve ser repetido até que todas as etapas sejam documentadas no livro de execução de atualização e o processo de atualização seja tranquilo.

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
   <td>Testando a implementação do AEM e o código associado no nível de publicação<br /> por meio da Dispatcher. Deve incluir critérios para atualizações de página e invalidação de cache <br />.</td>
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
   <td>Valide todas as integrações de terceiros nos níveis do Author e do Publish.</td>
  </tr>
  <tr>
   <td>Autenticação, segurança e permissões</td>
   <td>Todos os mecanismos de autenticação, como LDAP/SAML, devem ser validados.<br /> As permissões e os grupos devem ser testados nos níveis do Autor e do Publish<br />.</td>
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
   <td>O teste de carga deve ser executado nos níveis do Autor e do Publish que simulam cenários reais.</td>
  </tr>
 </tbody>
</table>

### Documentar o plano de teste e os resultados {#document-test-plan-and-results}

Deve ser criado um plano de teste que abranja as áreas de teste de implementação acima. Muitas vezes, faz sentido separar o plano de teste por Autor e listas de tarefas do Publish. Esse plano de teste deve ser executado em ambientes de Desenvolvimento, Controle de qualidade e Preparo antes da atualização dos ambientes de Produção. Os resultados dos testes e as métricas de desempenho devem ser capturados em ambientes inferiores para fornecer comparação ao atualizar ambientes de Preparo e Produção.
