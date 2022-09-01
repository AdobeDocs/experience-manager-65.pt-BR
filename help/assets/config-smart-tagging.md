---
title: Configurar a marcação de ativos usando o Serviço de conteúdo inteligente
description: Saiba como configurar a marcação inteligente e a marcação inteligente aprimorada no [!DNL Adobe Experience Manager], utilizando o Serviço de conteúdo inteligente.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 83e9ab570fac686fd53c9c2594cbfb2c05a89a0c
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 24%

---

# Preparar [!DNL Assets] para marcação inteligente {#configure-asset-tagging-using-the-smart-content-service}

Antes de começar a marcar seus ativos usando os Serviços de conteúdo inteligente, integre [!DNL Experience Manager Assets] com o Adobe Developer Console para aproveitar o serviço inteligente de [!DNL Adobe Sensei]. Depois de configurado, treine o serviço usando algumas imagens e uma tag .

>[!NOTE]
>
>* Os Serviços de conteúdo inteligente não estão mais disponíveis para novos [!DNL Experience Manager Assets] Clientes locais. Os clientes existentes no local, que já têm esse recurso ativado, podem continuar usando os Serviços de conteúdo inteligente.
>* Os Serviços de conteúdo inteligente estão disponíveis para [!DNL Experience Manager Assets] Clientes Managed Services que já tenham esse recurso ativado.
>* Novo [!DNL Experience Manager Assets] Os clientes do Managed Services podem seguir as instruções mencionadas neste artigo para configurar os Serviços de conteúdo inteligente.


Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte:

* [Integração com o Console do desenvolvedor](#integrate-adobe-io).
* [Treinar o Serviço de conteúdo inteligente](#training-the-smart-content-service).

* Instale o mais recente [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR).

## Integração com o Console do desenvolvedor {#integrate-adobe-io}

Ao fazer a integração com o Console do Adobe Developer, a variável [!DNL Experience Manager] O servidor autentica suas credenciais de serviço no gateway do Console do Adobe Developer antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente. Para fazer a integração, você precisa de uma conta da Adobe ID que tenha privilégios de administrador para a organização e a licença do Serviço de conteúdo inteligente adquirida e ativada para a organização.

Para configurar o Serviço de conteúdo inteligente, siga estas etapas de nível superior:

1. Para gerar uma chave pública, [Criar um serviço de conteúdo inteligente](#obtain-public-certificate) configuração em [!DNL Experience Manager]. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.

1. [Crie uma integração no Console do desenvolvedor](#create-adobe-i-o-integration) e faça upload da chave pública gerada.

1. [Configurar a implantação](#configure-smart-content-service) usando a chave da API e outras credenciais do Adobe Developer Console.

1. [Teste a configuração](#validate-the-configuration).

1. Opcionalmente, [ativar a marcação automática no upload de ativos](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obter certificado público criando a configuração do Serviço de conteúdo inteligente {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do desenvolvedor.

1. No [!DNL Experience Manager] interface do usuário, acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Cloud Services herdados]**.

1. Na página Cloud Services, clique em **[!UICONTROL Configurar agora]** under **[!UICONTROL Tags inteligentes de ativos]**.

1. No **[!UICONTROL Criar configuração]** , especifique um título e nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. No **[!UICONTROL Serviço de conteúdo inteligente AEM]** use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Por exemplo, `https://smartcontent.adobe.io/apac`. Você pode especificar `na`, `emea`ou, `apac` como as regiões onde a instância do autor de Experience Manager está hospedada.

   >[!NOTE]
   >
   >Se o Experience Manager Managed Service for provisionado antes de 1° de setembro de 2022, use o seguinte URL de serviço:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a ser fornecido posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo Serviço de conteúdo inteligente do Experience Manager para fornecer URL de serviço de conteúdo](assets/aem_scs.png)


   *Figura: Caixa de diálogo Serviço de conteúdo inteligente para fornecer URL de serviço de conteúdo*

   >[!NOTE]
   >
   >O URL fornecido como [!UICONTROL URL de serviço] não é acessível por meio do navegador e gera um erro 404. A configuração funciona bem com o mesmo valor da variável [!UICONTROL URL de serviço] parâmetro. Para obter o status geral do serviço e o cronograma de manutenção, consulte [https://status.adobe.com](https://status.adobe.com).

1. Clique em **[!UICONTROL Baixar certificado público para a integração OAuth]** e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/smart-tags-download-public-cert.png)


   *Figura: Configurações do serviço de marcação inteligente.*

#### Reconfigure quando um certificado expirar {#certrenew}

Depois que um certificado expira, ele não é mais confiável. Não é possível renovar um certificado expirado. Para adicionar um certificado, siga estas etapas.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique em **[!UICONTROL Armazenamento de chaves]** guia .

1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Armazenamento de chaves para adicionar um certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: Exclua as `similaritysearch` no Armazenamento de chaves para adicionar um certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. Para baixar um certificado público, clique em **[!UICONTROL Baixar certificado público para a integração OAuth]**.

1. Acesso [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes no **[!UICONTROL Integrações]** página. Faça upload do novo certificado. Para obter mais informações, consulte as instruções em [Criar integração com o Adobe Developer Console](#create-adobe-i-o-integration).

### Criar integração com o Adobe Developer Console {#create-adobe-i-o-integration}

Para usar APIs do Serviço de conteúdo inteligente, crie uma integração no Console do Adobe Developer para obter [!UICONTROL Chave da API] (gerado em [!UICONTROL ID DO CLIENTE] campo da integração do Adobe Developer Console), [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO]e [!UICONTROL SEGREDO DO CLIENTE] para [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração da nuvem em [!DNL Experience Manager].

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.

1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.

1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e escolha **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.

1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.

   [!UICONTROL Criar uma nova credencial de conta de serviço (JWT)] exibe a chave pública para a conta de serviço.

1. Clique em **[!UICONTROL Avançar]**.

1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**.

   Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores em [!UICONTROL Configurações do serviço de marcação inteligente de ativos] da configuração da nuvem em [!DNL Experience Manager] para configurar tags inteligentes.

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)


   *Figura: Detalhes da integração no Console do Adobe Developer*

### Configurar o Serviço de Conteúdo Inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores de [!UICONTROL ID DA CONTA TÉCNICA], [!UICONTROL ID DA ORGANIZAÇÃO], [!UICONTROL SEGREDO DO CLIENTE]e [!UICONTROL ID DO CLIENTE] da integração com o Adobe Developer Console. A criação de uma configuração de nuvem de Tags inteligentes permite a autenticação de solicitações de API do [!DNL Experience Manager] implantação.

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services herdados]** para abrir o [!UICONTROL Cloud Services] console.

1. Em **[!UICONTROL Tags inteligentes de ativos]**, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.

1. Para os campos [!UICONTROL Chave Da Api], [!UICONTROL ID da conta técnica], [!UICONTROL ID da organização]e [!UICONTROL Segredo do cliente], copie e use os seguintes valores gerados em [Integração com o Adobe Developer Console](#create-adobe-i-o-integration).

   | [!UICONTROL Configurações do serviço de marcação inteligente de ativos] | [!DNL Adobe Developer Console] campos de integração |
   |--- |--- |
   | [!UICONTROL Chave da API] | [!UICONTROL ID DO CLIENTE] |
   | [!UICONTROL ID da conta técnica] | [!UICONTROL ID DA CONTA TÉCNICA] |
   | [!UICONTROL ID da organização] | [!UICONTROL ID DA ORGANIZAÇÃO] |
   | [!UICONTROL Client Secret] | [!UICONTROL SEGREDO DO CLIENTE] |

### Validar a configuração {#validate-the-configuration}

Após concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.

1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** para abrir o console OSGi. Clique em **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Clique em `com.day.cq.dam.similaritysearch.internal.impl`. Ele abre **[!UICONTROL SemelhançaPesquisar diversas tarefas]**.

1. Clique em `validateConfigs()`. No **[!UICONTROL Validar configurações]** , clique em **[!UICONTROL Invocar]**.

Os resultados da validação são exibidos na mesma caixa de diálogo.

### Ativar a marcação inteligente na [!UICONTROL Ativo de atualização DAM] workflow (opcional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. Em [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.

1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.

1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM*

1. Abra a etapa no modo de edição. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar etapa de tag inteligente](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurar o fluxo de trabalho do Ativo de atualização do DAM e adicionar etapa de tag inteligente*

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho seja concluído mesmo se a etapa de marcação automática falhar.

   ![Configure o fluxo de trabalho Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecionar avanço do manipulador](assets/smart-tag-step-properties-workflow2.png)


   *Figura: Configure o fluxo de trabalho Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecionar avanço do manipulador*

   Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

   ![Configure o fluxo de trabalho Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecione ignorar sinalizador de tag inteligente](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configure o fluxo de trabalho Ativo de atualização do DAM para adicionar a etapa de tag inteligente e selecione ignorar sinalizador de tag inteligente.*

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e salve o fluxo de trabalho.

## Treinar o Serviço de conteúdo inteligente {#training-the-smart-content-service}

Para que o Serviço de conteúdo inteligente reconheça sua taxonomia comercial, execute-a em um conjunto de ativos que já incluem tags relevantes para sua empresa. Para marcar as imagens de sua marca com eficácia, o Serviço de conteúdo inteligente exige que as imagens de treinamento estejam em conformidade com determinadas diretrizes. Após o treinamento, o serviço pode aplicar a mesma taxonomia em um conjunto semelhante de ativos.

Você pode treinar o serviço várias vezes para melhorar sua capacidade de aplicar tags relevantes. Após cada ciclo de treinamento, execute um fluxo de trabalho de marcação e verifique se os ativos estão marcados adequadamente.

Você pode treinar o Serviço de conteúdo inteligente periodicamente ou de acordo com requisitos.

>[!NOTE]
>
>O fluxo de trabalho de treinamento é executado somente em pastas.

### Orientações para a formação {#guidelines-for-training}

Para obter melhores resultados, as imagens em seu conjunto de treinamento estão em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 30 imagens por tag. Mínimo de 500 pixels no lado maior.

**Coerência**: As imagens usadas para uma tag específica são visualmente semelhantes.

Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/coherence.png)

**Cobertura**: Use a variedade suficiente nas imagens do treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que a Experience Manager aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo.

Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço se concentra melhor em imagens com menos distração (planos de fundo proeminentes, acompanhamento não relacionado, como objetos/pessoas com o assunto principal).

Por exemplo, para a tag *sapato casual*, a segunda imagem não é um bom candidato à formação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como `raincoat` e `model-side-view`, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>A capacidade do Serviço de conteúdo inteligente de treinar em suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas no treinamento. Para obter melhores resultados, o Adobe recomenda o uso de imagens visualmente semelhantes para treinar o serviço para cada tag.

### Formação contínua {#periodic-training}

Você pode habilitar o Serviço de conteúdo inteligente para treinar periodicamente nos ativos e tags associadas em uma pasta. Abra o [!UICONTROL Propriedades] da pasta de ativos, selecione **[!UICONTROL Ativar Tags inteligentes]** nos termos do **[!UICONTROL Detalhes]** e salve as alterações.

![enable_smart_tags](assets/enable_smart_tags.png)

Depois que essa opção é selecionada para uma pasta, [!DNL Experience Manager] O executa um fluxo de trabalho de treinamento automaticamente para treinar o Serviço de conteúdo inteligente nos ativos da pasta e suas tags. Por padrão, o fluxo de trabalho de treinamento é executado semanalmente às 12h30 dos sábados.

### Treinamento sob demanda {#on-demand-training}

Você pode treinar o Serviço de conteúdo inteligente sempre que necessário no console Fluxo de trabalho.

1. Em [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. No **[!UICONTROL Modelos de fluxo de trabalho]** selecione o **[!UICONTROL Treinamento em Tags inteligentes]** e clique em **[!UICONTROL Iniciar fluxo de trabalho]** na barra de ferramentas.
1. No **[!UICONTROL Executar fluxo de trabalho]** navegue até a pasta de carga que inclui os ativos marcados para treinar o serviço.
1. Especifique um título para o fluxo de trabalho e adicione um comentário. Em seguida, clique em **[!UICONTROL Executar]**. Os ativos e tags são enviados para treinamento.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Depois que os ativos em uma pasta forem processados para treinamento, somente os ativos modificados serão processados em ciclos de treinamento subsequentes.

### Exibir relatórios de treinamento {#viewing-training-reports}

Para verificar se o Serviço de conteúdo inteligente é treinado em suas tags no conjunto de ativos de treinamento, analise o relatório do fluxo de trabalho de treinamento no console Relatórios .

1. Em [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. No **[!UICONTROL Relatórios de ativos]** página, clique em **[!UICONTROL Criar]**.
1. Selecione o **[!UICONTROL Treinamento em Tags inteligentes]** e clique em **[!UICONTROL Próximo]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório.

   O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o Serviço de conteúdo inteligente foi treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag.

   Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.

1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Baixar]** na barra de ferramentas. O relatório é baixado como uma planilha do Excel do Microsoft.

## Limitações           {#limitations}

* As tags inteligentes aprimoradas são baseadas em modelos de aprendizagem de imagens e suas tags. Esses modelos nem sempre são perfeitos na identificação de tags. A versão atual do Serviço de conteúdo inteligente tem as seguintes limitações:

   * Incapacidade de reconhecer sutis diferenças em imagens. Por exemplo, camisas finas versus camisas fixas regulares.
   * Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em T-shirts.
   * A marcação é compatível com as localidades que [!DNL Experience Manager] O é compatível com o . Para obter uma lista de idiomas, consulte [Notas de versão dos Serviços de conteúdo inteligente](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use o [!DNL Assets] Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!MORELIKETHIS]
>
>* [Visão geral e como treinar tags inteligentes](enhanced-smart-tags.md)
>* [Tutorial em vídeo sobre tags inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

