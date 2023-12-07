---
title: Controle do acesso a documentos protegidos por política
description: Veja como visualizar, gerenciar e controlar o acesso aos documentos protegidos por política.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# Controle do acesso a documentos protegidos por política {#controlling-access-to-policy-protected-documents}

Você pode controlar a maneira como os recipients usam seus documentos protegidos por política independentemente da abrangência da distribuição.

Usando a página Documentos, você pode executar estas tarefas:

* Pesquise e exiba os detalhes de documentos protegidos por política. Você pode ver informações sobre o nome do documento, nome do editor, nome da política e data em que a política foi aplicada. Se a política que protegeu um documento for excluída, você também poderá ver a ID da política excluída sob o nome da política. Os usuários podem visualizar e gerenciar seus próprios documentos protegidos por política. Os administradores podem visualizar e gerenciar todos os documentos protegidos por política.
* Alterar os detalhes da política aplicada a um documento. Os usuários podem editar suas próprias políticas, os administradores podem editar políticas compartilhadas e pessoais e os coordenadores de definições de políticas podem editar políticas compartilhadas nos conjuntos de políticas para os quais têm permissões. Você pode acessar a política associada a um documento diretamente na página Detalhes do documento.
* Revogar e restabelecer o acesso a um documento protegido por política. Os administradores podem revogar e restabelecer o acesso a qualquer documento. Os coordenadores de definições de políticas (que têm permissão para gerenciar documentos) podem revogar e restabelecer o acesso a documentos protegidos por políticas que usam políticas compartilhadas de seus conjuntos de políticas. Os usuários podem revogar o acesso a seus documentos protegidos por política se tiverem criado a política que está protegendo o documento ou se a política for compartilhada que permita esse recurso.
* Alternar a política aplicada a um documento. Os usuários que aplicam políticas a documentos podem alternar uma política se a criaram ou se for uma política compartilhada que ative esse recurso. Os coordenadores de definições de políticas podem trocar as políticas de seus conjuntos de políticas. Os administradores podem alternar as políticas aplicadas a qualquer documento.

Quando um documento é protegido por uma política e você revoga os privilégios de acesso ou altera a política aplicada, as alterações são efetivadas da seguinte maneira:

* Se o documento estiver on-line, as alterações serão aplicadas imediatamente, a menos que o usuário tenha o documento aberto. Nesse caso, o usuário deve fechar o documento para que as alterações entrem em vigor.
* Se um destinatário estiver usando o documento offline (por exemplo, em um laptop), as alterações entrarão em vigor na próxima vez que o destinatário sincronizar com a segurança do documento, abrindo qualquer documento protegido por política.

## Exibir informações sobre um documento {#view-information-about-a-document}

Para cada documento listado na página Documentos, você pode ver o nome do documento, o nome do editor, o nome da política e a data em que o documento foi protegido. Se a política que protegeu um documento tiver sido excluída, a ID da política será listada em Nome da política.

Você também pode exibir mais detalhes, descritos abaixo, sobre um documento específico na página Detalhes do documento:

>[!NOTE]
>
>Use o link Nome da política na página Detalhes do documento para acessar políticas geradas automaticamente no Microsoft Outlook para destinatários de um documento anexado a uma mensagem de email. Essas políticas não aparecem na página de políticas.

**Nome do documento:** O nome do documento selecionado.

**ID do documento:** Um identificador exclusivo que a segurança de documentos atribui quando uma política é aplicada ao documento. a segurança de documentos usa esse número para rastrear o documento.

**Status do documento:** Status do documento (por exemplo, ativo ou revogado).

**Editor:** Nome do usuário que anexou a política ao documento.

**Nome da política:** O nome da política usada para proteger o documento. Você pode clicar no nome para abrir a política. Use este link para acessar as políticas geradas pelo Acrobat para destinatários de um documento anexado a uma mensagem de email no Outlook. Essas políticas não aparecem na página Políticas.

**Tipo de política:** O tipo de política aplicado ao documento.

**Data de publicação:** A data em que a política foi aplicada ao documento.

**Iterações relacionadas:** Se o documento tiver iterações relacionadas, esse item também aparecerá na lista. Clique no link para exibir a lista de iterações relacionadas ao documento.

Os usuários podem exibir informações sobre seus documentos protegidos. Os administradores podem exibir informações sobre documentos que qualquer usuário protegeu com uma política. Os coordenadores de definições de políticas podem exibir informações sobre documentos protegidos por políticas de seus conjuntos de políticas.

1. Na página Segurança de documentos, clique em Documentos.
1. Na lista de documentos, clique no documento apropriado. A página Detalhes do documento é aberta, exibindo informações detalhadas sobre o documento. Esta página também fornece opções para revogar o acesso ao documento, alternar a política e exibir eventos relacionados a este documento.

## Exibir iterações relacionadas de um documento {#view-related-iterations-for-a-document}

Se o rastreamento de iterações relacionadas estiver ativado, é possível rastrear versões de um documento que vários usuários salvaram. Esse recurso é compatível somente com determinados aplicativos, como o PTC Pro/ENGINEER Wildfire.

Esse recurso é útil quando vários usuários estão colaborando e salvando diferentes versões do mesmo documento. a segurança de documentos pode controlar as várias iterações; portanto, é possível visualizar facilmente as informações do documento para as diferentes versões.

Se esse recurso estiver ativado, você poderá exibir as iterações relacionadas de um documento na página Documentos.

1. Exibir a página Detalhes do documento de um documento. (Consulte [Exibir informações sobre um documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Clique em Exibir iterações relacionadas. A opção só estará disponível se o recurso estiver habilitado. A lista de iterações relacionadas é exibida. Para cada iteração, você pode exibir as seguintes informações:

   * **Iteração:** O nome do arquivo. Ele pode ser diferente do nome de arquivo original e tem um número de versão anexado ao final dele.
   * **Editor:** O editor do documento original.
   * **Criado por:** O usuário que salvou a iteração.
   * **Data de criação:** A data e a hora em que a iteração foi salva.
   * **Política:** A política que protege a iteração. Diferentes iterações podem ser protegidas por políticas diferentes.

1. Para exibir a página Detalhes do documento para essa iteração, clique no nome de arquivo de uma iteração.

## Revogação e restabelecimento do acesso a documentos {#revoking-and-reinstating-access-to-documents}

Você pode revogar e restabelecer o acesso a documentos protegidos por política:

**Usuários:** Podem revogar ou restabelecer o acesso a documentos protegidos por eles com suas próprias políticas pessoais ou com políticas compartilhadas para as quais o recurso de revogação está ativado para o usuário que aplica a política. Os usuários que não puderem revogar o acesso a um documento ou alternar uma política precisam entrar em contato com o administrador.

**Administradores:** Pode revogar ou restabelecer privilégios de acesso a qualquer documento protegido por política, inclusive aqueles protegidos por políticas pessoais ou compartilhadas. Se um administrador revogar o acesso a um documento protegido por uma política compartilhada, somente um administrador poderá restabelecer os privilégios de acesso desse documento.

**Coordenadores de definições de políticas:** Podem revogar ou restabelecer privilégios de acesso para documentos protegidos por políticas de seus conjuntos de políticas.

Quando você revoga ou restaura privilégios de acesso a documentos, a alteração é efetivada nestes momentos:

* Se o documento estiver online e fechado, a alteração terá efeito na próxima vez que o destinatário sincronizar com a segurança de documentos, abrindo um documento protegido por política.
* Se o documento estiver online e aberto, a alteração será aplicada quando o destinatário fechar o documento.
* Se o documento estiver offline (em uso sem uma conexão com a Internet, como em um laptop), a alteração terá efeito na próxima vez que o destinatário sincronizar com a segurança do documento.

**Revogar acesso a um documento protegido por política**

1. Na página Segurança de documentos, clique em Documentos.
1. Marque a caixa de seleção ao lado do documento apropriado e clique em Revogar. Você pode revogar o acesso a vários documentos de uma vez.
1. Selecione uma mensagem para exibir aos usuários que tentarem abrir o documento após sua revogação:

   * **Mensagem geral:** Indica que o autor revogou o documento
   * **Documento encerrado:** Indica que o autor encerrou o documento
   * **Documento revisado**: indica que o autor revisou o documento

1. (Opcional) Se uma versão mais recente do documento estiver disponível, insira o URL e clique em Testar para verificar o URL.
1. Clique em OK e, em seguida, clique em OK novamente para retornar à página Documentos.

**Restaurar privilégios de acesso a documentos**

1. Na página Segurança de documentos, clique em Documentos.
1. Na lista de documentos, clique no documento apropriado.
1. Clique em Cancelar revogação e em OK.

## Alternar uma política aplicada a um documento {#switch-a-policy-that-is-applied-to-a-document}

Os usuários, os coordenadores de definições de políticas e os administradores podem alternar a política aplicada a um documento protegido por política (só é possível aplicar uma política de cada vez a um documento). Os usuários podem alternar políticas aplicadas a seus próprios documentos protegidos por política se criaram a política ou se a política for compartilhada e tiver esse recurso ativado. Caso contrário, o administrador ou o coordenador do conjunto de políticas deverá alternar a política. Os administradores podem alternar políticas para qualquer documento protegido por política do usuário. Os coordenadores de definições de políticas podem trocar as políticas de seus conjuntos de políticas.

Quando você alterna uma política, a nova política é aplicada da seguinte maneira:

* Se o documento estiver online e fechado, a alteração terá efeito na próxima vez que o destinatário sincronizar com a segurança de documentos, abrindo qualquer documento protegido por política online.
* Se o documento estiver online e aberto, a alteração entrará em vigor quando o usuário fechar o documento.
* Se o documento estiver offline (em uso sem uma conexão ativa com a Internet ou com a rede, como em um laptop), a alteração será aplicada na próxima vez que o usuário sincronizar com a segurança do documento abrindo um documento protegido por política online.

>[!NOTE]
>
>Para permitir acesso anônimo a um documento protegido por política que não tenha esse acesso no momento, remova a política existente no aplicativo cliente e aplique uma política que permita acesso anônimo. Se você alternar a política, os usuários ainda deverão fazer logon para acessar o documento.

1. Na página Segurança de documentos, clique em Documentos.
1. Na lista de documentos, clique no documento apropriado.
1. Clique em Alternar política. Uma lista de até 100 políticas é exibida.
1. Se a política desejada não for exibida, selecione Nome da Política ou ID da Política na lista Localizar, digite o nome ou ID e clique em Localizar.
1. Clique em uma nova regra na lista.
1. Clique em Alternar política e, em seguida, clique em OK para retornar à página Documentos.

## Pesquisar um documento {#search-for-a-document}

Você pode pesquisar documentos na página Documentos usando uma combinação de critérios de intervalo de datas e os critérios de pesquisa disponíveis na lista. Esses critérios incluem o nome do documento, o nome da política ou todos os documentos.

Algumas opções de pesquisa adicionais estão disponíveis somente para administradores:

**ID do documento:** Número de ID exclusivo que a segurança de documentos atribui ao documento quando a política é aplicada.

**Nome do documento:** Nome do documento.

**Nome do editor:** Nome do usuário que anexou a política ao documento. Você pode selecionar o usuário de todos os domínios ou de um domínio especificado.

**ID da política:** Número de ID da política anexada ao documento.

**Nome da política:** Nome da política anexada ao documento.

**Todos os documentos:** Todos os documentos protegidos por administradores e usuários. Usar a opção Todos os documentos para pesquisar pode retornar uma longa lista de documentos.

1. Na página Segurança de documentos, clique em Documentos.
1. Na lista Localizar, selecione os critérios de pesquisa necessários.

   Você pode especificar os critérios como ID do documento, nome do documento, nome do editor, ID da política, nome da política ou todos os documentos.

   Se você especificar o nome do publicador, clique no ícone Catálogo de Endereços e especifique o domínio em que deseja pesquisar o usuário, e clique em OK para retornar à página de pesquisa Documentos.

1. (Opcional) Na lista Data, selecione uma opção de intervalo de datas. Se você selecionar Datas personalizadas, digite a data no formato aaaa/mm/dd nas caixas exibidas ou use o Seletor de datas para especificar o intervalo de datas:

   * Clique no calendário para abrir o Seletor de datas.
   * Use as setas para localizar um ano e um mês.
   * Clique em um dia do mês no calendário.
   * Clique em OK para fechar o Seletor de datas.

1. Clique em Localizar.

## Classificar a lista de documentos {#sort-the-document-list}

Você pode classificar a lista de documentos por cabeçalho de coluna. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna é usada no momento para classificação. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Na página Segurança de documentos, clique em Documentos.
1. Clique no cabeçalho de coluna apropriado.
1. Para alterar a ordem de classificação, clique na coluna novamente.

## Adicionar página de capa a documentos protegidos por política {#add-cover-page-to-policy-protected-documents}

Se houver a maioria dos visualizadores que não são da Adobe PDF, se você abrir um documento protegido por segurança de documento, a primeira página será exibida como uma página em branco ou o aplicativo será anulado sem abrir o documento.

Você pode usar o suporte à Página 0 (Documento envolvedor) para permitir que visualizadores que não sejam do Adobe PDF abram um documento protegido e exibam uma página de capa no documento.

>[!NOTE]
>
>Ao visualizá-los (contendo uma Página 0) no Adobe Reader/Acrobat ou no Reader móvel, o documento protegido é aberto por padrão.

**Para adicionar uma página de capa a um documento protegido por política**

Use os seguintes processos no Workbench:

**Documento Protect Com Folha De Rosto:** Protege um documento PDF com a política especificada e adiciona uma página de capa ao documento

**Extrair documento protegido:** Extrai o documento PDF protegido por política do documento PDF com a página de capa

Use as seguintes APIs de segurança de documentos:

**protectDocumentWithCoverPage:** Protege um determinado PDF com a política especificada e retorna um documento com uma página de capa e o documento protegido como um anexo
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** Extrai o documento protegido que é um anexo no documento com uma página de capa. O documento com a página de capa pode ser criado usando o método protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
