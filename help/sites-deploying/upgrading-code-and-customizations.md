---
title: Atualização de código e personalizações
seo-title: Atualização de código e personalizações
description: Saiba mais sobre como atualizar o código personalizado no AEM.
seo-description: Saiba mais sobre como atualizar o código personalizado no AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '2204'
ht-degree: 0%

---


# Atualização de código e personalizações{#upgrading-code-and-customizations}

Ao planejar uma atualização, as seguintes áreas de uma implementação precisam ser investigadas e tratadas.

* [Atualizar a base de código](#upgrade-code-base)
* [Alinhar com a estrutura do repositório 6.5](#align-repository-structure)
* [Personalizações AEM](#aem-customizations)
* [Procedimento de teste](#testing-procedure)

## Visão geral {#overview}

1. **Detector**  de padrões - execute o Detector de padrões conforme descrito no planejamento de atualização e descrito detalhadamente  [nesta ](/help/sites-deploying/pattern-detector.md) página para obter um relatório do detector de padrões que contenha mais detalhes sobre áreas que precisam ser abordadas além das APIs/pacotes indisponíveis na versão de Público alvo do AEM. O relatório de Detecção de padrão deve fornecer uma indicação de quaisquer incompatibilidades no código. Se não houver nenhuma, sua implantação já será compatível com a versão 6.5, você ainda poderá optar por fazer um novo desenvolvimento para utilizar a funcionalidade 6.5, mas não precisará apenas para manter a compatibilidade. Se houver incompatibilidades reportadas, você poderá optar por a) Executar no modo de compatibilidade e adiar seu desenvolvimento para novos recursos 6.5 ou compatibilidade, b) Decidir fazer o desenvolvimento após a atualização e passar para a etapa 2. Consulte [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.

1. **Desenvolver base de código para 6.5 **- Criar uma ramificação ou repositório dedicado para a base de código para a versão do Público alvo. Use as informações da Compatibilidade de pré-atualização para planejar áreas de código a serem atualizadas.
1. **Compile com o pom de 6.5 Uber **- Atualize os POMs de base de código para apontar para o pod de 6.5 uber e compile o código em relação a isso.
1. **Atualização AEM personalizações*** - *Qualquer personalização ou extensão para AEM deve ser atualizada/validada para funcionar na versão 6.5 e adicionada à base de código 6.5. Inclui o UI Search Forms, Personalizações de ativos, qualquer coisa que use /mnt/overlay

1. **Implantação para o Ambiente**  6.5 - Uma instância limpa do AEM 6.5 (Autor + Publicação) deve estar em pé em um ambiente Dev/QA. A base de código atualizada e uma amostra representativa de conteúdo (da produção atual) devem ser implantadas.
1. **Validação do controle de qualidade e correção**  de erros - O controle de qualidade deve validar o aplicativo nas instâncias de Autor e Publicação da versão 6.5. Quaisquer erros encontrados devem ser corrigidos e confirmados para a base de códigos 6.5. Repita Dev-Cycle conforme necessário até que todos os erros sejam corrigidos.

Antes de continuar com uma atualização, você deve ter uma base de código de aplicativo estável que tenha sido testada completamente em relação à versão de público alvo do AEM. Com base em observações feitas em testes, pode haver maneiras de otimizar o código personalizado. Isso pode incluir a refatoração do código para evitar atravessar o repositório, a indexação personalizada para otimizar a pesquisa ou o uso de nós não ordenados no JCR, entre outros.

Além da opção de atualizar sua base de código e personalizações para trabalhar com a nova versão AEM, o 6.5 também ajuda a gerenciar suas personalizações com mais eficiência com o recurso Compatibilidade com versões anteriores, conforme descrito em [esta página](/help/sites-deploying/backward-compatibility.md).

Conforme mencionado acima e mostrado no diagrama abaixo, executar o [Detector de padrões](/help/sites-deploying/pattern-detector.md) na primeira etapa ajudará você a avaliar a complexidade geral da atualização e se deseja executar no modo de compatibilidade ou atualizar suas personalizações para usar todos os novos recursos do AEM 6.5. Consulte a página [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter mais detalhes.
[ ![opt_croped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Atualizar a Base de código {#upgrade-code-base}

### Criar uma ramificação dedicada para o código 6.5 no controle de versão {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todos os códigos e configurações necessários para sua implementação de AEM devem ser gerenciados usando alguma forma de controle de versão. Uma ramificação dedicada no controle de versão deve ser criada para gerenciar todas as alterações necessárias para a base de código na versão de público alvo do AEM. O teste iterativo da base de código em relação à versão de público alvo do AEM e as subsequentes correções de erros serão gerenciados nesta ramificação.

### Atualize a versão AEM Uber Jar {#update-the-aem-uber-jar-version}

O AEM Uber jar inclui todas as APIs AEM como uma única dependência no `pom.xml` do projeto Maven. É sempre uma prática recomendada incluir o Uber Jar como uma única dependência em vez de incluir dependências individuais AEM API. Ao atualizar a base de código, a versão do Uber Jar deve ser alterada para apontar para a versão de público alvo do AEM. Se o seu projeto foi desenvolvido em uma versão do AEM anterior à existência do Uber Jar, todas as dependências individuais AEM API devem ser removidas e substituídas por uma única inclusão do Uber Jar para a versão do público alvo do AEM. A base de código deve então ser recompilada em relação à nova versão do Uber Jar. Quaisquer APIs ou métodos obsoletos devem ser atualizados para serem compatíveis com a versão de público alvo do AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Uso gradual do Resolvedor de Recursos Administrativos {#phase-out-use-of-administrative-resource-resolver}

O uso de uma sessão administrativa por meio de `SlingRepository.loginAdministrative()` e `ResourceResolverFactory.getAdministrativeResourceResolver()` era bastante predominante em bases de código antes do AEM 6.0. Esses métodos foram descontinuados por motivos de segurança, pois proporcionam um nível de acesso muito amplo. [Em versões futuras do Sling, esses métodos serão removidos](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). É altamente recomendável refatorar qualquer código para usar Usuários do serviço. Mais informações sobre os Usuários do serviço e [como eliminar sessões administrativas podem ser encontradas aqui](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Query e índices Oak {#queries-and-oak-indexes}

Qualquer uso de query na base de códigos deve ser testado minuciosamente como parte da atualização da base de códigos. Para clientes que atualizam do Jackrabbit 2 (versões de AEM anteriores à 6.0), isso é especialmente importante, pois o Oak não indexa o conteúdo automaticamente e talvez seja necessário criar índices personalizados. Se você estiver atualizando de uma versão AEM 6.x, as definições de índice Oak podem ter sido alteradas e podem afetar query existentes.

Várias ferramentas para analisar e inspecionar o desempenho do query estão disponíveis:

* [Ferramentas de índice AEM](/help/sites-deploying/queries-and-indexing.md)

* [Ferramentas de Diagnóstico de Operações - Desempenho do Query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Oak Utils](https://oakutils.appspot.com/). Esta é uma ferramenta de código aberto que não é mantida pelo Adobe.

### Criação da interface clássica {#classic-ui-authoring}

A criação da interface de usuário clássica ainda está disponível no AEM 6.5, mas está sendo descontinuada. Mais informações podem ser encontradas [aqui](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Se seu aplicativo estiver sendo executado no momento no ambiente do autor da interface clássica, é recomendável atualizar para o AEM 6.5 e continuar usando a interface clássica. A migração para a interface de usuário de toque pode ser planejada como um projeto separado a ser concluído em vários ciclos de desenvolvimento. Para usar a interface clássica no AEM 6.5, várias configurações OSGi precisam ser confirmadas na base de código. Mais detalhes sobre como configurar isso podem ser encontrados [aqui](/help/sites-administering/enable-classic-ui.md).

## Alinhar com a estrutura do repositório 6.5 {#align-repository-structure}

Para facilitar as atualizações e garantir que as configurações não sejam substituídas durante uma atualização, o repositório é reestruturado na versão 6.4 para separar o conteúdo da configuração.

Portanto, várias configurações devem ser movidas para que não residam mais em `/etc`, como acontecia no passado. Para analisar o conjunto completo de preocupações de reestruturação do repositório que devem ser analisadas e acomodadas na atualização para AEM 6.4, consulte [Reestruturação do repositório no AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizações AEM {#aem-customizations}

Todas as personalizações do ambiente de criação AEM na versão de origem do AEM precisam ser identificadas. Depois de identificada, é recomendável que cada personalização seja armazenada no controle de versão ou no mínimo seja copiada como parte de um pacote de conteúdo. Todas as personalizações devem ser implantadas e validadas em um QA ou ambiente de armazenamento temporário executando a versão do público alvo do AEM antes da atualização da produção.

### Sobreposições em geral {#overlays-in-general}

É uma prática comum estender a funcionalidade AEM fora da caixa sobrepondo nós e/ou arquivos em /libs com nós adicionais em /apps. Essas sobreposições devem ser rastreadas no controle de versão e testadas em relação à versão de público alvo do AEM. Se um arquivo (JS, JSP, HTL) estiver sobreposto, é recomendável deixar um comentário sobre qual funcionalidade foi aumentada para um teste de regressão mais fácil na versão de público alvo do AEM. Mais informações sobre sobreposições em geral podem ser encontradas [aqui](/help/sites-developing/overlays.md). As instruções para sobreposições de AEM específicas podem ser encontradas abaixo.

### Atualizando Forms de Pesquisa Personalizada {#upgrading-custom-search-forms}

Os Aspectos de pesquisa personalizados exigem alguns ajustes manuais após a atualização para funcionarem corretamente. Para obter mais detalhes, consulte [Atualizando Forms](/help/sites-deploying/upgrading-custom-search-forms.md) de Pesquisa Personalizada.

### Personalizações da interface do usuário do Assets {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimento é necessário apenas para atualizações de versões anteriores à AEM 6.2.

As instâncias que possuem implantações personalizadas de Ativos precisam estar preparadas para a atualização. Isso é necessário para garantir que todo o conteúdo personalizado seja compatível com a nova estrutura de nós 6.4.

Você pode preparar personalizações para a interface do usuário do Assets executando o seguinte procedimento:

1. Na instância que precisa ser atualizada, abra o CRXDE Lite indo para *https://server:port/crx/de/index.jsp*

1. Vá para o seguinte nó:

   * `/apps/dam/content`

1. Renomeie o nó de conteúdo para **content_backup**. Você pode fazer isso clicando com o botão direito do mouse no painel do explorador no lado esquerdo da janela e escolhendo **Renomear**.

1. Depois que o nó tiver sido renomeado, crie um novo nó chamado conteúdo em `/apps/dam` chamado **content** e defina seu tipo de nó como **sling:Folder**.

1. Mova todos os nós filhos de **content_backup** para o nó de conteúdo recém-criado. Você pode fazer isso clicando com o botão direito do mouse em cada nó filho no painel explorador e selecionando **Mover**.

1. Exclua o nó **content_backup**.

1. Os nós atualizados abaixo de `/apps/dam` com o tipo de nó correto de `sling:Folder` devem ser salvos no controle de versão e implantados com a base de código ou em um backup mínimo como pacote de conteúdo.

### Geração de IDs de ativos para ativos existentes {#generating-asset-ids-for-existing-assets}

Para gerar IDs de ativos para ativos existentes, atualize os ativos ao atualizar sua instância de AEM para executar AEM 6.5. Isso é necessário para ativar o recurso [Insights do Assets](/help/assets/asset-insights.md). Para obter mais detalhes, consulte [Adicionar código incorporado](/help/assets/use-page-tracker.md#add-embed-code).

Para atualizar ativos, configure o pacote Associate Asset IDs no console JMX. Dependendo do número de ativos no repositório, `migrateAllAssets` pode levar muito tempo. Nossos testes internos estimam aproximadamente uma hora para 125 mil ativos no TarMK.

![1487758945977](assets/1487758945977.png)

Se você precisar de IDs de ativos para um subconjunto de todos os ativos, use a API `migrateAssetsAtPath`.

Para todos os outros fins, use a API `migrateAllAssets()`.

### Personalizações de script de InDesign {#indesign-script-customizations}

O Adobe recomenda colocar scripts personalizados no local `/apps/settings/dam/indesign/scripts`. Mais informações sobre personalizações de scripts de InDesign podem ser encontradas [aqui](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperando configurações do ContextHub {#recovering-contexthub-configurations}

As configurações do ContextHub são afetadas por uma atualização. As instruções sobre como recuperar as configurações existentes do ContextHub podem ser encontradas [aqui](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizações de Fluxo de Trabalho {#workflow-customizations}

É uma prática comum atualizar a modificação dos workflows prontos para uso para adicionar ou remover a funcionalidade desnecessária. Um fluxo de trabalho comum personalizado é o [!UICONTROL Ativo de atualização do DAM] fluxo de trabalho. Todos os workflows necessários para uma implementação personalizada devem ter backup e ser armazenados no controle de versão, pois podem ser substituídos durante uma atualização.

### Modelos editáveis {#editable-templates}

>[!NOTE]
>
>Este procedimento é necessário somente para atualizações de Sites usando Modelos editáveis do AEM 6.2

A estrutura para modelos editáveis foi alterada entre AEM 6.2 e 6.3. Se você estiver atualizando da versão 6.2 ou anterior e se o conteúdo do site for criado usando modelos editáveis, precisará usar a [Ferramenta de limpeza de nós responsivos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). A ferramenta deve executar **depois de** uma atualização para limpar o conteúdo. Ele precisará ser executado nos níveis Autor e Publicar.

### Alterações de implementação de CUG {#cug-implementation-changes}

A implementação de Grupos de usuários fechados mudou significativamente para atender às limitações de desempenho e escalabilidade em versões anteriores do AEM. A versão anterior do CUG foi descontinuada na versão 6.3 e a nova implementação só é suportada na interface do usuário de toque. Se você estiver atualizando de 6.2 ou anterior, as Instruções para migrar para a nova implementação do CUG podem ser encontradas [aqui](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedimento de teste {#testing-procedure}

Deve ser preparado um plano de teste abrangente para testar atualizações. O teste da base de código atualizada e o aplicativo precisarão ser feitos em ambientes menores primeiro. Quaisquer erros encontrados devem ser corrigidos de forma iterativa até que a base de código seja estável, somente então os ambientes de nível mais alto devem ser atualizados.

### Teste do procedimento de atualização {#testing-the-upgrade-procedure}

O procedimento de atualização como descrito aqui deve ser testado em ambientes Dev e QA, conforme documentado em seu manual de execução personalizado (consulte [Planejamento da atualização](/help/sites-deploying/upgrade-planning.md)). O procedimento de atualização deve ser repetido até que todas as etapas sejam documentadas no manual de execução da atualização e o processo de atualização seja suave.

### Áreas de teste de implementação {#implementation-test-areas-}

Abaixo estão áreas críticas de qualquer implementação AEM que deve ser coberta pelo seu plano de teste depois que o ambiente for atualizado e a base de código atualizada tiver sido implantada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de teste funcional</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Sites publicados</td>
   <td>Testando a implementação AEM e o código associado na camada de publicação<br /> por meio do despachante. Deve incluir critérios para atualizações de página e para a invalidação de cache<br />.</td>
  </tr>
  <tr>
   <td>Criação  </td>
   <td>Testando a implementação AEM e o código associado na camada Autor. Deve incluir páginas, criação de componentes e caixas de diálogo.</td>
  </tr>
  <tr>
   <td>Integrações com soluções de Marketing Cloud</td>
   <td>Validação de integrações com produtos como Analytics, DTM e Público alvo.</td>
  </tr>
  <tr>
   <td>Integrações com sistemas de terceiros</td>
   <td>Todas as integrações de terceiros devem ser validadas nos níveis de Autor e Publicação.</td>
  </tr>
  <tr>
   <td>Autenticação, segurança e permissões</td>
   <td>Quaisquer mecanismos de autenticação como LDAP/SAML devem ser validados.<br /> As permissões e os grupos devem ser testados tanto no Autor quanto no <br /> Editor.</td>
  </tr>
  <tr>
   <td>Query</td>
   <td>Os índices e query personalizados devem ser testados juntamente com o desempenho do query.</td>
  </tr>
  <tr>
   <td>Personalizações da interface</td>
   <td>Quaisquer extensões ou personalizações à interface do usuário AEM no ambiente do autor.</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td>Workflows e funcionalidade personalizados e/ou prontos para uso.</td>
  </tr>
  <tr>
   <td>Teste de desempenho</td>
   <td>O teste de carga deve ser executado em níveis de Autor e Publicação que simulam cenários reais.</td>
  </tr>
 </tbody>
</table>

### Plano de teste e resultados do documento {#document-test-plan-and-results}

Deve ser criado um plano de ensaio que abranja as áreas de ensaio de implementação acima referidas. Em muitos casos, fará sentido separar o plano de teste por listas de Autor e Publicação de tarefa. Este plano de teste deve ser executado em ambientes de desenvolvimento, controle de qualidade e estágio antes da atualização dos ambientes de produção. Os resultados do teste e as métricas de desempenho devem ser capturados em ambientes menores para fornecer comparação ao atualizar ambientes de estágio e de produção.
