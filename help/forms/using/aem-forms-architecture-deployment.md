---
title: Arquitetura e topologias de implantação do AEM Forms
description: Detalhes da arquitetura do AEM Forms e topologias recomendadas para clientes e clientes AEM novos e existentes que estão atualizando do LiveCycle ES4 para o AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 0%

---

# Arquitetura e topologias de implantação do AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html) |
| AEM 6.5 | Este artigo |

## Arquitetura {#architecture}

O AEM Forms é um aplicativo implantado no AEM como um pacote de AEM. O pacote é conhecido como pacote complementar do AEM Forms. O pacote complementar do AEM Forms contém serviços (provedores de API), que são implantados no contêiner OSGi AEM, e servlets ou JSPs (fornecendo funcionalidade de front-end e REST API) gerenciados pela estrutura Sling do AEM. O diagrama a seguir descreve essa configuração:

![Arquitetura do](assets/architecture.png)

A arquitetura do AEM Forms inclui os seguintes componentes:

* **Principais serviços do AEM:** Serviços básicos que o AEM fornece para um aplicativo implantado. Esses serviços incluem um repositório de conteúdo compatível com JCR, um contêiner de serviço OSGI, um mecanismo de fluxo de trabalho, uma loja de confiança, uma loja de chaves e assim por diante. Esses serviços estão disponíveis para o aplicativo do AEM Forms, mas não são fornecidos por pacotes do AEM Forms. Esses serviços são parte integrante da pilha geral de AEM e vários componentes da AEM Forms usam esses serviços.
* **Serviços da Forms:** Forneça funcionalidades relacionadas a formulários, como criar, montar, distribuir e arquivar documentos de PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com código de barras. Esses serviços estão disponíveis publicamente para consumo por código personalizado coimplantado no AEM.
* **Camada da Web:** JSPs ou servlets, criados em serviços comuns e de formulários, que fornecem as seguintes funcionalidades:

   * **Front-end de criação**: uma interface de usuário de criação e gerenciamento de formulários para criação e gerenciamento de formulários.
   * **Front-end de representação e envio de formulários**: uma interface direcionada ao usuário final para uso pelos usuários finais do AEM Forms (por exemplo, cidadãos que acessam um site governamental). Isso fornece funcionalidades de representação de formulário (formulário de exibição em um navegador da Web) e envio.
   * **REST APIs**: JSPs e servlets exportam um subconjunto de serviços de formulários para consumo remoto por clientes baseados em HTTP, como o SDK móvel de formulários.

**AEM Forms no OSGi:** Um ambiente AEM Forms no OSGi é um AEM Author padrão ou AEM Publish com pacote AEM Forms implantado nele. Você pode executar o AEM Forms no OSGi em um [ambiente de servidor único, farm e configurações em cluster](/help/sites-deploying/recommended-deploys.md). A configuração do cluster está disponível somente para instâncias do Autor AEM.

**AEM Forms no JEE:** O AEM Forms no JEE é um servidor do AEM Forms em execução na pilha do JEE. Ele tem o AEM Author com pacotes complementares do AEM Forms e recursos adicionais do AEM Forms JEE implantados em uma única pilha do JEE em execução em um servidor de aplicativos. Você pode executar o AEM Forms no JEE em configurações de servidor único e em cluster. O AEM Forms no JEE é necessário apenas para executar a segurança de documentos, o gerenciamento de processos e para clientes do LiveCycle que estão atualizando para o AEM Forms. Estes são alguns cenários adicionais para usar o AEM Forms no JEE:

* **Suporte ao espaço de trabalho do HTML (para clientes que usam o espaço de trabalho do HTML):** O AEM Forms no JEE habilita o logon único com instâncias de Processamento, atende a determinados ativos renderizados em instâncias de Processamento e lida com o envio de formulários renderizados no espaço de trabalho do HTML.
* **Processamento de dados avançado de formulário/comunicação interativa**: o AEM Forms no JEE pode ser usado para processar adicionalmente dados de comunicação interativa/de formulário (e salvar os resultados em um armazenamento de dados adequado) em casos de uso complexos em que são necessários recursos avançados de gerenciamento de processo.

O AEM Forms no JEE também inclui os seguintes serviços de suporte para os componentes AEM:

* **Gerenciamento integrado de usuários:** Permite que os usuários do AEM Forms no JEE sejam reconhecidos como formulários AEM em usuários OSGi e ajuda a habilitar o SSO para usuários OSGi e JEE. Isso é necessário para cenários em que o logon único entre formulários AEM no OSGi e o AEM Forms no JEE é necessário (por exemplo, espaço de trabalho HTML).
* **Hospedagem de ativos:** O AEM Forms no JEE pode fornecer ativos (por exemplo, formulários HTML5) renderizados no AEM Forms no OSGi.

A interface do usuário de criação do AEM Forms não oferece suporte à criação de documentos de registro (DOR), PDF forms e HTML5 Forms. Esses ativos são projetados usando o aplicativo Forms Designer independente e carregados individualmente no AEM Forms Manager. Como alternativa, para o AEM Forms no JEE, os formulários podem ser criados como ativos de aplicativo (no AEM Forms Workbench) e implantados no AEM Forms no servidor JEE.

O AEM Forms no OSGi e o AEM Forms no JEE têm recursos de fluxo de trabalho. Você pode criar e implantar rapidamente fluxos de trabalho básicos para várias tarefas nos formulários AEM no OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos do AEM Forms no JEE. Há alguma diferença no [recursos do fluxo de trabalho centrado em formulários no AEM Forms no OSGi e recurso de gerenciamento de processos do AEM Forms no JEE](capabilities-osgi-jee-workflows.md). O desenvolvimento e o gerenciamento de workflows centrados em formulários no AEM Forms no OSGi usam os familiares recursos de Caixa de entrada de AEM Workflow e AEM.

## Terminologias {#terminologies}

A imagem a seguir exibe várias configurações de servidor do Formulário AEM e seus componentes usados em uma implantação típica do AEM Forms:

![aem_forms_-_recommendations_topology](assets/aem_forms_-_recommendedtopology.png)

**Autor:** Uma instância do autor é um servidor do AEM Forms executado no modo padrão de execução do autor. Pode ser AEM Forms no JEE ou AEM Forms no ambiente OSGi. Destina-se a usuários internos, designers de formulários e comunicações interativas e desenvolvedores. Ela permite as seguintes funcionalidades:

* **Criação e gerenciamento de formulários e comunicações interativas:** Os designers e desenvolvedores podem criar e editar formulários adaptáveis e comunicações interativas, fazer upload de outros tipos de formulários criados externamente, por exemplo, formulários criados no Adobe Forms Designer e gerenciar esses ativos usando o console do Forms Manager.
* **Publicação de formulários e comunicações interativas:** Os ativos hospedados em uma instância de autor podem ser publicados em uma instância de publicação para executar operações de tempo de execução. A publicação de ativos usa recursos de replicação do AEM. O Adobe recomenda que um agente de replicação seja configurado em todas as instâncias do autor para enviar manualmente formulários publicados para instâncias de processamento e outro agente de replicação seja configurado nas instâncias de processamento com o *No recebimento* acionador ativado para replicar automaticamente os formulários recebidos para publicar instâncias.

**Publicar:** Uma instância de publicação é um servidor do AEM Forms em execução no modo de execução padrão do Publish. As instâncias do Publish se destinam a usuários finais de aplicativos baseados em formulário, por exemplo, usuários que acessam um site público e enviam formulários. Ela permite as seguintes funcionalidades:

* Renderização e envio do Forms para usuários finais.
* Transporte de dados brutos de formulário enviados para instâncias de processamento para processamento posterior e armazenamento no sistema de registro final. A implementação padrão fornecida no AEM Forms faz isso usando os recursos de replicação reversa do AEM. Uma implementação alternativa também está disponível para enviar diretamente os dados de formulário para servidores de processamento, em vez de salvá-los localmente primeiro (o último é um pré-requisito para a ativação da replicação reversa). Os clientes que estão preocupados com o armazenamento de dados potencialmente confidenciais em instâncias de publicação podem fazer isso [implementação alternativa](/help/forms/using/configuring-draft-submission-storage.md), já que as instâncias de processamento normalmente ficam em uma zona mais segura.
* Renderização e envio de comunicações e cartas interativas: uma comunicação e uma carta interativas são renderizadas em instâncias de publicação e os dados correspondentes são enviados às instâncias de processamento para armazenamento e pós-processamento. Os dados podem ser salvos localmente em uma instância de publicação e replicados revertidos para uma instância de processamento (a opção padrão) posteriormente ou enviados diretamente para a instância de processamento sem serem salvos na instância de publicação. A última implementação é útil para clientes preocupados com a segurança.

**Processando:** Uma instância do AEM Forms em execução no modo Autor sem usuários atribuídos ao grupo de gerenciadores de formulários. Você pode implantar o AEM Forms no JEE ou o AEM Forms no OSGi como uma instância de processamento. Os usuários não são atribuídos para garantir que as atividades de criação e gerenciamento de formulários não sejam executadas na instância de Processamento e ocorram somente na instância de Autor. Uma instância de Processamento permite as seguintes funcionalidades:

* **Processamento de dados de formulário brutos provenientes de uma instância do Publish:** Isso é feito principalmente em uma instância de Processamento por meio de workflows de AEM que são acionados quando os dados chegam. Os workflows podem usar a etapa Modelo de dados de formulário fornecida pronta para uso para arquivar os dados ou documentos em um armazenamento de dados adequado.
* **Armazenamento seguro de dados de formulário**: o processamento fornece um repositório por trás do firewall para dados de forma brutos que são isolados dos usuários. Nem os designers de formulário na instância do Autor nem os usuários finais na instância do Publish podem acessar esse repositório.

  >[!NOTE]
  >
  >A Adobe recomenda usar um armazenamento de dados de terceiros para salvar os dados processados finais em vez de usar o repositório AEM.

* **Armazenamento e pós-processamento de dados de correspondência provenientes de uma instância do Publish:** Os fluxos de trabalho do AEM executam o pós-processamento opcional das definições de correspondência. Esses workflows podem salvar os dados processados finais em um armazenamento de dados externo adequado.

* **Hospedagem do HTML Workspace**: uma instância de processamento hospeda o front-end para o HTML Workspace. O espaço de trabalho do HTML fornece a interface de usuário para atribuição de tarefa/grupo associada a processos de revisão e aprovação.

Uma instância de Processamento é configurada para ser executada no modo de execução do Autor porque:

* Ela permite a replicação reversa de dados de formulário brutos de uma instância do Publish. O manipulador de armazenamento de dados padrão requer o recurso de replicação reversa.
* Os fluxos de trabalho do AEM, que são o principal meio de processar dados de formulário brutos provenientes de uma instância do Publish, são recomendados para serem executados em um sistema no estilo do autor.

## Topologias físicas de amostra para o AEM Forms no JEE {#sample-physical-topologies-for-aem-forms-on-jee}

As topologias do AEM Forms no JEE recomendadas abaixo são principalmente para clientes que estão atualizando do LiveCycle ou de uma versão anterior do AEM Forms no JEE. A Adobe recomenda usar o AEM Forms no OSGi para instalações novas. Uma nova instalação do AEM Forms no JEE é recomendada apenas para usar os recursos de Segurança de documentos e Gerenciamento de processos.

### Topologia para usar serviços de documentos ou recursos de segurança de documentos {#topology-for-using-document-services-or-document-security-capabilities}

Os clientes do AEM Forms que planejam usar apenas serviços de documentos ou recursos de segurança de documentos podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar uma única instância do AEM Forms. Você também pode criar um cluster ou farm de servidores do AEM Forms, se necessário. Essa topologia é recomendada quando a maioria dos usuários acessa programaticamente os recursos do servidor do AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é útil em operações de processamento em lote de serviços de documento. Por exemplo, usar o serviço de saída para criar centenas de documentos PDF não editáveis diariamente.

Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer o planejamento de capacidade, o balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço PDF Generator para converter milhares de páginas por dia e adicionar assinaturas digitais para limitar o acesso a documentos, configure servidores AEM Forms separados para o serviço PDF Generator e recursos de assinatura digital. Ele ajuda a fornecer o melhor desempenho e a dimensionar os servidores independentemente uns dos outros.

![recursos básicos](assets/basic-features.png)

### Topologia para usar o gerenciamento de processos do AEM Forms {#topology-for-using-aem-forms-process-management}

Os clientes do AEM Forms que planejam usar os recursos de gerenciamento de processo do AEM Forms, por exemplo, o HTML Workspace pode ter uma topologia semelhante à exibida abaixo. O servidor do AEM Forms no JEE pode estar em uma configuração de servidor único ou cluster.

Se você estiver atualizando a partir do LiveCycle ES4, essa topologia espelha de perto o que você já tem no LiveCycle, exceto a adição do AEM Author incorporado ao AEM Forms no JEE. Além disso, não há alteração nos requisitos de clustering para clientes que executam um upgrade. Se você estava usando o AEM Forms em um ambiente em cluster, é possível continuar com o mesmo no AEM 6.5 Forms. Para uma nova instalação do AEM Forms do JEE para usar o HTML Workspace, executar a instância do autor do AEM incorporada ao ambiente do JEE é um requisito adicional.

O armazenamento de dados de formulário é um armazenamento de dados de terceiros usado para armazenar dados processados finais de formulários e comunicações interativas. Esse é um elemento opcional na topologia. Você também pode optar por configurar uma instância de processamento e usar seu repositório como o sistema final de registro, se necessário.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

A topologia é recomendada para os clientes que planejam usar o AEM Forms no servidor JEE para recursos de gerenciamento de processos (HTML Workspace) sem usar nenhum recurso de pós-processamento, formulários adaptáveis, formulários HTML5 e comunicação interativa.

### Topologia para usar formulários adaptáveis, formulários HTML5, recursos de comunicação interativa {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Os clientes do AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, HTML5 Forms, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para usar recursos de comunicação interativa do AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Você pode fazer as seguintes alterações/personalizações na topologia sugerida acima:

* O uso do aplicativo HTML Workspace e AEM Forms requer um autor ou instância de processamento de AEM. Você pode usar a instância do autor do AEM integrada ao AEM Forms no servidor JEE em vez de configurar um servidor externo adicional do autor do AEM.
* Uma instância de autoria ou processamento do AEM é necessária somente para fluxos de trabalho centrados no Forms em OSGi, formulários adaptáveis, portal de formulários e comunicação interativa.
* A interface do usuário do agente de comunicação interativa geralmente é executada na organização. Assim, você pode manter um servidor de publicação para a interface do usuário do agente na rede privada.
* Formulários AEM em instâncias OSGi integradas ao AEM Forms no servidor JEE também podem executar fluxos de trabalho centrados no Forms em OSGi e Pastas monitoradas.

## Exemplos de topologias físicas para usar o AEM Forms no OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologia para captura de dados, comunicação interativa, fluxo de trabalho centrado em formulários nos recursos do OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Os clientes do AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, HTML5 Forms, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para usar comunicações interativas e fluxos de trabalho centrados no Forms no recurso OSGi, por exemplo, para usar a Caixa de entrada AEM e o aplicativo AEM Forms para fluxos de trabalho de processo comercial.

![interative-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologia para usar recursos de pastas monitoradas para processamento em lote offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Os clientes do AEM Forms que planejam usar Pastas monitoradas para processamento em lote podem ter uma topologia semelhante à exibida abaixo. A topologia exibe um ambiente em cluster, mas você decide usar uma única instância ou um farm de servidores do AEM Forms, dependendo da carga. A fonte de dados de terceiros é seu próprio sistema de registro. Ele age como uma fonte de entrada para Pastas monitoradas. A topologia também exibe a saída no formato de um arquivo impresso. Você também pode armazenar o conteúdo de saída em um sistema de arquivos, enviar por email e usar outros métodos personalizados para consumir saída.

![offline-batch-processing-via-watch-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topologia para usar recursos de serviços de documentos para processamento offline baseado em API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Os clientes da AEM Forms que planejam usar somente o recurso de serviços de documento podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar um cluster de AEM Forms em servidores OSGi. Essa topologia é recomendada quando a maioria dos usuários acessa programaticamente (usando APIs) os recursos do servidor do AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é bastante útil em vários cenários de cliente de software. Por exemplo, vários clientes usando o serviço PDF Generator para criar documentos PDF por demanda.

Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer o planejamento de capacidade, o balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço PDF Generator para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço PDF Generator e recursos de formulários adaptáveis. Ele ajuda a fornecer o melhor desempenho e a dimensionar os servidores independentemente uns dos outros.

![processamento baseado em api offline](assets/offline-api-based-processing.png)
