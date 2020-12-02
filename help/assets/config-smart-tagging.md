---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada em [!DNL Adobe Experience Manager], usando o Serviço de conteúdo inteligente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 26%

---


# Preparar [!DNL Assets] para marcação inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de poder marcar seus ativos com o uso do Smart Content Services, integre [!DNL Experience ManageR Assets] ao Adobe Developer Console para aproveitar o serviço inteligente de [!DNL Adobe Sensei]. Depois de configurado, treine o serviço usando algumas imagens e uma tag.

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte:

* [Integração com o Console do desenvolvedor](#integrate-adobe-io).
* [Treinar o Serviço](#training-the-smart-content-service) de conteúdo inteligente.

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* Instale o service pack mais recente [Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## Integração com o Console do desenvolvedor {#integrate-adobe-io}

Quando você se integra ao Console do desenvolvedor do Adobe, o servidor [!DNL Experience Manager] autentica suas credenciais de serviço no gateway do Console do desenvolvedor do Adobe antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente. Para integrar você precisa de uma conta da Adobe ID que tenha privilégios de administrador para a organização e a licença do Serviço de conteúdo inteligente adquirida e ativada para sua organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. [Crie uma configuração do Smart Content ](#obtain-public-certificate) Service em  [!DNL Experience Manager] para gerar uma chave pública. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.

1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.

1. [Configure sua ](#configure-smart-content-service) implantação usando a chave da API e outras credenciais do Adobe Developer Console.

1. [Teste a configuração](#validate-the-configuration).

1. Como opção, [habilite a marcação automática no upload de ativos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Criar configuração do Smart Content Service para obter certificado público {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do desenvolvedor.

1. Na interface do usuário [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Cloud Services herdados]**.

1. Na página Cloud Services, clique em **[!UICONTROL Configurar agora]** em **[!UICONTROL Tags inteligentes de ativos]**.

1. Na caixa de diálogo **[!UICONTROL Criar configuração]**, especifique um título e um nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. Na caixa de diálogo **[!UICONTROL AEM Smart Content Service]**, use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a ser fornecido posteriormente). Clique em **[!UICONTROL OK]**.

   ![caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer o URL do serviço de conteúdo](assets/aem_scs.png)


   *Figura: Caixa de diálogo do Serviço de conteúdo inteligente para fornecer o URL do serviço de conteúdo*

   >[!NOTE]
   >
   >O URL fornecido como [!UICONTROL URL do serviço] não está acessível pelo navegador e gera um erro 404. A configuração funciona bem com o mesmo valor do parâmetro [!UICONTROL URL do serviço]. Para obter o status geral do serviço e a programação de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar Certificado Público para Integração OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configurações do serviço de marcação inteligente*

#### Reconfigurar quando um certificado expirar {#certrenew}

Depois que um certificado expira, ele não é mais confiável. Não é possível renovar um certificado expirado. Para adicionar um novo certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique na guia **[!UICONTROL Keystore]**.

1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Keystore para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: exclua a entrada `similaritysearch` existente no Armazenamento de chaves para adicionar um novo certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. Para baixar um certificado público, clique em **[!UICONTROL Baixar Certificado Público para Integração OAuth]**.

1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes na página **[!UICONTROL Integrações]**. Carregue o novo certificado. Para obter mais informações, consulte as instruções em [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### Criar integração do Console do desenvolvedor do Adobe {#create-adobe-i-o-integration}

Para usar APIs do Smart Content Service, crie uma integração no Console do Desenvolvedor do Adobe para obter [!UICONTROL chave da API] (gerada no campo [!UICONTROL ID CLIENTE] da integração do Console do Desenvolvedor do Adobe), [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID da ORGANIZAÇÃO] e &lt;a SECRET/>CLIENT T] para [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração de nuvem em [!DNL Experience Manager].[!UICONTROL 

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.

   A página [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública da conta de serviço recém-configurada.

1. Clique em **[!UICONTROL Avançar]**.

1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**.

   Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores em [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração de nuvem em [!DNL Experience Manager] para configurar tags inteligentes.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)


   *Figura: Detalhes da integração no Adobe Developer Console*

### Configurar o Serviço de Conteúdo Inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID da ORGANIZAÇÃO], [!UICONTROL CLIENT SECRET] e [!UICONTROL ID CLIENTE] da integração do Console do desenvolvedor do Adobe. A criação de uma configuração em nuvem de Tags inteligentes permite a autenticação de solicitações de API da implantação [!DNL Experience Manager].

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services herdados]** para abrir o console [!UICONTROL Cloud Services].

1. Em **[!UICONTROL Tags inteligentes de ativos]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave da Api], [!UICONTROL ID da Conta Técnica], [!UICONTROL ID da Organização] e [!UICONTROL Segredo do Cliente], copie e utilize os seguintes valores gerados em [integração do Console do Desenvolvedor do Adobe](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do serviço de marcação inteligente de ativos] | [!DNL Adobe Developer Console] campos de integração |
   |--- |--- |
   | [!UICONTROL Chave da API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da conta técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Client Secret] | [!UICONTROL SEGREDO DO CLIENTE] |

### Validar a configuração {#validate-the-configuration}

Depois de concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu servidor [!DNL Experience Manager] em `https://[aem_server]:[port]`.

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console Web]** para abrir o console OSGi. Clique em **[!UICONTROL Main] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL SimilaridadePesquisar Tarefas Diversas]**.

1. Clique em `validateConfigs()`. Na caixa de diálogo **[!UICONTROL Validar configurações]**, clique em **[!UICONTROL Chamar]**.

Os resultados da validação são exibidos na mesma caixa de diálogo.

### Habilitar marcação inteligente no fluxo de trabalho [!UICONTROL DAM Update Asset] (Opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. Em [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

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

## Treinar o Serviço de Conteúdo Inteligente {#training-the-smart-content-service}

Para que o Serviço de conteúdo inteligente reconheça a taxonomia de sua empresa, execute-a em um conjunto de ativos que já incluem tags relevantes para sua empresa. Para marcar com eficácia as imagens de sua marca, o Serviço de conteúdo inteligente exige que as imagens de treinamento estejam em conformidade com determinadas diretrizes. Após o treinamento, o serviço pode aplicar a mesma taxonomia em um conjunto de ativos semelhante.

Você pode treinar o serviço várias vezes para melhorar sua capacidade de aplicar tags relevantes. Após cada ciclo de treinamento, execute um fluxo de trabalho de marcação e verifique se seus ativos estão marcados corretamente.

Você pode treinar o Serviço de conteúdo inteligente periodicamente ou com base em requisitos.

>[!NOTE]
>
>O fluxo de trabalho de treinamento é executado somente em pastas.

### Diretrizes para treinamento {#guidelines-for-training}

Para obter melhores resultados, as imagens em seu conjunto de treinamento devem estar em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 30 imagens por tag. Mínimo de 500 pixels no lado maior.

**Coerência**: As imagens de uma tag devem ser visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Deve haver uma variedade suficiente de imagens no treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que a Experience Manager aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como `raincoat` e `model-side-view`, adicione ambas as tags no ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas para treinamento. Para obter melhores resultados, o Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço de cada tag.

### Treinamento periódico {#periodic-training}

Você pode ativar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e tags associadas em uma pasta. Abra a página [!UICONTROL Propriedades] da sua pasta de ativos, selecione **[!UICONTROL Ativar Tags Inteligentes]** na guia **[!UICONTROL Detalhes]** e salve as alterações.

![enable_smart_tags](assets/enable_smart_tags.png)

Depois que essa opção é selecionada para uma pasta, [!DNL Experience Manager] executa um fluxo de trabalho de treinamento automaticamente para treinar o Serviço de conteúdo inteligente nos ativos da pasta e suas tags. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 do sábado.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de Fluxo de Trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Treinamento de Tags Inteligentes]** e clique em **[!UICONTROL Fluxo de Trabalho do Start]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]**, navegue até a pasta de carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e as tags são enviados para treinamento.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Depois que os ativos em uma pasta são processados para treinamento, somente os ativos modificados são processados em ciclos de treinamento subsequentes.

### Relatórios de treinamento de visualização {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, reveja o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de tags inteligentes]** e clique em **[!UICONTROL Próximo]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para visualização do relatório, clique em **[!UICONTROL Visualização]** na barra de ferramentas.
1. Revise os detalhes do relatório.

   O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o Serviço de conteúdo inteligente foi treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag.

   Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.

1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha do Microsoft Excel.

## Limitações           {#limitations}

* Tags inteligentes aprimoradas são baseadas em modelos de aprendizado de imagens e suas tags. Esses modelos nem sempre são perfeitos para identificar tags. A versão atual do Serviço de conteúdo inteligente tem as seguintes limitações:

   * Incapacidade de reconhecer diferenças sutis nas imagens. Por exemplo, camisas finas versus camisetas comuns.
   * Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em camisetas.
   * A marcação é suportada nas localidades em que [!DNL Experience Manager] é suportado. Para obter uma lista de idiomas, consulte [Notas de versão do Smart Content Services](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar Tags inteligentes](enhanced-smart-tags.md)
>* [Tutorial em vídeo sobre tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

