---
title: Gerenciamento de projetos - Lista de verificação de práticas recomendadas
description: O gerenciamento de um projeto para implementar o Adobe Experience Manager (AEM) requer planejamento e compreensão. As Listas de verificação do projeto são um conjunto de práticas recomendadas para a entrega do projeto. Elas orientam você em todas as fases do ciclo de vida do projeto e fornecem monitoramento de alto nível do seu status.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Developer,Leader
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '3212'
ht-degree: 0%

---

# Gerenciamento de projetos - Lista de verificação de práticas recomendadas{#managing-projects-best-practices-checklist}

O gerenciamento de um projeto para implementar o Adobe Experience Manager (AEM) requer planejamento e compreensão, para que você esteja ciente dos problemas e decisões (relacionadas) que devem ser tomadas antes e durante a implementação do projeto.

Para ajudá-lo, as práticas recomendadas consistem em:

* Uma [lista de verificação interativa](/help/managing/best-practices-checklist.md) que permite acompanhar e monitorar seu progresso com essas práticas recomendadas.

   * Define entradas e entregáveis de acordo com fase, marco e persona.
   * Fornece visões gerais automatizadas (qualidade, integridade e integridade) para indicar o progresso e a integridade do projeto.

* Documentação baseada na [lista de verificação](/help/managing/best-practices-checklist.md) que detalha:

   * Análise de [Pulsação do projeto](#projectheartbeat).
   * Visão geral de [Status por Função](#status-by-role).
   * [Fases e Etapas](#phases-and-milestones).
   * [Persona-chave](#persona) e seu envolvimento em cada estágio (relevante).
   * Um [Glossário](/help/managing/best-practices-glossary.md) dos [Documentos e Entregas Necessários](#required-documents-and-deliverables).

* [Mais material de referência](/help/managing/best-practices-further-reference.md) para fornecer mais detalhes sobre áreas específicas.

## Painel do Project Heartbeat {#project-heartbeat-dashboard}

A planilha **Pulsação do projeto** fornece uma visão geral gráfica das métricas críticas para o seu projeto:

* **Qualidade da fase**

   * Indica a qualidade dos [Documentos e Produtos Necessários](#required-documents-and-deliverables) em todo o projeto.

* **Integridade da Fase**

   * Um indicador de status de alto nível para o seu projeto; útil para destacar áreas que podem estar em risco.

* **Completude da Fase**

   * Em qualquer momento durante o projeto, isso indica quanto já foi concluído para cada fase do projeto.

## Status por Função {#status-by-role}

A planilha **Status por Função** mostra o detalhamento de [**Integridade**, **Qualidade e &#x200B;** Integridade&#x200B;**](#projectheartbeat) por &#x200B;** [Fase](#phases-and-milestones)**&#x200B; e &#x200B;** [Pessoa](#persona)**.

## Fases e etapas {#phases-and-milestones}

O plano do projeto é dividido em fases distintas (alto nível).

Cada fase contém seus próprios marcos. Para cada [persona](#persona) (ou função), os marcos relevantes são listados, juntamente com os documentos necessários para produzir os resultados definidos.

>[!NOTE]
>
>Não há uma relação 1:1 direta entre os documentos necessários individuais e os materiais para entrega.

### Preparação {#preparation}

A preparação do projeto é a base de todo o projeto. Definir os principais requisitos, juntamente com metas e expectativas claras para:

* **Razão Comercial**

   * As razões fundamentais e justificativas para realizar o projeto.

* **Escopo e Agendamento**

   * Um escopo básico e um cronograma aproximado devem ser disponibilizados para definir o que é necessário e dentro de qual período de tempo; se isso ajudar a esclarecer a situação, você também poderá definir o que está fora do escopo.

A maneira como você prepara, planeja e executa seu projeto e implementa sua solução é afetada pelas restrições sob as quais você está operando. Por exemplo, orçamento fixo, cronograma fixo, quantidade de conteúdo, qualidade necessária.

Como sempre, ajustar qualquer um dos fatores afeta os outros. Por exemplo, reduzir o tempo, mas exigir o mesmo nível de qualidade, provavelmente aumentará o preço e reduzirá a quantidade de conteúdo que você pode atender. O orçamento é muitas vezes um fator chave, de modo que tais relações não podem ser esquecidas.

Os quatro fatores:

![fases_projeto](assets/projectphases_fourphases.png)

#### Etapas {#milestones}

* **Validação**

  Nesta fase, você deve validar e confirmar as metas do projeto; por exemplo:

   * O que você deseja alcançar/fornecer?
   * Quem se beneficia?
   * Qual é o escopo?

      * Se ajudar a esclarecer a situação, você também poderá definir o que está fora do escopo.

   * Como você define sucesso?
   * Como você avalia o sucesso?
   * Quais são os requisitos técnicos e de negócios?
   * Há sistemas herdados a serem substituídos e, em caso afirmativo, há dados a serem migrados?
   * Quem está envolvido?
   * Como você avalia o progresso?
   * Com que frequência você analisa o progresso durante a vida útil do projeto?

* **Orçamento**

  Antes de iniciar qualquer projeto, você precisa de uma estimativa confiável e realista de quanto custa implementar:

   * Use as informações da etapa de validação como base para as estimativas.
   * Seja realista em suas estimativas.
   * Considere e respeite quaisquer diretrizes, processos ou restrições do cliente aos quais o cliente esteja sujeito.
   * Considere os processos de contingência e revisão se uma revisão ou refinamento do orçamento for necessário posteriormente.
   * Lembre-se de que os custos vêm de muitas formas, como compras, uso de recursos e taxas, entre outras.

### Planejamento {#planning}

O planejamento de seu projeto consolida a preparação. Aqui, você deve começar a converter os objetivos e as expectativas em um roteiro bem definido que consiste em tarefas concretas, vinculadas a uma comunicação clara, com revisões rigorosas para medir o progresso.

#### Etapas {#milestones-1}

* **Transferência**

  Uma entrega limpa garante que a pessoa/grupos apropriados estejam cientes de suas responsabilidades no projeto.

  Detalhes completos devem ser fornecidos/gerados para garantir que tenham uma compreensão completa de todos os aspectos relevantes, incluindo o roteiro, o escopo, as metas, os requisitos e os KPIs.

* **Avaliação de riscos**

  Para evitar surpresas desagradáveis, use a avaliação de risco para identificar e quantificar possíveis riscos, juntamente com seu impacto e probabilidade.

  Isso deve ser feito no início do ciclo de vida do projeto para garantir que todas as vulnerabilidades sejam identificadas e avaliadas. Com base nas conclusões, você pode informar às partes interessadas se os requisitos completos podem ser implementados e, se necessário, se é possível planejar a tomada e o rastreamento de ações apropriadas.

* **Comunicação**

  A comunicação é sempre a chave para o sucesso de qualquer projeto. Comunicar de forma clara e eficiente para garantir que todos estejam:

   * Trabalhar para os mesmos objetivos básicos
   * Da mesma base de informações
   * Com os mesmos canais

* **Início**

  A reunião de abertura é usada para conscientizar que o projeto está começando. É uma boa oportunidade para:

   * Convidar todas as partes interessadas (ou, pelo menos, representantes de grupos).
   * Apresentar os principais fatos sobre o projeto.
   * Responda às perguntas.
   * Certifique-se de que todos tenham a mesma base de conhecimento.
   * Consiga o compromisso de todos os que estarão envolvidos - isso terá que ser conquistado.

      * Ao envolver os principais players (incluindo autores em potencial) no início do projeto, você aumenta as chances de obter seu compromisso com o projeto.

### Preparação de desenvolvimento {#development-preparation}

O planejamento do desenvolvimento é fundamental para garantir que seu projeto seja construído com base em um design sólido por uma equipe que tenha o conhecimento necessário.

#### Etapas {#milestones-2}

* **Equipe de desenvolvimento formada e treinada**

  Antes de iniciar em qualquer projeto, você deve garantir que sua equipe de desenvolvimento tenha a equipe adequada e que todos os membros da equipe sejam treinados para a tarefa em andamento.

* **Arquitetura do conteúdo**

  A arquitetura de conteúdo define e descreve a arquitetura futura do conteúdo; incluindo:

   * A árvore de conteúdo; incluindo ativos
   * Estruturas básicas; incluindo campanhas e assim por diante.
   * Estruturas multisite e multilíngues (MSM, Tradução e assim por diante)
   * Conteúdo de suporte (incluindo tags e conceitos de marcação)
   * Estratégias de reutilização de conteúdo e cache

* **Arquitetura do Sistema**

  A arquitetura do sistema define a visualização conceitual do seu sistema; incluindo (entre outras informações):

   * [Estrutura do sistema](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) para todos os ambientes necessários
   * Subsistemas
   * Sistemas de terceiros
   * Interfaces; hardware, software e interação humana
   * Servidores para cada ambiente; consulte os [Requisitos técnicos](/help/sites-deploying/technical-requirements.md) e as [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md)

   * Processos para cada ambiente; por exemplo, requisitos de implantação e manutenção
   * Atividades de manutenção (Datastore GC, otimização de TarPM e assim por diante)
   * Cache do [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR)
   * [Publicação/Compartilhamento de Autor](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)
   * Desempenho para o lado do cliente (minificação JS, concat, sprites css, número total de solicitações http e outros)

* **Arquitetura de Aplicativo**

  A arquitetura do aplicativo define e descreve o comportamento dos aplicativos propostos.

  Tem como foco:

   * Como eles interagem entre si e com os usuários.
   * Os dados a serem consumidos e produzidos pelos aplicativos, em vez de sua estrutura interna.

  As definições devem abranger:

   * Estrutura básica de código do projeto
   * Artefatos de código (pacotes, pacotes e assim por diante)
   * Detalhamentos dos modelos/componentes e seus relacionamentos
   * Detalhes de alto nível das personalizações necessárias (sobreposições específicas serão exibidas posteriormente)
   * Design de workflows exigidos pela solução (por exemplo, criação de conteúdo, aprovação, publicação, transformações, importações e exportações)
   * Consideração especial para qualquer módulo complexo, como MSM, Commerce, integração de terceiros

* **Integração do sistema**

  A integração do sistema exige que você planeje (e depois implemente):

   * Como todos os subsistemas e [integrações de soluções](/help/sites-administering/integration.md) são reunidos para funcionar como um sistema coerente
   * Como qualquer sistema de terceiros é integrado; juntamente com considerações especiais, como offline/online, do lado do cliente/do lado do navegador ou tratamento de fallover quando um sistema de terceiros estiver inativo

* **Conceito de Teste**

  Antes de iniciar o desenvolvimento, você deve elaborar um conceito detalhado e abrangente de todos os requisitos de [teste](/help/sites-developing/planning.md) para o seu projeto.

  Isso deve incluir (entre outros):

   * Detalhes de todos os testes a serem executados
   * Preparação de qualquer conteúdo necessário para esses testes
   * Informações sobre as ferramentas de ensaio a utilizar
   * Indicação de alto nível de quem estará envolvido em testes; especialmente grupos fora da equipe de controle de qualidade
   * Detalhes da automação de teste; por exemplo, com o modo de Desenvolvedor Selenium ou AEM

* **Design da experiência**

  O Experience Design (XD) envolve a criação da experiência do usuário para sua solução.

  A experiência do usuário deve ser analisada e desenvolvida para os autores e usuários finais do site.

* **Instalação de Suporte**

  Antes do desenvolvimento, todos os processos de suporte necessários para implantar, liberar, testar e relatar problemas devem ser estabelecidos.

  Consulte também o [Portal de Suporte do Adobe](https://experienceleague.adobe.com/?support-solution=General&support-tab=home#support).

### Planejamento e operações de operações {#operations-planning-and-operations}

Da mesma forma, as operações devem ser planejadas corretamente para garantir que você tenha os ambientes necessários, para todos os estágios do ciclo de vida do projeto. Você também precisa dos processos apropriados para mantê-los.

#### Etapas {#milestones-3}

* **Permissões**

  Você precisa planejar e implementar um Conceito de funções e direitos para todos os usuários/grupos que usarão a solução.

  Por exemplo:

   * Uma lista de funções (isto é, grupos) com `read`/ `write` definições de acesso para cada

   * Definição do uso de privilégios que afetam o ambiente de publicação; por exemplo, `replicate`
   * Para usuários com privilégios mínimos, os workflows devem ser definidos
   * Os usuários do grupo `editor` não devem ter direitos de `admin` nem fazer parte do grupo `administrators`

  Para obter mais informações, consulte [Administração e Segurança do Usuário](/help/sites-administering/security.md).

* **Monitoramento e manutenção**

  Monitoramento e manutenção são aspectos fundamentais para garantir a operação perfeita de sua solução assim que ela entrar em funcionamento. Para isso, é necessário definir:

   * O que precisa de monitoramento
   * Tarefas de manutenção, tanto regulares quanto para casos especiais

  Consulte também [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) para obter mais informações.

* **Migração**

  Qualquer conteúdo do sistema herdado deve ser revisado e validado para migração.

* **Plano de Recuperação**

  Certifique-se de que você tenha um plano de recuperação em vigor. Em uma situação de emergência, isso deve estar disponível para proteger o uso de produção do AEM. Isso deve abranger situações como backup, restauração, failover e outras.

### Desenvolvimento {#development}

O desenvolvimento é uma fase crucial que requer mais do que apenas codificação.

#### Etapas {#milestones-4}

* **Ambiente de desenvolvimento**

  Planeje e documente seu ambiente de desenvolvimento, incluindo:

   * Arquitetura
   * [Ferramentas de desenvolvimento](/help/sites-developing/dev-tools.md)

      * Um ambiente típico consiste em:

         * um sistema de rastreamento de problemas, como o Jira
         * um IDE; como o Eclipse
         * uma ferramenta de gerenciamento de compilação, como o Maven
         * uma ferramenta para integração contínua, como o Jenkins
         * uma ferramenta para controle de versão, como GIT/SVN
         * um gerenciador de repositório de artefatos de build; como Archiva/Nexus

   * Integração/dependências de software de terceiros
   * [Integração/dependências da solução](/help/sites-administering/integration.md)
   * Cadência de implantação

* **Testar Sistema**

  Planeje e documente seu ambiente de teste, incluindo:

   * Arquitetura
   * Dependências em builds de desenvolvimento; incluindo builds noturnos
   * Possibilidades ou limitações de teste de integração/dependências de software de terceiros
   * Ferramentas de teste
   * Estratégia de teste automatizada

* **Sistema de produção**

  Planeje e documente seu ambiente de produção, incluindo:

   * Arquitetura
   * Cadência de implantação
   * Integração/dependências de software de terceiros
   * Configuração de segurança
   * Desempenho da linha de base verificado ao executar os [Testes do Dia Difícil](/help/sites-developing/tough-day.md) na configuração de produção
   * Requisitos para testes de desempenho; consulte [Práticas recomendadas para o Quality Assurance](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integração**

  Planeje, documente e teste todos os aspectos do sistema e da [integração da solução](/help/sites-administering/integration.md), incluindo:

   * Uma estratégia de teste automatizada
   * Processos automatizados para [mover aplicativos do desenvolvimento para o teste e, em seguida, para a produção](/help/managing/enterprise-devops.md#code-movement)
   * Processos automatizados para [mover conteúdo da produção para teste e desenvolvimento](/help/managing/enterprise-devops.md#content-movement)

* **Migração**

  Planeje, documente e teste todos os aspectos da migração de conteúdo; incluindo:

   * Arquitetura de conteúdo
   * Estratégia de migração

* **Comunicação**

  Garantir que todos os membros da equipe e o pessoal do projeto estejam atualizados, conforme necessário.

* **Documentação**

  Documentar a solução completamente; incluindo:

   * Manual de operações
   * Qualquer personalização que possa afetar as atualizações
   * Notas de versão

### Desempenho e teste {#performance-and-testing}

Quando o novo aplicativo estiver disponível, ele deverá passar por testes rigorosos de funcionalidade e [desempenho](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Qualquer equipe de ensaio deve ser autorizada a manter-se neutra e a apresentar os resultados dos ensaios.
>
>É responsabilidade do Gerente de projetos avaliar quaisquer implicações dos resultados e decidir sobre a ação apropriada.

#### Etapas {#milestones-5}

* **Teste de Aceitação do Usuário Final**

  [O UAT (teste de aceitação de usuário](/help/sites-developing/acceptance-signoff.md)) é fundamental para garantir que:

   * A solução atende às necessidades do usuário/cliente
   * Os clientes/usuários aceitam a solução (função, design e desempenho)

  Deve haver uma lista de verificação formalizada para a entrega ao cliente; idealmente automatizada e executada à noite com base em um instantâneo. Os resultados devem ser enviados ao gerente do projeto e à equipe de desenvolvimento

* **Testes de Desempenho e Carga**

  Os testes de desempenho e carga são usados para garantir que a solução atenda aos níveis de desempenho necessários, em cargas médias e de pico.

  Para obter mais informações sobre o teste de desempenho, consulte:

   * [Teste de desempenho](/help/sites-deploying/configuring-performance.md)
   * [Como planejar e executar testes](/help/sites-developing/planning.md)

   * [Diretrizes básicas de desempenho](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >Esse processo deve ser continuado durante o uso normal do AEM, mas essas etapas iniciais são as mais importantes.

### Implantação {#rollout}

A implantação do seu novo aplicativo precisa de um planejamento cuidadoso para garantir uma ativação tranquila. Isso inclui confirmar um alto nível de segurança, treinar todos os possíveis usuários e fazer várias simulações para confirmar que todas as questões foram tratadas.

#### Etapas {#milestones-6}

* **Preparação**

  A preparação e o planejamento ajudarão a garantir uma implantação tranquila.

* **Treinamento**

  Assegurar que todo o pessoal envolvido foi treinado.

  Consulte [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) no catálogo de cursos.

* **Administradores treinados**

  Certifique-se de que os administradores da solução tenham:

   * Foi treinado
   * Recebeu o material de treinamento adequado
   * Recebeu a documentação apropriada

* **Usuários Treinados**

  Certifique-se de que os autores tenham:

   * Foi treinado
   * Recebeu o material de treinamento adequado
   * Recebida a documentação apropriada; por exemplo, o Guia do usuário

* **Testes de Penetração**

  Testes de penetração simulam um ataque em um sistema de computador para identificar possíveis falhas de segurança.

* **Testes de Penetração/Segurança**

  Para garantir a segurança de sua solução, realize testes de penetração específicos, juntamente com uma gama mais ampla de testes de segurança.

  Consulte a [Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md) para obter mais detalhes.

### Go Live {#go-live}

Você quer que sua ativação seja a mais suave possível. Novamente, as etapas finais precisam planejar uma execução limpa.

#### Etapas {#milestones-7}

* **Preparação**

  A preparação e o planejamento ajudarão a garantir uma ativação tranquila.

* **Segurança**

  Confirme a segurança da solução para usuários internos e externos e seu conteúdo.

* **Fallback**

  Garantir que todos os sistemas, procedimentos e mecanismos necessários para o fallback estejam em vigor antes da ativação.

* **Suporte**

  Garantir que os serviços de suporte estejam no local e prontos.

* **Transição**

  Planeje e execute a transição para seu ambiente de produção e seus usuários.

* **Implantação**

  Prepare e execute seus testes de fumaça.

## Perfil {#persona}

As listas de verificação são criadas por persona. Essas são as funções com participação significativa no ciclo de vida do projeto.

Há também alguns [outros perfis](#other-persona) envolvidos em tarefas específicas.

### Patrocinador do Projeto {#project-sponsor}

O patrocinador do projeto é:

* Responsável por fornecer/apresentar o business case do projeto.
* Chave para modelar e definir o escopo do projeto; incluindo:

   * a definição e os critérios de sucesso
   * os KPIs principais

* Fornecer os principais marcos com base no roteiro do cliente.

### Gerenciador de Projetos {#project-manager}

O gerente de projeto é:

* Responsável pela entrega geral do projeto com base nos requisitos (por exemplo, escopo, KPIs, critérios e definição de sucesso) fornecidos pelo patrocinador do projeto.
* Responsável por definir o orçamento e os recursos do projeto com base nesse orçamento.
* O principal ponto de comunicação para todos os perfis envolvidos no projeto.

### Arquiteto {#architect}

O arquiteto de soluções:

* É responsável pelo projeto de alto nível da solução e do sistema.
* Ajuda a definir a estratégia de implementação do AEM. Por exemplo, se é necessário implementar uma instalação em cluster, um standby frio ou quando uma rede de entrega de conteúdo (CDN) é necessária.
* Defina também a arquitetura da solução AEM com base nos requisitos do cliente. Isso pode incluir o conceito de funções de usuário (com direitos relacionados), a relação entre modelos e componentes ou quando usar o gerenciamento multisite.

### Analista de negócios {#business-analyst}

O analista de negócios:

* É o principal responsável por coletar e analisar os requisitos de alto nível e, em seguida, transformá-los em especificações:

   * para o gerente de projeto usar ao planejar o desenvolvimento
   * para a equipe de desenvolvimento trabalhar durante a criação e o desenvolvimento.

* Trabalha em conjunto com o cliente para analisar os requisitos. Eles comparam esses itens com:

   * A definição de sucesso.
   * Os critérios para o sucesso.
   * KPIs (baseados em negócios e desempenho).

### Líder de desenvolvimento {#development-lead}

O líder de desenvolvimento:

* É responsável pela entrega técnica do projeto.
* É responsável por selecionar uma metodologia de desenvolvimento que esteja em conformidade com os requisitos do cliente.
* Elabora a estratégia de desenvolvimento:

   * garantir que esteja alinhado aos KPIs de negócios e desempenho
   * tendo em conta os critérios de sucesso e a definição de

* Trabalha em estreita colaboração com o arquiteto (especialmente ao elaborar a estratégia de desenvolvimento do AEM) para definir aspectos como a relação entre modelos e componentes, a estratégia de integração para aplicativos de terceiros e qualquer funcionalidade especializada.

### Líder de qualidade {#quality-lead}

O lead de qualidade:

* É responsável pela qualidade do delivery; garantindo que atenda aos critérios para o sucesso e a quaisquer KPIs definidos pelo cliente.
* Define as métricas de qualidade, se alinha a todas as partes interessadas, elabora os planos de teste e garante que eles sejam executados.
* Cria e entrega relatórios aos participantes do projeto.

### Engenheiro de sistemas {#system-engineer}

O engenheiro de sistema:

* É responsável pela supervisão da infraestrutura do projeto.
* É responsável por:

   * a configuração de ambientes internos de desenvolvimento e teste
   * para corresponder esses sistemas aos sistemas clientes

* Fornece recomendações de hardware, monitora as várias implementações e oferece suporte a operações antes e depois da ativação.

### Líder de segurança {#security-lead}

O líder de segurança:

* É responsável pelo conceito geral de segurança da solução, garantindo que ela esteja alinhada a quaisquer requisitos e políticas do cliente.
* Fornece um conceito de segurança, operações de segurança e recomendações para quaisquer conceitos de segurança baseados em hardware, como zonas e firewalls.

### Outra persona {#other-persona}

* Partes interessadas

   * Pessoas (geralmente da empresa) que têm interesse (participação) no sucesso do projeto. Eles frequentemente contribuem para o orçamento.

* Legal

   * É necessário aconselhamento jurídico na negociação de contratos.

* Treinadores

   * Dependendo da escala e da natureza do projeto, os formadores especializados podem ser utilizados para desenvolver e apresentar sessões de formação para os grupos relevantes.

* Escritores técnicos

   * Dependendo da escala e da natureza do projeto, escritores técnicos especializados podem ser usados para escrever diretrizes e manuais para grupos específicos. Por exemplo, um Manual de manutenção para administradores do sistema ou um Guia do usuário para os autores.

* Administradores do sistema

   * Responsável pelo funcionamento contínuo do sistema.

* Autores e usuários finais

   * As pessoas que usam o sistema para criar e manter o conteúdo do site.

## Documentos necessários e materiais de entrega {#required-documents-and-deliverables}

As listas de verificação abrangem os **Documentos Necessários** e **Entregáveis** para cada marco.

* Não há nenhuma relação 1:1 entre elas; por exemplo, um grupo de documentos necessários pode resultar em uma única entrega.
* Um produto de uma pessoa pode ser um documento necessário para outra pessoa durante o mesmo marco.

### Documentos necessários {#required-documents}

Os **Documentos Necessários** são necessários à pessoa apropriada ao produzir seus materiais de entrega.

Para cada **Documento necessário**, o perfil deve indicar:

* **S/N**: se ele foi recebido.
* **1-3**: uma indicação da qualidade do documento recebido.

### Entregáveis {#deliverables}

Para cada marco, os perfis apropriados são responsáveis por fornecer documentos específicos e, portanto, por assumir suas responsabilidades por um marco específico.

Para cada **Produto**, o perfil deve indicar:

* **S/N**: se ele foi concluído.

Os resultados finais geralmente são usados como **Documentos Necessários** para o marco atual ou posterior.

## Práticas recomendadas relacionadas {#related-best-practices}

Para obter as práticas recomendadas sobre implantação, administração, desenvolvimento ou criação, consulte o seguinte:

* Outras práticas recomendadas e diretrizes relacionadas ao gerenciamento de um projeto do AEM:
   * [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md)
   * [DevOps empresarial &#x200B;](/help/managing/enterprise-devops.md)
   * [Práticas recomendadas de gerenciamento de SEO e URL](/help/managing/seo-and-url-management.md)
   * [AEM e diretrizes de acessibilidade na Web](/help/managing/web-accessibility.md)
   * [Regulamento Geral sobre a Proteção de Dados](/help/managing/data-protection-and-privacy.md)* [Implantação e Manutenção de Práticas Recomendadas](/help/sites-deploying/best-practices.md)
* [Administração de práticas recomendadas](/help/sites-administering/administer-best-practices.md)
* [Desenvolvimento de práticas recomendadas](/help/sites-developing/best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)

## Principais áreas de documentação {#key-documentation-areas}

* Documentação do AEM
Além disso, as seguintes seções da documentação do AEM são de especial interesse (no entanto, esta lista não é exaustiva):

   * [Segurança](/help/sites-developing/security.md)
   * [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
   * [DevOps empresarial &#x200B;](/help/managing/enterprise-devops.md)
   * [Dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md)
   * Conceitos do AEM:

      * [Desenvolvimento - noções básicas](/help/sites-developing/the-basics.md)
      * [Conceitos do MSM](/help/sites-administering/msm.md)
      * [Linguagem de Modelo do HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR)

* Documentação relacionada

   * Adobe Experience Cloud - [Planejamento para a Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/core-services.html)
