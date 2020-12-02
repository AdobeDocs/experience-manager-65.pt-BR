---
title: Gerenciamento de projetos - Lista de verificação de práticas recomendadas
seo-title: Gerenciamento de projetos - Lista de verificação de práticas recomendadas
description: O gerenciamento de um projeto para implementar a Adobe Experience Manager (AEM) requer planejamento e compreensão. As Listas de verificação do projeto são destinadas a um conjunto de práticas recomendadas para o delivery do projeto. Elas o orientam por todas as fases do ciclo de vida do projeto e fornecem um monitoramento de alto nível do seu status atual.
seo-description: O gerenciamento de um projeto para implementar a Adobe Experience Manager (AEM) requer planejamento e compreensão. As Listas de verificação do projeto são destinadas a um conjunto de práticas recomendadas para o delivery do projeto. Elas o orientam por todas as fases do ciclo de vida do projeto e fornecem um monitoramento de alto nível do seu status atual.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

---


# Gerenciamento de projetos - Lista de verificação de práticas recomendadas{#managing-projects-best-practices-checklist}

O gerenciamento de um projeto para implementar a Adobe Experience Manager (AEM) requer planejamento e compreensão para garantir que você esteja ciente dos problemas e das decisões (relacionadas) que você precisa tomar (antes e durante a implementação do projeto).

Para ajudá-lo, as práticas recomendadas consistem em:

* Uma [lista de verificação interativa](/help/managing/best-practices-checklist.md) que permite rastrear e monitorar seu progresso com essas práticas recomendadas.

   * Define entradas e resultados de acordo com fase, marco e persona.
   * Fornece visões gerais automatizadas (qualidade, integridade e integridade) para indicar progresso e integridade do projeto.

* A documentação, baseada diretamente na [checklist](/help/managing/best-practices-checklist.md), detalha o seguinte:

   * [Análise do ](#projectheartbeat) Heartbeatanalysis do Project.
   * [Status por ](#status-by-role) Roleoverview.
   * [Fases e marcos](#phases-and-milestones).
   * [Principais ](#persona) personalidades e o seu envolvimento em todas as fases (relevantes).
   * Um [Glossário](/help/managing/best-practices-glossary.md) dos [Documentos e materiais de entrega necessários](#required-documents-and-deliverables).

* [Outros ](/help/managing/best-practices-further-reference.md) referenciadores para fornecer mais detalhes sobre áreas específicas.

## Painel do Project Heartbeat {#project-heartbeat-dashboard}

A planilha **Project Heartbeat** fornece uma visão geral gráfica das métricas críticas para o seu projeto:

* **Qualidade da fase**

   * Indica a qualidade de [Documentos obrigatórios e materiais de entrega](#required-documents-and-deliverables) no projeto.

* **Fase de saúde**

   * Um indicador de status de alto nível para o seu projeto; útil para destacar áreas que podem estar em risco.

* **Complexidade da fase**

   * Em qualquer momento durante o projeto, isso indica o quanto já foi concluído para cada fase do projeto.

## Status por função {#status-by-role}

A planilha **Status por Função** mostra o detalhamento de [**Estado de Funcionamento**, **Qualidade** e **Integridade**](#projectheartbeat) por **[Fase](#phases-and-milestones)** e **[Pessoa](#persona)**.

## Fases e marcos {#phases-and-milestones}

O plano de projeto é dividido em fases distintas (de alto nível).

Cada fase contém seus próprios marcos. Para cada [persona](#persona) (ou função), os marcos relevantes são listados, juntamente com os documentos necessários para produzir os resultados definidos.

>[!NOTE]
>
>Não há uma relação 1:1 direta entre os documentos individuais obrigatórios e os materiais de entrega.

### Preparação {#preparation}

A preparação de seu projeto é a base de todo o projeto. É necessário definir os principais requisitos junto com metas e expectativas claras para:

* **Razão comercial**

   * As razões fundamentais e a justificação para a realização do projeto.

* **Âmbito e Programação**

   * Deve ser disponibilizado um âmbito básico e um calendário aproximado para definir o que é necessário e dentro de que prazo; se isso ajudar a esclarecer a situação, você também pode definir o que está fora do escopo.

A maneira como você prepara, planeja e executa seu projeto e implementa sua solução será afetada pelas restrições que você está operando, por exemplo, orçamento fixo, linha do tempo fixa, quantidade de conteúdo, qualidade necessária.

Como sempre, o ajuste de qualquer um dos fatores terá impacto nos outros. Por exemplo, reduzir o tempo, mas exigir o mesmo nível de qualidade provavelmente aumentará o preço e reduzirá a quantidade de conteúdo que você pode atender. O orçamento é muitas vezes um fator fundamental, pelo que essas relações não podem ser esquecidas.

Os Quatro Fatores:

![project_fases_quatro fases](assets/projectphases_fourphases.png)

#### Marcos {#milestones}

* **Validação**

   Nesta fase, é necessário validar e confirmar os objetivos do projeto; por exemplo:

   * O que você deseja obter/fornecer?
   * Quem beneficiará?
   * Qual é o âmbito?

      * Se isso ajudar a esclarecer a situação, você também pode definir o que está fora do escopo.
   * Como você definirá o sucesso?
   * Como você vai medir o sucesso?
   * Quais são os requisitos, comerciais e técnicos?
   * Há sistemas herdados a serem substituídos e, em caso afirmativo, há dados a serem migrados?
   * Quem estará envolvido?
   * Como você vai medir o progresso?
   * Com que frequência você irá analisar o progresso durante a vida do projeto?


* **Orçamento**

   Antes de start de qualquer projeto, você precisa de uma estimativa confiável e realista do custo de implementação:

   * Use as informações do marco de validação como base para as estimativas.
   * Seja realista em suas estimativas.
   * Considere e respeite quaisquer diretrizes, processos ou restrições que o cliente possa estar sujeito.
   * Considere os processos de contingência e de revisão caso seja necessária uma revisão ou um aperfeiçoamento do orçamento numa fase posterior.
   * Lembre-se de que os custos vêm de muitas formas. Compras, utilização de recursos e taxas, entre outros.

### Planejamento {#planning}

O planejamento do projeto consolida a preparação. Neste caso, é necessário start a conversão das metas e expectativas num roteiro bem definido, que consiste em tarefas concretas, vinculadas por uma comunicação clara, com revisões rigorosas para medir o progresso.

#### Marcos {#milestones-1}

* **Entrega**

   Uma entrega limpa garante que a pessoa/grupos apropriados estejam cientes de suas responsabilidades dentro do projeto.

   Devem ser fornecidos/gerados todos os pormenores para garantir que têm um entendimento completo de todos os aspectos relevantes, incluindo o roteiro, o âmbito, os objetivos, os requisitos e os KPI.

* **Avaliação do risco**

   Para evitar surpresas desagradáveis, utilize a avaliação de risco para identificar e quantificar quaisquer riscos potenciais, juntamente com o seu impacto e probabilidade.

   Tal deve ser feito no início do ciclo de vida do projeto, a fim de garantir a identificação e avaliação das eventuais vulnerabilidades. Com base nas conclusões, você pode informar as partes interessadas sobre se os requisitos completos podem ser implementados e, se necessário, se é possível planejar ações apropriadas a serem tomadas e rastreadas.

* **Comunicação**

   A comunicação é sempre a chave para o sucesso de qualquer projeto. Você precisa se comunicar de forma clara e eficiente para garantir que todos sejam:

   * Trabalhar para os mesmos objetivos básicos
   * Da mesma base de informações
   * Com os mesmos canais

* **Desligar**

   A reunião Kick Off é usada para conscientizar que o projeto está sendo iniciado. É uma boa oportunidade para:

   * Convidar todas as partes interessadas (ou, pelo menos, representantes de grupos).
   * Apresente os principais fatos sobre o projeto.
   * Responda perguntas.
   * Garantir que todos tenham a mesma base de conhecimento.
   * Assumir o compromisso de todos os que irão participar - isso terá de ser conseguido.

      * Ao envolver os principais jogadores (incluindo os futuros autores) no próprio start do projeto, você aumenta suas chances de se comprometerem com o projeto.

### Preparação para desenvolvimento {#development-preparation}

O planejamento do desenvolvimento é fundamental para garantir que seu projeto seja construído com base em um design sólido por uma equipe que tenha o conhecimento necessário.

#### Marcos {#milestones-2}

* **Equipe de desenvolvimento com pessoal e treinamento**

   Antes de iniciar qualquer projeto, você deve garantir que sua equipe de desenvolvimento tenha a equipe apropriada e que todos os membros da equipe sejam treinados para a tarefa em mãos.

* **Arquitetura de conteúdo**

   A arquitetura de conteúdo define e descreve a arquitetura futura do conteúdo; incluindo:

   * A árvore de conteúdo; incluindo ativos
   * Estruturas de base; incluindo campanhas, etc.
   * Estruturas de vários sites e vários idiomas (MSM, Tradução, etc.)
   * Conteúdo de suporte (incluindo tags e conceitos de marcação)
   * Estratégias de armazenamento em cache e reutilização de conteúdo

* **Arquitetura do sistema**

   A arquitetura do sistema define a visualização conceitual do seu sistema; incluindo (entre outras informações):

   * [Estrutura ](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) do sistema para todos os ambientes necessários
   * Subsistemas
   * Sistemas de terceiros
   * Interfaces; hardware, software e interação humana
   * Servidores para cada ambiente; consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md) e [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md)

   * Processos para cada ambiente; por exemplo, requisitos de implantação e manutenção
   * Atividades de manutenção (armazenamento de dados GC, otimização TarPM etc.)
   * [](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)Armazenamento em cache do Dispatcher
   * [](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) ClusteringPublish/Authorshare
   * Desempenho para o cliente (minify JS, concat, sprites css, número total de solicitações http e outras)

* **Arquitetura de aplicativos**

   A arquitetura do aplicativo define e descreve o comportamento dos aplicativos propostos.

   O foco é:

   * Como eles interagirão entre si e com os usuários.
   * Os dados a serem consumidos e produzidos pelas aplicações, e não pela sua estrutura interna.

   As definições devem abranger:

   * Estrutura básica do código para o projeto
   * Artefatos de código (pacotes, pacotes etc.)
   * Detalhamentos dos modelos/componentes e suas relações
   * Detalhes de alto nível das personalizações necessárias (sobreposições específicas serão seguidas posteriormente)
   * Design de workflows exigidos pela solução (por exemplo, criação de conteúdo, aprovação, publicação, transformações, importações, exportações etc.)
   * Consideração especial para qualquer módulo complexo, como MSM, Commerce, integração de terceiros


* **Integração do sistema**

   A integração do sistema exige que você planeje (em seguida, implemente):

   * Como todos os sub-sistemas e [integrações de solução](/help/sites-administering/integration.md) serão reunidos para operar como um sistema coerente
   * Como serão integrados quaisquer sistemas de terceiros; juntamente com quaisquer considerações especiais, como offline/online, gerenciamento no lado do cliente/navegador ou falha quando um sistema de terceiros está inativo

* **Conceito de teste**

   Antes de iniciar o desenvolvimento, você deve elaborar um conceito abrangente e detalhado de todos os [requisitos de teste](/help/sites-developing/planning.md) do seu projeto.

   Isso deve incluir (entre outros):

   * Pormenores de todos os ensaios a efetuar
   * Preparação de qualquer conteúdo necessário para esses ensaios
   * Informação sobre quaisquer ferramentas de ensaio a utilizar
   * Indicação de alto nível de quem participará nos testes; especialmente grupos fora da equipe de controle de qualidade
   * Pormenores da automatização dos ensaios; por exemplo, com o modo Selenium ou AEM Developer

* **Experience Design**

   O Experience Design (XD) envolve a criação da experiência do usuário para a sua solução.

   A experiência do usuário deve ser analisada e desenvolvida tanto para seus autores quanto para os usuários finais de seu site.

* **Configuração de suporte**

   Antes do desenvolvimento, todos os processos de suporte, necessários para implantar, liberar, testar e relatar problemas, devem ser definidos.

   Consulte também o [Portal de suporte do Adobe](https://helpx.adobe.com/br/marketing-cloud/contact-support.html).

### Operações e Planejamento {#operations-planning-and-operations}

Da mesma forma, as operações devem ser adequadamente planejadas para garantir que você tenha os ambientes necessários - para todas as etapas do ciclo de vida do projeto. Você também precisa dos processos apropriados para mantê-los.

#### Marcos {#milestones-3}

* **Permissões**

   Você precisa planejar e implementar um Conceito de funções e direitos para todos os usuários/grupos que usarão a solução.

   Por exemplo:

   * Uma lista de funções (ou seja, grupos) com `read`/ `write` definições de acesso para cada

   * Definição do uso de privilégios que afetam o ambiente de publicação; por exemplo, `replicate`
   * Para usuários com privilégios mínimos, os workflows devem ser definidos
   * Os usuários do grupo `editor` não devem ter `admin` direitos nem fazer parte do grupo `administrators`

   Para obter mais informações, consulte [Administração e segurança do usuário](/help/sites-administering/security.md).

* **Monitoramento e manutenção**

   O monitoramento e a manutenção são aspectos fundamentais para garantir o funcionamento regular da solução após sua entrada em funcionamento. Para isso, é necessário definir:

   * O que precisa de monitoramento
   * Tarefas de manutenção; regular e para casos especiais

   Consulte também [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) para obter mais informações.

* **Migração**

   Qualquer conteúdo do sistema herdado deve ser revisado e validado para migração.

* **Plano de recuperação**

   Verifique se você tem um plano de recuperação em vigor. Numa situação de emergência, tal deve estar disponível para garantir a utilização da AEM na produção. Isso deve abranger situações como backup, restauração, falhas e outras.

### Desenvolvimento {#development}

O desenvolvimento é uma fase crucial que requer mais do que apenas codificação.

#### Marcos {#milestones-4}

* **Ambiente de desenvolvimento**

   Planeje e documento seu ambiente de desenvolvimento, incluindo:

   * Arquitetura
   * [Ferramentas de desenvolvimento](/help/sites-developing/dev-tools.md)

      * Um ambiente comum consiste em:

         * Um sistema de controlo de emissões; como Jira
         * um IDE; como o Eclipse
         * um instrumento de gestão de edifícios; como Maven
         * um instrumento de integração contínua; como Jenkins
         * uma ferramenta para o controlo de versão; como GIT/SVN
         * um gestor de repositório de artefatos de construção; como Archiva/Nexus
   * Integração/dependências de software de terceiros
   * [Integração/dependências da solução](/help/sites-administering/integration.md)
   * Carência de implantação


* **Sistema de teste**

   Planeje e documento seu ambiente de teste, incluindo:

   * Arquitetura
   * Dependências dos edifícios de desenvolvimento; incluindo edifícios noturnos
   * As possibilidades ou limitações de testar a integração/dependências de software de terceiros
   * Ferramentas de teste
   * Estratégia de teste automatizada

* **Sistema de produção**

   Planeje e documento seu ambiente de produção, incluindo:

   * Arquitetura
   * Carência de implantação
   * Integração/dependências de software de terceiros
   * Configuração de segurança
   * Desempenho da linha de base verificado com a execução de [Testes de Dia Difícil](/help/sites-developing/tough-day.md) na configuração de produção
   * Requisitos aplicáveis aos ensaios de desempenho; consulte [Práticas recomendadas para o controle de qualidade](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integração**

   Planeje, documento e teste todos os aspectos do sistema e [integração da solução](/help/sites-administering/integration.md), incluindo:

   * Uma estratégia de teste automatizado
   * Processos automatizados para [mover aplicativos do desenvolvimento para o teste e, em seguida, produção](/help/managing/enterprise-devops.md#code-movement)
   * Processos automatizados para [mover conteúdo da produção para teste e desenvolvimento](/help/managing/enterprise-devops.md#content-movement)

* **Migração**

   Planeje, documento e teste todos os aspectos da migração de conteúdo; incluindo:

   * Arquitetura de conteúdo
   * Estratégia de migração

* **Comunicação**

   Certifique-se de que todos os membros da equipe e pessoal do projeto estejam atualizados, conforme necessário.

* **Documentação**

   Documento total da solução; incluindo:

   * Manual de Operações
   * Quaisquer personalizações que possam afetar as atualizações
   * Notas de versão

### Desempenho e teste {#performance-and-testing}

Quando o novo aplicativo estiver disponível, ele precisará passar por testes rigorosos, tanto para funcionalidade quanto para [desempenho](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Qualquer equipe de ensaio deve poder manter-se neutra e apresentar os resultados dos ensaios.
>
>Cabe ao gestor do projeto avaliar as implicações dos resultados e decidir as medidas adequadas.

#### Marcos {#milestones-5}

* **Teste de aceitação do usuário final**

   [O teste](/help/sites-developing/acceptance-signoff.md)  de aceitação do usuário (UAT) é crucial para garantir que:

   * A solução atende aos requisitos do usuário/cliente
   * O cliente/usuários aceitam a solução (função, design e desempenho)

   Deve haver uma lista de verificação formalizada para entrega ao cliente; idealmente automatizado e executado à noite com base em um instantâneo. Os resultados devem ser enviados ao gestor do projeto e à equipe de desenvolvimento

* **Testes de desempenho e carga**

   Os testes de desempenho e de carga são usados para garantir que a solução atenda aos níveis de desempenho necessários, em média e cargas máximas.

   Para obter mais informações sobre testes de desempenho, consulte:

   * [Teste de desempenho](/help/sites-deploying/configuring-performance.md)
   * [Como planejar e executar testes](/help/sites-developing/planning.md)

   * [Diretrizes básicas de desempenho](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >Este processo terá de ser prosseguido durante a utilização normal de AEM, mas estas fases iniciais são as mais cruciais.

### Implantação {#rollout}

A implantação do novo aplicativo precisa de planejamento cuidadoso para garantir um Go Live suave. Isso inclui confirmar um alto nível de segurança, treinar todos os possíveis usuários e fazer várias passagens a seco para confirmar que todas as questões foram tratadas.

#### Marcos {#milestones-6}

* **Preparação**

   A preparação e o planejamento ajudarão a garantir uma implementação sem problemas.

* **Treinamento**

   Garantir que toda a equipe envolvida tenha recebido formação.

   Consulte [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) no catálogo de cursos.

* **Administradores treinados**

   Certifique-se de que seus administradores de solução tenham:

   * Foi treinado
   * Recebido o material de treinamento adequado
   * Recebida a documentação apropriada

* **Usuários treinados**

   Certifique-se de que seus autores tenham:

   * Foi treinado
   * Recebido o material de treinamento adequado
   * Recebida a documentação apropriada; por exemplo, o Guia do Usuário

* **Ensaios de penetração**

   Os testes de penetração simulam um ataque em um sistema de computador para identificar possíveis deficiências de segurança.

* **Ensaios de Penetração/Segurança**

   Para garantir a segurança da sua solução, execute testes de penetração específicos, juntamente com uma grande variedade de testes de segurança.

   Consulte a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) para obter mais detalhes.

### Go Live {#go-live}

Você quer que seu Go Live seja o mais suave possível. Novamente, as etapas finais precisam de planejamento para execução limpa.

#### Marcos {#milestones-7}

* **Preparação**

   A preparação e o planejamento ajudarão a garantir uma vida útil suave.

* **Segurança**

   Confirme a segurança de sua solução para usuários internos e externos e seu conteúdo.

* **Fallback**

   Certifique-se de que todos os sistemas, procedimentos e mecanismos necessários para o fallback estejam implementados antes de entrar em funcionamento.

* **Suporte**

   Verifique se os serviços de suporte estão no local e prontos.

* **Transição**

   Planeje e execute a transição para o ambiente de produção e os usuários.

* **Reversão**

   Prepare e execute seus testes de fumaça.

## Persona {#persona}

As listas de verificação são projetadas por pessoas. Estes são os papéis com um envolvimento significativo no ciclo de vida do projeto.

Há também algumas [outras personas](#other-persona) envolvidas em tarefas específicas.

### Patrocinador do projeto {#project-sponsor}

O patrocinador do projeto é:

* Responsável por fornecer/apresentar o business case do projeto.
* Chave para definir e definir o âmbito do projeto; incluindo:

   * a definição e os critérios de sucesso
   * os principais KPIs

* Forneça os principais marcos com base no roteiro do cliente.

### Gerenciador de projetos {#project-manager}

O gerente do projeto é:

* Responsável pelo delivery global do projeto com base nos requisitos (por exemplo, âmbito, KPI, critérios de sucesso e definição) fornecidos pelo patrocinador do projeto.
* Responsável pela definição do orçamento e pelo financiamento do projeto com base nesse orçamento.
* O principal ponto de comunicação para todas as pessoas envolvidas no projeto.

### Arquiteto {#architect}

O arquiteto da solução:

* É responsável pelo design de alto nível da solução e do sistema.
* Ajuda a definir a estratégia de implementação para AEM. Por exemplo, se é necessário implementar uma instalação em cluster, ou um modo de espera frio, ou quando uma rede de delivery de conteúdo (CDN) é necessária.
* Defina também a arquitetura da solução AEM com base nos requisitos do cliente. Isso pode incluir o conceito de funções de usuário (com direitos relacionados), a relação entre modelos e componentes ou quando usar o gerenciamento de vários sites.

### Analista de negócios {#business-analyst}

O analista de negócios:

* É o principal responsável por coletar e analisar os requisitos de alto nível e depois transformá-los em especificações:

   * para que o gerente do projeto use ao planejar o desenvolvimento
   * para a equipe de desenvolvimento trabalhar durante o projeto e desenvolvimento.

* Trabalha em conjunto com o cliente para analisar os requisitos. Eles combinam com:

   * A definição de sucesso.
   * Os critérios para o sucesso.
   * KPIs (baseados em negócios e desempenho).

### Lead de desenvolvimento {#development-lead}

O líder em desenvolvimento:

* É responsável pelo delivery técnico do projeto.
* É responsável por selecionar uma metodologia de desenvolvimento que esteja em conformidade com os requisitos do cliente.
* Elaborar a estratégia de desenvolvimento:

   * garantindo que ele esteja alinhado aos KPIs de negócios e desempenho
   * tendo em conta os critérios de sucesso e a definição

* Trabalha em conjunto com o arquiteto (especialmente ao elaborar a estratégia de desenvolvimento para AEM) para definir aspectos como a relação entre modelos e componentes, a estratégia de integração para aplicativos de terceiros e qualquer funcionalidade especializada.

### Chumbo de qualidade {#quality-lead}

O líder de qualidade:

* É responsável pela qualidade do delivery; assegurar que cumpre os critérios de sucesso e quaisquer KPI definidos pelo cliente.
* Define as métricas de qualidade, alinhadas com todos os participantes, elabora os planos de teste e garante que eles sejam executados.
* Cria e entrega relatórios aos participantes do projeto.

### Engenheiro de sistema {#system-engineer}

O engenheiro de sistemas:

* É responsável pela supervisão da infraestrutura do projeto.
* É responsável por:

   * a configuração de ambientes internos de desenvolvimento e teste
   * para corresponder esses sistemas aos sistemas clientes

* Fornece recomendações de hardware, monitora as várias implementações e fornece suporte às operações antes e depois de entrar em funcionamento.

### líder de segurança {#security-lead}

O líder em segurança:

* É responsável pelo conceito geral de segurança da solução, garantindo que ela esteja alinhada a quaisquer requisitos e políticas do cliente.
* Oferece um conceito de segurança, operações de segurança e recomendações para quaisquer conceitos de segurança baseados em hardware; como zonas e firewalls.

### Outra Pessoa {#other-persona}

* Partes interessadas

   * Pessoas (muitas vezes da empresa) que têm interesse (participação) no sucesso do projeto. Elas contribuem muitas vezes para o orçamento.

* Legal

   * Na negociação dos contratos é necessário aconselhamento jurídico.

* Formadores

   * Em função da dimensão e da natureza do projeto, podem ser utilizados formadores especializados para desenvolver e apresentar sessões de formação para os grupos relevantes.

* Escritores técnicos

   * Dependendo da dimensão e da natureza do projeto, os escritores técnicos especializados podem ser utilizados para escrever orientações e manuais para grupos específicos; Por exemplo, um manual de manutenção para administradores de sistema ou um guia do usuário para os autores.

* Administradores de sistema

   * Responsável pelo funcionamento contínuo do sistema.

* Autores e usuários finais

   * As pessoas que usarão o sistema para criar e manter o conteúdo de seu site.

## Documentos obrigatórios e materiais de entrega {#required-documents-and-deliverables}

As listas de verificação abrangem os **Documentos obrigatórios** e **Materiais de entrega** para cada marco.

* Não existe relação 1:1 entre estes. por exemplo, um grupo de documentos obrigatórios pode resultar em um único material para distribuição.
* Uma entrega de uma pessoa pode ser um documento obrigatório para outra pessoa durante o mesmo marco.

### Documentos obrigatórios {#required-documents}

Os **Documentos obrigatórios** são necessários para a pessoa apropriada ao produzir seus resultados.

Para cada **Documento obrigatório** a pessoa deve indicar:

* **S/N**: se foi recebido.
* **1-3**: Uma indicação da qualidade do documento recebido.

### Produtos {#deliverables}

Para cada marco, a pessoa adequada é responsável por fornecer documentos específicos e, portanto, assumir suas responsabilidades por um marco específico.

Para cada **Material a Entregar** a pessoa deve indicar:

* **S/N**: se foi concluído.

Os resultados são frequentemente usados como **Documentos obrigatórios** para o marco atual ou posterior.

## Práticas recomendadas relacionadas {#related-best-practices}

Para obter as práticas recomendadas de implantação, administração, desenvolvimento ou criação, consulte:

* Outras práticas recomendadas e diretrizes relacionadas ao Gerenciamento de um projeto AEM:
   * [Diretrizes de dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md) 
   * [DevOps empresarial](/help/managing/enterprise-devops.md)
   * [Práticas recomendadas de gerenciamento de SEO e URL](/help/managing/seo-and-url-management.md)
   * [AEM e as diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md)
   * [Regulamento](/help/managing/data-protection-and-privacy.md) geral de proteção de dados*  [Implementação e manutenção das práticas recomendadas](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas de administração](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de desenvolvimento](/help/sites-developing/best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)

## Principais áreas de documentação {#key-documentation-areas}

* Documentação AEM
Além disso, as seguintes seções da documentação AEM são de especial interesse (no entanto, esta lista não é exaustiva):

   * [Segurança](/help/sites-developing/security.md)
   * [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
   * [DevOps empresarial](/help/managing/enterprise-devops.md)
   * [Dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md)
   * Conceitos de AEM:

      * [Desenvolvimento - noções básicas](/help/sites-developing/the-basics.md)
      * [Conceitos de MSM](/help/sites-administering/msm.md)
      * [Linguagem de modelo HTML (HTL)](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html)

* Documentação relacionada

   * Adobe Experience Cloud - [Planejamento para o Adobe Experience Cloud](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)

