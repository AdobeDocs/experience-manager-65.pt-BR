---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada [!DNL Adobe Experience Manager], usando o Serviço de conteúdo inteligente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 26%

---


# Preparar [!DNL Assets] para marcação inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de poder marcar seus ativos em start usando o Smart Content Services, integre-se [!DNL Experience ManageR Assets] ao Adobe Developer Console para aproveitar o serviço inteligente de [!DNL Adobe Sensei]. Depois de configurado, treine o serviço usando algumas imagens e uma tag.

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte:

* [Integração com o Console do desenvolvedor](#integrate-adobe-io).
* [Treinar o Serviço](#training-the-smart-content-service)de conteúdo inteligente.

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* Instale o service pack [mais recente do](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)Experience Manager.

## Integração com o Console do desenvolvedor {#integrate-adobe-io}

Quando você se integra ao Console do desenvolvedor do Adobe, o [!DNL Experience Manager] servidor autentica suas credenciais de serviço no gateway do Console do desenvolvedor do Adobe antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente. Para integrar você precisa de uma conta da Adobe ID que tenha privilégios de administrador para a organização e a licença do Serviço de conteúdo inteligente adquirida e ativada para sua organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. [Crie uma configuração do Smart Content Service](#obtain-public-certificate) em [!DNL Experience Manager] para gerar uma chave pública. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.

1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.

1. [Configure sua implantação](#configure-smart-content-service) usando a chave da API e outras credenciais do Adobe Developer Console.

1. [Teste a configuração](#validate-the-configuration).

1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Criar configuração do Smart Content Service para obter certificado público {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do desenvolvedor.

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Cloud Services]** herdados.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. Na caixa de diálogo **[!UICONTROL Criar configuração]** , especifique um título e um nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. Na caixa de diálogo **[!UICONTROL AEM Serviço]** de conteúdo inteligente, use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a ser fornecido posteriormente). Clique em **[!UICONTROL OK]**.

   ![caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer o URL do serviço de conteúdo](assets/aem_scs.png)


   *Figura: Caixa de diálogo do Serviço de conteúdo inteligente para fornecer o URL do serviço de conteúdo*

   >[!NOTE]
   >
   >O URL fornecido como URL  de serviço não pode ser acessado pelo navegador e gera um erro 404. A configuração funciona bem com o mesmo valor do parâmetro de URL [!UICONTROL do] serviço. Para obter o status geral do serviço e a programação de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar certificado público para integração]** OAuth e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configurações do serviço de marcação inteligente*

#### Reconfigure when a certificate expires {#certrenew}

Depois que um certificado expira, ele não é mais confiável. Não é possível renovar um certificado expirado. Para adicionar um novo certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Click **[!UICONTROL Keystore]** tab.

1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Keystore para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: exclua a entrada `similaritysearch` existente no Armazenamento de chaves para adicionar um novo certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes na página **[!UICONTROL Integrações]** . Carregue o novo certificado. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### Criar integração do Console do desenvolvedor do Adobe {#create-adobe-i-o-integration}

Para usar as APIs do Serviço de conteúdo inteligente, crie uma integração no Console do desenvolvedor do Adobe para obter a chave [!UICONTROL da] API (gerada no campo ID [!UICONTROL do] CLIENTE da integração do Console do desenvolvedor do Adobe), a ID [!UICONTROL da conta]TÉCNICA, a ID [!UICONTROL da]ORGANIZAÇÃO e o segredo [!UICONTROL do]  [!DNL Experience Manager]CLIENT para configurações de serviço de marcação inteligente doAssets.

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.

   A página [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública da conta de serviço recém-configurada.

1. Clique em **[!UICONTROL Avançar]**.

1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**.

   Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores em [!UICONTROL Assets Smart Tagging Service Settings] da configuração da nuvem [!DNL Experience Manager] para configurar tags inteligentes.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)


   *Figura: Detalhes da integração no Adobe Developer Console*

### Configurar o Serviço de conteúdo inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos ID [!UICONTROL DA CONTA]TÉCNICA, ID [!UICONTROL da]ORGANIZAÇÃO, SECRETO CLIENTE e ID [!UICONTROL do] CLIENTE da integração do Console do desenvolvedor do Adobe. A criação de uma configuração em nuvem de Tags inteligentes permite a autenticação de solicitações de API da [!DNL Experience Manager] implantação.

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > Cloud Services **** herdados para abrir o console [!UICONTROL Cloud Services] .

1. Em Tags **[!UICONTROL inteligentes de]** ativos, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos Chave [!UICONTROL da]Api, ID [!UICONTROL da conta]técnica, ID [!UICONTROL da]organização e Segredo [!UICONTROL do]cliente, copie e use os seguintes valores gerados na integração [do Console do desenvolvedor do](#create-adobe-i-o-integration)Adobe.

   | [!UICONTROL Configurações do serviço de marcação inteligente de ativos] | [!DNL Adobe Developer Console] campos de integração |
   |--- |--- |
   | [!UICONTROL Chave da API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da conta técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Client Secret] | [!UICONTROL SEGREDO DO CLIENTE] |

### Validar a configuração {#validate-the-configuration}

Depois de concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.

1. Vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web para abrir o console do OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL SemelhançaPesquise Tarefas]** diversas.

1. Clique em `validateConfigs()`. Na caixa de diálogo **[!UICONTROL Validar configurações]** , clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos na mesma caixa de diálogo.

### Habilitar marcação inteligente no fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM (Opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.

1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM*

1. Abra a etapa no modo de edição. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar a etapa da tag inteligente](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar a etapa da tag inteligente*

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho seja concluído mesmo se a etapa de marcação automática falhar.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa da tag inteligente e selecionar avanço do manipulador](assets/smart-tag-step-properties-workflow2.png)


   *Figura: Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa da tag inteligente e selecionar avanço do manipulador*

   Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa da tag inteligente e selecionar ignorar sinalizador da tag inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configurar o fluxo de trabalho do Ativo de atualização do DAM para adicionar a etapa da tag inteligente e selecionar ignorar sinalizador da tag inteligente*

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e salve o fluxo de trabalho.

## Treinar o Serviço de conteúdo inteligente {#training-the-smart-content-service}

Para que o Serviço de conteúdo inteligente reconheça a taxonomia de sua empresa, execute-a em um conjunto de ativos que já incluem tags relevantes para sua empresa. Para marcar com eficácia as imagens de sua marca, o Serviço de conteúdo inteligente exige que as imagens de treinamento estejam em conformidade com determinadas diretrizes. Após o treinamento, o serviço pode aplicar a mesma taxonomia em um conjunto de ativos semelhante.

Você pode treinar o serviço várias vezes para melhorar sua capacidade de aplicar tags relevantes. Após cada ciclo de treinamento, execute um fluxo de trabalho de marcação e verifique se seus ativos estão marcados corretamente.

Você pode treinar o Serviço de conteúdo inteligente periodicamente ou com base em requisitos.

>[!NOTE]
>
>O fluxo de trabalho de treinamento é executado somente em pastas.

### Orientações para a formação {#guidelines-for-training}

Para obter melhores resultados, as imagens em seu conjunto de treinamento devem estar em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 30 imagens por tag. Mínimo de 500 pixels no lado maior.

**Coerência**: As imagens de uma tag devem ser visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Deve haver uma variedade suficiente de imagens no treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que a Experience Manager aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para o *modelo de tag-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. For example, for tags, such as `raincoat` and `model-side-view`, add both the tags on the eligible asset before including it for training.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas para treinamento. Para obter melhores resultados, o Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço de cada tag.

### Formação contínua {#periodic-training}

Você pode ativar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e tags associadas em uma pasta. Abra a página [!UICONTROL Propriedades] da sua pasta de ativos, selecione **[!UICONTROL Ativar tags]** inteligentes na guia **[!UICONTROL Detalhes]** e salve as alterações.

![enable_smart_tags](assets/enable_smart_tags.png)

Quando essa opção for selecionada para uma pasta, [!DNL Experience Manager] executará um fluxo de trabalho de treinamento automaticamente para treinar o Serviço de conteúdo inteligente nos ativos da pasta e em suas tags. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 do sábado.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]** , navegue até a pasta de carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e as tags são enviados para treinamento.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Depois que os ativos em uma pasta são processados para treinamento, somente os ativos modificados são processados em ciclos de treinamento subsequentes.

### Relatórios de treinamento de visualização {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, reveja o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Then, click **[!UICONTROL Create]** from the toolbar.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Revise os detalhes do relatório.

   O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o Serviço de conteúdo inteligente foi treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag.

   Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.

1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha do Microsoft Excel.

## Limitações           {#limitations}

* Tags inteligentes aprimoradas são baseadas em modelos de aprendizado de imagens e suas tags. Esses modelos nem sempre são perfeitos para identificar tags. A versão atual do Serviço de conteúdo inteligente tem as seguintes limitações:

   * Incapacidade de reconhecer diferenças sutis nas imagens. Por exemplo, camisas finas versus camisetas comuns.
   * Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em camisetas.
   * A marcação é suportada nas localidades nas quais [!DNL Experience Manager] há suporte. Para obter uma lista de idiomas, consulte Notas [de versão do](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html)Smart Content Services.

* Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar Tags inteligentes](enhanced-smart-tags.md)
>* [Tutorial em vídeo sobre tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

