---
title: Criar e gerenciar políticas
seo-title: Criar e gerenciar políticas
description: Uma política é um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Você pode criar e gerenciar vários tipos de políticas usando formulários AEM.
seo-description: Uma política é um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Você pode criar e gerenciar vários tipos de políticas usando formulários AEM.
uuid: 72be06f3-3e90-495e-8425-72380d95704a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fa054d30-c7dc-4b64-acf1-cbcbe8827df5
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Creating and managing policies {#creating-and-managing-policies}

Uma *política* define um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Um conjunto *de* políticas é usado para agrupar um conjunto de políticas que têm um objetivo comercial comum. Esses conjuntos de políticas são disponibilizados para um subconjunto de usuários no sistema. Para obter detalhes sobre políticas, consulte [Políticas e documentos](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents)protegidos por política.

## Tipos de políticas {#types-of-policies}

A segurança do Documento fornece os seguintes tipos de políticas.

**Políticas pessoais**

Os usuários podem criar, editar, copiar, excluir e aplicar suas próprias políticas com configurações adequadas a uma situação específica. Somente a pessoa que cria uma política e os administradores podem acessar essa política pessoal. As políticas pessoais são exibidas na guia Minhas políticas da página Políticas.

Os usuários convidados também podem criar, editar, copiar e excluir políticas pessoais se o administrador ativar esse recurso.

**Políticas compartilhadas**

Administradores e coordenadores de definição de política criam políticas compartilhadas com base nos requisitos de confidencialidade que sua organização identifica para diferentes tipos de documentos e usuários. As políticas compartilhadas estão contidas em conjuntos de políticas e estão disponíveis para todos os usuários autorizados (editores de documentos, coordenadores de conjuntos de políticas e recipient de documentos) para um determinado conjunto de políticas. Os administradores e coordenadores de definição de política podem ativar e desativar políticas compartilhadas. As políticas compartilhadas são exibidas nos conjuntos de políticas, na guia Conjuntos de políticas da página Políticas.

Quando você instala a segurança do documento pela primeira vez, ela contém uma política compartilhada, chamada *Restringir a todos os principais*. Quando essa política é aplicada a um documento, qualquer usuário que possa fazer logon na segurança do documento pode acessar o documento. Essa política está localizada no conjunto de políticas chamado Conjunto *de Políticas* Globais. Por padrão, essa política não está ativada. Você pode ativá-la se atender às necessidades de sua organização.

**Políticas geradas automaticamente pelo Microsoft Outlook**

Usando o Acrobat, é possível aplicar políticas a documentos que você envia como anexos de email no Microsoft Outlook. No Outlook, é possível proteger um documento usando uma política existente ou uma política gerada automaticamente gerada pelo Acrobat com configurações de confidencialidade padrão e se aplica ao documento anexado a uma mensagem de email. (Consulte a Ajuda *[do](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*Acrobat.)

>[!NOTE]
>
>Para que uma política esteja disponível no Outlook, é necessário definir a política como favorita no Acrobat. Todas as outras políticas, incluindo aquelas em que você está no Editor, não são exibidas no Outlook.

## Quem pode criar e gerenciar políticas e conjuntos de políticas {#who-can-create-and-manage-policies-and-policy-sets}

A forma como você interage com políticas e conjuntos de políticas depende de sua função na organização:

**Usuários:** Os usuários podem criar, editar e excluir suas políticas pessoais. Os usuários convidados também podem criar políticas pessoais se o administrador ativar esse recurso.

**Coordenadores de definição de políticas:** Os coordenadores dos conjuntos de políticas podem criar e gerenciar políticas compartilhadas nos conjuntos de políticas em que são designados como coordenadores. Um coordenador de conjunto de políticas é tipicamente um especialista na organização que pode melhor criar as políticas num conjunto de políticas específico.

**Administradores:** Os administradores podem editar as políticas pessoais de qualquer usuário. Eles podem criar políticas compartilhadas. Eles também podem criar, editar e excluir conjuntos de políticas e designar coordenadores de conjuntos de políticas.

Para obter detalhes sobre as várias funções de segurança do documento, consulte [Sobre usuários](/help/forms/using/admin-help/document-security.md#about-document-security-users)de segurança do documento.

## Criar e editar políticas {#creating-and-editing-policies}

Os usuários podem criar ou editar políticas pessoais para uso próprio. Administradores e coordenadores de definição de política podem criar ou editar políticas compartilhadas para sua organização.

### Considerações para políticas de edição {#considerations-for-editing-policies}

Quando você edita uma política, as alterações afetam documentos que a política protege atualmente, bem como documentos que a política protege posteriormente. Por exemplo, se você remover recipient de uma política atualmente aplicada a um documento, os recipient não poderão mais abrir o documento.

O status do documento determina quando a alteração entra em vigor:

* Se o documento estiver on-line, as alterações serão aplicadas imediatamente, a menos que o usuário tenha o documento aberto. Nesse caso, o usuário deve fechar a documento para que as alterações entrem em vigor.
* Se um recipient estiver usando o documento offline (por exemplo, em um laptop), as alterações entrarão em vigor na próxima vez que o recipient colocar o documento online e sincronizar com a segurança do documento, abrindo qualquer documento protegido por política.

>[!NOTE]
>
>As políticas que o Acrobat gera automaticamente para os recipient de documentos anexados a mensagens de email no Microsoft Outlook não aparecem na lista de política. É possível visualização dessas políticas apenas abrindo a página Detalhes do Documento para o documento associado.

Quando você edita políticas, essas restrições se aplicam:

* Os usuários convidados só poderão editar políticas se o administrador ativar esse recurso. Se não for possível editar políticas, a opção Editar não estará disponível.
* Os coordenadores de definição de política podem editar políticas em conjuntos de políticas somente se tiverem as permissões corretas. O superusuário ou administrador do conjunto de políticas define essas permissões na interface do administrador de segurança do documento.
* Se a política tiver uma marca d&#39;água configurada que o administrador excluiu desde que a política foi criada, essa marca d&#39;água não será mais aplicada aos documentos se você editar e salvar a política. As marcas d&#39;água excluídas permanecerão em vigor somente para políticas existentes, desde que você não edite a política. Se você editar a política, deverá selecionar outra marca d&#39;água para substituir a que foi excluída.
* Não é possível conceder acesso anônimo a um documento editando a política aplicada no momento. Se você editar a política, os usuários ainda deverão fazer logon para acessar o documento. Para aplicar acesso anônimo a esse documento, primeiro remova a política no aplicativo cliente e depois aplique outra política que permita acesso anônimo.
* As políticas que o Acrobat gera automaticamente para os recipient de um documento anexado a uma mensagem de email no Microsoft Outlook não aparecem na lista de política. Para acessar essa política, localize o documento na página Documentos, abra a página Detalhes do Documento e clique no nome da política na lista de detalhes do documento.

**Criar ou editar uma política**

1. Na página Segurança do documento, clique em Políticas e em uma destas guias:

   * Para criar ou editar uma política pessoal, clique na guia Minha política.
   * Para criar ou editar uma política compartilhada, se você tiver permissão, clique na guia Conjuntos de políticas e no nome do conjunto de políticas apropriado e clique na guia Políticas.

1. Clique em Novo ou selecione a política que deseja editar na lista.
1. Na caixa Nome, digite um nome que identifique exclusivamente a política. Na caixa Descrição, descreva o que a política faz e quando usá-la. Se a política estiver em um conjunto de políticas, o nome e a descrição serão exibidos na lista de políticas para todos os usuários especificados. As políticas pessoais estão disponíveis somente para o usuário e os administradores.

   Os seguintes caracteres não podem ser usados no nome ou na descrição:

   * sinal de menor que (&lt;)
   * sinal de maior que (>)
   * E comercial (&amp;)
   * aspas simples (&#39;)
   * aspas duplos (&quot;)
   * barra invertida (\)
   * barra (/)
   Se você usar o seguinte caractere no nome ou descrição, eles serão convertidos em espaços:

   * retorno do carro (caractere ASCII 13)
   * nova linha (caractere ASCII 10).
   >[!NOTE]
   >
   >É possível criar um nome de política que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot;, são considerados iguais. Quando alguém cria uma política, uma comparação é feita para verificar se uma política com o mesmo nome já existe. A comparação não pode distinguir entre nomes que são os mesmos, exceto caracteres acentuados. Pressupõe-se que a política já foi adicionada ao banco de dados e que a nova política não foi adicionada.

1. Adicione usuários e grupos à política e defina as permissões apropriadas. (Consulte [Usuários e grupos](creating-policies.md#users-and-groups).)
1. Em Configurações gerais, selecione as opções apropriadas. (Consulte Configurações [gerais](creating-policies.md#general-settings).)
1. (Opcional) Se aplicável, selecione um provedor de autorização externo e especifique suas propriedades. Se você não quiser usar um provedor de autorização externo, clique em Remover provedor padrão.

   Um provedor de autorização externo é usado para configurar propriedades dentro da política e, quando selecionado, o provedor de autorização externo usa essas informações para avaliar a política. As propriedades disponíveis são configuradas pelo administrador e pela pessoa que instala o software.

1. Em Configurações avançadas, selecione as opções apropriadas. (Consulte Configurações [](creating-policies.md#advanced-settings)avançadas.)
1. Em Configurações avançadas inalteráveis, selecione as opções apropriadas. (Consulte Configurações [](creating-policies.md#unchangeable-advanced-settings)avançadas inalteráveis.)
1. Clique em Salvar. A política é exibida na lista de políticas. Um ícone com um círculo vermelho aparece ao lado da nova política, indicando que ela ainda está desativada.

   Para disponibilizar a política para os usuários, ative-a. (Consulte [Ativar ou desativar políticas](creating-policies.md#enable-or-disable-shared-policies)compartilhadas.)

### Usuários e grupos {#users-and-groups}

Na área Usuários e grupos, especifique os usuários que têm acesso a documentos protegidos com a política. Para cada usuário ou grupo especificado, você também define os privilégios de uso do documento.

>[!NOTE]
>
>O editor do documento é o usuário que protege o documento com a política. Esse usuário é sempre incluído por padrão em uma política, com direitos de acesso completos, incluindo recursos de revogação e de alternância de políticas. No entanto, os administradores podem alterar os direitos de acesso do editor do documento para políticas compartilhadas. Por exemplo, o administrador pode impedir que o editor do documento revogue o acesso ao documento ou altere a política.

**Adicionar usuário ou grupo:** Para adicionar um usuário ou grupo de usuários, clique em Adicionar usuário ou grupo e clique em Pesquisa avançada para localizar usuários ou grupos. Os usuários incluem os usuários internos de sua organização e usuários convidados que se registraram com a segurança do documento. Quando você seleciona essa opção, a página Adicionar usuário ou grupo é exibida:

* Na caixa Localizar, digite o nome do usuário ou grupo ou o endereço de email.
* Na lista Using (Uso), selecione Name (Nome) ou Email.
* Na lista Tipo, selecione Usuário ou Grupo.
* Selecione o domínio que deseja pesquisar na lista In e clique em Localizar.
* Quando os resultados forem retornados, selecione o usuário ou grupo a ser adicionado e clique em Adicionar.

>[!NOTE]
>
>Se você digitar um nome de usuário convidado ou endereço de email correto e nenhum resultado for retornado, o usuário talvez ainda não tenha se registrado ou a conta poderá ser excluída. Você pode tentar adicionar o usuário como um tipo de usuário convidado ou entrar em contato com o administrador.

**Convidar novo usuário:** Para adicionar um usuário convidado, clique em Convidar novo usuário, digite o endereço de email do usuário na caixa exibida e clique em Convidar. Essa opção está disponível somente se o administrador a ativou. Quando você adiciona novos usuários convidados a uma política, a segurança do documento envia um e-mail de convite de inscrição se os usuários ainda não tiverem sido convidados a se registrar. Os usuários devem usar o link no email para criar uma conta e, em seguida, devem ativá-la.

Depois de se inscreverem, os usuários convidados podem usar documentos protegidos por política para os quais têm autorização. Dependendo dos recursos ativados pelo administrador, os usuários externos podem ter permissão para aplicar políticas a documentos, criar, editar e excluir políticas e adicionar outros usuários externos às políticas.

**Adicionar usuário anônimo:** Para permitir o acesso anônimo do usuário, clique em Adicionar usuário anônimo. Esta opção está disponível somente se o administrador ativou o acesso anônimo do usuário para a segurança do documento. (Consulte Configurar o servidor de segurança do documento.) Esta opção concede a todos o acesso a documentos protegidos por esta política, independentemente de terem uma conta de segurança de documento. Se você selecionar essa opção, não poderá adicionar outros tipos de usuários à política.

>[!NOTE]
>
>Para permitir o acesso anônimo a um documento protegido por política que atualmente não o tem, remova a política existente e aplique uma política que permita o acesso anônimo. Se você alternar ou alterar a política existente, os usuários ainda deverão fazer logon para acessar o documento.

#### Especificar as permissões do documento para usuários e grupos {#specify-the-document-permissions-for-users-and-groups}

Você pode especificar permissões de documento para um usuário ou grupo de cada vez, ou pode selecionar vários usuários e grupos da lista e alterar suas permissões usando as opções na área de cabeçalhos de coluna.

Por padrão, todos os documentos protegidos por política têm uma permissão que permite aos usuários abri-los online.

A guia Permissões e opções é exibida na segurança do documento.

Essas permissões de documento estão disponíveis na guia Permissões. Você pode aplicar essas permissões a arquivos PDF, PTC Pro/E e Microsoft Office.

**Imprimir:** Permite que o usuário imprima um documento protegido por essa política. Para arquivos Office e Pro/E, você pode marcar a caixa de seleção Imprimir para permitir a impressão ou limpá-la para impedir a impressão. Se você marcar a caixa de seleção Mostrar permissões personalizadas para PDF, poderá selecionar uma destas opções:

**Não permitido:** O usuário não tem permissão para imprimir o PDF.

**Permitido:** O usuário tem permissão para imprimir o PDF.

**Baixa resolução. Unicamente:** O usuário tem permissão para imprimir o PDF em baixa resolução.

**Modificar:** Permite que o usuário modifique um documento protegido por essa política. Para arquivos do Office e Pro/E, você pode marcar a caixa de seleção Modificar para permitir modificações ou limpá-las para impedir modificações. Se você marcar a caixa de seleção Mostrar permissões personalizadas para PDF, poderá selecionar uma destas opções:

**Não permitido:** O usuário não tem permissão para modificar o PDF.

**Qualquer:** O usuário pode modificar o PDF.

**Colaborar:** O usuário tem permissão para colaborar com outras pessoas, usando as opções Colaborar no Adobe Acrobat. Essa permissão permite que o usuário copie dados de formulário mesmo se a permissão Copiar não for fornecida explicitamente na política.

**Alterar páginas:** O usuário tem permissão para adicionar e remover páginas e editar conteúdo no PDF.

**Preencher e assinar:** O usuário tem permissão para preencher campos de formulário no PDF e assiná-lo.

**Copiar:** Permite que o usuário copie o texto de um documento protegido com esta política.

**Leitor de tela:** Essa permissão será exibida se você marcar a caixa de seleção Mostrar permissões personalizadas para PDF. Quando essa opção é selecionada, o Adobe Acrobat tem permissão para adicionar tags temporárias ao PDF para melhorar sua legibilidade com um leitor de tela.

Essas permissões de documento estão disponíveis na guia Opções. Você pode aplicar essas permissões a arquivos PDF, PTC Pro/E e Microsoft Office:

**Offline:** Permite que o usuário visualização um documento offline protegido por essa política.

**Validade da permissão:** Selecione Permissões sempre válidas ou defina um período de validade das permissões de documento. Se você selecionar um período de validade, clique nos ícones de calendário para selecionar uma data e use as setas para especificar o horário no formato de 24 horas.

Para políticas compartilhadas, os administradores podem desativar os seguintes privilégios para o editor do documento (o usuário que aplica a política a um documento):

**Revogar:** Permite que o editor do documento revogue os privilégios de acesso ao documento.

**Comutador:** Permite que o editor do documento alterne os privilégios da política.

### Configurações gerais {#general-settings}

A área Configurações gerais contém as seguintes configurações:

**Período de validade:** O período de tempo durante o qual o documento protegido por política está acessível aos recipient autorizados. É possível escolher entre essas opções de período de validade:

**O Documento não será válido após:** O documento pode ser acessado pelo número especificado de dias a partir do momento em que o documento foi protegido.

**O Documento não será válido após esta data:** O documento é válido a partir da data em que a política é aplicada ao documento até a data final especificada.

**Válido de, para:** O documento é válido durante as datas especificadas. Você pode usar o calendário para selecionar uma data, quando aplicável, clicando no ícone do calendário.

**O Documento é sempre válido:** O período de validade do documento não expira.

>[!NOTE]
>
>As datas de validade baseiam-se no fuso horário do sistema de segurança do documento, não no fuso horário do computador local.

**Auditoria:** Ative ou desative a auditoria dos eventos associados a um documento protegido por política. Por exemplo, a segurança do documento pode gravar eventos como tentativas de abrir um documento. eventos auditados são exibidos na lista na página Eventos. Se você não selecionar essa opção, a segurança do documento não registrará eventos para documentos associados à política.

>[!NOTE]
>
>O administrador também deve habilitar a auditoria do servidor na página de configuração Auditoria e Configurações de privacidade para que o recurso de auditoria funcione.

**Rastreamento de uso estendido:** Ative ou desative o rastreamento de uso estendido. A segurança do documento oferece suporte ao rastreamento de eventos do usuário associados a várias operações executadas em um arquivo PDF. O objeto de segurança do documento pode ser acessado usando um Java Script. Um clique de botão, um arquivo multimídia que está sendo reproduzido ou o salvamento de um arquivo são alguns exemplos de eventos que podem ser disparados de um PDF protegido por política. Usando o objeto de segurança do documento, também é possível recuperar informações do usuário. O rastreamento de eventos pode ser ativado no servidor de segurança do documento no nível global ou em um nível de política.

**Período de Locação Offline Automática:** O número máximo de dias em que o recipient pode usar o documento offline protegido por política (sem uma conexão ativa com a Internet ou a rede). Quando o período de empréstimo expirar, o recipient deverá sincronizar o documento novamente para continuar a usá-lo.

### Provedores de autorização externos {#external-authorization-providers}

Selecione os provedores de autenticação externos se você já tiver configurado algum. Os provedores disponíveis são listados.

### Configurações da autenticação {#authentication-settings}

É possível substituir as configurações de autenticação que você configurou no servidor e especificar as opções de autenticação relevantes para essa política. Selecione Substituir configurações de autenticação global e selecione as opções de autenticação relevantes para esta política. As seguintes opções de autenticação estão disponíveis:

**Permitir Autenticação de Senha de Nome de Usuário:** Selecione esta opção para permitir que os aplicativos clientes usem a autenticação de nome de usuário/senha ao se conectar ao servidor.

**Permitir autenticação Kerberos:** Selecione essa opção para permitir que os aplicativos clientes usem a autenticação Kerberos ao se conectar ao servidor.

**Permitir Autenticação de Certificado de Cliente:** Selecione esta opção para permitir que os aplicativos clientes usem autenticação de certificado ao se conectar ao servidor.

**Permitir Autenticação** Estendida Selecione para habilitar autenticação estendida. A seleção dessa opção permite que os aplicativos clientes usem autenticação estendida. A autenticação estendida fornece processos de autenticação personalizados e diferentes opções de autenticação configuradas no servidor de segurança do Documento

Se você estiver substituindo as configurações de autenticação global, poderá escolher as opções de autenticação relevantes para esta política. Por exemplo, se você ativou três opções de autenticação (nome de usuário e senha, certificado de cliente e autenticação estendida) no servidor, é possível substituir essa configuração global e selecionar somente autenticação estendida para essa política. Você deve garantir que a opção de autenticação selecionada aqui já esteja configurada no servidor. Neste exemplo, não é possível selecionar Kerberos como opção de autenticação porque ela não está configurada no servidor.

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

### Configurações avançadas {#advanced-settings}

A área Configurações avançadas contém as seguintes configurações:

**Marca d&#39;água dinâmica:** Selecione uma marca d&#39;água para ser exibida dinamicamente nas páginas de um documento (por exemplo, quando um recipient imprime o documento). As marcas d&#39;água dinâmicas identificam exclusivamente um documento, ajudando assim a garantir a confidencialidade do documento e evitando a violação dos direitos autorais. Por exemplo, o administrador pode configurar uma marca d&#39;água dinâmica que exibe a data atual, o nome de usuário ou o identificador da pessoa que está usando o documento ou o nome da política usada para proteger o documento. Uma marca d&#39;água também pode exibir elementos gráficos ou de texto personalizados se configurado. Os administradores configuram as opções de marcas d&#39;água e os administradores e usuários podem aplicá-las às políticas.

(Consulte [Configurar marcas d&#39;água](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)dinâmicas.)

Se você estiver editando uma política e o administrador tiver excluído uma marca d&#39;água configurada selecionada anteriormente para essa política, uma nota será exibida na página Editar política. Nesse caso, se estiver salvando o documento editado, selecione uma nova marca d&#39;água se quiser que ela apareça no documento.

>[!NOTE]
>
>Para políticas que fornecem acesso anônimo ao usuário, o nome de usuário e o identificador de um usuário anônimo não são exibidos como uma marca d&#39;água mesmo se você selecionar esse tipo de marca d&#39;água.

**Usar somente plug-ins certificados do Acrobat para PDF:** Quando selecionada para uma política, essa opção especifica que o Acrobat 8.0 e posterior deve ser executado no modo certificado ao abrir documentos protegidos com a política. Quando o Acrobat é executado no modo certificado, ele não carregará plug-ins de terceiros.

Selecione essa opção se estiver preocupado com o recipient que está escrevendo um plug-in que pode contornar qualquer proteção de documento no Acrobat 8.0 e posterior. Não selecione essa opção se os recipient do documento precisarem usar plug-ins de terceiros no Acrobat para interagir com documentos.

Essa opção ativa somente o modo certificado no Acrobat 8.0 ou posterior; o administrador deve desativar o acesso ao Acrobat 7.0.

(Consulte [Configurar o servidor](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)de segurança do documento.)

Essa opção não se aplica ao Adobe Reader.

**Mensagem de erro de acesso negado:** Uma mensagem que aparece para qualquer pessoa que tente abrir um documento protegido por política sem permissão. Esta mensagem é exibida no Acrobat. Os clientes que não podem exibir esta mensagem exibem uma mensagem padrão para indicar que o acesso foi negado.

### Configurações avançadas inalteráveis {#unchangeable-advanced-settings}

A área Configurações avançadas inalteráveis contém as seguintes configurações. Não é possível alterar essas configurações depois de salvar a política.

**Algoritmo de criptografia e comprimento da chave:** Usada para proteger seus documentos. É possível escolher uma destas opções:

* AES de 128 bits
* AES 256 bits. Somente o Acrobat 9.0 e posteriores oferecem suporte para essa opção. Para usar a criptografia AES 256 para arquivos PDF, obtenha e instale os arquivos da política de jurisdição de força ilimitada do Java Cryptography Extension (JCE). Esses arquivos substituem os arquivos local_policy.jar e US_export_policy.jar na pasta [JAVE_HOME]/lib/security. Por exemplo, se você estiver usando o Sun JDK 1.6, copie os arquivos baixados para a pasta [dep root]/Java/jdk1.6.0_26/lib/security. Você pode baixar esses arquivos de Downloads [do](https://java.sun.com/javase/downloads/index.jsp)Java SE.
* Sem criptografia. Atualmente, o Acrobat 9.0 e versões posteriores oferecem suporte para essa opção. Se você selecionar essa opção, as opções Restrições de Documento serão desativadas. Essa opção pode ser útil se você quiser usar a segurança do documento para auditoria do documento ou controle de versão, mas não quiser criptografar o documento.

**Restrições de Documento:** Selecione os componentes do documento PDF a serem criptografados. Outros aplicativos clientes criptografam o documento inteiro, mas não arquivos vinculados ou incorporados. É possível escolher uma destas opções:

* O documento inteiro, incluindo seus anexos e metadados. *Os metadados* são informações sobre o documento e seu conteúdo que podem ser visualizações na caixa de diálogo Propriedades do documento ou no menu Avançado do Acrobat. No Acrobat, é possível anexar arquivos de tipos diferentes (por exemplo, arquivos de texto, áudio e vídeo) a documentos PDF.
* O documento e seus anexos, mas não os metadados.
* Somente os anexos do documento. É possível criptografar os anexos em um arquivo PDF sem criptografar o conteúdo do documento.

## Ativar ou desativar políticas compartilhadas {#enable-or-disable-shared-policies}

Para disponibilizar uma política compartilhada, o administrador ou o coordenador do conjunto de políticas deve ativá-la. É possível ativar novas políticas ou políticas anteriormente desativadas. Uma política compartilhada que você desabilita ainda é imposta para documentos protegidos com essa política.

Um X vermelho é exibido ao lado de uma política desativada.

>[!NOTE]
>
>Os administradores não podem desativar políticas pessoais e os usuários não podem ativar e desativar suas próprias políticas.

1. Na página Segurança do documento, clique em Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Clique no nome do conjunto de políticas apropriado e clique na guia Políticas.
1. Marque a caixa de seleção ao lado da política apropriada, clique em Ativar ou Desativar e clique em OK.

## Informações de Visualização sobre uma política {#view-information-about-a-policy}

Usando a guia Minhas políticas, você pode pesquisar políticas pessoais.

Os conjuntos de políticas criados pelos administradores são listados na guia Conjuntos de políticas da página Políticas com informações sobre o conjunto de políticas, incluindo seu nome, a data criada e modificada e uma descrição. Clique no nome de um conjunto de políticas para ver seus detalhes. Os coordenadores do conjunto de políticas que têm permissão para gerenciar políticas podem criar políticas compartilhadas dentro de um conjunto de políticas específico.

Quando você cria ou edita uma política, uma página é exibida onde você pode configurar detalhes como nome da política, níveis de permissão, configurações de confidencialidade e os recipient a serem incluídos na política.

O administrador pode definir as seguintes configurações de confidencialidade para uma política:

* Opções gerais de confidencialidade do documento, como o período de validade do documento e o período de empréstimo offline
* Os usuários autorizados e as restrições e privilégios de documento para cada um desses usuários
* Opções avançadas de confidencialidade do documento, incluindo marcas d&#39;água dinâmicas e criptografia de documento

Os usuários podem visualização as políticas que criaram e as políticas compartilhadas às quais têm acesso. Os administradores podem visualização todas as políticas compartilhadas e pessoais que estão na segurança do documento.

Você pode visualização informações mais detalhadas sobre uma política que aparece na lista, incluindo os usuários ou grupos incluídos na política e as configurações de confidencialidade especificadas para esses usuários.

>[!NOTE]
>
>As políticas que o Acrobat gera automaticamente para os recipient de documentos anexados a mensagens de email no Microsoft Outlook não aparecem na lista de política. É possível visualização dessas políticas apenas abrindo a página Detalhes do Documento para o documento associado.

1. Na página Segurança do documento, clique em Políticas e, em seguida, clique na guia Minhas políticas.
1. Preencha as informações de pesquisa para procurar políticas pessoais.
1. Selecione a política apropriada na lista.
1. Na página Detalhes da política, você pode ver detalhes sobre a política, editar a política ou eventos de visualização relacionados à política.

## Procurar políticas {#search-for-policies}

Os administradores podem pesquisar por políticas compartilhadas e por políticas pessoais que foram criadas por outros usuários.

1. Para procurar uma política compartilhada, clique em Políticas e, em seguida, clique na guia Conjuntos de políticas. Clique em um conjunto de políticas na lista e clique na guia Políticas.

   Para procurar uma política pessoal, na página de segurança do documento, clique em Políticas e, em seguida, clique na guia Minhas políticas.

1. Na lista Localizar, selecione uma destas opções:

   **ID da política:** O número de identificação da política gerado quando o usuário cria a política. Você deve digitar a ID exata da política.

   **Nome da política:** O nome da política. Você pode procurar parte ou todo o nome da política.

1. Na caixa de texto, digite o valor correspondente. Por exemplo, se você selecionou Nome da política, digite o nome da política que está procurando.
1. Na lista de exibição, selecione o número de resultados a serem exibidos e clique em Localizar. Os resultados da pesquisa são exibidos.
1. (Opcional) Para visualização dos detalhes da política, clique na política.

## Copiar uma política {#copy-a-policy}

É possível copiar uma política existente e salvá-la com um novo nome e descrição. Copiar políticas é uma maneira eficiente de criar novas políticas usando as configurações existentes.

Usuários externos podem copiar políticas somente se o administrador ativar esse recurso. Se não for possível criar políticas, a opção Copiar não estará disponível.

1. Na página de segurança do documento, clique em Políticas e na guia Minha política.
1. Selecione a política apropriada na lista.
1. Na página Detalhes da política, clique em Copiar.
1. Na caixa Nome da nova política, digite o nome da nova política. Opcionalmente, digite uma nova Descrição.

   Os seguintes caracteres não podem ser usados no nome ou na descrição:

   * sinal de menor que (&lt;)
   * sinal de maior que (>)
   * E comercial (&amp;)
   * aspas simples (&#39;)
   * aspas duplos (&quot;)
   * barra invertida (\)
   * barra (/)
   Se você usar o seguinte caractere no nome ou descrição, eles serão convertidos em espaços:

   * retorno do carro (caractere ASCII 13)
   * nova linha (caractere ASCII 10).
   >[!NOTE]
   >
   >É possível criar um nome de política que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot;, são considerados iguais. Quando alguém cria uma política, uma comparação é feita para verificar se uma política com o mesmo nome já existe. A comparação não pode distinguir entre nomes que são os mesmos, exceto caracteres acentuados. Pressupõe-se que a política já foi adicionada ao banco de dados e que a nova política não foi adicionada.

1. Clique em OK.

## Excluir uma política {#delete-a-policy}

É possível excluir políticas que você criou. Os administradores podem excluir políticas que qualquer usuário criou. Os coordenadores de conjunto de políticas podem excluir políticas em seus conjuntos de políticas. Uma política que você exclui ainda é imposta para documentos protegidos com essa política. É possível excluir mais de uma política de cada vez.

Os usuários convidados podem excluir políticas somente se o administrador ativar esse recurso. Se não for possível excluir políticas, a opção de exclusão não estará disponível.

1. Na página Segurança do documento, clique em Políticas.
1. Clique na guia Minha política.
1. Para excluir uma política compartilhada, clique na guia Conjuntos de políticas e clique no nome do conjunto de políticas apropriado.
1. Marque a caixa de seleção ao lado da política apropriada, clique em Excluir e, em seguida, clique em OK.

>[!NOTE]
>
>Você deve usar o aplicativo cliente para remover políticas de documentos. (Consulte a Ajuda do Acrobat ou a Ajuda apropriada das extensões do Acrobat Reader DC.)

## Classificar a lista de política {#sort-the-policy-list}

Você pode classificar a lista de política por cabeçalho de coluna para encontrar políticas mais facilmente. Um ícone de triângulo ao lado do cabeçalho da coluna indica qual coluna está sendo usada para classificar no momento. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Na página Segurança do documento, clique em Políticas e clique na guia Conjunto de políticas.
1. Selecione um conjunto de políticas e clique na guia Políticas.
1. Clique no cabeçalho da coluna apropriada.
1. Para alterar a ordem de classificação, clique na coluna novamente.

