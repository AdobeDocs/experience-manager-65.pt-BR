---
title: Recursos e aprimoramentos principais cumulativos na versão Adobe Experience Manager 6.5.
description: Uma lista cumulativa dos principais recursos e aprimoramentos feitos no Adobe Experience Manager 6.5 em relação às oito versões anteriores do service pack.
content-type: reference
docset: aem65
feature: Release Information
role: User, Admin
source-git-commit: 4fab3f80e01c2b7c3e4ebdc4bffdedb6f5f39d11
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 13%

---


# Principais recursos e aprimoramentos cumulativos

Uma lista cumulativa dos principais recursos e aprimoramentos do Adobe Experience Manager 6.5 nas oito versões anteriores do service pack.

Consulte também [Notas de versão mais recentes do Service Pack do Adobe Experience Manager 6.5](/help/release-notes/release-notes.md).

## AEM 6.5, Service Pack 18 — 7 de dezembro de 2023

* Ativação do usuário do Editor de páginas do Sites/Componente de imagem para fazer referência a ativos do Cloud Service remoto de Ativos. (SITES-13448, SITES-13433)
* O AEM agora é compatível com a classificação do lado do servidor para agilizar a navegação do projeto na exibição em lista. Os nós de projeto são classificados com base na coluna selecionada pelo usuário antes de aparecer na interface.

### [!DNL Forms]

* **Novos componentes principais do formulário adaptável**: guias verticais, Termos e condições e Caixa de seleção são adicionados para aprimorar a escalabilidade dos formulários.
   * **[Componente da caixa de seleção](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de caixa de seleção. Permite que os usuários façam escolhas binárias, selecionando ou desmarcando uma opção específica. Normalmente, ela aparece como uma pequena caixa que pode ser clicada ou tocada para alternar entre dois estados: marcado e desmarcado. A caixa de seleção é um elemento de formulário comum usado para apresentar uma opção sim/não ou verdadeira/falsa.

   * **[Componente dos Termos e condições](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de Termos e condições. Ela permite que os autores do Forms introduzam uma seção específica no formulário em que os usuários recebem os termos, condições ou contratos legais associados ao uso de um serviço, produto ou plataforma. Esse componente foi projetado para informar os usuários sobre as regras, regulamentos e obrigações aos quais eles estão concordando ao enviar o formulário.

     ![Guias verticais, Termos e condições e componentes Caixa de seleção](/help/forms/using/assets/forms-components.png)

   * **[Componente de guias verticais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: o Forms adaptável baseado em Componentes principais agora pode organizar o conteúdo do formulário em uma lista vertical de guias, fornecendo um layout estruturado e navegável. O uso de guias verticais em um formulário pode aprimorar a experiência geral do usuário simplificando a navegação e melhorando a organização do conteúdo do formulário, especialmente em situações em que um formulário contém várias seções ou informações complexas.

* **[Versão de 64 bits do AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: A versão de 64 bits do AEM Forms Designer oferece desempenho, escalabilidade e gerenciamento de memória aprimorados para potencializar a experiência de criação de formulários. Com a arquitetura de 64 bits, você pode executar projetos ainda maiores e mais complexos com facilidade, garantindo fluxos de trabalho de design ininterruptos e eficiência otimizada. Aumente os recursos de design de formulário e abrace o futuro do AEM Forms Designer com esta versão de última geração.

* **[Conectar um Forms adaptável com a lista Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: o AEM Forms fornece uma integração OOTB para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você use os recursos de Listas do SharePoint. Você pode configurar a Lista de SharePoint Microsoft® como uma fonte de dados para um Modelo de dados de formulário e usar a ação de envio Enviar usando Modelo de dados de formulário para conectar um Formulário adaptável à Lista de SharePoint.

* **[Suporte para configurar propriedades do documento de registro para fragmentos de formulário adaptável](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Agora é possível personalizar facilmente os fragmentos do Formulário adaptável e seus campos no editor de Formulário adaptável.

* **XMLFM de 64 bits**: a iteração de 64 bits do XMLFM apresenta desempenho aprimorado, escalabilidade e gerenciamento refinado de memória. É o primeiro serviço nativo de 64 bits implantado no lado do servidor. Ao utilizar sua capacidade inerente de acessar recursos de memória maiores em comparação ao seu equivalente de 32 bits, o XMLFM de 64 bits capacita o manuseio ininterrupto de cargas de trabalho de renderização maiores. Esse marco não só representa um salto no desempenho, como também introduz aprimoramentos importantes na estrutura de serviço nativa no AEM Forms Server. Essa atualização possibilita ao AEM Forms Server oferecer suporte ininterrupto a qualquer serviço nativo de 64 bits.

## AEM 6.5, Service Pack 18 — 24 de agosto de 2023

* Assets, Dynamic Media - [Suporte a faixas de várias legendas e áudio para vídeos no Dynamic Media](/help/assets/video.md#about-msma)—Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis em um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.
* Ativos - Nos resultados da Pesquisa, agora é possível navegar até o local da pasta que contém um ativo para permitir que você execute várias tarefas de gerenciamento de ativos.
* O Seletor de polaris de sites em fragmentos de conteúdo melhorou o desempenho.
* Ativação do usuário do Editor de páginas do Sites/Componente de imagem para fazer referência a ativos do Cloud Service remoto de Ativos.
* Para localizar rapidamente um projeto na exibição em Lista, onde você pode ter muitos projetos em seu sistema, o Adobe agora é compatível com a classificação do lado do servidor. Os nós de projeto são classificados no backend com base na coluna selecionada pelo usuário antes de renderizá-los na interface.
* O AEM 6.5.18.0 é compatível com MongoDB 5.0 para 6.0.

### [!DNL Forms]

* **[Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)** - Agora você pode chamar uma função personalizada (usando a Biblioteca do cliente) em resposta a um erro retornado por um serviço externo. Além disso, você pode fornecer uma resposta personalizada aos usuários finais. Como alternativa, você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode chamar um fluxo de trabalho personalizado no backend para códigos de erro específicos ou informar ao cliente que o serviço está inativo

* **[Etapa de fluxo de trabalho aprimorada do Adobe Sign](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - A etapa de fluxo de trabalho do Adobe Sign em fluxos de trabalho de AEM está disponível com as seguintes melhorias.

   * **Segurança aprimorada com autenticação baseada em ID do governo para Adobe Sign** - A Autenticação com ID do governo da Adobe Acrobat Sign oferece uma camada adicional de verificação. Ele permite aos usuários autenticar sua identidade usando IDs emitidas pelo governo (CNH, identificação nacional, passaporte). Ao usar documentos de identificação confiáveis, esse aprimoramento adiciona um nível extra de confiança ao processo de assinatura, tornando-o ideal para cenários que exigem maior segurança, conformidade e validação do usuário.

   * **Maior transparência com a trilha de auditoria de documentos do Adobe Sign** : use o recurso Trilha de auditoria para obter insights detalhados sobre o ciclo de vida dos documentos do Adobe Sign. Com a Trilha de auditoria, agora é possível manter um registro abrangente de todas as ações e interações relacionadas aos documentos. Isso inclui detalhes como quem visualizou, editou ou assinou o documento, além de carimbos de data e hora para cada evento. Esse aprimoramento é fundamental para manter a conformidade, resolver disputas e garantir a integridade de seus contratos digitais.


   * **As funções dos destinatários do Contrato foram estendidas além apenas do Signatário** - O Adobe Acrobat Sign permite que você expanda as funções dos recipients do Contrato além apenas do Signatário para melhor corresponder aos requisitos de fluxo de trabalho. Quando habilitado, cada recipient em um Contrato tem sua função configurável individualmente, sendo que Signatário é o padrão.


* **[Instalador completo do AEM Forms no JEE](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** - O service pack traz um instalador completo para AEM Forms no JEE que oferece suporte para várias combinações de software novas, incluindo:
   * Microsoft® Windows Server 2022
   * Diretório ativo Microsoft® 2022
   * Oracle WebLogic 14C no Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Conector JDBC do MySQL 8

Se você estiver instalando ou planejando usar o software mais recente para o seu Forms AEM 6.5 no ambiente JEE, o Adobe recomenda o uso do instalador completo do Forms AEM 6.5.18.0 no JEE. Para explorar a lista completa de softwares recém-adicionados e obsoletos, consulte a documentação do AEM Forms no JEE ou do AEM Forms no OSGi.

## AEM 6.5, Service Pack 17 — 25 de maio de 2023

* **Melhorias na experiência de pesquisa**: agora você pode executar rapidamente as seguintes operações nos ativos exibidos nos resultados da pesquisa:
   * Criar um fluxo de trabalho
   * Criar uma versão
   * Criar ou remover relação de ativos

  Não é necessário navegar até o local do ativo e exibir suas propriedades para executar essas operações.
* **Dynamic Media _Instantâneo_**: experimente com imagens de teste ou URLs Dynamic Media para ver a saída de diferentes modificadores de imagem e otimizações de Imagem inteligente para tamanho de arquivo (com entrega de WebP e AVIF), largura de banda da rede e Proporção de pixels do dispositivo. Consulte [Instantâneo do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=pt-BR).
* **Transmissão DASH com o Dynamic Media** - Novo protocolo (DASH - Dynamic Adaptive Streaming over HTTP) iniciado para transmissão adaptável na entrega de vídeo do Dynamic Media (com CMAF ativado). Disponível agora para todas as regiões, [habilitado por meio de um tíquete de suporte](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integração do Experience Manager Sites e dos fragmentos de conteúdo ao Assets Next-Generation Dynamic Media** : os usuários do Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media agora podem usar esses ativos hospedados em nuvem para criação e entrega com instâncias locais ou do Managed Services do Experience Manager Sites 6.5.

### [!DNL Forms]

* **[Formulários adaptáveis no editor de páginas do AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: agora você pode usar o editor de páginas do AEM para criar e adicionar rapidamente vários formulários às páginas dos sites. Essa funcionalidade permite que os autores de conteúdo criem uma experiência perfeita para a captura de dados nas páginas de sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos empresariais. É possível:
   * Criar um formulário adaptável arrastando e soltando componentes de formulário no componente de Container de formulários adaptáveis do editor de sites do AEM ou de fragmentos de experiência.
   * Usar o assistente de formulários adaptáveis no editor de sites do AEM para criar formulários independentes de qualquer página de site, o que oferece a liberdade de reutilizar esses formulários em várias páginas.
   * Adicionar vários formulários a uma página de site, simplificando a experiência do usuário e fornecendo maior flexibilidade.
* **[Suporte ao reCAPTCHA Enterprise no Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: adição de suporte ao reCAPTCHA Enterprise no Experience Manager Forms, fornecendo proteção aprimorada contra atividades fraudulentas e spam, além do suporte existente ao Google reCAPTCHA v2.
* **[Suporte ao Adobe Acrobat Sign para o governo com Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: o AEM Forms agora se integra ao Adobe Acrobat Sign para o governo (compatível com FedRAMP). Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas ao governo (departamentos e agências governamentais). A integração com o Adobe Acrobat Sign para órgãos governamentais permite que parceiros da Adobe e clientes governamentais usem assinaturas eletrônicas em formulários adaptáveis para alguns dos ramos de negócios mais essenciais e confidenciais. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com o nível moderado de conformidade do FedRAMP, proporcionando tranquilidade aos clientes governamentais da Adobe.
* **Habilitar a integração do Salesforce com o Experience Manager Forms para troca de dados**: configure a integração entre o Experience Manager Forms e o aplicativo Salesforce usando o fluxo de credenciais do cliente OAuth 2.0. Essa capacidade permite a autenticação e autorização diretas e seguras do aplicativo e permite uma comunicação perfeita sem o envolvimento do usuário.
* **Otimização e funcionalidade aprimorada do motor de workflow**: aumente o desempenho dos mecanismos de workflow minimizando o número de instâncias de workflow. Além de `COMPLETED` e `RUNNING` valores de status, o workflow também suporta três novos valores de status: `ABORTED`, `SUSPENDED`, e `FAILED`.

## AEM 6.5, Service Pack 16 — 23 de fevereiro de 2023

O novo protocolo DASH (Dynamic Adaptive Streaming over HTTP) suporta o lançamento para transmissão adaptável de taxa de bits na entrega de vídeo do Dynamic Media (com CMAF [Formato de aplicativo de mídia comum] ativado).

* A transmissão adaptável (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos.
* DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.
* Disponível agora na Ásia-Pacífico e na América do Norte (a ser ativado por meio de um tíquete de suporte); em breve na Europa-Oriente Médio-África.

Consulte [Habilitar DASH na sua conta](/help/assets/video.md#enable-dash).

### [!DNL Forms]

* [Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR) permita que os desenvolvedores criem, publiquem e gerenciem formulários interativos que possam ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional.

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) são um conjunto de 24 componentes de código aberto, compatíveis com BEM, que foram criados com base nos Componentes principais do WCM no Adobe Experience Manager. Esses componentes são de código aberto e fornecem aos desenvolvedores a capacidade de personalizar e estender facilmente esses componentes para atender às necessidades específicas de sua organização. Qualquer pessoa com habilidades existentes para personalizar [Componentes principais do WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html) O pode personalizar e estilizar facilmente esses componentes.

* O serviço de extensão de Reader no OSGi agora fornece opções separadas para habilitar direitos de uso de importação e exportação em um PDF para importar ou exportar dados no Adobe Acrobat Reader.

## AEM 6.5, Service Pack 15 — 24 de novembro de 2022

### [!DNL Forms]

* O AEM Forms Designer agora está disponível em [Localidade espanhola](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
* Agora você pode usar [OAuth2 para autenticar com os protocolos de servidor de email do Microsoft® Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Você pode definir [Revalidar no servidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=pt-br#enabling-server-side-validation-br) para true para identificar os campos ocultos para exclusão de um Documento de registro no lado do servidor.
* O AEM Forms Designer requer a versão de 32 bits do Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Service Pack 14 — 25 de agosto de 2022

Somente correções de erros.

## AEM 6.5, Service Pack 13 — 26 de maio de 2022

* Usar CAPTCHA invisível em um formulário adaptável: agora é possível usar um CAPTCHA invisível para mostrar o desafio de CAPTCHA somente em caso de atividade suspeita. Se nenhuma atividade suspeita for encontrada, o desafio de CAPTCHA não será exibido. Isso ajuda a avaliar o preenchimento de formulários por humanos sem requisitos de caixa de seleção, reduz os esforços de personalização e melhora a experiência do usuário final.

* Adição de suporte para buscar cabeçalhos de resposta no pós-processador do modelo de dados de formulário para endpoints REST.

* Agora, ao gerar um arquivo de tradução do Formulário adaptável, a mesma sequência de textos que o arquivo XLIFF gerado é idêntica à sequência de componentes no Formulário adaptável correspondente.

* Quando você localiza um Formulário adaptável e faz até mesmo uma pequena alteração no texto do idioma base, a tradução completa fica ausente para todos os outros idiomas. O problema foi corrigido no [!DNL Experience Manager] 6.5.13.0

* Melhorias de acessibilidade para o Forms:

   * Adição de suporte para leitores de tela para reconhecer o cabeçalho e o corpo de uma tabela como entidades contínuas e conectadas. Isso ajuda os leitores de tela a navegar pelas tabelas corretamente. (NPR-37139)
   * Adição de suporte para leitores de tela para interromper a navegação no espaço de trabalho do HTML até que uma caixa de diálogo seja aberta.

## AEM 6.5, Service Pack 12 — 24 de fevereiro de 2022

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações de atualização, exclusão, renomeação e movimentação nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites.
* As implantações de push de uma origem de cópia ativa em várias cópias ativas agora são possíveis por padrão, sem exigir uma configuração de blueprint.
* O status das operações assíncronas em andamento agora é mostrado na interface para ajudar a impedir que os usuários acionem acidentalmente várias operações assíncronas no mesmo caminho.
* O suporte para autenticação baseada em IMS é fornecido para APIs do Analytics 2.0.
* Suporte de API para o fragmento de experiência do tipo oferta JSON.
* A solicitação de oferta agora é fornecida para a oferta de Exclusão (API do fragmento de experiência) no IMS.
* O repositório integrado (Apache Jackrabbit Oak) ainda permanece na versão 1.22.9.
