---
title: Planejando sua atualização
description: Este artigo ajuda a estabelecer metas, fases e resultados claros ao planejar a atualização do AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 0dea2b3e-fd7c-4811-a04a-6852ffc1e6d6
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '2399'
ht-degree: 0%

---

# Planejando sua atualização{#planning-your-upgrade}

## Visão geral do projeto AEM {#aem-project-overview}

O AEM é frequentemente usado em implantações de alto impacto que podem atender a milhões de usuários. Normalmente, há aplicativos personalizados implantados nas instâncias, o que aumenta a complexidade. Qualquer esforço para atualizar essa implantação precisa ser tratado metodicamente.

Este guia ajuda a estabelecer metas, fases e resultados claros ao planejar sua atualização. Concentra-se na execução e nas diretrizes gerais do projeto. Embora forneça uma visão geral das etapas de atualização reais, ele se refere aos recursos técnicos disponíveis, quando apropriado. Deve ser utilizado com os recursos técnicos disponíveis referidos no documento.

O processo de atualização do AEM precisa ser cuidadosamente tratado nas fases de planejamento, análise e execução, com os principais resultados definidos para cada fase.

É possível atualizar diretamente do AEM versões 6.0 e até 6.5. Os clientes que executam a versão 5.6.x ou inferior precisam primeiro atualizar para a versão 6.0 ou superior, com a recomendação do 6.0(SP3). Além disso, o novo formato Oak Segment Tar é usado agora para o Segment Node Store desde a versão 6.3, e a migração do repositório para esse novo formato é obrigatória mesmo para as versões 6.0, 6.1 e 6.2.

>[!CAUTION]
>
>Se você estiver atualizando do AEM 6.2 para o 6.3, é necessário atualizar das versões (**6.2-SP1-CFP1 - -6.2SP1-CFP12.1** ou **6.2SP1-CFP15** a partir de. Caso contrário, se você estiver atualizando do **6.2SP1-CFP13/6.2SP1CFP14** para AEM 6.3, você também deve atualizar para pelo menos a versão **6.3.2.2**. Caso contrário, o AEM Sites falhará após a atualização.

## Escopo e requisitos de atualização {#upgrade-scope-requirements}

Abaixo você encontrará uma lista de áreas afetadas em um projeto típico de atualização do AEM:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Impacto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Sistema Operacional</td>
   <td>Efeitos incertos, mas sutis</td>
   <td>No momento da atualização do AEM, pode ser a hora de atualizar também o sistema operacional e isso pode ter algum impacto.</td>
  </tr>
  <tr>
   <td>Java™ Runtime</td>
   <td>Impacto moderado</td>
   <td>O AEM 6.3 exige o JRE 1.7.x (64 bits) ou posterior. O JRE 1.8 é a única versão atualmente compatível com o Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Impacto moderado</td>
   <td>A Limpeza de revisão online requer grátis<br /> espaço em disco igual a 25% do tamanho do repositório e 15% de espaço livre em heap<br /> para concluir com êxito. Talvez seja necessário atualizar seu hardware para<br /> garantir recursos suficientes para a Limpeza de revisão on-line para<br /> executar. Além disso, se atualizar de uma versão anterior ao AEM 6, não haverá<br /> podem ser requisitos adicionais de armazenamento.</td>
  </tr>
  <tr>
   <td>Repositório de conteúdo (CRX ou Oak)</td>
   <td>Alto impacto</td>
   <td>A partir da versão 6.1, o AEM não é compatível com o CRX2, portanto, uma migração para<br /> O Oak (CRX3) é necessário se estiver atualizando de uma versão mais antiga. O AEM 6.3 tem<br /> implementou um novo Armazenamento de nós de segmento que também requer uma migração. A variável<br /> a ferramenta crx2oak é usada para essa finalidade.</td>
  </tr>
  <tr>
   <td>Componentes/conteúdo do AEM</td>
   <td>Impacto moderado</td>
   <td><code>/libs</code> e <code>/apps</code> são facilmente tratados por meio da atualização, mas <code>/etc</code> geralmente requer alguma reaplicação manual de personalizações.</td>
  </tr>
  <tr>
   <td>Serviços de AEM</td>
   <td>Baixo impacto</td>
   <td>A maioria dos serviços principais de AEM é testada para atualização. Essa é uma área de baixo impacto.</td>
  </tr>
  <tr>
   <td>Serviços de aplicativos personalizados</td>
   <td>Impacto baixo a alto</td>
   <td>Dependendo do aplicativo e da personalização, pode haver<br /> dependências na JVM, nas versões do sistema operacional e em algumas indexações relacionadas<br /> alterações, pois os índices não são gerados automaticamente no Oak.</td>
  </tr>
  <tr>
   <td>Conteúdo personalizado do aplicativo</td>
   <td>Impacto baixo a alto</td>
   <td>O conteúdo que não será tratado por meio da atualização pode ser submetido a backup<br /> antes da atualização e, em seguida, movido de volta para o repositório.<br /> A maior parte do conteúdo pode ser manuseada por meio da ferramenta de migração.</td>
  </tr>
 </tbody>
</table>

É importante garantir que você esteja executando um sistema operacional compatível, Java™ runtime, httpd e versão do Dispatcher. Para obter mais informações, consulte [Página de requisitos técnicos do AEM 6.5](/help/sites-deploying/technical-requirements.md). A atualização desses componentes precisará ser contabilizada no plano do projeto e deverá ocorrer antes da atualização do AEM.

## Fases do projeto {#project-phases}

Muito trabalho é dedicado ao planejamento e à execução de uma atualização do AEM. Para esclarecer os diferentes esforços que entram nesse processo, a Adobe dividiu os exercícios de planejamento e execução em fases separadas. Nas seções abaixo, cada fase resulta em um material de entrega que é usado com frequência em uma fase futura do projeto.

### Planejamento para treinamento do autor {#planning-for-author-training}

Com qualquer nova versão, há possíveis alterações na interface do usuário e nos fluxos de trabalho do usuário que podem ser introduzidas. Além disso, novas versões apresentam novos recursos que podem ser benéficos para a empresa usar. A Adobe recomenda revisar as alterações funcionais introduzidas e organizar um plano para treinar os usuários sobre como usá-las de maneira eficaz.

![unu_cropped](assets/unu_cropped.png)

Os novos recursos do AEM 6.5 podem ser encontrados em [a seção AEM do adobe.com](/help/release-notes/release-notes.md). Observe quaisquer alterações nas interfaces do usuário ou nos recursos do produto que são normalmente usadas em sua organização. Ao examinar os novos recursos, anote também qualquer item que possa ser útil para a sua organização. Depois de analisar o que mudou no AEM 6.5, desenvolva um plano de treinamento para seus autores. Isso pode envolver o uso de recursos disponíveis gratuitamente, como vídeos de ajuda ou treinamento formal oferecido por meio do [Serviços de aprendizado digital Adobe](https://learning.adobe.com/).

### Criando um Plano de Teste {#creating-a-test-plan}

A implementação do AEM em cada cliente é exclusiva e foi personalizada para atender às suas necessidades de negócios. Como resultado, é importante determinar todas as personalizações feitas no sistema para que possam ser incluídas em um plano de teste. Esse plano de teste alimentará o processo de controle de qualidade que o Adobe executa na instância atualizada.

![plano de teste](assets/test-plan.png)

O ambiente de produção exato precisa ser duplicado e testes devem ser executados nele após a atualização para garantir que todos os aplicativos e códigos personalizados ainda sejam executados conforme desejado. Regressar toda a personalização e executar testes de desempenho, carga e segurança. Ao organizar seu plano de teste, cubra todas as personalizações feitas no sistema, além das interfaces do usuário e dos fluxos de trabalho prontos para uso usados em suas operações diárias. Eles podem incluir serviços e servlets OSGI personalizados, integrações com a Adobe Experience Cloud, integrações com terceiros por meio de conectores AEM, integrações personalizadas de terceiros, componentes e modelos personalizados, sobreposições de interface do usuário personalizadas no AEM e fluxos de trabalho personalizados. Para clientes que migram de uma versão anterior ao AEM 6, quaisquer consultas personalizadas devem ser analisadas, pois podem precisar ser indexadas. Para clientes que já estão em uma versão AEM 6.x, essas consultas ainda devem ser testadas para garantir que seus índices continuem funcionando de forma eficaz após a atualização.

### Determinando as alterações necessárias na arquitetura e na infraestrutura {#determining-architectural-and-infrastructure-changes-needed}

Ao atualizar, é possível que você também precise atualizar outros componentes em sua pilha técnica, como o sistema operacional ou a JVM. Além disso, é possível que, devido a alterações na composição do repositório, hardware adicional seja necessário. Isso só ocorre com clientes que migram de instâncias anteriores à 6.x, mas é importante considerar. Por fim, pode haver a necessidade de mudanças em suas práticas operacionais, incluindo monitoramento, manutenção, backup e processos de recuperação de desastres.

![doi_cropped](assets/doi_cropped.png)

Revise os Requisitos técnicos para o AEM 6.5 e certifique-se de que seu hardware e software atuais serão suficientes. Para ver possíveis alterações nos processos operacionais, consulte os seguintes documentos:

**Monitoramento e manutenção:**

[Painel de operações](/help/sites-administering/operations-dashboard.md)

[Práticas recomendadas de monitoramento de ativos](/help/assets/assets-monitoring-best-practices.md)

[Recursos do Monitoring Server usando a console JMX](/help/sites-administering/jmx-console.md)

[Limpeza de revisão](/help/sites-deploying/revision-cleanup.md)

**Backup/restauração e recuperação de desastres:**

[Backup e restauração](/help/sites-administering/backup-and-restore.md)

[Desempenho e escalabilidade](/help/sites-deploying/performance.md)

[Como executar AEM com TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md)

#### Considerações sobre a reestruturação de conteúdo {#content-restructuring-considerations}

O AEM introduziu alterações na estrutura do repositório que ajudarão a facilitar as atualizações. As alterações envolvem mover o conteúdo da pasta /etc para pastas, incluindo /libs, /apps e /content, com base no fato de o Adobe ou um cliente possuir o conteúdo, limitando assim as chances de substituir o conteúdo durante os lançamentos. A reestruturação do repositório foi feita de maneira que não deve exigir alterações de código no momento da atualização da versão 6.5, embora seja recomendável analisar os detalhes em [Reestruturação do repositório no AEM](/help/sites-deploying/repository-restructuring.md) ao planejar uma atualização.

### Avaliando a complexidade da atualização {#assessing-upgrade-complexity}

Devido à grande variedade na quantidade e na natureza das personalizações que os clientes do Adobe aplicam em seus ambientes AEM, é importante reservar algum tempo para determinar o nível geral de esforço que deve ser esperado na atualização.

Há duas abordagens que você pode seguir para avaliar a complexidade da atualização: uma fase preliminar pode usar o Detector de padrões recém-introduzido, que está disponível para ser executado nas instâncias do AEM 6.1, 6.2 e 6.3. O detector de padrões é a maneira mais fácil de avaliar a complexidade geral da atualização esperada usando padrões relatados. O relatório de detector de padrões inclui padrões para identificar APIs indisponíveis que estão em uso pela base de código personalizada (isso foi feito usando verificações de compatibilidade de pré-atualização na versão 6.3).

Após a avaliação inicial, uma próxima etapa mais abrangente pode ser executar uma atualização em uma instância de teste e executar alguns testes básicos de fumaça. O Adobe também fornece alguns . Além disso, a [Recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md) deve ser revisada não apenas para a versão para a qual você está atualizando, mas também para qualquer versão entre as versões de origem e de destino. Por exemplo, se estiver atualizando do AEM 6.2 para o 6.5, é importante revisar os recursos obsoletos e removidos do AEM 6.3, além daqueles do AEM 6.5.

![trei_cropped](assets/trei_cropped.png)

O Detector de padrões introduzido recentemente no deve fornecer uma estimativa bastante precisa do que esperar durante uma atualização para a maioria dos casos. No entanto, para personalizações e implantações mais complexas nas quais você tem alterações incompatíveis, é possível atualizar uma instância de desenvolvimento para AEM 6.5 de acordo com as instruções em [Execução de uma atualização no local](/help/sites-deploying/in-place-upgrade.md). Depois de concluído, execute alguns testes de alto nível de fumaça nesse ambiente. O objetivo deste exercício não é concluir exaustivamente o inventário de casos de teste e produzir um inventário formal de defeitos, mas fornecer uma estimativa aproximada da quantidade de trabalho que será necessária para atualizar o código para a compatibilidade com a versão 6.5. Quando combinado com o [Detecção de padrões](/help/sites-deploying/pattern-detector.md) e as alterações de arquitetura determinadas na seção anterior, uma estimativa aproximada pode ser fornecida à equipe de gerenciamento do projeto para o planejamento da atualização.

### Criação do Runbook de Atualização e Reversão {#building-the-upgrade-and-rollback-runbook}

Embora o Adobe tenha documentado o processo de upgrade de uma instância AEM, o layout de rede, a arquitetura de implantação e as personalizações de cada cliente exigem o ajuste e a personalização dessa abordagem. Por esse motivo, o Adobe incentiva você a revisar toda a documentação fornecida e usá-la para informar um runbook específico do projeto que descreve os procedimentos específicos de atualização e reversão que você seguirá no ambiente. Se estiver atualizando do CRX2, avalie quanto tempo a migração de conteúdo levará ao mudar do CRX2 para o Oak. Para repositórios grandes, isso pode ser substancial.

![diagrama-runbook](assets/runbook-diagram.png)

O Adobe forneceu procedimentos de atualização e reversão no [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md) instruções passo a passo para aplicar a atualização em Executando uma [Atualização no local](/help/sites-deploying/in-place-upgrade.md). Essas instruções devem ser revisadas e consideradas com a arquitetura do sistema, as personalizações e a tolerância ao tempo de inatividade para determinar os procedimentos de comutação e reversão apropriados que serão executados durante o upgrade. Quaisquer alterações na arquitetura ou nos tamanhos do servidor devem ser incluídas ao elaborar o runbook personalizado. É importante observar que isso deve ser tratado como um primeiro rascunho. À medida que sua equipe conclui os ciclos de controle de qualidade e desenvolvimento e implanta a atualização no ambiente de preparo, provavelmente será necessário realizar algumas etapas adicionais. Idealmente, esse documento deve conter informações suficientes para que, se fosse entregue a um membro da equipe de operações, ele pudesse concluir a atualização completamente a partir das informações contidas nele.

### Desenvolvendo um plano de projeto {#developing-a-project-plan}

O resultado dos exercícios anteriores pode ser usado para criar um plano de projeto que abranja os cronogramas esperados para seus esforços de teste ou desenvolvimento, treinamento e execução de atualização real.

![plano-projeto-desenvolvimento](assets/develop-project-plan.png)

Um plano de projeto abrangente deve incluir:

* Finalização dos planos de desenvolvimento e teste
* Atualização de ambientes de desenvolvimento e controle de qualidade
* Atualização da base de código personalizado para AEM 6.5
* Um ciclo de teste e correção de controle de qualidade
* Atualização do ambiente de preparo
* Integração, desempenho e teste de carga
* Certificação de ambiente
* Go live

### Execução de desenvolvimento e controle de qualidade {#performing-development-and-qa}

A Adobe forneceu procedimentos para [Atualização de código e personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) para ser compatível com o AEM 6.5. À medida que esse processo iterativo é executado, as alterações devem ser feitas no runbook, conforme necessário. Consulte também [Compatibilidade com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) sobre informações sobre como suas personalizações podem permanecer compatíveis com versões anteriores, geralmente sem exigir desenvolvimento imediatamente após a atualização.

![patru_cropped](assets/patru_cropped.png)

O processo de desenvolvimento e teste é geralmente iterativo. Devido a personalizações, as alterações feitas durante a atualização podem tornar uma seção inteira do produto inutilizável. Depois que os desenvolvedores abordarem a causa raiz do problema e a equipe de teste tiver acesso para testar esses recursos, haverá a possibilidade de descobrir problemas adicionais. À medida que são descobertos problemas que exigem ajustes no processo de atualização, adicione-os ao runbook de atualização personalizado. Após várias iterações de teste e correção, a base de código deve ser totalmente validada e pronta para implantação no ambiente de preparo.

### Teste final {#final-testing}

A Adobe recomenda uma rodada final de testes depois que a base de código tiver sido certificada pela equipe de controle de qualidade da sua organização. Esta rodada de testes envolverá a validação do runbook em um ambiente de preparo, seguida por rodadas de aceitação do usuário, desempenho e testes de segurança.

![cinci_cropped](assets/cinci_cropped.png)

Essa etapa é essencial, pois é a única vez que você pode validar as etapas no runbook em relação a um ambiente semelhante à produção. Depois que o ambiente for atualizado, é importante dar aos usuários finais algum tempo para fazer logon e passar pelas atividades que eles realizam ao usar o sistema em suas atividades diárias. Não é incomum que os usuários estejam usando uma parte do sistema que não foi considerada anteriormente. Encontrar e corrigir problemas nessas áreas antes da ativação pode ajudar a evitar paralisações dispendiosas da produção. Como uma nova versão do AEM contém alterações significativas na plataforma subjacente, também é importante executar testes de desempenho, carga e segurança no sistema como se ele estivesse sendo iniciado pela primeira vez.

### Execução da atualização {#performing-the-upgrade}

Depois que a aprovação final for recebida de todas as partes interessadas, é hora de executar os procedimentos de runbook definidos. O Adobe forneceu etapas para atualização e reversão no [Procedimento de atualização](/help/sites-deploying/upgrade-procedure.md) e as etapas de instalação em Execução de uma [Atualização no local](/help/sites-deploying/in-place-upgrade.md) como ponto de referência.

![execute-upgrade](assets/perform-upgrade.png)

O Adobe forneceu algumas etapas nas instruções de atualização para validação do ambiente. Isso inclui verificações básicas como varredura dos registros de atualização e verificação de que todos os pacotes OSGi foram iniciados corretamente, mas o Adobe também recomenda a validação com seus próprios casos de teste com base nos processos de negócios. A Adobe também recomenda verificar o cronograma de limpeza de revisão on-line do AEM e rotinas relacionadas para garantir que elas estejam ocorrendo durante um período de silêncio para sua empresa. Essas rotinas são essenciais para o desempenho a longo prazo do AEM.
