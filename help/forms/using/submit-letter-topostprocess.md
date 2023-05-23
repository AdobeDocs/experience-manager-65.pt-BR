---
title: Pós-processamento de cartas e comunicações interativas
seo-title: Post Processing of Letters
description: O pós-processamento de cartas no Gerenciamento de correspondência permite criar processos de postagem de AEM e Forms, como impressão e email, e integrá-los às suas cartas.
seo-description: Post Processing of Letters in Correspondence Management lets you create AEM and Forms post processes, such as print and email, and integrate them with your letters.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Pós-processamento de cartas e comunicações interativas{#post-processing-of-letters-and-interactive-communications}

## Pós-processamento {#post-processing}

Os agentes podem associar e executar fluxos de trabalho de pós-processamento em cartas e comunicações interativas. O pós-processo a ser executado pode ser selecionado na exibição Propriedades do modelo Carta. Você pode configurar processos de correio para enviar e-mails, imprimir, enviar fax ou arquivar suas cartas finais.

![Pós-processamento](assets/ppoverview.png)

Para associar processos de publicação a cartas ou comunicações interativas, primeiro é necessário configurar os processos de publicação. Dois tipos de fluxos de trabalho podem ser executados em cartas enviadas:

1. **Forms Workflow:** Estes são os workflows de gerenciamento de processo do AEM Forms no JEE. Instruções para configuração [Forms Workflow](#formsworkflow).

1. **Fluxo de trabalho do AEM:** Os fluxos de trabalho do AEM também podem ser usados como processos de postagem para cartas enviadas. Instruções para configuração [Fluxo de trabalho do AEM](../../forms/using/aem-forms-workflow.md).

## Fluxo de trabalho dos formulários {#formsworkflow}

1. No AEM, abra Configuração do console da Web do Adobe Experience Manager para o servidor usando o seguinte URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Gerenciador de configurações](assets/2configmanager-1.png)

1. Nesta página, localize a Configuração do SDK do cliente da AEM Forms e expanda-a clicando nela.
1. No URL do servidor, digite o nome do AEM Forms no servidor JEE, os detalhes de logon e clique em **Salvar**.

   ![Insira o nome do servidor do LiveCycle](assets/1cofigmanager.png)

1. Especifique o nome de usuário e a senha.
1. Verifique se sun.util.calendar foi adicionado à Configuração do firewall de desserialização.

   Incluir na lista de permissões Acesse Configuração do firewall de desserialização e, em classes ➡ de prefixos de pacote, adicione sun.util.calendar.

1. Agora seus servidores estão mapeados e os processos de publicação no AEM Forms no JEE estão disponíveis na interface do usuário AEM ao criar cartas.

   ![Criar tela de carta com os processos de publicação listados](assets/0configmanager.png)

1. Para autenticar um processo/serviço, copie o nome de um processo, volte para a página Configurações do console da Web do Adobe Experience Manager > Configuração do SDK do cliente AEM Forms e adicione o processo como um novo serviço.

   Por exemplo, se a lista suspensa na página Propriedades da carta exibir o nome do processo como Forms Workflow -> ValidCCPostProcess/SaveXML, adicione um Nome do serviço como `ValidCCPostProcess/SaveXML`.

1. Para usar workflows do AEM Forms no JEE para pós-processamento, configure os parâmetros e as saídas necessários. Os valores padrão dos parâmetros são indicados abaixo.

   Vá para a página Configurações do console da Web do Adobe Experience Manager > **[!UICONTROL Configurações do gerenciamento de correspondência]** e configure os seguintes parâmetros:

   1. **inPDFDoc (parâmetro de documento PDF):** Um documento PDF como entrada. Esta entrada contém a letra renderizada como entrada. Os nomes de parâmetro indicados são configuráveis. Elas podem ser definidas nas configurações do Gerenciamento de correspondência a partir da configuração.
   1. **inXMLDoc (parâmetro de dados XML):** Um documento XML como entrada. Essa entrada contém dados inseridos pelo usuário na forma de XML.
   1. **inXDPDoc (parâmetro de documento XDP):** Um documento XML como entrada. Esta entrada contém o layout subjacente (XDP).
   1. **inAttachmentDocs (parâmetro Attachment Documents):** Um parâmetro de entrada de lista. Esta entrada contém todos os anexos como entrada.
   1. **redirectURL (Saída de URL de redirecionamento):** Um tipo de saída indicando o URL para o qual redirecionar.

   Seu fluxo de trabalho de formulários deve ter um parâmetro de documento PDF ou parâmetro de dados XML como entrada com o mesmo nome especificado em **[!UICONTROL Configurações do gerenciamento de correspondência]**. Isso é necessário para que o processo seja listado na lista suspensa Pós-processamento.

## Configurações na instância de publicação {#settings-on-the-publish-instance}

1. fazer logon em `https://localhost:publishport/aem/forms`.
1. Navegue até **[!UICONTROL Cartas]** para exibir a carta publicada que está disponível na instância de publicação.
1. Defina as configurações de AEM DS. Consulte [Definição das configurações de AEM DS](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>Ao usar workflows Forms ou AEM, antes de fazer qualquer envio do servidor de publicação, é necessário definir o serviço de configurações do DS. Caso contrário, o envio do Formulário não terá êxito.

## Recuperação de instâncias de carta {#letter-instances-retrieval}

As instâncias de cartas salvas podem ser manipuladas ainda mais, como a recuperação de instâncias de cartas e a exclusão de instâncias de cartas, usando as seguintes APIs definidas em LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API do lado do servidor</strong></td>
   <td><strong>Nome da operação</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><p>LetterInstanceVO Pública</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Gera uma exceção ICCE; </p> </td>
   <td>getLetterInstance</td>
   <td>Buscar a ocorrência de carta especificada </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) gera ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Excluída a ocorrência de carta especificada </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) gera ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Essa API busca instâncias de cartas com base no parâmetro de consulta de entrada. Para buscar todas as instâncias de correspondência, o parâmetro de consulta pode ser passado como nulo.<br /> </td>
  </tr>
  <tr>
   <td>letterInstanceExists(String letterInstanceName) booleana pública lança ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Verificar se existe uma LetterInstance com o nome especificado </td>
  </tr>
 </tbody>
</table>

## Associando um processo de publicação a uma carta {#associating-a-post-process-with-a-letter}

Na interface do usuário do CCR, conclua as seguintes etapas para associar um pós-processo a uma correspondência:

1. Passe o mouse sobre uma letra e toque **Propriedades da exibição**.
1. Selecione **Editar**.
1. Nas Propriedades básicas, usando o menu suspenso Pós-processo, selecione o pós-processo a ser associado à correspondência. Tanto o AEM quanto os processos de post relacionados ao Forms estão listados no menu suspenso.
1. Toque **Salvar**.
1. Depois de configurar a correspondência com o pós-processamento, publique a correspondência e, opcionalmente, na instância de publicação, especifique o URL de processamento no serviço de Configurações do AEM DS. Isso garante que o pós-processo seja executado na instância de processamento.

## Recarregar uma instância de carta de rascunho  {#reloaddraft}

Uma instância de carta de rascunho pode ser recarregada na interface usando o seguinte url:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID: a ID exclusiva da instância de carta enviada.

Para obter mais informações sobre como salvar um rascunho de carta, consulte [Salvar rascunhos e enviar instâncias de carta](../../forms/using/create-correspondence.md#savingdrafts).
