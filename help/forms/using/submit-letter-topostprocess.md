---
title: Pós-processamento de cartas e comunicações interativas
seo-title: Pós-processamento de cartas
description: O pós-processamento de cartas no Gerenciamento de correspondência permite criar processos de postagem do AEM e Forms, como impressão e email, e integrá-los às suas cartas.
seo-description: O pós-processamento de cartas no Gerenciamento de correspondência permite criar processos de postagem do AEM e Forms, como impressão e email, e integrá-los às suas cartas.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Pós-processamento de cartas e comunicações interativas{#post-processing-of-letters-and-interactive-communications}

## Pós-processamento {#post-processing}

Os agentes podem associar e executar fluxos de trabalho de pós-processamento em cartas e comunicações interativas. O processo de postagem a ser executado pode ser selecionado na exibição Propriedades do modelo Carta . Você pode configurar processos de publicação para enviar emails, imprimir, fax ou arquivar suas cartas finais.

![Pós-processamento](assets/ppoverview.png)

Para associar processos de publicação a letras ou comunicações interativas, primeiro é necessário configurar os processos de publicação. Dois tipos de workflows podem ser executados em cartas enviadas:

1. **Forms Workflow:** Estes são os workflows de gerenciamento de processos do AEM Forms em JEE. Instruções para configuração de [Forms Workflow](#formsworkflow).

1. **Fluxo de trabalho AEM:** AEM fluxos de trabalho também podem ser usados como processos de publicação para cartas enviadas. Instruções para configurar [AEM Fluxo de trabalho](../../forms/using/aem-forms-workflow.md).

## Fluxo de trabalho dos formulários {#formsworkflow}

1. Em AEM, abra a Configuração do Adobe Experience Manager Web Console para seu servidor usando o seguinte URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Gerenciador de configurações](assets/2configmanager-1.png)

1. Nesta página, localize a Configuração do SDK do cliente do AEM Forms e expanda-a clicando nela.
1. No URL do servidor, insira o nome do AEM Forms no servidor JEE, os detalhes de logon e clique em **Salvar**.

   ![Insira o nome do servidor do LiveCycle](assets/1cofigmanager.png)

1. Especifique o nome de usuário e a senha.
1. Certifique-se de que sun.util.calendar é adicionado à Configuração do firewall de desserialização.

   Vá para Configuração do firewall de desserialização e, em Incluir na lista de permissões classes de prefixos do pacote, adicione sun.util.calendar.

1. Agora seus servidores são mapeados e os processos de publicação no AEM Forms no JEE estão disponíveis na interface do usuário AEM ao criar cartas.

   ![Criar tela de carta com processos de publicação listados](assets/0configmanager.png)

1. Para autenticar um processo/serviço, copie o nome de um processo e volte para a página Configurações do console da Web do Adobe Experience Manager > Configuração do SDK do cliente do AEM Forms e adicione o processo como um novo serviço.

   Por exemplo, se a lista suspensa na página Propriedades da letra exibir o nome do processo como Forms Workflow -> ValidCCPostProcess/SaveXML, adicione um Nome de Serviço como `ValidCCPostProcess/SaveXML`.

1. Para usar o AEM Forms em workflows JEE para pós-processamento, configure os parâmetros e as saídas necessários. Os valores padrão dos parâmetros são indicados abaixo.

   Vá para a página Configurações do console da Web do Adobe Experience Manager > **[!UICONTROL Configurações do gerenciamento de correspondência]** e configure os seguintes parâmetros:

   1. **inPDFDoc (parâmetro de documento PDF):** um documento PDF como entrada. Esta entrada contém a letra renderizada como entrada. Os nomes de parâmetro indicados são configuráveis. Eles podem ser configurados nas configurações do Gerenciamento de correspondência na configuração.
   1. **inXMLDoc (parâmetro de dados XML):** um documento XML como entrada. Essa entrada contém dados inseridos pelo usuário no formato XML.
   1. **inXDPDoc (parâmetro de documento XDP):** um documento XML como entrada. Esta entrada contém layout subjacente (XDP).
   1. **inAttachmentDocs (parâmetro Attachment Documents):** um parâmetro de entrada de lista. Esta entrada contém todos os anexos como entrada.
   1. **redirectURL (Redirect URL Output):** um tipo de saída que indica o url para o qual redirecionar.

   Seu fluxo de trabalho de formulários deve ter um parâmetro de documento PDF ou um parâmetro de dados XML como entrada com o mesmo nome especificado em **[!UICONTROL Configurações de gerenciamento de correspondência]**. Isso é necessário para que o processo seja listado na lista suspensa Processo de postagem .

## Configurações na instância de publicação {#settings-on-the-publish-instance}

1. faça logon em `https://localhost:publishport/aem/forms`.
1. Navegue até **[!UICONTROL Cartas]** para exibir a carta publicada que está disponível na instância de publicação.
1. Defina as Configurações do AEM DS. Consulte [Definir AEM configurações do DS](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>Ao usar workflows do Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário configurar o serviço de configurações do DS. Caso contrário, a apresentação do formulário não será válida.

## Recuperação de instâncias de cartas {#letter-instances-retrieval}

As instâncias de carta salvas podem ser mais manipuladas, como recuperação de instâncias de carta e exclusão de instâncias de carta, usando as seguintes APIs definidas em LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API do lado do servidor</strong></td>
   <td><strong>Nome da operação</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><p>CartaInstânciaPúblicaVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Emite ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Buscar a instância de letra especificada </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) lança ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Excluída a instância de carta especificada </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) lança ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Essa API busca instâncias de letras com base no parâmetro de consulta de entrada. Para buscar todas as instâncias de letra, o parâmetro de consulta pode ser passado como nulo.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) lança ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Verifique se existe uma LetterInstance pelo nome fornecido </td>
  </tr>
 </tbody>
</table>

## Associar um processo de publicação a uma letra {#associating-a-post-process-with-a-letter}

Na interface do usuário do CCR, conclua as seguintes etapas para associar um processo de publicação a uma letra:

1. Passe o mouse sobre uma letra e toque em **Exibir propriedades**.
1. Selecione **Editar**.
1. Nas Propriedades básicas, usando o menu suspenso Processo de postagem , selecione o processo de postagem a ser associado à carta. Os processos de publicação relacionados ao AEM e ao Forms estão listados na lista suspensa.
1. Toque em **Salvar**.
1. Depois de configurar a carta com o Processo de postagem, publique a carta e, opcionalmente, na instância de publicação, especifique o URL de processamento no serviço de Configurações AEM DS. Isso garante que o processo de publicação seja executado na instância de processamento.

## Recarregar uma instância de carta de rascunho  {#reloaddraft}

Uma instância de carta de rascunho pode ser recarregada na interface do usuário usando o seguinte url:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID: A ID exclusiva da instância da carta enviada.

Para obter mais informações sobre como salvar uma carta de rascunho, consulte [Salvar rascunhos e enviar instâncias de carta](../../forms/using/create-correspondence.md#savingdrafts).
