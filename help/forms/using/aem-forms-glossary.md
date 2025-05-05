---
title: Glossário do AEM Forms
description: O Glossário do AEM Forms fornece uma lista abrangente dos principais termos, definições e conceitos usados no Adobe Experience Manager Forms (AEM Forms), ajudando os usuários a entender e trabalhar com formulários adaptáveis e recursos relacionados.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# Glossário do AEM Forms

## [Formulários adaptáveis](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

Formulários dinâmicos e responsivos que ajustam o layout e a apresentação com base no dispositivo e na entrada do usuário, aprimorando a experiência do usuário em várias plataformas. Inclui lógica condicional, vinculação de dados dinâmicos e comportamento baseado em regras.

## [Controle de Versão do Formulário Adaptável](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

Capacidade de gerenciar várias versões de um formulário no repositório, usando o controle de versão de nó JCR. Garante trilhas de auditoria e reversão fácil para formulários adaptáveis.

## [Integração do Adobe Analytics Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Fornece insights detalhados sobre as interações do usuário (por exemplo, quedas de campo, tempo gasto por seção) usando o Adobe Analytics, permitindo a otimização orientada por dados do design do formulário.

## [Pacote complementar do AEM Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Um aplicativo implantado no Adobe Experience Manager (AEM) como um pacote, contendo serviços (provedores de API) e servlets ou JSPs gerenciados pela estrutura AEM Sling.

## [AEM Forms no JEE](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Uma opção de implantação do AEM Forms que aproveita os servidores Java Enterprise Edition (JEE), fornecendo escalabilidade de nível empresarial, gerenciamento de transações e suporte para fluxos de trabalho corporativos complexos.

## [AEM Forms no OSGi](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

O AEM Forms no ambiente OSGi é o AEM Author padrão ou o pacote AEM Publish com AEM Forms implantado nele. Você pode executar o AEM Forms no OSGi em um único ambiente de servidor, Farm e configurações em cluster. A configuração do cluster está disponível somente para instâncias do Autor AEM.

## [Adobe Sign no AEM Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

Um serviço RESTful para fluxos de trabalho de assinatura digital seguros e contínuos. Ele se integra ao AEM Forms usando autenticação baseada em OAuth, permitindo coleções de assinaturas automatizadas e rastreamento em tempo real.

## [Serviços de documento da AEM Forms 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

APIs fornecidas pela camada da Web do AEM Forms para consumo remoto por clientes baseados em HTTP, como o SDK móvel de formulários.Funcionalidades no AEM Forms que permitem a criação, montagem, distribuição e arquivamento de documentos PDF, adição de assinaturas digitais e decodificação de Forms com código de barras.

| **Nome do Serviço** | **Descrição** | **Link de Documentação** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Serviço do Forms** | Renderize PDF forms usando modelos e XML, integre dados de formulário para importação/exportação e aceite renderização baseada em fragmento. | [Documentação de serviço do Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Serviço de saída** | Gera documentos mesclando dados com modelos em formatos como PDF, PCL ou PostScript. | [Documentação do Serviço de Saída](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Serviço de Assembler** | Combina, reorganiza, valida e aumenta documentos PDF e XDP. | [Documentação do Serviço de Assembler](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **Serviço ConvertPDF** | Converte documentos PDF em formatos PostScript ou de imagem como PNG, JPEG ou TIFF. | [Documentação do ConvertPDF Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Serviço Forms com código de barras** | Extrai dados de códigos de barras em arquivos TIFF e PDF para automatizar os processos de captura de dados. | [Documentação de serviço do Forms com códigos de barras](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance Service** | Criptografa, decodifica, assina digitalmente e aplica políticas de segurança de documentos aos PDF. | [Documentação do DocAssurance Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **Serviço de PDF Generator** | Converte formatos de arquivo nativos (por exemplo: Microsoft Word, Excel) em documentos PDF. | [Documentação de serviço do PDF Generator](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [APIs de as a Cloud Service de comunicação do Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

O AEM Forms as a Cloud Service fornece ferramentas avançadas para gerenciar formulários e fluxos de trabalho de comunicação, oferecendo suporte para a criação contínua de formulários digitais, captura de dados e comunicações personalizadas. As APIs de comunicação na nuvem fornecem geração, manipulação, validação e integração seguras de documentos sob demanda e em lote com sistemas externos por meio de HTTP, garantindo operações simplificadas e seguras.

| **Nome do Serviço** | **Descrição** | **Link de Documentação** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Geração de documentos** | Combine um modelo (XFA ou PDF) com dados XML para gerar documentos em formatos de PDF e impressão, como formatos PS, PCL, DPL, IPL e ZPL. | [Documentação de geração de documentos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=pt-BR#document-generation) |
| **Manipulação de documentos** | Combine e reorganize documentos do PDF. | [Documentação de manipulação de documentos](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **Conversão de documentos** | Converta um PDF em PDF/A e verifique a conformidade com PDF/A. | [Documentação de conversão de documentos](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **Assurance do documento** | Adicionar ou remover campos de assinatura, assinar, certificar, criptografar, descriptografar e aplicar direitos de uso a documentos do PDF. | [Documentação do Assurance do documento](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **Assinaturas Digitais** | Integra o Adobe Sign para assinatura eletrônica segura de formulários e documentos. | [Documentação de assinaturas digitais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=pt-BR#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

Um aplicativo de desktop para criar, editar e implantar workflows, bem como gerenciar processos de negócios centrados em formulários. Ele fornece integração com serviços e sistemas back-end.

## [Arquétipo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/overview)

Um modelo ou padrão no AEM usado para gerar um novo projeto com uma estrutura predefinida, facilitando a padronização, a configuração rápida e a adesão às práticas recomendadas de desenvolvimento do AEM.

## [Instância do Autor](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

O ambiente em que os criadores e administradores de conteúdo projetam, criam e gerenciam conteúdo antes de publicá-lo. Oferece suporte a controle de versão, visualização e teste.

## [Front-end de Criação](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Uma interface de usuário para criação e gerenciamento de formulários no AEM Forms.

## [Bloco de formulários adaptáveis](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

Uma unidade de encapsulamento que agrupa logicamente componentes e metadados relacionados, permitindo o manuseio dinâmico de dados e fácil escalabilidade em formulários de várias etapas.

## [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/introduction)

Blocos de construção reutilizáveis prontos para uso para criar formulários, incluindo campos de formulário, contêineres de layout, botões e outros elementos interativos.

## [Gerenciamento de correspondência](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

Um módulo que permite que as empresas criem, gerenciem e entreguem correspondência personalizada usando modelos, regras e fontes de dados predefinidos. Inclui modelos de cartas, comunicações com o cliente e geração de lote.

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

O Java Content Repository (JCR) integrado no AEM, que armazena dados estruturados e não estruturados, permitindo o armazenamento hierárquico de conteúdo, modelos e configurações.

## [Componente personalizado](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Um componente personalizado que estende a funcionalidade do AEM Forms, desenvolvido com o uso de Modelos Sling, Sightly (HTL) e Java. Normalmente usado para lógica de negócios exclusiva ou interatividade avançada do lado do cliente.

## [XCI Personalizado (Informações de Configuração XML)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

No Adobe Experience Manager (AEM) Forms, um arquivo XCI (Informações de configuração XML) personalizado permite que os administradores definam propriedades de renderização específicas para formulários e documentos. Ao definir as configurações XCI no console de administração, é possível substituir os padrões do sistema por opções personalizadas, garantindo um processamento e uma apresentação de formulários personalizados.

## [Integração de dados](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Integração contínua de fontes de dados externas, como bancos de dados, serviços da Web ou APIs REST, em formulários e fluxos de trabalho para permitir experiências do usuário dinâmicas e personalizadas.

## [Fontes de dados](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

Interfaces para integração de dados externos em formulários, incluindo JDBC para bancos de dados relacionais, endpoints REST para serviços da Web e OData para sistemas SAP. Gerenciado por meio da estrutura de integração de dados da AEM Forms.

## [Fragmentos do documento](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/letters-correspondences/lists)

Componentes reutilizáveis de documentos, como cabeçalhos, rodapés, isenções de responsabilidade ou cláusulas, que podem ser incluídos dinamicamente em formulários ou correspondência para garantir a consistência.

## [Documento de Registro (DoR)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

Um recurso no AEM Forms que gera uma versão de arquivamento não editável de um formulário enviado, normalmente no formato PDF, preservando o conteúdo e o layout exatos como um registro da transação.

## [Edge Delivery Services](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/overview)

Entrega de conteúdo otimizada para o AEM Forms, garantindo latência reduzida para ativos como formulários, temas e bibliotecas de clientes, em que os autores podem atualizar e publicar conteúdo rapidamente.

## [Integração do Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Envolve a conexão do AEM Forms a sistemas corporativos (por exemplo, SAP, Salesforce) usando pacotes e conectores OSGi, com suporte a fluxos de dados bidirecionais e atualizações em tempo real.

## [Revisão do formulário](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

Um recurso orientado por fluxo de trabalho que permite às partes interessadas revisar formulários adaptáveis, adicionar anotações e aprovar alterações antes de publicar. Usa a Caixa de entrada e o gerenciamento de tarefas do AEM.

## [Modelo de dados de formulário (FDM)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

Uma camada de representação que conecta formulários adaptáveis a fontes de dados de back-end, permitindo a integração com serviços Web RESTful, serviços SOAP e OData. O FDM permite que os autores de formulários mapeiem campos de formulário diretamente para estruturas de dados de back-end, garantindo uma sincronização perfeita da entrada do usuário com sistemas externos.

## [Localização de formulário](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

O processo de formulários adaptáveis para suportar vários idiomas e configurações regionais, garantindo que os formulários sejam acessíveis e fáceis de usar para um público diversificado.

## [Portal de formulários](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Os componentes do Forms Portal equipam os desenvolvedores da Web com componentes para criar e personalizar um Forms Portal em sites criados usando o Adobe Experience Manager (AEM). Ele permite que os usuários descubram, acessem e enviem formulários com eficiência em plataformas da Web e móveis.

## [Front-end de Representação e Envio de Formulário](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Uma interface de usuário final no AEM Forms que permite aos usuários visualizar e enviar formulários por meio de um navegador da Web.

## [Conjuntos de formulários](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

Uma coleção de formulários relacionados agrupados para serem apresentados como uma única entidade aos usuários, permitindo que processos complexos de coleta de dados sejam divididos em seções gerenciáveis.

## [Forms Designer](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

Um aplicativo independente usado para criar o modelo de formulários no formulário XDP e usá-lo no AEM Forms para gerar o Documento de registro.

## [Fluxo de trabalho centrado no Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

Um conjunto de etapas automatizadas ou manuais no AEM Forms que gerenciam processos de negócios, como aprovação de documentos, publicação de conteúdo ou notificações do usuário.

## [Comunicação interativa](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

Uma implementação personalizada para gerenciar comunicações altamente personalizadas e multicanais. Ele combina dados de várias fontes, como sistemas CRM ou ERP, para fornecer comunicações em formatos como Web, móvel, email e impressão.

## [JCR (Java Content Repository)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

Um repositório hierárquico, baseado em padrões, para armazenamento de conteúdo, configurações e metadados no AEM, que oferece suporte ao armazenamento estruturado e não estruturado de dados.

## [Cartas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

Comunicações geradas pelo cliente aproveitando os Serviços de documento da AEM Forms. As cartas são criadas usando uma combinação de modelos XDP, modelos de dados e fragmentos reutilizáveis, garantindo a escalabilidade em cenários de alto volume.

## [Metadados no AEM Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

Os metadados permitem a categorização e a recuperação eficientes de ativos. O AEM Forms inclui metadados predefinidos para cada tipo de ativo e permite personalização. Ele também fornece ferramentas para criar, gerenciar e trocar metadados sem interrupções.

## [Gerador de PDF](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

Uma ferramenta no AEM Forms que converte vários formatos de arquivo (por exemplo: Word, Excel, PowerPoint) em documentos PDF e fornece recursos como criptografia, marca d&#39;água e mesclagem.

## [Instância do Publish](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

O ambiente no AEM que fornece conteúdo ao vivo aos usuários finais. Ele fornece formulários, páginas e outras experiências digitais com desempenho otimizado.

## [Editor de regras](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

Uma ferramenta visual no Adaptive Forms que permite aos autores definir regras e lógica personalizadas para campos de formulário, como visibilidade, validação e pré-preenchimento de dados, sem exigir conhecimento em codificação.

## [Assinaturas Escritas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

Um recurso no AEM Forms que permite que os usuários assinem formulários eletronicamente desenhando sua assinatura diretamente no formulário com o uso de um mouse ou dispositivo habilitado para toque.

## [Enviar Ação no AEM Forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

Ações do lado do servidor ou do lado do cliente executadas no envio do formulário. Os exemplos incluem chamadas de API REST, chamar um fluxo de trabalho ou gravar dados em um JCR (Java Content Repository).

## [Temas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

Estruturas de estilo orientadas por CSS aplicadas a formulários adaptáveis, utilizando MENOS/SASS para pré-processadores. Os temas garantem a conformidade com as diretrizes de marca e os padrões de acessibilidade. Você pode personalizar um tema, alterar seus elementos de design, layout, cores, tipografia e, às vezes, o código subjacente.

## [Modelo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

Blueprints para formulários adaptáveis, incluindo elementos estruturais (campos, layouts) e scripts pré-configurados, você pode criar e personalizar novos modelos ou usar modelos prontos para uso existentes.

## [Camada da Web](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Inclui JSPs ou servlets criados em serviços comuns da e de formulários, fornecendo funcionalidades como front-end de criação, front-end de representação e envio de formulários e APIs REST.

## [XDP (Pacote de Dados XML)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

Um formato de arquivo usado no AEM Forms para projetar e estruturar formulários, permitindo a renderização como PDF ou HTML enquanto suporta conteúdo dinâmico e interatividade.

## [XFA (Arquitetura XML Forms)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

Uma tecnologia herdada para criar PDF forms interativos e dinâmicos. Os formulários XFA permitem recursos avançados, como ajustes de layout dinâmicos, scripts e integração contínua com sistemas de back-end.

## [Esquema XML ou JSON](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

Uma estrutura padronizada usada para definir o formato e a organização dos dados XML ou JSON em formulários e fluxos de trabalho. Esses esquemas garantem o manuseio consistente de dados e permitem a interoperabilidade com sistemas externos.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->