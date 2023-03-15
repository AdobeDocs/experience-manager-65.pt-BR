---
title: Topologias de arquitetura e implantação do AEM Forms
seo-title: Architecture and deployment topologies for AEM Forms
description: Detalhes da arquitetura da AEM Forms e topologias recomendadas para clientes de AEM novos e existentes e clientes que atualizam do LiveCycle ES4 para o AEM Forms.
seo-description: Architecture details for AEM Forms and recommended topologies for new and existing AEM customers and customers upgrading from LiveCycle ES4 to AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '2460'
ht-degree: 0%

---

# Topologias de arquitetura e implantação do AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Arquitetura {#architecture}

O AEM Forms é um aplicativo implantado no AEM como um pacote AEM. O pacote é conhecido como pacote complementar do AEM Forms. O pacote do complemento AEM Forms contém ambos os serviços (provedores de API), que são implantados no contêiner OSGi do AEM, e servlets ou JSPs (fornecendo funcionalidade de front-end e de API REST) gerenciados pela estrutura AEM Sling. O diagrama a seguir descreve essa configuração:

Arquitetura do ![](assets/architecture.png)

A arquitetura do AEM Forms inclui os seguintes componentes:

* **Serviços principais de AEM:** Serviços básicos que AEM fornecem a um aplicativo implantado. Esses serviços incluem um repositório de conteúdo compatível com JCR, um contêiner de serviço OSGI, um mecanismo de fluxo de trabalho, um armazenamento de confiança, um armazenamento de chaves e assim por diante. Esses serviços estão disponíveis para o aplicativo AEM Forms, mas não são fornecidos por pacotes AEM Forms. Esses serviços são parte integrante da pilha de AEM geral e vários componentes do AEM Forms usam esses serviços.
* **Serviços Forms:** Forneça funcionalidades relacionadas a formulários, como criar, montar, distribuir e arquivar documentos do PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com códigos de barras. Esses serviços estão disponíveis publicamente para consumo pelo código personalizado implantado em AEM.
* **Camada da Web:** JSPs ou servlets, integrados aos serviços comuns e de formulários, que fornecem as seguintes funcionalidades:

   * **Fante de criação**: Uma interface de usuário de criação e gerenciamento de formulários para criação e gerenciamento de formulários.
   * **Front-end de renderização e envio de formulário**: Uma interface voltada para o usuário final para uso pelos usuários finais da AEM Forms (por exemplo, cidadãos que acessam um site do governo). Isso fornece a representação de formulário (formulário de exibição em um navegador da Web) e as funcionalidades de envio.
   * **REST APIs**: Os JSPs e servlets exportam um subconjunto de serviços de formulários para consumo remoto por clientes baseados em HTTP, como o SDK móvel de formulários.

**AEM Forms no OSGi:** Um ambiente AEM Forms em OSGi é o autor padrão do AEM ou publicação do AEM com o pacote AEM Forms implantado nele. Você pode executar o AEM Forms no OSGi em um [ambiente de servidor único, farm e configurações em cluster](/help/sites-deploying/recommended-deploys.md). A configuração de cluster está disponível somente para instâncias do Autor do AEM.

**AEM Forms no JEE:** O AEM Forms no JEE é o servidor AEM Forms em execução na pilha JEE. Ele tem o AEM Author com pacotes complementares do AEM Forms e recursos adicionais do AEM Forms JEE co-implantados em uma única pilha JEE em execução em um servidor de aplicativos. Você pode executar o AEM Forms no JEE em configurações de servidor único e clusterizadas. O AEM Forms no JEE é necessário apenas para executar a segurança de documentos, o gerenciamento de processos e para clientes do LiveCycle que atualizam para o AEM Forms. Estes são alguns cenários adicionais para usar o AEM Forms no JEE:

* **Suporte ao espaço de trabalho HTML (para clientes que usam o espaço de trabalho HTML):** O AEM Forms no JEE habilita o logon único com instâncias de processamento, fornece determinados ativos renderizados em instâncias de processamento e lida com o envio de formulários renderizados no espaço de trabalho do HTML.
* **Processamento avançado de dados de formulário/comunicação interativa**: O AEM Forms no JEE pode ser usado para processar adicionalmente dados de formulário/comunicação interativa (e salvar os resultados em um armazenamento de dados adequado) em casos de uso complexos em que são necessários recursos avançados de gerenciamento de processos.

O AEM Forms no JEE também inclui os seguintes serviços de suporte aos componentes do AEM:

* **Gerenciamento integrado de usuários:** Permite que os usuários do AEM Forms no JEE sejam reconhecidos como formulários AEM em usuários do OSGi e ajuda a habilitar o SSO para usuários do OSGi e JEE. Isso é necessário para cenários em que o logon único entre formulários AEM no OSGi e AEM Forms no JEE é necessário (por exemplo, HTML workspace).
* **Hospedagem de ativos:** O AEM Forms no JEE pode fornecer ativos (por exemplo, formulários HTML5) renderizados no AEM Forms no OSGi.

A interface do usuário de criação do AEM Forms não oferece suporte à criação de Documento de registro (DOR), PDF forms e HTML5 Forms. Esses ativos são projetados usando o aplicativo Forms Designer independente e carregados individualmente no AEM Forms Manager. Como alternativa, para o AEM Forms no JEE, os formulários podem ser projetados como ativos de aplicativo (no AEM Forms Workbench) e implantados no AEM Forms no servidor JEE.

O AEM Forms no OSGi e o AEM Forms no JEE têm recursos de fluxo de trabalho. Você pode criar e implantar rapidamente workflows básicos para várias tarefas nos formulários de AEM no OSGi, sem precisar instalar o recurso completo de Gerenciamento de Processos do AEM Forms no JEE. Há alguma diferença no [recursos de fluxo de trabalho centrado em formulários no AEM Forms no OSGi e capacidade de gerenciamento de processos do AEM Forms no JEE](capabilities-osgi-jee-workflows.md). O desenvolvimento e o gerenciamento de fluxos de trabalho centrados em formulários no AEM Forms no OSGi usam os recursos familiares Fluxo de trabalho AEM e Caixa de entrada AEM.

## Terminologias {#terminologies}

A imagem a seguir exibe várias configurações AEM do servidor do Formulário e seus componentes usados em uma implantação típica do AEM Forms:

![aem_forms_-_recomdedtopologia](assets/aem_forms_-_recommendedtopology.png)

**Autor:** Uma instância de autor é um servidor AEM Forms em execução no modo de execução Autor padrão. Pode ser AEM Forms no JEE ou AEM Forms no ambiente OSGi. Destina-se a usuários internos, formulários e designers de comunicação interativos e desenvolvedores. Ela ativa as seguintes funcionalidades:

* **Criação e gerenciamento de formulários e comunicações interativas:** Os designers e desenvolvedores podem criar e editar formulários adaptáveis e comunicações interativas, carregar outros tipos de formulários criados externamente, por exemplo, formulários criados no Adobe Forms Designer, e gerenciar esses ativos usando o console do Forms Manager.
* **Publicação de formulário e comunicação interativa:** Os ativos hospedados em uma instância de autor podem ser publicados em uma instância de publicação para executar operações de tempo de execução. A publicação de ativos usa os recursos de replicação do AEM. O Adobe recomenda que um agente de replicação seja configurado em todas as instâncias do autor para enviar formulários publicados manualmente para instâncias de processamento e outro agente de replicação é configurado nas instâncias de processamento com a variável *Ao receber* acionador habilitado para replicar automaticamente os formulários recebidos para publicar instâncias.

**Publicar:** Uma instância de publicação é um servidor AEM Forms em execução no modo de execução de Publicação padrão. As instâncias de publicação destinam-se a usuários finais de aplicativos baseados em formulário, por exemplo, usuários que acessam um site público e enviam formulários. Ela ativa as seguintes funcionalidades:

* Renderização e envio do Forms para usuários finais.
* Transporte de dados brutos de formulários enviados para instâncias de processamento para processamento e armazenamento no sistema de registro final. A implementação padrão fornecida no AEM Forms faz isso usando os recursos de replicação reversa do AEM. Uma implementação alternativa também está disponível para enviar os dados do formulário diretamente para os servidores de processamento, em vez de salvá-los localmente primeiro (o último é um pré-requisito para a ativação da replicação reversa). Os clientes que têm preocupações com o armazenamento de dados potencialmente confidenciais em instâncias de publicação podem entrar para isso [implementação alternativa](/help/forms/using/configuring-draft-submission-storage.md), já que as instâncias de processamento normalmente estão em uma zona mais segura.
* Renderização e envio de comunicações e cartas interativas: Uma comunicação interativa e uma carta são renderizadas em instâncias de publicação e os dados correspondentes são enviados às instâncias de processamento para armazenamento e pós-processamento. Os dados podem ser salvos localmente em uma instância de publicação e replicados de forma reversa em uma instância de processamento (a opção padrão) posteriormente ou enviados diretamente para a instância de processamento sem salvar na instância de publicação. A última implementação é útil para clientes com consciência de segurança.

**Processamento:** Uma instância do AEM Forms em execução no modo de execução Autor sem usuários atribuídos ao grupo forms-manager. Você pode implantar o AEM Forms no JEE ou AEM Forms no OSGi como uma instância de processamento. Os usuários não são atribuídos para garantir que as atividades de criação e gerenciamento de formulários não sejam executadas na instância de processamento e ocorram somente na instância de Autor. Uma Instância de processamento ativa as seguintes funcionalidades:

* **Processamento de dados de formulário brutos que chegam de uma instância de publicação:** Isso é obtido principalmente em uma instância de processamento por meio de AEM workflows que são acionados na chegada dos dados. Os fluxos de trabalho podem usar a etapa Modelo de dados de formulário fornecida pronta para o uso para arquivar os dados ou documentos em um armazenamento de dados adequado.
* **Armazenamento seguro de dados de formulário**: O processamento fornece um repositório por trás do firewall para dados de formulários brutos que são isolados dos usuários. Nem os designers de formulários na instância Autor nem os usuários finais na instância Publicar podem acessar esse repositório.

   >[!NOTE]
   >
   >O Adobe recomenda usar um armazenamento de dados de terceiros para salvar os dados processados finais em vez de usar AEM repositório.

* **Armazenamento e pós-processamento de dados de correspondência provenientes de uma instância de publicação:** AEM workflows executam o pós-processamento opcional das definições de letras correspondentes. Esses workflows podem salvar os dados processados finais em um armazenamento de dados externo adequado.

* **Hospedagem no HTML Workspace**: Uma instância de processamento hospeda o front-end para o HTML Workspace. A área de trabalho do HTML fornece a interface do usuário para atribuição de tarefa/grupo associada para processos de revisão e aprovação.

Uma instância de processamento está configurada para ser executada no modo de execução Autor porque:

* Ela permite a replicação reversa de dados de formulário brutos de uma instância de publicação. O manipulador de armazenamento de dados padrão requer o recurso de replicação reversa.
* AEM Workflows, que são o principal meio de processamento de dados de formulário brutos provenientes de uma instância de Publicação, são recomendados para serem executados em um sistema de estilo de autor.

## Amostra de topologias físicas para AEM Forms no JEE {#sample-physical-topologies-for-aem-forms-on-jee}

As topologias AEM Forms em JEE recomendadas abaixo são principalmente para clientes que atualizam do LiveCycle ou de uma versão anterior do AEM Forms no JEE. O Adobe recomenda usar AEM Forms em OSGi para instalações novas. Uma nova instalação do AEM Forms no JEE é recomendada apenas para usar recursos de Segurança de documentos e Gerenciamento de processos.

### Topologia para usar serviços de documento ou recursos de segurança de documento {#topology-for-using-document-services-or-document-security-capabilities}

Os clientes da AEM Forms que planejam usar somente serviços de documento ou recursos de segurança de documento podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar uma única instância do AEM Forms. Você também pode criar um cluster ou farm de servidores da AEM Forms, se necessário. Essa topologia é recomendada quando a maioria dos usuários acessa programaticamente os recursos do servidor AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é útil em operações de processamento em lote de serviços de documento. Por exemplo, usando o serviço de saída para criar centenas de documentos PDF não editáveis diariamente.

Embora a AEM Forms permita que você configure e execute todas as funcionalidades de um único servidor, no entanto, você deve fazer planejamento de capacidade, balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF para converter milhares de páginas por dia e adicionar assinaturas digitais para limitar o acesso a documentos, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de assinatura digital. Ele ajuda a fornecer desempenho ideal e dimensionar os servidores independentemente uns dos outros.

![recursos básicos](assets/basic-features.png)

### Topologia para usar o gerenciamento de processos do AEM Forms {#topology-for-using-aem-forms-process-management}

Os clientes da AEM Forms que planejam usar os recursos de gerenciamento de processos do AEM Forms, por exemplo, o HTML Workspace pode ter uma topologia semelhante à exibida abaixo. O AEM Forms no servidor JEE pode estar em uma única configuração de servidor ou cluster.

Se você estiver atualizando do LiveCycle ES4, essa topologia se espelhará estreitamente com o que você já tem no LiveCycle, exceto pela adição do AEM Author incorporado ao AEM Forms no JEE. Além disso, não há alteração nos requisitos de cluster para clientes que executam uma atualização. Se você estava usando o AEM Forms em um ambiente em cluster, é possível continuar com o mesmo no AEM 6.5 Forms. Para uma nova instalação do AEM Forms do JEE para usar o HTML Workspace, executar AEM instância do autor incorporada ao ambiente JEE é um requisito adicional.

O armazenamento de dados de formulário é um armazenamento de dados de terceiros usado para armazenar dados processados finais de formulários e comunicações interativas. Esse é um elemento opcional na topologia. Você também pode optar por configurar uma instância de processamento e usar seu repositório como o sistema final de registro, se necessário.

![topology_for_using htmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

A topologia é recomendada para os clientes que planejam usar o AEM Forms no servidor JEE para recursos de gerenciamento de processos (HTML Workspace) sem usar nenhum pós-processamento, formulários adaptáveis, formulários HTML5 e recursos de comunicação interativos.

### Topologia para usar formulários adaptáveis, formulários HTML5, recursos de comunicação interativa {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Os clientes da AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, HTML5 Forms, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para usar recursos de comunicação interativos do AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Você pode fazer as seguintes alterações/personalizações na topologia sugerida acima:

* O uso do HTML Workspace e do aplicativo AEM Forms requer um autor ou uma instância de processamento de AEM. Você pode usar a instância do autor de AEM incorporada ao AEM Forms no servidor JEE em vez de configurar um servidor de autor de AEM externo adicional.
* Uma instância de Autor ou Processamento do AEM é necessária apenas para fluxos de trabalho centrados no Forms no OSGi, formulários adaptáveis, portal de formulários e comunicação interativa.
* a interface do usuário do agente de comunicação interativa geralmente é executada na organização. Portanto, você pode manter um servidor de publicação para a interface do usuário do agente na rede privada.
* Os formulários AEM na instância OSGi integrada ao AEM Forms no servidor JEE também podem executar fluxos de trabalho centrados no Forms em OSGi e Pastas vigiadas.

## Amostra de topologias físicas para usar o AEM Forms no OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologia para captura de dados, comunicação interativa, fluxo de trabalho centralizado em formulários nos recursos OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Os clientes da AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, HTML5 Forms, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para usar comunicações interativas e fluxos de trabalho centrados na Forms no recurso OSGi, por exemplo, para usar AEM Caixa de entrada e o aplicativo AEM Forms para fluxos de trabalho de processos comerciais.

![interative-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologia para usar recursos de pasta monitorada para processamento em lote offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Os clientes do AEM Forms que planejam usar Pastas vigiadas para o processamento em lote podem ter uma topologia semelhante à exibida abaixo. A topologia exibe um ambiente em cluster, mas você decide usar uma única instância ou um farm de servidores da AEM Forms, dependendo da carga. A fonte de dados de terceiros é seu próprio sistema de registro. Ele atua como uma fonte de entrada para Pastas vigiadas. A topologia também exibe a saída no formulário de um arquivo impresso. Você também pode armazenar o conteúdo de saída em um sistema de arquivos, enviar por email e usar outros métodos personalizados para consumir saída.

![processamento em lote offline-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topologia para usar recursos de serviços de documento para processamento offline baseado em API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Os clientes da AEM Forms que planejam usar somente o recurso de serviços de documento podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar um cluster do AEM Forms em servidores OSGi. Essa topologia é recomendada quando a maioria dos usuários acessa programaticamente (usando APIs) o servidor do AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é bastante útil em vários cenários de clientes de software. Por exemplo, vários clientes que usam o serviço PDF Generator para criar documentos PDF sob demanda.

Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer o planejamento da capacidade, o balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de formulários adaptáveis. Ele ajuda a fornecer desempenho ideal e dimensionar os servidores independentemente uns dos outros.

![processamento com base em api offline](assets/offline-api-based-processing.png)
