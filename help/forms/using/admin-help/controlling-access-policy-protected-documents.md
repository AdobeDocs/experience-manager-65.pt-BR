---
title: Controle do acesso a documentos protegidos por política
seo-title: Controle do acesso a documentos protegidos por política
description: Veja como você pode visualização, gerenciar e controlar o acesso aos documentos protegidos por política.
seo-description: Veja como você pode visualização, gerenciar e controlar o acesso aos documentos protegidos por política.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 0%

---


# Controle do acesso a documentos protegidos por política {#controlling-access-to-policy-protected-documents}

Você pode controlar a maneira como os recipient usam seus documentos protegidos por política, não importa quão amplamente você os distribua.

Usando a página Documentos, você pode fazer estas tarefas:

* Procure e visualização os detalhes de documentos protegidos por política. Você pode ver informações sobre o nome do documento, o nome do editor, o nome da política e a data em que a política foi aplicada. Se a política que protegeu um documento for excluída, você também poderá ver a ID da política excluída no nome da política. Os usuários podem visualização e gerenciar seus próprios documentos protegidos por política. Os administradores podem visualização e gerenciar todos os documentos protegidos por política.
* Altere os detalhes da política aplicada a um documento. Os usuários podem editar suas próprias políticas, os administradores podem editar políticas compartilhadas e pessoais e os coordenadores de definição de políticas podem editar políticas compartilhadas nos conjuntos de políticas para os quais eles têm permissões. Você pode acessar a política associada a um documento diretamente da página Detalhes do Documento.
* Revogar e restabelecer o acesso a um documento protegido por política. Os administradores podem revogar e restabelecer o acesso a qualquer documento. Os coordenadores de definição de política (que têm permissão para gerenciar documentos) podem revogar e reinstalar o acesso a documentos protegidos por política que usam políticas compartilhadas de seus conjuntos de políticas. Os usuários podem revogar o acesso aos documentos protegidos por política se criarem a política que está protegendo o documento ou se a política for compartilhada que permite esse recurso.
* Alterne a política aplicada a um documento. Os usuários que aplicam políticas a documentos podem alternar uma política se a tiverem criado ou se for uma política compartilhada que habilite esse recurso. Os coordenadores de definição de políticas podem trocar as políticas dos seus conjuntos de políticas. Os administradores podem alternar as políticas aplicadas a qualquer documento.

Quando um documento é protegido por uma política e você revoga privilégios de acesso ou alterna a política aplicada, as alterações entram em vigor da seguinte maneira:

* Se o documento estiver on-line, as alterações serão aplicadas imediatamente, a menos que o usuário tenha o documento aberto. Nesse caso, o usuário deve fechar a documento para que as alterações entrem em vigor.
* Se um recipient estiver usando o documento offline (por exemplo, em um laptop), as alterações entrarão em vigor na próxima vez que o recipient sincronizar com a segurança do documento, abrindo qualquer documento protegido por política.

## Informações de visualização sobre um documento {#view-information-about-a-document}

Para cada documento listado na página Documentos, você pode ver o nome do documento, o nome do editor, o nome da política e a data em que o documento foi protegido. Se a política que protegeu um documento tiver sido excluída, a ID da política será listada em Nome da política.

Você também pode visualização mais detalhes, descritos abaixo, sobre um documento específico na página Detalhes do Documento:

>[!NOTE]
>
>Você deve usar o link Nome da política na página Detalhes do Documento para acessar as políticas geradas automaticamente no Microsoft Outlook para recipient de um documento anexado a uma mensagem de email. Essas políticas não aparecem na página de políticas.

**Nome do documento:** O nome do documento selecionado.

**ID do documento:** Um identificador exclusivo que a segurança do documento atribui quando uma política é aplicada ao documento. A segurança do documento usa esse número para rastrear o documento.

**Status do documento:** Status do documento (por exemplo, ativo ou revogado).

**Editor:** Nome do usuário que anexou a política ao documento.

**Nome da política:** o nome da política usada para proteger o documento. Você pode clicar no nome para abrir a política. Você deve usar esse link para acessar as políticas geradas pela Acrobat para recipient de um documento anexado a uma mensagem de email no Outlook. Essas políticas não aparecem na página Políticas.

**Tipo de política:** o tipo de política que foi aplicada ao documento.

**Data de publicação:** A data em que a política foi aplicada ao documento.

**Iterações relacionadas:** Se o documento tiver iterações relacionadas, esse item também aparecerá na lista. Clique no link para visualização da lista de iterações relacionadas ao documento.

Os usuários podem visualização informações sobre seus documentos protegidos. Os administradores podem visualização informações sobre documentos que qualquer usuário protegeu com uma política. Os coordenadores de definição de política podem visualização informações sobre documentos que são protegidos por políticas de seus conjuntos de políticas.

1. Na página de segurança do documento, clique em Documentos.
1. Na lista dos documentos, clique no documento apropriado. A página Detalhes do Documento é aberta, exibindo informações detalhadas sobre o documento. Esta página também fornece opções para revogar o acesso ao documento, alterar a política e exibir eventos relacionados a este documento.

## iterações relacionadas à visualização para um documento {#view-related-iterations-for-a-document}

Se o rastreamento de iterações relacionadas estiver ativado, é possível rastrear versões de um documento que vários usuários salvaram. Esse recurso é suportado apenas por determinados aplicativos, como PTC Pro/ENGINEER Wildfire.

Esse recurso é útil quando vários usuários estão colaborando e salvando versões diferentes do mesmo documento. A segurança do documento pode acompanhar as várias iterações; portanto, você pode visualização facilmente as informações do documento para as diferentes versões.

Se esse recurso estiver ativado, você poderá visualização as iterações relacionadas de um documento da página Documentos.

1. Visualização na página Detalhes do Documento de um documento. (Consulte [Informações de Visualização sobre um documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Clique em Iterações relacionadas à Visualização. A opção estará disponível somente se o recurso estiver ativado. A lista de iterações relacionadas é exibida. Para cada repetição, você pode visualização as seguintes informações:

   * **Iteração:** O nome do arquivo. Pode ser diferente do nome de arquivo original e tem um número de versão anexado ao final.
   * **Editor:** o editor do documento original.
   * **Criado por:** o usuário que salvou a iteração.
   * **Data de criação:** a data e a hora em que a iteração foi salva.
   * **Política:** A política que protege a iteração. Diferentes iterações podem ser protegidas por políticas diferentes.

1. Para exibir a página Detalhes do Documento para essa iteração, clique no nome de arquivo de uma iteração.

## Revogando e reinstalando o acesso aos documentos {#revoking-and-reinstating-access-to-documents}

Você pode revogar e reinstalar o acesso a documentos protegidos por política:

**Usuários:** pode revogar ou restabelecer o acesso aos documentos que protegem com suas próprias políticas pessoais ou com políticas compartilhadas para as quais o recurso de revogação está ativado para o usuário que aplica a política. Os usuários que não puderem revogar o acesso a um documento ou alterar uma política precisam entrar em contato com o administrador.

**Administradores:** podem revogar ou restabelecer privilégios de acesso a qualquer documento protegido por política, incluindo aqueles protegidos por políticas pessoais ou compartilhadas. Se um administrador revogar o acesso a um documento protegido por uma política compartilhada, somente um administrador poderá reinstalar os privilégios de acesso desse documento.

**Coordenadores de definição de política:** podem revogar ou restabelecer privilégios de acesso para documentos protegidos por políticas de seus conjuntos de políticas.

Quando você revoga ou reinstala os privilégios de acesso ao documento, a alteração entra em vigor nessas horas:

* Se o documento estiver online e fechado, a alteração entrará em vigor na próxima vez que o recipient sincronizar com a segurança do documento, abrindo um documento protegido por política.
* Se o documento estiver on-line e aberto, a alteração entrará em vigor quando o recipient fechar o documento.
* Se o documento estiver offline (em uso sem uma conexão com a Internet, como em um laptop), a alteração entrará em vigor na próxima vez que o recipient for sincronizado com a segurança do documento.

**Revogar o acesso a um documento protegido por política**

1. Na página de segurança do documento, clique em Documentos.
1. Marque a caixa de seleção ao lado do documento apropriado e clique em Revogar. Você pode revogar o acesso a vários documentos de cada vez.
1. Selecione uma mensagem para exibir aos usuários que tentarem abrir o documento depois que ele for revogado:

   * **Mensagem geral:** indica que o autor revogou o documento
   * **Documento finalizado:** indica que o autor encerrou o documento
   * **Documento revisado**: Indica que o autor revisou o documento

1. (Opcional) Se uma versão mais recente do documento estiver disponível, insira o URL e clique em Testar para verificar o URL.
1. Clique em OK e, em seguida, clique em OK novamente para retornar à página Documentos.

**Reinstale os privilégios de acesso ao documento**

1. Na página de segurança do documento, clique em Documentos.
1. Na lista dos documentos, clique no documento apropriado.
1. Clique em Cancelar revogação e em OK.

## Alternar uma política aplicada a um documento {#switch-a-policy-that-is-applied-to-a-document}

Os usuários, os coordenadores de definição de política e os administradores podem alternar a política aplicada a um documento protegido por política (você pode aplicar somente uma política de cada vez a um documento). Os usuários podem alternar políticas aplicadas a seus próprios documentos protegidos por política se criarem a política ou se a política for compartilhada e tiver esse recurso ativado. Caso contrário, o administrador ou o coordenador do conjunto de políticas deverá alternar a política. Os administradores podem alternar políticas para qualquer documentos protegido por política do usuário. Os coordenadores de definição de políticas podem trocar as políticas dos seus conjuntos de políticas.

Quando você alterna uma política, a nova política é aplicada da seguinte maneira:

* Se o documento estiver on-line e fechado, a alteração entrará em vigor na próxima vez que o recipient sincronizar com a segurança do documento, abrindo qualquer documento protegido por política on-line.
* Se o documento estiver online e aberto, a alteração entrará em vigor quando o usuário fechar o documento.
* Se o documento estiver offline (em uso sem uma conexão ativa de Internet ou rede, como em um laptop), a alteração será aplicada na próxima vez que o usuário sincronizar com a segurança do documento, abrindo um documento protegido por política online.

>[!NOTE]
>
>Para permitir o acesso anônimo a um documento protegido por política que atualmente não tem esse acesso, remova a política existente no aplicativo cliente e aplique uma política que permita o acesso anônimo. Se você alterar a política, os usuários ainda precisarão fazer logon para acessar o documento.

1. Na página de segurança do documento, clique em Documentos.
1. Na lista dos documentos, clique no documento apropriado.
1. Clique em Alternar política. Uma lista de até 100 políticas é exibida.
1. Se a política desejada não for exibida, selecione Nome da política ou ID da política na lista Localizar, digite o nome ou a ID e clique em Localizar.
1. Clique em uma nova política na lista.
1. Clique em Alternar política e, em seguida, clique em OK para retornar à página Documentos.

## Procurar um documento {#search-for-a-document}

Você pode pesquisar documentos na página Documentos usando uma combinação de critérios de intervalo de datas e critérios de pesquisa disponíveis na lista. Esses critérios incluem o nome do documento, o nome da política ou todos os documentos.

Algumas opções de pesquisa adicionais estão disponíveis somente para administradores:

**ID do documento: número** único de ID que a segurança do documento atribui ao documento quando a política é aplicada.

**nome do documento:** Nome do documento.

**Nome do editor:** Nome do usuário que anexou a política ao documento. Você pode selecionar o usuário de todos os domínios ou de um domínio especificado.

**ID da política:número de** ID da política anexada ao documento.

**Nome da política:** Nome da política anexada ao documento.

**Todos os documentos:** Todos os documentos protegidos por administradores e usuários. Usar a opção Todos os Documentos para pesquisar pode retornar uma longa lista de documentos.

1. Na página de segurança do documento, clique em Documentos.
1. Na lista Localizar, selecione os critérios de pesquisa necessários.

   Você pode especificar os critérios como ID do documento, nome do documento, nome do editor, ID da política, nome da política ou todos os documentos.

   Se você especificar o nome do editor, clique no ícone Catálogo de endereços e especifique o domínio no qual deseja pesquisar o usuário, e clique em OK para retornar à página de pesquisa de Documentos.

1. (Opcional) Na lista Data, selecione uma opção de intervalo de datas. Se você selecionar Datas personalizadas, digite a data no formato aaaa/mm/dd nas caixas exibidas ou use o Seletor de datas para especificar o intervalo de datas:

   * Clique no calendário para abrir o Seletor de datas.
   * Use as setas para encontrar um ano e um mês.
   * Clique em um dia do mês no calendário.
   * Clique em OK para fechar o Seletor de datas.

1. Clique em Localizar.

## Classifique a lista do documento {#sort-the-document-list}

É possível classificar a lista de documentos por cabeçalho de coluna. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna está sendo usada para classificar no momento. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Na página de segurança do documento, clique em Documentos.
1. Clique no cabeçalho da coluna apropriada.
1. Para alterar a ordem de classificação, clique na coluna novamente.

## Adicionar página de capa a documentos protegidos por política {#add-cover-page-to-policy-protected-documents}

No caso da maioria dos visualizadores que não são da Adobe PDF, se você abrir um documento protegido pela segurança do documento, a primeira página será exibida como uma página em branco ou o aplicativo será abortado sem abrir o documento.

Você pode usar o suporte para Página 0 (Documento do invólucro) para permitir que visualizadores que não sejam o Adobe PDF abram um documento protegido e exibam uma página de capa no documento.

>[!NOTE]
>
>Ao exibir esses documentos (que contêm uma Página 0) no Adobe Reader/Acrobat ou no Reader móvel, o documento protegido é aberto por padrão.

**Para adicionar a página de capa a um documento protegido por política**

Use os seguintes processos no Workbench:

**Documento Protect com página de capa:** Protege um documento PDF com a política especificada e adiciona uma página de capa ao documento

**Extrair Documento protegido:** extrai o documento PDF protegido por política do documento PDF com a capa

Use as seguintes APIs de segurança de documento:

**protectDocumentWithCoverPage:** Protege um determinado PDF com a política especificada e retorna um documento com uma página de capa e o documento protegido como um anexo 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** Extrai o documento protegido que é um anexo no documento com a página de capa. O documento com a folha de rosto pode ser criado usando o método protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`