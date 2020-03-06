---
title: Planejamento da atualização
seo-title: Planejamento da atualização
description: Este artigo ajuda a estabelecer objetivos, fases e resultados ao planejar a atualização do AEM.
seo-description: Este artigo ajuda a estabelecer objetivos, fases e resultados ao planejar a atualização do AEM.
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# Planejamento da atualização{#planning-your-upgrade}

## Visão geral do projeto AEM {#aem-project-overview}

O AEM é usado com frequência em implantações de alto impacto que podem servir a milhões de usuários. Na maioria dos casos, existem aplicativos personalizados que são implantados nas instâncias, o que aumenta a complexidade. Qualquer esforço de atualização dessa implantação deve ser feito de forma metódica.

Este guia ajuda a estabelecer objetivos, fases e resultados ao planejar sua atualização. Centra-se na execução e orientações gerais do projeto. Embora forneça uma visão geral das etapas de atualização reais, ela se refere aos recursos técnicos disponíveis, quando adequado. Deve ser utilizado em conjugação com os recursos técnicos disponíveis referidos no documento.

O processo de atualização do AEM precisa de fases de planejamento, análise e execução cuidadosamente manipuladas com os principais resultados finais definidos para cada fase.

Observe que é possível atualizar diretamente do AEM versões 6.0 e até 6.5. Os clientes com 5.6.x ou menos precisam atualizar primeiro para a versão 6.0 ou superior, sendo recomendado o 6.0(SP3). Além disso, o novo formato OAK Segment Tar é usado agora para o Segment Node Store desde 6.3, e a migração do repositório para esse novo formato é obrigatória mesmo para 6.0, 6.1 e 6.2.

>[!CAUTION]
>
>Se você estiver atualizando do AEM 6.2 para o 6.3, é necessário atualizar das versões (**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**) ou **6.2SP1-CFP15** em diante. Caso contrário, se você estiver atualizando de **6.2SP1-CFP13/6.2SP1CFP14** para AEM 6.3, também deverá atualizar para pelo menos a versão **6.3.2.2**. Caso contrário, o AEM Sites falharia após a atualização.

## Escopo e requisitos de atualização {#upgrade-scope-requirements}

Abaixo, você encontrará uma lista das áreas afetadas em um projeto de atualização típico do AEM:

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
   <td>No momento da atualização do AEM, talvez seja hora de atualizar o sistema operacional também e isso pode causar algum impacto.</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>Impacto moderado</td>
   <td>O AEM 6.3 requer JRE 1.7.x (64 bits) ou posterior. O JRE 1.8 é a única versão atualmente suportada pela Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Impacto moderado</td>
   <td>A Limpeza de revisão online requer espaço livre<br /> em disco igual a 25% do tamanho do repositório e 15% de espaço<br /> livre no heap para ser concluída com êxito. Talvez seja necessário atualizar seu hardware para<br /> garantir recursos suficientes para que a Limpeza de revisão online seja totalmente<br /> executada. Além disso, ao atualizar de uma versão anterior ao AEM 6, pode haver<br /> requisitos adicionais de armazenamento.</td>
  </tr>
  <tr>
   <td>Repositório de conteúdo (CRX ou Oak)</td>
   <td>Elevado impacto</td>
   <td>A partir da versão 6.1, o AEM não oferece suporte ao CRX2, portanto, uma migração para<br /> Oak (CRX3) é necessária se você atualizar de uma versão anterior. O AEM 6.3 implementou<br /> uma nova Loja de Nó de Segmento que também exige uma migração. A ferramenta<br /> crx2oak é usada para essa finalidade.</td>
  </tr>
  <tr>
   <td>Componentes/conteúdo do AEM</td>
   <td>Impacto moderado</td>
   <td><code>/libs</code> e <code>/apps</code> são facilmente manipulados por meio da atualização, mas <code>/etc</code> geralmente exigem uma reaplicação manual das personalizações.</td>
  </tr>
  <tr>
   <td>Serviços AEM</td>
   <td>Baixo impacto</td>
   <td>A maioria dos serviços principais do AEM é testada para atualização. Esta é uma área de baixo impacto.</td>
  </tr>
  <tr>
   <td>Serviços de aplicativos personalizados</td>
   <td>Baixo a alto impacto</td>
   <td>Dependendo do aplicativo e da personalização, pode haver<br /> dependências em JVM, versões do sistema operacional e algumas alterações relacionadas<br /> à indexação, já que os índices não são gerados automaticamente no Oak.</td>
  </tr>
  <tr>
   <td>Conteúdo personalizado do aplicativo</td>
   <td>Baixo a alto impacto</td>
   <td>É possível fazer backup<br /> do conteúdo que não será manipulado por meio da atualização antes que a atualização ocorra e, em seguida, ser movido de volta para o repositório.<br /> A maioria dos conteúdos pode ser feita por meio da ferramenta de migração.</td>
  </tr>
 </tbody>
</table>

É importante garantir que você esteja executando um sistema operacional suportado, Java runtime, httpd e Dispatcher version. Para obter mais informações, consulte a página [Requisitos técnicos do](/help/sites-deploying/technical-requirements.md)AEM 6.5. A atualização desses componentes precisará ser contabilizada no seu plano de projeto e deve ocorrer antes da atualização do AEM.

## Fases do projeto {#project-phases}

Muito trabalho é feito para planejar e executar uma atualização do AEM. A fim de clarificar os diferentes esforços desenvolvidos neste processo, dividimos os exercícios de planeamento e execução em fases separadas. Nas seções abaixo, cada fase resulta em um material de entrega que geralmente é aproveitado por uma fase futura do projeto.

### Planejamento para treinamento de autor {#planning-for-author-training}

Com qualquer nova versão, há possíveis alterações na interface do usuário e nos fluxos de trabalho do usuário que podem ser introduzidas. Além disso, novas versões apresentam novos recursos que podem ser benéficos para a empresa aproveitar. Recomendamos a revisão das alterações funcionais que foram introduzidas e a organização de um plano para treinar seus usuários a aproveitá-las de forma eficaz.

![unu_croped](assets/unu_cropped.png)

Novos recursos do AEM 6.5 podem ser encontrados na seção AEM [do adobe.com](/help/release-notes/release-notes.md). Anote todas as alterações feitas nas interfaces de usuário ou nos recursos do produto que geralmente são usados em sua organização. Conforme você olha pelos novos recursos, também anote qualquer item que possa ser valioso para sua organização. Depois de examinar o que mudou no AEM 6.5, desenvolva um plano de treinamento para seus autores. Isso pode envolver o aproveitamento de recursos disponíveis gratuitamente, como vídeos de recursos helpx ou treinamento formal oferecido pelos Serviços [de aprendizado digital da](https://www.adobe.com/training.html)Adobe.

### Criação de um plano de teste {#creating-a-test-plan}

A implementação do AEM por cada cliente é exclusiva e foi personalizada para atender às suas necessidades de negócios. Como resultado, é importante determinar todas as personalizações feitas no sistema para que possam ser incluídas em um plano de teste. Esse plano de teste acionará o processo de QA que executamos na instância atualizada.

![plano de ensaio](assets/test-plan.png)

O ambiente de produção exato precisa ser duplicado e os testes devem ser executados nele após a atualização para garantir que todos os aplicativos e código personalizado ainda sejam executados conforme desejado. Você precisa recuperar toda a sua personalização e executar testes de desempenho, carga e segurança. Ao organizar seu plano de teste, certifique-se de cobrir todas as personalizações feitas no sistema, além das interfaces de usuário e fluxos de trabalho prontos para uso que são aproveitados em suas operações diárias. Eles podem incluir serviços e servlets OSGI personalizados, integrações à Adobe Marketing Cloud, integrações com terceiros por meio de conectores AEM, integrações personalizadas de terceiros, componentes e modelos personalizados, sobreposições de interface personalizadas no AEM e fluxos de trabalho personalizados. Para clientes que migram de uma versão anterior ao AEM 6, quaisquer consultas personalizadas devem ser analisadas, pois podem precisar ser indexadas. Para os clientes que já estão em uma versão AEM 6.x, essas consultas ainda devem ser testadas para garantir que seus índices continuem a funcionar com eficácia após a atualização.

### Determinando as mudanças de arquitetura e infraestrutura necessárias {#determining-architectural-and-infrastructure-changes-needed}

Durante a atualização, é possível que você também precise atualizar outros componentes na pilha técnica, como o sistema operacional ou JVM. Além disso, é possível que, devido a alterações na configuração do repositório, seja necessário hardware adicional. Isso geralmente só ocorre para clientes que migram de instâncias anteriores ao 6.x, mas é importante considerar. Por fim, pode haver mudanças necessárias em suas práticas operacionais, incluindo monitoramento, manutenção e processos de backup e recuperação de desastres.

![doi_croped](assets/doi_cropped.png)

Examine os requisitos técnicos do AEM 6.5 e verifique se seu hardware e software atuais serão suficientes. Para obter possíveis alterações nos processos operacionais, consulte os seguintes documentos:

**Monitorização e manutenção:**

[Painel de operações](/help/sites-administering/operations-dashboard.md)

[Práticas recomendadas de monitoramento de ativos](/help/assets/assets-monitoring-best-practices.md)

[Monitorando Recursos do Servidor Usando o Console JMX](/help/sites-administering/jmx-console.md)

[Limpeza de revisão](/help/sites-deploying/revision-cleanup.md)

**Backup/restauração e recuperação de desastres:**

[Backup e restauração](/help/sites-administering/backup-and-restore.md)

[Desempenho e escalabilidade](/help/sites-deploying/performance.md)

[Como executar o AEM com TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md)

#### Considerações sobre reestruturação de conteúdo {#content-restructuring-considerations}

O AEM introduziu alterações na estrutura do repositório que ajudarão a tornar as atualizações mais ininterruptas. As alterações envolvem mover o conteúdo da pasta /etc para pastas, incluindo /libs, /apps e /content, com base no fato de a Adobe ou um cliente possuir o conteúdo, limitando assim as chances de sobrescrever o conteúdo durante as versões. A reestruturação do repositório foi feita de modo que não deve exigir alterações de código no momento da atualização do 6.5, embora seja recomendável rever os detalhes na reestruturação do [repositório no AEM](/help/sites-deploying/repository-restructuring.md) enquanto planeja uma atualização.

### Avaliação da complexidade da atualização {#assessing-upgrade-complexity}

Devido à grande variedade na quantidade e na natureza das personalizações que nossos clientes aplicam aos seus ambientes AEM, é importante passar algum tempo adiantado para determinar o nível geral de esforço que deve ser esperado em sua atualização.

Existem duas abordagens que você pode adotar para avaliar a complexidade da atualização, uma fase preliminar pode apenas usar o Detector de padrão recém-introduzido que está disponível para ser executado nas instâncias do AEM 6.1, 6.2 e 6.3. O detector de padrões é a maneira mais fácil de avaliar a complexidade geral da atualização que é esperada usando padrões relatados. O relatório do detector de padrões inclui padrões para identificar APIs indisponíveis que estão em uso pela base de código personalizada (isso foi feito usando verificações de compatibilidade de pré-atualização na seção 6.3).

Após a avaliação inicial, uma etapa seguinte mais abrangente poderia ser a realização de uma atualização em uma instância de teste e a realização de alguns testes básicos de fumaça. A Adobe também fornece alguns . Além disso, a lista de Recursos [removidos e](/help/release-notes/deprecated-removed-features.md) obsoletos deve ser revisada não apenas para a versão para a qual você está atualizando, mas também para qualquer versão entre as versões de origem e de destino. Por exemplo, se você atualizar do AEM 6.2 para o 6.5, é importante revisar os recursos obsoletos e removidos do AEM 6.3, além dos do AEM 6.5.

![trei_croped](assets/trei_cropped.png)

O Detector de padrões introduzido recentemente deve fornecer uma estimativa bastante precisa do que esperar durante uma atualização na maioria dos casos. No entanto, para personalizações e implantações mais complexas em que você tenha alterações incompatíveis, é possível atualizar uma instância de desenvolvimento para o AEM 6.5 de acordo com as instruções em [Realizar uma atualização](/help/sites-deploying/in-place-upgrade.md)no local. Depois de concluído, faça alguns testes de fumaça de alto nível neste ambiente. O objetivo deste exercício não é completar exaustivamente o inventário do caso de teste e produzir um inventário formal de defeitos, mas fornecer uma estimativa aproximada da quantidade de trabalho que será necessária para atualizar o código para a compatibilidade com o 6.5. Quando combinada com a Detecção [de](/help/sites-deploying/pattern-detector.md) padrões e as alterações arquitetônicas que foram determinadas na seção anterior, uma estimativa aproximada pode ser fornecida à equipe de gerenciamento do projeto para planejar a atualização.

### Criando o Runbook Upgrade e Rollback {#building-the-upgrade-and-rollback-runbook}

Embora a Adobe tenha documentado o processo de atualização de uma instância do AEM, o layout de rede, a arquitetura de implantação e as personalizações de cada cliente exigirão o ajuste e a personalização dessa abordagem. Por esse motivo, recomendamos que você reveja toda a documentação que fornecemos e use-a para informar um runbook específico do projeto que descreve os procedimentos específicos de atualização e reversão que você seguirá em seu ambiente. Se você estiver atualizando do CRX2, certifique-se de avaliar quanto tempo a migração de conteúdo levará ao mudar do CRX2 para o Oak. Para grandes repositórios, poderia ser substancial.

![diagrama do runbook](assets/runbook-diagram.png)

Fornecemos procedimentos de atualização e reversão no procedimento [de](/help/sites-deploying/upgrade-procedure.md) atualização, bem como instruções passo a passo para aplicar a atualização em Realizar uma atualização [no local](/help/sites-deploying/in-place-upgrade.md). Essas instruções devem ser analisadas e levadas em consideração com a arquitetura do sistema, as personalizações e a tolerância ao tempo de inatividade para determinar os procedimentos apropriados de alternância e reversão que você executará durante a atualização. Quaisquer alterações na arquitetura ou no tamanho do servidor devem ser incluídas ao criar seu runbook personalizado. É importante notar que este aspecto deve ser tratado como um primeiro projeto. À medida que sua equipe conclui seus ciclos de controle de qualidade e desenvolvimento e implanta a atualização para o ambiente de preparo temporário, é provável que a necessidade de algumas etapas adicionais seja necessária. Idealmente, este documento deve conter informações suficientes para que, se ele for entregue a um membro da equipe de operações, ele possa concluir a atualização completamente a partir das informações contidas nele.

### Desenvolvimento de um plano de projeto {#developing-a-project-plan}

Podemos usar o resultado dos exercícios anteriores para criar um plano de projeto que cubra os prazos esperados para nossos esforços de teste ou desenvolvimento, treinamento e execução de atualização real.

![plano de desenvolvimento](assets/develop-project-plan.png)

Um plano de projeto abrangente deve incluir:

* Finalização dos planos de desenvolvimento e teste
* Atualização dos ambientes de desenvolvimento e controle de qualidade
* Atualização da base de código personalizada para o AEM 6.5
* Um teste de QA e um ciclo de correção
* Atualização do ambiente de preparo
* Integração, desempenho e teste de carga
* Certificação ambiental
* Ir ao vivo

### Execução do desenvolvimento e controle de qualidade {#performing-development-and-qa}

Fornecemos procedimentos para que o Código de [atualização e as Personalizações](/help/sites-deploying/upgrading-code-and-customizations.md) sejam compatíveis com o AEM 6.5. Como esse processo iterativo é executado, as alterações devem ser feitas no runbook conforme necessário. Consulte também Compatibilidade [com versões anteriores no AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obter informações sobre como suas personalizações podem permanecer compatíveis com versões anteriores na maioria dos casos, sem necessidade de desenvolvimento imediatamente após a atualização.

![patru_croped](assets/patru_cropped.png)

O processo de desenvolvimento e teste costuma ser iterativo. Devido às personalizações, as alterações feitas durante a atualização podem tornar potencialmente inutilizável uma seção inteira do produto. Depois que os desenvolvedores abordarem a causa básica do problema e a equipe de teste tiver acesso para testar esses recursos, há o potencial para descobrir problemas adicionais. À medida que forem detectados problemas que exijam ajustes no processo de atualização, adicione-os ao seu runbook de atualização personalizado. Após várias iterações de teste e correção, a base de código deve ser totalmente validada e pronta para implantação no ambiente de preparo.

### Teste final {#final-testing}

Recomendamos uma rodada final de testes depois que a base de códigos tiver sido certificada pela equipe de controle de qualidade de sua organização. Essa rodada de testes envolverá a validação do runbook em um ambiente de preparo, seguido de rondas de aceitação, desempenho e teste de segurança do usuário.

![cinci_croped](assets/cinci_cropped.png)

Essa etapa é vital, pois é a única vez que você pode validar as etapas no runbook em relação a um ambiente semelhante à produção. Depois que o ambiente for atualizado, é importante permitir que os usuários finais façam logon e passem pelas atividades que fazem ao usar o sistema em suas atividades diárias. Não é raro os usuários aproveitarem uma parte do sistema que não foi considerada anteriormente. Encontrar e corrigir problemas nessas áreas antes de entrar em operação pode ajudar a evitar paralisações dispendiosas na produção. Como uma nova versão do AEM contém mudanças significativas na plataforma subjacente, também é importante executar testes de desempenho, carga e segurança no sistema como se o iniciássemos pela primeira vez.

### Execução da atualização {#performing-the-upgrade}

Depois de receber o logoff final de todas as partes interessadas, é tempo de executar os procedimentos do runbook que foram definidos. Fornecemos etapas para atualização e reversão no procedimento [de](/help/sites-deploying/upgrade-procedure.md) atualização e etapas de instalação em Realização de uma atualização [](/help/sites-deploying/in-place-upgrade.md) no local como ponto de referência.

![performance-upgrade](assets/perform-upgrade.png)

Fornecemos algumas etapas nas instruções de atualização para a validação do ambiente. Isso inclui verificações básicas, como a verificação dos registros de atualização e verificação de que todos os pacotes OSGi foram iniciados corretamente, mas recomendamos também a validação com seus próprios casos de teste, com base nos processos de negócios. Também recomendamos verificar o agendamento da Limpeza online de revisão do AEM e as rotinas relacionadas para garantir que elas ocorrerão durante um período de silêncio para sua empresa. Essas rotinas são essenciais para o desempenho a longo prazo do AEM.
