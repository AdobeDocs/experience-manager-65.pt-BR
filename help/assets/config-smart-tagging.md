---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada no [!DNL Adobe Experience Manager], utilizando o Serviço de conteúdo inteligente.
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

Antes de começar a marcar seus ativos usando os Serviços de conteúdo inteligente, integre [!DNL Experience Manager Assets] com o Adobe Developer Console para usar o serviço inteligente do [!DNL Adobe Sensei]. Depois de configurado, treine o serviço usando algumas imagens e uma tag.

>[!NOTE]
>
>* Os Serviços de conteúdo inteligente não estão mais disponíveis para novos [!DNL Experience Manager Assets] Clientes no local. Os clientes locais existentes que já têm esse recurso ativado podem continuar usando os Serviços de conteúdo inteligente.
>* Os Serviços de conteúdo inteligente estão disponíveis para [!DNL Experience Manager Assets] Clientes do Managed Services que já têm esse recurso ativado.
>* Novo [!DNL Experience Manager Assets] Os clientes do Managed Services podem seguir as instruções mencionadas neste artigo para configurar os Serviços de conteúdo inteligente.

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte:

* [Integração com o console do Adobe Developer](#integrate-adobe-io).
* [Treinar o serviço de conteúdo inteligente](#training-the-smart-content-service).

* Instalar o mais recente [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR).

## Integração com o console do Adobe Developer {#integrate-adobe-io}

Ao integrar com o Console do Adobe Developer, a variável [!DNL Experience Manager] O servidor do autentica suas credenciais de serviço no gateway do Console do Adobe Developer antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente. Para integrar o, é necessário ter uma conta do Adobe ID com privilégios de administrador para a organização e uma licença do Serviço de conteúdo inteligente adquirida e ativada para a organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. Para gerar uma chave pública, [Criar um serviço de conteúdo inteligente](#obtain-public-certificate) configuração no [!DNL Experience Manager]. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.

1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.

1. [Configurar a implantação](#configure-smart-content-service) usar a chave de API e outras credenciais do Console do Adobe Developer.

1. [Teste a configuração](#validate-the-configuration).

1. Opcionalmente, [ativar marcação automática no upload de ativos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obter certificado público criando uma configuração do Serviço de conteúdo inteligente {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do Adobe Developer.

1. No [!DNL Experience Manager] interface de usuário, acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]**.

1. Na página Cloud Service, clique em **[!UICONTROL Configurar agora]** em **[!UICONTROL Tags inteligentes de ativos]**.

1. No **[!UICONTROL Criar configuração]** especifique um título e nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. No **[!UICONTROL Serviço de conteúdo inteligente AEM]** use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por exemplo, `https://smartcontent.adobe.io/apac`. Você pode especificar `na`, `emea`ou, `apac` como as regiões onde a instância do autor do Experience Manager está hospedada.

   >[!NOTE]
   >
   >Se o Serviço gerenciado de Experience Manager for provisionado antes de 1° de setembro de 2022, use o seguinte URL de serviço:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a serem fornecidos posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer URL do serviço de conteúdo](assets/aem_scs.png)


   *Figura: Caixa de diálogo Serviço de conteúdo inteligente para fornecer URL do serviço de conteúdo*

   >[!NOTE]
   >
   >O URL fornecido como [!UICONTROL URL do serviço] não é acessível por meio do navegador e gera um erro 404. A configuração funciona bem com o mesmo valor de [!UICONTROL URL do serviço] parâmetro. Para obter o status geral do serviço e a programação de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar certificado público para a integração com o OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: configurações do serviço de marcação inteligente.*

#### Reconfigure quando um certificado expirar {#certrenew}

Depois que um certificado expira, ele deixa de ser confiável. Não é possível renovar um certificado expirado. Para adicionar um certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique em **[!UICONTROL Armazenamento de chaves]** guia.

1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Armazenamento de chaves para adicionar um certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: Excluir o existente `similaritysearch` entrada na Keystore para adicionar um certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. Para baixar um certificado público, clique em **[!UICONTROL Baixar certificado público para a integração com o OAuth]**.

1. Access [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes na **[!UICONTROL Integrações]** página. Faça upload do novo certificado. Para obter mais informações, consulte as instruções em [Criar integração do Console do Adobe Developer](#create-adobe-i-o-integration).

### Criar integração do Console do Adobe Developer {#create-adobe-i-o-integration}

Para usar as APIs do Serviço de conteúdo inteligente, crie uma integração no Console do Adobe Developer para obter [!UICONTROL Chave de API] (gerado em [!UICONTROL ID DO CLIENTE] campo de integração do Adobe Developer Console), [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], e [!UICONTROL SEGREDO DO CLIENTE] para [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração de nuvem no [!DNL Experience Manager].

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.

   [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública da conta de serviço.

1. Clique em **[!UICONTROL Avançar]**.

1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**.

   Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores no [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração de nuvem no [!DNL Experience Manager] para configurar tags inteligentes.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)


   *Figura: Detalhes da integração no Console do Adobe Developer*

### Configurar o serviço de conteúdo inteligente {#configure-smart-content-service}

>[!CAUTION]
>
>Anteriormente, as configurações feitas com Credenciais JWT agora estavam sujeitas a desativação no console do Adobe Developer. Não será possível criar novas credenciais JWT após 3 de junho de 2024. Essas configurações não podem mais ser criadas ou atualizadas, mas podem ser migradas para configurações OAuth.
> Consulte [Configuração de integrações IMS para AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>Consulte [Etapas para configurar o OAuth para usuários locais](#config-oauth-onprem)
> Consulte [Solução de problemas de tags inteligentes para credenciais do OAuth](#config-smart-tagging.md)

Para configurar a integração, use os valores de [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], [!UICONTROL SEGREDO DO CLIENTE], e [!UICONTROL ID DO CLIENTE] da integração do Console do Adobe Developer. A criação de uma configuração de nuvem de Tags inteligentes permite a autenticação de solicitações de API do [!DNL Experience Manager] implantação.

1. Entrada [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Service herdados]** para abrir o [!UICONTROL Cloud Service] console.

1. No **[!UICONTROL Tags inteligentes de ativos]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave da API], [!UICONTROL ID da conta técnica], [!UICONTROL ID da organização], e [!UICONTROL Segredo do cliente], copie e use os seguintes valores gerados em [Integração do console do Adobe Developer](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do serviço de marcação inteligente de ativos] | [!DNL Adobe Developer Console] campos de integração |
   |--- |--- |
   | [!UICONTROL Chave da API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da conta técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Segredo do cliente] | [!UICONTROL SEGREDO DO CLIENTE] |

### Configurar OAuth para usuários locais {#config-oauth-onprem}

#### Pré-requisitos {#prereqs-config-oauth-onprem}

Um escopo de autorização é uma cadeia de caracteres OAuth que contém os seguintes pré-requisitos:

* Crie uma nova integração OAuth no [Console do desenvolvedor](https://developer.adobe.com/console/user/servicesandapis) usar `ClientID`, `ClientSecretID`, e `OrgID`.
* Adicionar os seguintes arquivos neste caminho `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configurar OAuth para usuários locais {#steps-config-oauth-onprem}

1. Adicione ou atualize as propriedades abaixo em `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Atualize o `auth.token.provider.client.id` com a ID do cliente da nova configuração do OAuth.
   * Atualizar `auth.access.token.request` para `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Renomeie o arquivo para `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Execute as etapas abaixo em `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Atualize a propriedade auth.ims.client.secret com o Segredo do cliente da nova integração OAuth.
   * Renomeie o arquivo para `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Salve todas as alterações no console de desenvolvimento do repositório de conteúdo, por exemplo, CRXDE.
5. Navegue até `/system/console/configMgr` e substitua a configuração OSGi de `.<randomnumber>` para `-<randomnumber>`.
6. Excluir a configuração antiga de `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
7. Reinicie o console.

### Validar a configuração {#validate-the-configuration}

Após concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acessar o [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.

1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** para abrir o console OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL Tarefas Diversas de SimilaritySearch]**.

1. Clique em `validateConfigs()`. No **[!UICONTROL Validar configurações]** clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos no mesmo diálogo.

### Ativar marcação inteligente no [!UICONTROL Ativo de atualização DAM] fluxo de trabalho (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. Entrada [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.

1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.*

1. Abra a etapa no modo de edição. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configurar o fluxo de trabalho do ativo de atualização do DAM e adicionar a etapa de tag inteligente](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurar o fluxo de trabalho do ativo de atualização do DAM e adicionar a etapa de tag inteligente*

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho seja concluído mesmo se a etapa de marcação automática falhar.

   ![Configure o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecione o avanço do manipulador](assets/smart-tag-step-properties-workflow2.png)


   *Figura: configurar o fluxo de trabalho do ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecionar o avanço do manipulador*

   Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

   ![Configure o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecione Ignorar sinalizador de tag inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: configure o fluxo de trabalho do ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecione Ignorar sinalizador de tag inteligente.*

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

**Coerência**: as imagens usadas para uma tag específica são visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: use variedade suficiente nas imagens do treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que o Experience Manager aprenda a focar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem destacada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Distração/obstrução**: O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *sapato casual*, a segunda imagem não é um bom candidato para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como `raincoat` e `model-side-view`, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar em suas tags e aplicá-las em outras imagens depende da qualidade de imagens usadas para treinamento. Para obter melhores resultados, a Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço para cada tag.

### Formação periódica {#periodic-training}

Você pode ativar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e nas tags associadas em uma pasta. Abra o [!UICONTROL Propriedades] da sua pasta de ativos, selecione **[!UICONTROL Ativar tags inteligentes]** no **[!UICONTROL Detalhes]** e salve as alterações.

![enable_smart_tags](assets/enable_smart_tags.png)

Depois que essa opção for selecionada para uma pasta, [!DNL Experience Manager] O executa um fluxo de trabalho de treinamento automaticamente para treinar o Serviço de conteúdo inteligente nos ativos da pasta e suas tags. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 aos sábados.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. Entrada [!DNL Experience Manager] , vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. No **[!UICONTROL Modelos de fluxo de trabalho]** selecione a **[!UICONTROL Treinamento de tags inteligentes]** e clique em **[!UICONTROL Iniciar fluxo de trabalho]** na barra de ferramentas.
1. No **[!UICONTROL Executar fluxo de trabalho]** , navegue até a pasta carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e as tags são enviados para treinamento.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Quando os ativos em uma pasta forem processados para treinamento, somente os ativos modificados serão processados nos ciclos de treinamento subsequentes.

### Exibir relatórios de treinamento {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, revise o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Entrada [!DNL Experience Manager] , vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.
1. No **[!UICONTROL Relatórios de ativos]** clique em **[!UICONTROL Criar]**.
1. Selecione o **[!UICONTROL Treinamento de tags inteligentes]** e, em seguida, clique em **[!UICONTROL Próxima]** na barra de ferramentas.
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
   * A marcação é compatível com localidades que [!DNL Experience Manager] O é compatível com o.

* Para pesquisar ativos com tags inteligentes (regular ou aprimorado), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar tags inteligentes](enhanced-smart-tags.md)
>* [Solução de problemas de tags inteligentes para credenciais do OAuth](config-oauth.md)
>* [Tutorial em vídeo sobre tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
