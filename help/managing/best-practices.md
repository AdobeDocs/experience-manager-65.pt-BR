---
title: Gerenciamento de projetos - Lista de verificação de práticas recomendadas
seo-title: Managing Projects - Best Practices Checklist
description: O gerenciamento de um projeto para implementar o Adobe Experience Manager (AEM) requer planejamento e compreensão. As Listas de verificação de projeto servem como um conjunto de práticas recomendadas para a entrega do projeto. Elas orientam você em todas as fases do ciclo de vida do projeto e fornecem um monitoramento de alto nível do seu status atual.
seo-description: Managing a project to implement Adobe Experience Manager (AEM) requires planning and understanding. The Project Checklists are intended as a set of best practices for project delivery. They guide you through all phases of the project life cycle and provide high level monitoring of your current status.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---

# Gerenciamento de projetos - Lista de verificação de práticas recomendadas{#managing-projects-best-practices-checklist}

O gerenciamento de um projeto para implementar o Adobe Experience Manager (AEM) requer planejamento e compreensão para garantir que você esteja ciente dos problemas e das decisões (relacionadas) que devem ser feitas (antes e durante a implementação do projeto).

Para ajudá-lo, as práticas recomendadas consistem em:

* Um [lista de verificação interativa](/help/managing/best-practices-checklist.md) Isso permite rastrear e monitorar o progresso com essas práticas recomendadas.

   * Define entradas e resultados de acordo com fase, marco e persona.
   * Fornece visões gerais automatizadas (qualidade, integridade e integridade) para indicar progresso e integridade do projeto.

* Documentação, baseada diretamente no [lista de verificação](/help/managing/best-practices-checklist.md), que detalha o seguinte:

   * [Heartbeat de projeto](#projectheartbeat) análise.
   * [Status por função](#status-by-role) visão geral.
   * [Fases e marcos](#phases-and-milestones).
   * [Key Persona](#persona) e o seu envolvimento em todas as fases (relevantes).
   * A [Glossário](/help/managing/best-practices-glossary.md) do [Documentos e Entregas Necessários](#required-documents-and-deliverables).

* [Referência adicional](/help/managing/best-practices-further-reference.md) material para fornecer mais detalhes sobre áreas específicas.

## Painel do Heartbeat do projeto {#project-heartbeat-dashboard}

O **Heartbeat de projeto** A planilha fornece uma visão geral gráfica das métricas críticas para o seu projeto:

* **Qualidade da Fase**

   * Indica a qualidade da [Documentos e Entregas Necessários](#required-documents-and-deliverables) no projeto.

* **Integridade da Fase**

   * Um indicador de status de alto nível para o seu projeto; útil para destacar áreas que podem estar em risco.

* **Integridade da Fase**

   * Em qualquer momento durante o projeto, isso indica o quanto já foi concluído em cada fase do projeto.

## Status por função {#status-by-role}

O **Status por função** a planilha mostra o detalhamento detalhado de [**Saúde**, **Qualidade** e **Integridade**](#projectheartbeat) por **[Fase](#phases-and-milestones)** e **[Persona](#persona)**.

## Fases e marcos {#phases-and-milestones}

O plano de projeto é dividido em fases distintas (de alto nível).

Cada fase contém seus próprios marcos. Para cada [persona](#persona) (ou função), os marcos relevantes são listados, juntamente com os documentos necessários para produzir os resultados finais definidos.

>[!NOTE]
>
>Não há uma relação direta 1:1 entre os documentos individuais necessários e os deliveries.

### Preparação {#preparation}

A preparação de seu projeto é a base de todo o projeto. Você precisa definir requisitos-chave juntamente com metas e expectativas claras para:

* **Razão Comercial**

   * As razões fundamentais e a justificação para a realização do projeto.

* **Escopo e Programação**

   * Deve ser disponibilizado um âmbito básico e um calendário aproximado para definir o que é necessário e dentro de que prazo; se isso ajudar a esclarecer a situação, você também pode definir o que está fora do escopo.

A maneira como você prepara, planeja e executa seu projeto e implementa sua solução será afetada pelas restrições que você está operando, por exemplo, orçamento fixo, linha do tempo fixo, quantidade de conteúdo, qualidade necessária.

Como sempre, o ajuste de qualquer um dos fatores afetará os outros. Por exemplo, reduzir o tempo, mas exigir o mesmo nível de qualidade provavelmente aumentará o preço e, ao mesmo tempo, reduzirá a quantidade de conteúdo que pode ser atendido. O orçamento é frequentemente um fator fundamental, pelo que estas relações não podem ser esquecidas.

Os Quatro Fatores:

![projetosfases_quatro](assets/projectphases_fourphases.png)

#### Marcos {#milestones}

* **Validação**

   Nesta fase, é necessário validar e confirmar os objetivos do projeto; por exemplo:

   * O que você deseja obter/fornecer?
   * Quem vai beneficiar?
   * Qual é o âmbito de aplicação?

      * Se ajudar a esclarecer a situação, também pode definir o que está fora do âmbito de aplicação.
   * Como você definirá o sucesso?
   * Como você vai medir o sucesso?
   * Quais são os requisitos, os negócios e os requisitos técnicos?
   * Há sistemas herdados a serem substituídos e, em caso afirmativo, há dados a serem migrados?
   * Quem estará envolvido?
   * Como você irá medir o progresso?
   * Com que frequência você analisará os progressos durante a vida do projeto?


* **Orçamento**

   Antes de iniciar qualquer projeto, você precisa de uma estimativa confiável e realista do custo de implementação:

   * Use informações do marco de validação como base para as estimativas.
   * Seja realista em suas estimativas.
   * Considere e respeite quaisquer diretrizes, processos ou restrições do cliente que ele possa estar sujeito.
   * Considerar os processos de contingência e de revisão caso seja necessária uma revisão ou um aperfeiçoamento do orçamento numa fase posterior.
   * Lembre-se de que os custos vêm de muitas formas; compras, utilização de recursos e taxas, entre outros.

### Planejamento {#planning}

Planejamento do projeto consolida a preparação. Neste ponto, é necessário começar a converter os objetivos e as expectativas num roteiro bem definido, que consista em tarefas concretas, vinculadas por uma comunicação clara, com revisões rigorosas para medir o progresso.

#### Marcos {#milestones-1}

* **Transmissão**

   Uma entrega limpa garante que as pessoas/grupos apropriados estejam cientes de suas responsabilidades dentro do projeto.

   Devem ser fornecidos/gerados todos os pormenores para garantir a sua plena compreensão de todos os aspectos relevantes, incluindo o roteiro, o âmbito de aplicação, os objetivos, os requisitos e os KPI.

* **Avaliação de riscos**

   Para evitar surpresas desagradáveis, utilize a avaliação de risco para identificar e quantificar quaisquer riscos potenciais juntamente com o seu impacto e probabilidade.

   Tal deve ser feito no início do ciclo de vida do projeto, a fim de assegurar que quaisquer vulnerabilidades sejam identificadas e avaliadas. Com base nos resultados, você pode informar os seus participantes sobre se os requisitos completos podem ser implementados e, se necessário, se é possível planejar ações apropriadas a serem tomadas e rastreadas.

* **Comunicação**

   A comunicação é sempre fundamental para o sucesso de qualquer projeto. Você precisa se comunicar de forma clara e eficiente para garantir que todos sejam:

   * Trabalhar para os mesmos objetivos básicos
   * Da mesma base de informações
   * Com os mesmos canais

* **Desligar**

   O encontro Kick Off é usado para conscientizar que o projeto está iniciando. É uma boa oportunidade para:

   * Convidar todas as partes interessadas (ou, pelo menos, representantes de grupos).
   * Apresente fatos-chave sobre o projeto.
   * Responda perguntas.
   * Garantir que todos tenham a mesma base de conhecimento.
   * Obtenha o compromisso de todos os que irão participar - isso terá de ser ganho.

      * Ao envolver os principais players (incluindo autores em potencial) no início do projeto, você aumenta suas chances de conseguir seu compromisso com o projeto.

### Preparação para o desenvolvimento {#development-preparation}

O planejamento do desenvolvimento é fundamental para garantir que seu projeto seja construído com base em um projeto sólido por uma equipe que tenha o conhecimento necessário.

#### Marcos {#milestones-2}

* **Equipe de desenvolvimento com equipe e treinamento**

   Antes de iniciar qualquer projeto, você deve garantir que sua equipe de desenvolvimento tenha a equipe adequada e que todos os membros da equipe sejam treinados para a tarefa em andamento.

* **Arquitetura de conteúdo**

   A arquitetura de conteúdo define e descreve a arquitetura futura do conteúdo; incluindo:

   * A árvore de conteúdo; incluindo ativos
   * Estruturas de base; incluindo campanhas, etc.
   * Estruturas de vários sites e vários idiomas (MSM, Tradução, etc.)
   * Conteúdo compatível (incluindo tags e conceitos de marcação)
   * Armazenamento em cache e estratégias de reutilização de conteúdo

* **Arquitetura do sistema**

   A arquitetura do sistema define a visão conceitual do sistema; incluindo (entre outras informações):

   * [Estrutura do sistema](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) para todos os ambientes necessários
   * Subsistemas
   * Sistemas de terceiros
   * Interfaces; hardware, software e interação humana
   * Servidores para cada ambiente; consulte o [Requisitos técnicos](/help/sites-deploying/technical-requirements.md) e [Diretrizes de dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md)

   * Processos para cada ambiente; por exemplo, requisitos de implantação e manutenção
   * Atividades de manutenção (Datastore GC, otimização do TarPM etc.)
   * [](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)Armazenamento em cache do Dispatcher
   * [Geração de cluster](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) Publicar/Autorcompartilhar
   * Desempenho no lado do cliente (minify JS, concat, sprites de css, número total de solicitações http e outras)

* **Arquitetura do aplicativo**

   A arquitetura de aplicativos define e descreve o comportamento dos aplicativos propostos.

   Tem como foco:

   * Como eles interagem entre si e com os usuários.
   * Os dados a serem consumidos e produzidos pelas aplicações, em vez da sua estrutura interna.

   As definições devem abranger:

   * Estrutura básica do código para o projeto
   * Artefatos de código (pacotes, pacotes etc.)
   * Detalhamentos dos modelos/componentes e seus relacionamentos
   * Detalhes de alto nível das personalizações necessárias (as sobreposições específicas serão seguidas posteriormente)
   * Design de fluxos de trabalho necessários para a solução (por exemplo, criação de conteúdo, aprovação, publicação, transformações, importações, exportações etc.)
   * Consideração especial para qualquer módulo complexo, como MSM, Commerce, integração de terceiros


* **Integração do sistema**

   A integração do sistema exige que você planeje (e depois implemente):

   * Como todos os sub-sistemas e [integrações de soluções](/help/sites-administering/integration.md) será reunido para funcionar como um sistema coerente
   * Como quaisquer sistemas de terceiros serão integrados; juntamente com quaisquer considerações especiais, como offline/online, lado do cliente/navegador ou tratamento de falhas quando um sistema de terceiros está inativo

* **Conceito de teste**

   Antes de iniciar o desenvolvimento, você deve elaborar um conceito abrangente e detalhado de todos [teste](/help/sites-developing/planning.md) requisitos para o seu projeto.

   Isso deve incluir (entre outros):

   * Pormenores de todos os ensaios a efetuar
   * Preparação de qualquer conteúdo necessário para esses ensaios
   * Informações sobre quaisquer ferramentas de ensaio a utilizar
   * Indicação de alto nível de quem irá participar nos ensaios; grupos especialmente fora da equipe de controle de qualidade
   * Pormenores da automatização dos ensaios; por exemplo, com o Selenium ou o modo Desenvolvedor de AEM

* **Design da experiência**

   O Experience Design (XD) envolve projetar a experiência do usuário para sua solução.

   A experiência do usuário deve ser analisada e desenvolvida para seus autores e usuários finais de seu site.

* **Configuração de suporte**

   Antes do desenvolvimento, todos os processos de suporte, necessários para implantar, lançar, testar e relatar, devem ser configurados.

   Consulte também a [Portal de suporte do Adobe](https://helpx.adobe.com/br/marketing-cloud/contact-support.html).

### Planejamento de Operações e Operações {#operations-planning-and-operations}

Da mesma forma, as operações devem ser planejadas adequadamente para garantir que você tenha os ambientes necessários - para todos os estágios do ciclo de vida do projeto. Você também precisa dos processos apropriados para mantê-los.

#### Marcos {#milestones-3}

* **Permissões**

   Você precisa planejar e implementar um Conceito de funções e direitos para todos os usuários/grupos que usarão a solução.

   Por exemplo:

   * Uma lista de funções (ou seja, grupos) com `read`/ `write` definições de acesso para cada

   * Definição do uso de privilégios que afetam o ambiente de publicação; por exemplo, `replicate`
   * Para usuários com privilégios mínimos, os workflows devem ser definidos
   * Usuários na `editor` não deve ter `admin` nem fazer parte da `administrators` grupo

   Para obter mais informações, consulte [Administração e segurança do usuário](/help/sites-administering/security.md).

* **Monitoramento e manutenção**

   O monitoramento e a manutenção são aspectos fundamentais para garantir o bom funcionamento da solução após sua ativação. Para isso, você precisa definir:

   * O que precisa de monitoramento
   * Tarefas de manutenção; regular e em casos especiais

   Consulte também [Monitoramento e manutenção](/help/sites-deploying/monitoring-and-maintaining.md) para obter mais informações.

* **Migração**

   Qualquer conteúdo do sistema herdado deve ser revisado e validado para migração.

* **Plano de recuperação**

   Certifique-se de ter um plano de recuperação em vigor. Numa situação de emergência, tal deve estar disponível para garantir a utilização da AEM na produção. Isso deve abranger situações como backup, restauração, falover e outras.

### Desenvolvimento {#development}

O desenvolvimento é uma fase crucial que requer mais do que apenas codificação.

#### Marcos {#milestones-4}

* **Ambiente de desenvolvimento**

   Planeje e documente seu ambiente de desenvolvimento, incluindo:

   * Arquitetura
   * [Ferramentas de desenvolvimento](/help/sites-developing/dev-tools.md)

      * Um ambiente típico consiste em:

         * Um sistema de controlo de emissões; como Jira
         * um IDE; como o Eclipse
         * um instrumento de gestão da construção; como Maven
         * um instrumento de integração contínua; como Jenkins
         * uma ferramenta para o controlo de versão; como GIT/SVN
         * um gerenciador de repositório de artefatos de compilação; como Archiva/Nexus
   * Integração/dependências de software de terceiros
   * [Integração/dependências da solução](/help/sites-administering/integration.md)
   * Carência de implantação


* **Sistema de teste**

   Planeje e documente seu ambiente de teste, incluindo:

   * Arquitetura
   * Dependências em construções de desenvolvimento; incluindo criações noturnas
   * As possibilidades ou limitações de testes de integração/dependências de software de terceiros
   * Ferramentas de teste
   * Estratégia de teste automatizada

* **Sistema de produção**

   Planeje e documente seu ambiente de produção, incluindo:

   * Arquitetura
   * Carência de implantação
   * Integração/dependências de software de terceiros
   * Configuração de segurança
   * Desempenho da linha de base verificado ao executar o [Testes de Dia Difícil](/help/sites-developing/tough-day.md) na configuração de produção
   * Requisitos para os ensaios de desempenho; see [Práticas recomendadas para garantia de qualidade](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integração**

   Planejar, documentar e testar todos os aspectos do sistema e [integração de soluções](/help/sites-administering/integration.md), incluindo:

   * Uma estratégia de teste automatizado
   * Processos automatizados para [mover aplicativos de desenvolvimento para teste, em seguida, produção](/help/managing/enterprise-devops.md#code-movement)
   * Processos automatizados para [mover o conteúdo da produção para teste e desenvolvimento](/help/managing/enterprise-devops.md#content-movement)

* **Migração**

   Planejar, documentar e testar todos os aspectos da migração de conteúdo; incluindo:

   * Arquitetura de conteúdo
   * Estratégia de migração

* **Comunicação**

   Certifique-se de que todos os membros da equipe e o pessoal do projeto sejam mantidos atualizados, conforme necessário.

* **Documentação**.

   Documentar completamente a solução; incluindo:

   * Manual de operações
   * Qualquer personalização que possa afetar as atualizações
   * Notas de versão

### Desempenho e testes {#performance-and-testing}

Quando o novo aplicativo estiver disponível, ele precisará ser submetido a testes rigorosos, tanto para funcionalidade quanto para [desempenho](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Qualquer equipe de ensaio deve ser mantida neutra e apresentar os resultados dos ensaios.
>
>Compete ao Gestor de Projetos avaliar as implicações dos resultados e decidir sobre as medidas adequadas.

#### Marcos {#milestones-5}

* **Teste de aceitação do usuário final**

   [Teste de aceitação do usuário](/help/sites-developing/acceptance-signoff.md) (UAT) é fundamental para assegurar que:

   * A solução atende aos requisitos do usuário/cliente
   * O cliente/usuários aceitam a solução (função, design e desempenho)

   Deve existir uma lista de verificação formalizada para a transferência do cliente; idealmente automatizada e executada durante a noite em relação a um instantâneo. Os resultados devem ser enviados ao gestor do projeto e à equipe de desenvolvimento

* **Testes de desempenho e carregamento**

   Os testes de desempenho e carga são usados para garantir que a solução atenda aos níveis de desempenho necessários, em média e cargas máximas.

   Para obter mais informações sobre testes de desempenho, consulte:

   * [Teste de desempenho](/help/sites-deploying/configuring-performance.md)
   * [Como planejar e executar testes](/help/sites-developing/planning.md)

   * [Diretrizes básicas de desempenho](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >Este processo terá de ser prosseguido durante a utilização normal da AEM, mas estas fases iniciais são as mais cruciais.

### Implantação {#rollout}

A implantação de seu novo aplicativo precisa de um planejamento cuidadoso para garantir uma ativação tranquila. Isso inclui confirmar um alto nível de segurança, treinar todos os usuários em potencial e fazer vários exercícios para confirmar que todos os problemas foram resolvidos.

#### Marcos {#milestones-6}

* **Preparação**

   A preparação e o planejamento ajudarão a garantir uma implantação tranquila.

* **Treinamento**

   Assegurar que todo o pessoal envolvido foi treinado.

   Consulte [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) no catálogo do curso.

* **Administradores treinados**

   Certifique-se de que os administradores da solução tenham:

   * Treinado
   * Recebido o material de formação adequado
   * Recebida a documentação apropriada

* **Usuários treinados**

   Certifique-se de que os autores tenham:

   * Treinado
   * Recebido o material de formação adequado
   * Recebida a documentação apropriada; por exemplo, o Guia do usuário

* **Testes de Penetração**

   Os testes de penetração simulam um ataque em um sistema de computador para identificar possíveis fragilidades de segurança.

* **Testes de Penetração/Segurança**

   Para garantir a segurança de sua solução, execute testes de penetração específicos, juntamente com uma grande variedade de testes de segurança.

   Consulte a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) para obter mais detalhes.

### Go Live {#go-live}

Você quer que seu Go Live seja o mais suave possível. Novamente, as etapas finais precisam de planejamento para execução limpa.

#### Marcos {#milestones-7}

* **Preparação**

   A preparação e o planejamento ajudarão a garantir uma ativação tranquila.

* **Segurança**

   Confirme a segurança da solução para usuários internos e externos e seu conteúdo.

* **Fallback**

   Certifique-se de que todos os sistemas, procedimentos e mecanismos necessários para o fallback estejam em vigor antes de entrar em funcionamento.

* **Suporte**

   Certifique-se de que os serviços de suporte estejam no local e prontos.

* **Transição**

   Planeje e execute a transição para seu ambiente de produção e seus usuários.

* **Implantação**

   Prepare e execute seus testes de fumaça.

## Perfil {#persona}

As listas de verificação são projetadas por persona. Estas são as funções com um envolvimento significativo no ciclo de vida do projeto.

Há também alguns [outras personas](#other-persona) que estejam envolvidos em tarefas específicas.

### Patrocinador do projeto {#project-sponsor}

O patrocinador do projeto é:

* Responsável por fornecer/apresentar o caso comercial do projeto.
* Chave para definir e definir o âmbito do projeto; incluindo:

   * a definição e os critérios de sucesso
   * os KPIs principais

* Forneça os principais marcos com base no roteiro do cliente.

### Gerenciador de Projetos {#project-manager}

O gerente do projeto é:

* Responsável pela execução global do projeto com base nos requisitos (por exemplo, âmbito, KPI, critérios de sucesso e definição) fornecidos pelo patrocinador do projeto.
* Responsável pela definição do orçamento e pelo financiamento do projeto com base nesse orçamento.
* O principal ponto de comunicação para todas as pessoas envolvidas no projeto.

### Arquiteto {#architect}

O arquiteto da solução:

* É responsável pelo design de alto nível da solução e do sistema.
* Ajuda a definir a estratégia de implementação para AEM. Por exemplo, se é necessário implementar uma instalação em cluster ou um modo de espera frio ou quando é necessária uma rede de entrega de conteúdo (CDN).
* Defina também a arquitetura da solução AEM com base nos requisitos do cliente. Isso pode incluir o conceito de funções de usuário (com direitos relacionados), a relação entre modelos e componentes ou quando usar o gerenciamento de vários sites.

### Analista de negócios {#business-analyst}

O analista de negócios:

* É o principal responsável por reunir e analisar os requisitos de alto nível e depois transformá-los em especificações:

   * para que o gerente do projeto use ao planejar o desenvolvimento
   * para que a equipe de desenvolvimento possa trabalhar durante o projeto e desenvolvimento.

* Trabalha em conjunto com o cliente para analisar os requisitos. Eles combinam estes itens com:

   * A definição de sucesso.
   * Os critérios de sucesso.
   * KPIs (baseados em negócios e desempenho).

### Líder de desenvolvimento {#development-lead}

O líder em desenvolvimento:

* É responsável pela entrega técnica do projeto.
* É responsável por selecionar uma metodologia de desenvolvimento que esteja em conformidade com os requisitos do cliente.
* Elaborar a estratégia de desenvolvimento:

   * garantir que esteja alinhada aos KPIs de negócios e desempenho
   * tendo em conta os critérios de sucesso e a definição

* Trabalha em estreita colaboração com o arquiteto (especialmente ao elaborar a estratégia de desenvolvimento para AEM) para definir aspectos como a relação entre modelos e componentes, a estratégia de integração para aplicativos de terceiros e qualquer funcionalidade especializada.

### Líder de qualidade {#quality-lead}

O chumbo de qualidade:

* É responsável pela qualidade da entrega; assegurar que satisfaz os critérios de sucesso e quaisquer KPIs definidos pelo cliente.
* Define as métricas de qualidade, juntamente com todas as partes interessadas, elabora os planos de teste e garante que sejam executadas.
* Cria e fornece relatórios aos participantes do projeto.

### Engenheiro de Sistemas {#system-engineer}

O engenheiro de sistemas:

* É responsável pela supervisão da infraestrutura do projeto.
* É responsável por:

   * configuração de ambientes internos de desenvolvimento e teste
   * para combinar esses sistemas com os sistemas clientes

* Fornece recomendações de hardware, monitora as várias implementações e fornece suporte às operações antes e depois do lançamento.

### Líder de segurança {#security-lead}

O cliente potencial de segurança:

* É responsável pelo conceito geral de segurança da solução, garantindo que ela seja alinhada a quaisquer requisitos e políticas do cliente.
* Fornece um conceito de segurança, operações de segurança e recomendações para qualquer conceito de segurança baseado em hardware; como zonas e firewalls.

### Outras Persona {#other-persona}

* Partes interessadas

   * Pessoas (muitas vezes da empresa) que têm interesse (interesses) no sucesso do projeto. Muitas vezes contribuem para o orçamento.

* Legal

   * É necessário aconselhamento jurídico aquando da negociação de contratos.

* Formadores

   * Em função da dimensão e da natureza do projeto, podem ser utilizados formadores especializados para desenvolver e apresentar sessões de formação para os grupos em causa.

* Escritores Técnicos

   * Dependendo da dimensão e da natureza do projeto, os autores técnicos especializados podem ser utilizados para escrever orientações e manuais para grupos específicos; Por exemplo, um manual de manutenção para administradores de sistema ou um guia do usuário para os autores.

* Administradores do sistema

   * Responsável pelo funcionamento contínuo do sistema.

* Autores e usuários finais

   * As pessoas que usarão o sistema para criar e manter o conteúdo do seu site.

## Documentos e Entregas Necessários {#required-documents-and-deliverables}

As listas de verificação abrangem a **Documentos necessários** e **Deliverables** para cada marco.

* Não há relação 1:1 entre elas; por exemplo, um grupo de documentos necessários pode resultar em um único delivery.
* Um delivery de uma pessoa pode ser um documento obrigatório para outra pessoa durante o mesmo marco.

### Documentos necessários {#required-documents}

O **Documentos necessários** são necessárias para a pessoa adequada ao produzir seus resultados.

Para cada **Documento necessário** a pessoa deve indicar:

* **S/N**: Se foi recebido.
* **1-3**: Uma indicação da qualidade do documento recebido.

### Deliverables {#deliverables}

Para cada marco, a pessoa apropriada é responsável por fornecer documentos específicos e, portanto, assumir suas responsabilidades por um marco específico.

Para cada **Entregável** a pessoa deve indicar:

* **S/N**: Se foi concluído.

Os deliveries são frequentemente usados como **Documentos necessários** para o marco atual ou posterior.

## Práticas recomendadas relacionadas {#related-best-practices}

Para obter as práticas recomendadas de implantação, administração, desenvolvimento ou criação, consulte o seguinte:

* Outras práticas recomendadas e diretrizes relacionadas ao gerenciamento de um projeto de AEM:
   * [Diretrizes de dimensionamento do hardware ](/help/managing/hardware-sizing-guidelines.md)
   * [DevOps empresarial ](/help/managing/enterprise-devops.md)
   * [Práticas recomendadas de gerenciamento de SEO e URL](/help/managing/seo-and-url-management.md)
   * [AEM e as diretrizes de acessibilidade da Web](/help/managing/web-accessibility.md)
   * [Regulamento Geral sobre a Proteção de Dados](/help/managing/data-protection-and-privacy.md)* [Práticas recomendadas de implantação e manutenção](/help/sites-deploying/best-practices.md)
* [Práticas recomendadas de administração](/help/sites-administering/administer-best-practices.md)
* [Práticas recomendadas de desenvolvimento](/help/sites-developing/best-practices.md)
* [Práticas recomendadas de criação](/help/sites-authoring/best-practices.md)

## Principais áreas de documentação {#key-documentation-areas}

* AEM Documentação Além disso, as seguintes seções AEM documentação são de especial interesse (no entanto, essa lista não é exaustiva):

   * [Segurança](/help/sites-developing/security.md)
   * [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md)
   * [DevOps empresarial ](/help/managing/enterprise-devops.md)
   * [Dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md)
   * Conceitos de AEM:

      * [Desenvolvimento - noções básicas](/help/sites-developing/the-basics.md)
      * [Conceitos do MSM](/help/sites-administering/msm.md)
      * [Linguagem de modelo do HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

* Documentação relacionada

   * Adobe Experience Cloud - [Planejamento da Adobe Experience Cloud](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
