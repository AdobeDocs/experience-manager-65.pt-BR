---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada no  [!DNL Adobe Experience Manager], usando o Serviço de Conteúdo Inteligente.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 19%

---

# Preparar [!DNL Assets] para marcação inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de começar a marcar seus ativos usando os Serviços de Conteúdo Inteligente, integre o [!DNL Experience Manager Assets] ao Adobe Developer Console para usar o serviço inteligente do [!DNL Adobe Sensei]. Depois de configurado, treine o serviço usando algumas imagens e uma tag.

>[!NOTE]
>
>* Os Serviços de Conteúdo Inteligente não estão mais disponíveis para novos [!DNL Experience Manager Assets] clientes locais. Os clientes locais existentes que já têm esse recurso ativado podem continuar usando os Serviços de conteúdo inteligente.
>* Os Serviços de Conteúdo Inteligente estão disponíveis para [!DNL Experience Manager Assets] clientes atuais do Managed Services que já têm esse recurso habilitado.
>* Os novos clientes do Managed Services [!DNL Experience Manager Assets] podem seguir as instruções mencionadas neste artigo para configurar os Serviços de Conteúdo Inteligente.

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte:

* [Integrar ao Adobe Developer Console](#integrate-adobe-io).
* [Treine o Serviço de Conteúdo Inteligente](#training-the-smart-content-service).

* Instale o [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR) mais recente.

## Integrar ao Adobe Developer Console {#integrate-adobe-io}

Quando você integra com o Adobe Developer Console, o servidor do [!DNL Experience Manager] autentica suas credenciais de serviço no gateway do Adobe Developer Console antes de encaminhar sua solicitação ao Serviço de Conteúdo Inteligente. Para integrar o, é necessário ter uma conta do Adobe ID com privilégios de administrador para a organização e uma licença do Serviço de conteúdo inteligente adquirida e ativada para a organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. Para gerar uma chave pública, [Crie uma configuração do Serviço de Conteúdo Inteligente](#obtain-public-certificate) em [!DNL Experience Manager]. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.

1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.

1. [Configure sua implantação](#configure-smart-content-service) usando a chave de API e outras credenciais da Adobe Developer Console.

1. [Teste a configuração](#validate-the-configuration).

1. Opcionalmente, [habilite a marcação automática no carregamento de ativos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obter certificado público criando uma configuração do Serviço de conteúdo inteligente {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Adobe Developer Console.

1. Na interface de usuário do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]**.

1. Na página Cloud Service, clique em **[!UICONTROL Configurar agora]** em **[!UICONTROL Tags inteligentes da Assets]**.

1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um título e nome para a configuração de Tags Inteligentes. Clique em **[!UICONTROL Criar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de Conteúdo Inteligente do AEM]**, use os seguintes valores:

   **[!UICONTROL URL de Serviço]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por exemplo, `https://smartcontent.adobe.io/apac`. Você pode especificar `na`, `emea` ou `apac` como as regiões onde a instância do autor do Experience Manager está hospedada.

   >[!NOTE]
   >
   >Se o Serviço gerenciado de Experience Manager for provisionado antes de 1° de setembro de 2022, use o seguinte URL de serviço:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a serem fornecidos posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo do Serviço de Conteúdo Inteligente do Experience Manager para fornecer a URL do serviço de conteúdo](assets/aem_scs.png)


   *Figura: caixa de diálogo Serviço de Conteúdo Inteligente para fornecer a URL do serviço de conteúdo*

   >[!NOTE]
   >
   >A URL fornecida como [!UICONTROL URL de Serviço] não pode ser acessada pelo navegador e gera um erro 404. A configuração funciona bem com o mesmo valor do parâmetro [!UICONTROL URL de Serviço]. Para obter o status geral do serviço e o agendamento de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar Certificado Público para Integração com o OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configurações do serviço de marcação inteligente.*

#### Reconfigure quando um certificado expirar {#certrenew}

Depois que um certificado expira, ele deixa de ser confiável. Não é possível renovar um certificado expirado. Para adicionar um certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique na guia **[!UICONTROL Armazenamento de chaves]**.

1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Armazenamento de Chaves para adicionar um certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: exclua a entrada `similaritysearch` existente no Armazenamento de Chaves para adicionar um certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. Para baixar um certificado público, clique em **[!UICONTROL Baixar Certificado Público para Integração com o OAuth]**.

1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de Conteúdo Inteligente existentes na página **[!UICONTROL Integrações]**. Faça upload do novo certificado. Para obter mais informações, consulte as instruções em [Criar integração com o Adobe Developer Console](#create-adobe-i-o-integration).

### Criar integração do Adobe Developer Console {#create-adobe-i-o-integration}

Para usar APIs do Serviço de Conteúdo Inteligente, crie uma integração no Adobe Developer Console para obter a [!UICONTROL Chave de API] (gerada no campo [!UICONTROL ID do CLIENTE] da integração com o Adobe Developer Console), a [!UICONTROL ID da CONTA TÉCNICA], a [!UICONTROL ID DA ORGANIZAÇÃO] e o [!UICONTROL SEGREDO DO CLIENTE] para as [!UICONTROL Configurações do Serviço de Marcação Inteligente da Assets] da configuração de nuvem em [!DNL Experience Manager].

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.

   A página [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública da conta de serviço.

1. Clique em **[!UICONTROL Avançar]**.

1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**.

   Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores nas [!UICONTROL Configurações do Serviço de Marcação Inteligente da Assets] da configuração de nuvem no [!DNL Experience Manager] para configurar marcas inteligentes.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)


   *Figura: Detalhes da integração no Adobe Developer Console*

### Configurar o serviço de conteúdo inteligente {#configure-smart-content-service}

>[!CAUTION]
>
>Anteriormente, as configurações feitas com Credenciais JWT agora estavam sujeitas a desativação no Adobe Developer Console. Não será possível criar novas credenciais JWT após 3 de junho de 2024. Essas configurações não podem mais ser criadas ou atualizadas, mas podem ser migradas para configurações OAuth.
> Consulte [Configuração de integrações IMS para AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>Consulte [Etapas para configurar o OAuth para usuários locais](#config-oauth-onprem)
> Consulte [Solução de problemas de tags inteligentes para credenciais do OAuth](#config-smart-tagging.md)

Para configurar a integração, use os valores dos campos [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], [!UICONTROL SEGREDO DO CLIENTE] e [!UICONTROL ID DO CLIENTE] da integração com o Adobe Developer Console. Criar uma configuração de nuvem de Tags Inteligentes permite a autenticação de solicitações de API da implantação [!DNL Experience Manager].

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services herdados]** para abrir o console [!UICONTROL Cloud Services].

1. Nas **[!UICONTROL Tags inteligentes do Assets]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave da API], [!UICONTROL ID da Conta Técnica], [!UICONTROL ID da Organização] e [!UICONTROL Segredo do Cliente], copie e use os seguintes valores gerados na [integração com o Adobe Developer Console](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do Serviço de Marcação Inteligente do Assets] | Campos de integração do [!DNL Adobe Developer Console] |
   |--- |--- |
   | [!UICONTROL Chave de API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da Conta Técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da Organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Segredo do cliente] | [!UICONTROL SEGREDO DO CLIENTE] |

### Configurar OAuth para usuários locais {#config-oauth-onprem}

#### Pré-requisitos {#prereqs-config-oauth-onprem}

Um escopo de autorização é uma cadeia de caracteres OAuth que contém os seguintes pré-requisitos:

* Crie uma nova integração OAuth no [Developer Console](https://developer.adobe.com/console/user/servicesandapis) usando o `ClientID`, `ClientSecretID` e `OrgID`.
* Adicionar os seguintes arquivos no caminho `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configurar OAuth para usuários locais {#steps-config-oauth-onprem}

1. Adicionar ou atualizar as propriedades abaixo em `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Atualize o `auth.token.provider.client.id` com a ID de cliente da nova configuração OAuth.
   * Atualizar `auth.access.token.request` para `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Renomeie o arquivo para `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Execute as etapas abaixo em `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Atualize a propriedade auth.ims.client.secret com o Segredo do cliente da nova integração OAuth.
   * Renomear o arquivo para `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Salve todas as alterações no console de desenvolvimento do repositório de conteúdo, por exemplo, CRXDE.
5. Navegue até `/system/console/configMgr` e substitua a configuração OSGi de `.<randomnumber>` até `-<randomnumber>`.
6. Exclua a configuração antiga para `"Access Token provider name: adobe-ims-similaritysearch"` em `/system/console/configMgr`.
7. Reinicie o console.

### Validar a configuração {#validate-the-configuration}

Após concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu servidor [!DNL Experience Manager] em `https://[aem_server]:[port]`.

1. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** para abrir o console OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL Tarefas Diversas de SimilaritySearch]**.

1. Clique em `validateConfigs()`. Na caixa de diálogo **[!UICONTROL Validar Configurações]**, clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos no mesmo diálogo.

### Habilitar marcação inteligente no fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. Em [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.

1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.

1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: etapa para adicionar ativo de marca inteligente após a etapa de miniatura do processo no fluxo de trabalho [!UICONTROL Ativo de atualização DAM].*

1. Abra a etapa no modo de edição. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar a etapa de marca inteligente](assets/smart-tag-step-properties-workflow1.png)


   *Figura: configurar o fluxo de trabalho Atualizar ativo do DAM e adicionar a etapa de marca inteligente*

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho seja concluído mesmo se a etapa de marcação automática falhar.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de marca inteligente e selecionar o manipulador avançado](assets/smart-tag-step-properties-workflow2.png)


   *Figura: configure o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de marca inteligente e selecione o manipulador avançado*

   Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de marca inteligente e selecionar ignorar sinalizador de Marca Inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: configure o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de marca inteligente e selecione Ignorar sinalizador de Marca Inteligente.*

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e salve o fluxo de trabalho.

## Treinar o serviço de conteúdo inteligente {#training-the-smart-content-service}

Para que o Serviço de conteúdo inteligente reconheça sua taxonomia comercial, execute-a em um conjunto de ativos que já incluem tags relevantes para sua empresa. Para marcar com eficiência as imagens da sua marca, o Serviço de conteúdo inteligente exige que as imagens de treinamento estejam em conformidade com determinadas diretrizes. Após o treinamento, o serviço pode aplicar a mesma taxonomia a um conjunto semelhante de ativos.

Você pode treinar o serviço várias vezes para melhorar sua capacidade de aplicar tags relevantes. Após cada ciclo de treinamento, execute um fluxo de trabalho de marcação e verifique se os ativos estão marcados corretamente.

Você pode treinar o Serviço de conteúdo inteligente periodicamente ou conforme necessário.

>[!NOTE]
>
>O fluxo de trabalho de treinamento é executado somente em pastas.

### Diretrizes para treinamento {#guidelines-for-training}

Para obter melhores resultados, as imagens no seu conjunto de treinamento estão em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 30 imagens por tag. Mínimo de 500 pixels no lado maior.

**Coerência**: imagens usadas para uma marca específica são visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: use variedade suficiente nas imagens do treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que o Experience Manager aprenda a focar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem destacada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Distração/obstrução**: o serviço treina melhor imagens que têm menos distração (planos de fundo proeminentes, acompanhamentos não relacionados, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *casual-shoes*, a segunda imagem não é um bom candidato para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como `raincoat` e `model-side-view`, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar em suas tags e aplicá-las em outras imagens depende da qualidade de imagens usadas para treinamento. Para obter melhores resultados, a Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço para cada tag.

### Formação periódica {#periodic-training}

Você pode ativar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e nas tags associadas em uma pasta. Abra a página [!UICONTROL Propriedades] da pasta de ativos, selecione **[!UICONTROL Habilitar Tags Inteligentes]** na guia **[!UICONTROL Detalhes]** e salve as alterações.

![habilitar_marcas_inteligentes](assets/enable_smart_tags.png)

Depois que essa opção é selecionada para uma pasta, o [!DNL Experience Manager] executa automaticamente um fluxo de trabalho de treinamento para treinar o Serviço de Conteúdo Inteligente nos ativos da pasta e suas marcas. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 aos sábados.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. Na interface do [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de Fluxo de Trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Treinamento de Tags Inteligentes]** e clique em **[!UICONTROL Iniciar Fluxo de Trabalho]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Executar Fluxo de Trabalho]**, navegue até a pasta de carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e as tags são enviados para treinamento.

   ![caixa_de_diálogo_de_fluxo](assets/workflow_dialog.png)

>[!NOTE]
>
>Quando os ativos em uma pasta forem processados para treinamento, somente os ativos modificados serão processados nos ciclos de treinamento subsequentes.

### Exibir relatórios de treinamento {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, revise o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na interface do [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de Tags Inteligentes]** e clique em **[!UICONTROL Avançar]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório.

   O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o Serviço de conteúdo inteligente foi treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag.

   Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.

1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Baixar]** na barra de ferramentas. O relatório é baixado como uma planilha do Microsoft Excel.

## Limitações {#limitations}

* As tags inteligentes aprimoradas se baseiam em modelos de aprendizagem de imagens e suas tags. Esses modelos nem sempre são perfeitos para identificar tags. A versão atual do Serviço de conteúdo inteligente tem as seguintes limitações:

   * Incapacidade de reconhecer diferenças sutis nas imagens. Por exemplo, camisetas finas versus camisetas convencionais.
   * Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em camisetas.
   * Há suporte para marcação nas localidades nas quais [!DNL Experience Manager] tem suporte.

* Para pesquisar ativos com marcas inteligentes (comuns ou aprimoradas), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar Tags Inteligentes](enhanced-smart-tags.md)
>* [Solução de problemas de marcas inteligentes para credenciais do OAuth](config-oauth.md)
>* [Tutorial em vídeo sobre marcas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
