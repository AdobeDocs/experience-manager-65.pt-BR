---
title: Criação e gerenciamento de políticas
description: Uma política é um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Você pode criar e gerenciar vários tipos de políticas usando formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 5e57451c-1a89-442c-8404-841e95d5ceff
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 0%

---

# Criação e gerenciamento de políticas {#creating-and-managing-policies}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Uma *política* define um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Um *conjunto de políticas* é usado para agrupar um conjunto de políticas que têm uma finalidade comercial comum. Esses conjuntos de políticas são então disponibilizados a um subconjunto de usuários no sistema. Para obter detalhes sobre políticas, consulte [Políticas e documentos protegidos por política](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipos de políticas {#types-of-policies}

A segurança de documentos fornece os seguintes tipos de políticas.

**Políticas pessoais**

Os usuários podem criar, editar, copiar, excluir e aplicar suas próprias políticas com configurações apropriadas a uma situação específica. Somente a pessoa que cria uma política e o administrador podem acessar essa política pessoal. As políticas pessoais são exibidas na guia Minhas Políticas da página Políticas.

Os usuários convidados também poderão criar, editar, copiar e excluir políticas pessoais se o administrador ativar esse recurso.

**Políticas compartilhadas**

Os administradores e coordenadores de definições de políticas criam políticas compartilhadas com base nos requisitos de confidencialidade que sua organização identifica para diferentes tipos de documentos e usuários. As políticas compartilhadas estão contidas em conjuntos de políticas e estão disponíveis a todos os usuários autorizados (editores de documentos, coordenadores de definições de políticas e destinatários de documentos) para um conjunto de políticas específico. Os administradores e coordenadores de definições de políticas podem ativar e desativar políticas compartilhadas. As políticas compartilhadas aparecem nos conjuntos de políticas na guia Conjuntos de políticas da página Políticas.

Quando você instala a segurança de documentos pela primeira vez, ela contém uma política compartilhada, denominada *Restringir a todas as entidades de segurança*. Quando essa política é aplicada a um documento, qualquer usuário que possa fazer logon na segurança de documentos pode acessar o documento. Esta política está no conjunto de políticas denominado *Conjunto de Políticas Globais*. Por padrão, essa política não está ativada. Você pode ativá-lo se ele atender às necessidades de sua organização.

**Políticas geradas automaticamente pelo Microsoft® Outlook**

Usando o Acrobat, você pode aplicar políticas a documentos enviados como anexos de email no Microsoft® Outlook. No Outlook, você pode proteger um documento usando uma política existente. Ou você pode usar uma política gerada automaticamente que o Acrobat gera com configurações de confidencialidade padrão e se aplica ao documento anexado a uma mensagem de email. (Consulte a *[Ajuda do Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Para que uma política esteja disponível no Outlook, você deve defini-la como um favorito no Acrobat. Todas as outras políticas, incluindo aquelas em que você é o Editor, não são exibidas no Outlook.

## Quem pode criar e gerenciar políticas e conjuntos de políticas {#who-can-create-and-manage-policies-and-policy-sets}

A maneira como você interage com políticas e conjuntos de políticas depende da sua função na organização:

**Usuários:** Os usuários podem criar, editar e excluir suas políticas pessoais. Usuários convidados também podem criar políticas pessoais se o administrador habilitar esse recurso.

**Coordenadores de definições de políticas:** os coordenadores de definições de políticas podem criar e gerenciar políticas compartilhadas nos conjuntos de políticas em que são designados como coordenadores. Um coordenador de conjunto de políticas normalmente é um especialista na organização que pode criar melhor as políticas em um conjunto de políticas específico.

**Administradores:** Os administradores podem editar as políticas pessoais de qualquer usuário. Eles podem criar políticas compartilhadas. Eles também podem criar, editar e excluir conjuntos de políticas e designar coordenadores de definições de políticas.

Para obter detalhes sobre as várias funções de segurança de documentos, consulte [Sobre usuários da segurança de documentos](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Criação e edição de políticas {#creating-and-editing-policies}

Os usuários podem criar ou editar políticas pessoais para uso próprio. Os administradores e coordenadores de definições de políticas podem criar ou editar políticas compartilhadas para sua organização.

### Considerações para a edição de políticas {#considerations-for-editing-policies}

Quando você edita uma política, as alterações afetam documentos que a política protege atualmente e documentos que a política protege posteriormente. Por exemplo, se você remover destinatários de uma política aplicada a um documento, os destinatários não poderão mais abrir o documento.

O status do documento determina quando a alteração entra em vigor:

* Se o documento estiver on-line, as alterações serão aplicadas imediatamente, a menos que o usuário tenha o documento aberto. Nesse caso, o usuário deve fechar o documento para que as alterações entrem em vigor.
* Se um destinatário estiver usando o documento offline (por exemplo, em um laptop), as alterações entrarão em vigor na próxima vez que o destinatário colocar o documento online. Em seguida, ele é sincronizado com a segurança de documentos, abrindo qualquer documento protegido por política.

>[!NOTE]
>
>As políticas geradas automaticamente pelo Acrobat para os destinatários de documentos anexados a mensagens de email no Microsoft® Outlook não aparecem na lista de políticas. Você pode exibir essas políticas somente abrindo a página Detalhes do documento do documento associado.

Quando você edita políticas, estas restrições se aplicam:

* Os usuários convidados só poderão editar políticas se o administrador habilitar esse recurso. Se não for possível editar políticas, a opção Editar não estará disponível.
* Os coordenadores de definições de políticas podem editar políticas nos conjuntos de políticas somente se tiverem as permissões corretas. O superusuário ou o administrador do conjunto de políticas define essas permissões na interface do administrador da segurança de documentos.
* Se a política tiver uma marca d&#39;água configurada que o administrador excluiu desde que a política foi criada, essa marca d&#39;água não será mais aplicada aos documentos se você editar e salvar a política. As marcas d&#39;água excluídas permanecem em vigor somente para políticas existentes, desde que você não edite a política. Se você editar a política, deverá selecionar outra marca d&#39;água para substituir a excluída.
* Você não pode conceder acesso anônimo a um documento editando a política aplicada. Se você editar a política, os usuários ainda deverão fazer logon para acessar o documento. Para aplicar acesso anônimo a este documento, primeiro remova a política no aplicativo cliente e, em seguida, aplique outra política que permita acesso anônimo.
* As políticas geradas automaticamente pelo Acrobat para os destinatários de um documento anexado a uma mensagem de email no Microsoft Outlook não aparecem na lista de políticas. Para acessar essa política, localize o documento na página Documentos, abra a página Detalhes do documento e clique no nome da política na lista de detalhes do documento.

**Criar ou editar uma política**

1. Na página Segurança de documentos, clique em Políticas e clique em uma dessas guias:

   * Para criar ou editar uma regra pessoal, clique na guia Minha regra.
   * Para criar ou editar uma política compartilhada, se você tiver permissão, clique na guia Conjuntos de políticas, clique no nome apropriado do conjunto de políticas e, em seguida, clique na guia Políticas.

1. Clique em Novo ou selecione na lista a política que deseja editar.
1. Na caixa Nome, digite um nome que identifique exclusivamente a política. Na caixa Descrição, descreva o que a política faz e quando usá-la. Se a política estiver em um conjunto de políticas, o nome e a descrição serão exibidos na lista de políticas para todos os usuários especificados. As políticas pessoais estão disponíveis somente para o usuário e os administradores.

   Os caracteres a seguir não podem ser usados no nome ou na descrição:

   * sinal de menor que (&lt;)
   * sinal de maior que (>)
   * E comercial (&amp;)
   * aspas simples (&#39;)
   * aspas duplas (&quot;)
   * barra invertida (\)
   * barra (/)

   Se você usou o seguinte caractere no nome ou na descrição, eles serão convertidos em espaços:

   * retorno de carro (caractere ASCII 13)
   * nova linha (caractere ASCII 10).

   >[!NOTE]
   >
   >É possível criar um nome de política que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot;, são considerados iguais. Quando alguém cria uma política, é feita uma comparação para verificar se existe uma política com o mesmo nome. A comparação não pode distinguir entre nomes que são iguais, exceto para caracteres acentuados. Pressupõe-se que a política já esteja adicionada ao banco de dados e a nova não esteja adicionada.

1. Adicione usuários e grupos à política e defina as permissões apropriadas. (Consulte [Usuários e grupos](creating-policies.md#users-and-groups).)
1. Em Configurações gerais, selecione as opções apropriadas. (Consulte [Configurações Gerais](creating-policies.md#general-settings).)
1. (Opcional) Se aplicável, selecione um provedor de autorização externo e especifique suas propriedades. Se você não quiser usar um provedor de autorização externo, clique em Remover Provedor Padrão.

   Um provedor de autorização externo é usado para configurar propriedades na política e, quando selecionado, o provedor de autorização externo usa essas informações para avaliar a política. As propriedades disponíveis são configuradas pelo administrador e pela pessoa que instala o software.

1. Em Configurações avançadas, selecione as opções apropriadas. (Consulte [Configurações Avançadas](creating-policies.md#advanced-settings).)
1. Em Configurações avançadas inalteráveis, selecione as opções apropriadas. (Consulte [Configurações Avançadas Inalteráveis](creating-policies.md#unchangeable-advanced-settings).)
1. Clique em Salvar. A política aparece na lista de políticas. Um ícone com um círculo vermelho é exibido ao lado da nova política, indicando que ainda está desativado.

   Para disponibilizar a política para os usuários, ative-a. (Consulte [Habilitar ou desabilitar políticas compartilhadas](creating-policies.md#enable-or-disable-shared-policies).)

### Usuários e grupos {#users-and-groups}

Na área Usuários e grupos, especifique os usuários que têm acesso a documentos protegidos com a política. Para cada usuário ou grupo especificado, você também define os privilégios de uso do documento.

>[!NOTE]
>
>O editor do documento é o usuário que protege o documento com a política. Esse usuário é sempre incluído por padrão em uma política, com direitos de acesso totais, incluindo recursos de revogação e troca de políticas. No entanto, os administradores podem alterar os direitos de acesso do editor do documento para políticas compartilhadas. Por exemplo, o administrador pode restringir o editor de documentos de revogar o acesso aos documentos ou alternar a política.

**Adicionar Usuário ou Grupo:** Para adicionar um usuário ou grupo de usuários, clique em Adicionar Usuário ou Grupo e, em seguida, clique em Pesquisa Avançada para encontrar usuários ou grupos. Os usuários incluem os usuários internos da organização e os usuários convidados que se registraram com segurança de documentos. Quando você seleciona essa opção, a página Adicionar Usuário ou Grupo é exibida:

* Na caixa Localizar, digite o nome do usuário ou do grupo ou o endereço de email.
* Na lista Utilizando, selecione Nome ou Email.
* Na lista Tipo, selecione Usuário ou Grupo.
* Selecione o domínio que deseja pesquisar na lista Em e clique em Localizar.
* Quando os resultados forem retornados, selecione o usuário ou grupo a ser adicionado e clique em Adicionar.

>[!NOTE]
>
>Se você inserir um nome de usuário convidado ou endereço de email correto e nenhum resultado for retornado, o usuário pode ainda não ter se registrado ou a conta pode ser excluída. Você pode tentar adicionar o usuário como um tipo de usuário convidado ou entrar em contato com o administrador.

**Convidar novo usuário:** Para adicionar um usuário convidado, clique em Convidar novo usuário, digite o endereço de email do usuário na caixa exibida e clique em Convidar. Essa opção só estará disponível se tiver sido habilitada pelo administrador. Quando você adiciona novos usuários convidados a uma política, a segurança de documentos envia um email de convite de registro se os usuários ainda não tiverem sido convidados a se registrar. Os usuários devem usar o link no email para criar uma conta e, em seguida, devem ativar a conta.

Após o registro, os usuários convidados podem usar documentos protegidos por política para os quais têm autorização. Dependendo dos recursos ativados pelo administrador, os usuários externos podem ter permissão para aplicar políticas a documentos, criar, editar e excluir políticas e adicionar outros usuários externos às políticas.

**Adicionar usuário anônimo:** Para permitir acesso de usuário anônimo, clique em Adicionar usuário anônimo. Essa opção só estará disponível se o administrador tiver ativado o acesso de usuário anônimo para a segurança de documentos. (Consulte Configurar o servidor de segurança de documentos.) Essa opção concede a todos o acesso a documentos protegidos por essa política, independentemente de terem ou não uma conta de segurança de documentos. Se você selecionar essa opção, não poderá adicionar outros tipos de usuários à política.

>[!NOTE]
>
>Para permitir acesso anônimo a um documento protegido por política que não o possua no momento, remova a política existente e aplique uma política que permita acesso anônimo. Se você alternar ou alterar a política existente, os usuários ainda deverão fazer logon para acessar o documento.

#### Especificar as permissões de documento para usuários e grupos {#specify-the-document-permissions-for-users-and-groups}

Você pode especificar permissões de documento para um usuário ou grupo por vez ou pode selecionar vários usuários e grupos na lista e alterar suas permissões usando as opções na área de cabeçalhos de coluna.

Por padrão, todos os documentos protegidos por política têm uma permissão que permite que os usuários os abram enquanto estiverem online.

A guia Permissões e opções é exibida em Segurança do documento.

Essas permissões de documento estão disponíveis na guia Permissões. Você pode aplicar essas permissões aos arquivos PDF, PTC Pro/E e Microsoft Office.

**Imprimir:** permite que o usuário imprima um documento protegido por esta política. Para arquivos do Office e Pro/E, você pode marcar a caixa de seleção Imprimir para permitir a impressão ou desmarcá-la para impedir a impressão. Se você marcar a caixa de seleção Mostrar permissões personalizadas para PDF, será possível selecionar entre estas opções:

**Não permitido:** o usuário não tem permissão para imprimir o PDF.

**Permitido:** o usuário tem permissão para imprimir o PDF.

**Baixa resolução. somente:** usuário pode imprimir o PDF em baixa resolução.

**Modificar:** permite que o usuário modifique um documento protegido por esta política. Para arquivos do Office e Pro/E, você pode marcar a caixa de seleção Modificar para permitir modificações ou desmarcá-la para evitar modificações. Se você marcar a caixa de seleção Mostrar permissões personalizadas para PDF, será possível selecionar entre estas opções:

**Não permitido:** o usuário não tem permissão para modificar o PDF.

**Qualquer:** usuário pode modificar o PDF.

**Colaborar:** o usuário tem permissão para colaborar com outras pessoas usando as opções Colaborar no Adobe Acrobat. Essa permissão possibilita que o usuário copie dados de formulário mesmo que a permissão Copiar não seja explicitamente fornecida na política.

**Alterar páginas:** o usuário tem permissão para adicionar e remover páginas e editar conteúdo no PDF.

**Fill &amp; Sign:** usuário pode preencher campos de formulário no PDF e assiná-lo.

**Copiar:** permite que o usuário copie texto de um documento protegido por esta política.

**Reader de tela:** essa permissão será exibida se você marcar a caixa de seleção Mostrar Permissões Personalizadas para PDF. Quando essa opção é selecionada, a Adobe Acrobat tem permissão para adicionar tags temporárias ao PDF para melhorar sua legibilidade com um leitor de tela.

Essas permissões de documento estão disponíveis na guia Opções. Você pode aplicar essas permissões aos arquivos PDF, PTC Pro/E e Microsoft Office:

**Offline:** permite que o usuário exiba um documento offline protegido por esta política.

**Validade da Permissão:** Selecione Permissões São Sempre Válidas ou defina um período de validade de permissão de documento. Se você selecionar um período de validade, clique no ícone de calendário para selecionar uma data e usar as setas para especificar a hora no formato de 24 horas.

Para políticas compartilhadas, os administradores podem desativar os seguintes privilégios para o editor do documento (o usuário que aplica a política a um documento):

**Revogar:** Permite que o editor de documentos revogue privilégios de acesso a documentos.

**Alternar:** Permite que o fornecedor do documento alterne privilégios de diretiva.

### Configurações gerais {#general-settings}

A área Configurações gerais contém as seguintes configurações:

**Período de Validade:** O período durante o qual o documento protegido por política está acessível aos destinatários autorizados. Você pode escolher entre estas opções de período de validade:

**O documento não será válido após:** O documento fica acessível pelo número especificado de dias a partir de quando o documento foi protegido.

**O documento não será válido após esta data:** O documento é válido a partir da data em que a política é aplicada ao documento até a data final especificada.

**Válido de, a:** O documento é válido durante as datas especificadas. Você pode usar o calendário para selecionar uma data, onde aplicável, clicando no ícone do calendário.

**O documento é sempre válido:** O período de validade do documento não expira.

>[!NOTE]
>
>As datas de validade são baseadas no fuso horário do sistema de segurança de documentos, não no fuso horário do computador local.

**Auditoria:** habilite ou desabilite a auditoria dos eventos associados a um documento protegido por política. Por exemplo, a segurança de documentos pode registrar eventos como tentativas de abrir um documento. Os eventos auditados são exibidos na lista da página Eventos. Se você não selecionar essa opção, a segurança de documentos não registrará eventos para documentos associados à política.

>[!NOTE]
>
>O administrador também deve habilitar a auditoria do servidor na página de configuração Auditoria e Configurações de Privacidade para que o recurso de auditoria funcione.

**Rastreamento de Uso Estendido:** Habilite ou desabilite o Rastreamento de Uso Estendido. A segurança de documentos oferece suporte ao rastreamento de eventos de usuário associados a várias operações executadas em um arquivo PDF. O objeto de segurança do documento pode ser acessado usando um Java Script. Um clique de botão, um arquivo multimídia que está sendo reproduzido ou o salvamento de um arquivo são alguns exemplos de eventos que são acionados a partir de um PDF protegido por política. Usando o objeto de segurança de documentos, você também pode recuperar informações do usuário. O rastreamento de eventos pode ser ativado no servidor de segurança de documentos em nível global ou em nível de política.

**Período de Concessão Offline Automático:** O número máximo de dias que o destinatário pode usar o documento protegido por política offline (sem uma conexão ativa com a Internet ou com a rede). Quando o período de concessão expirar, o recipient deverá sincronizar o documento novamente para continuar a usá-lo.

### Provedores de autorização externos {#external-authorization-providers}

Selecione os provedores de autenticação externa se você já tiver configurado algum. Os provedores disponíveis estão listados.

### Configurações da autenticação {#authentication-settings}

Você pode substituir as configurações de autenticação configuradas no servidor e especificar as opções de autenticação relevantes para esta política. Selecione Substituir configurações de autenticação global e, em seguida, selecione as opções de autenticação relevantes para esta política. As seguintes opções de autenticação estão disponíveis:

**Permitir Autenticação de Senha de Nome de Usuário:** selecione esta opção se desejar habilitar os aplicativos cliente para usar autenticação de nome de usuário/senha ao se conectar ao servidor.

**Permitir Autenticação Kerberos:** selecione esta opção se desejar permitir que os aplicativos clientes usem a autenticação Kerberos ao se conectarem ao servidor.

**Permitir Autenticação de Certificado de Cliente:** selecione esta opção se desejar habilitar os aplicativos cliente para usar autenticação de certificado ao se conectar ao servidor.

**Permitir Autenticação Estendida** Selecione para habilitar a autenticação estendida. A seleção dessa opção permite que os aplicativos clientes usem autenticação estendida. A autenticação estendida fornece processos de autenticação personalizados e diferentes opções de autenticação configuradas no servidor de Segurança de documentos

Se você estiver substituindo as configurações de autenticação global, poderá escolher as opções de autenticação relevantes para esta política. Por exemplo, se você ativou três opções de autenticação (nome de usuário e senha, certificado do cliente e autenticação estendida) no servidor, é possível substituir essa configuração global e selecionar apenas a autenticação estendida para essa política. Verifique se a opção de autenticação selecionada aqui já está configurada no servidor. Neste exemplo, não é possível selecionar Kerberos como a opção de autenticação porque ele não está configurado no servidor.

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

### Configurações avançadas {#advanced-settings}

A área Configurações avançadas contém as seguintes configurações:

**Marca d&#39;água Dinâmica:** selecione uma marca d&#39;água a ser exibida dinamicamente nas páginas de um documento (por exemplo, quando um destinatário imprime o documento). As marcas d&#39;água dinâmicas identificam exclusivamente um documento, ajudando assim a garantir a confidencialidade do documento e evitando a violação de direitos autorais. Por exemplo, o administrador pode configurar uma marca d&#39;água dinâmica que exibe a data atual, o nome de usuário ou o identificador da pessoa que está usando o documento. Ou o nome da política usada para proteger o documento. Uma marca d&#39;água também pode exibir texto personalizado ou elementos gráficos, se configurado. Os administradores configuram as opções de marca d&#39;água e os administradores e usuários podem aplicá-las às políticas.

(Consulte [Configurar marcas d&#39;água dinâmicas](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Se você estiver editando uma política e o administrador tiver deletado uma marca d&#39;água configurada que você selecionou anteriormente para essa política, uma observação será exibida na página Editar Política. Nesse caso, se você estiver salvando o documento editado, selecione uma nova marca d&#39;água se desejar que uma apareça no documento.

>[!NOTE]
>
>Para políticas que fornecem acesso anônimo ao usuário, o nome do usuário e o identificador de um usuário anônimo não são exibidos como uma marca d&#39;água mesmo se você selecionar esse tipo de marca d&#39;água.

**Usar Somente Plug-ins Certificados do Acrobat para PDF:** Quando selecionada para uma política, esta opção especifica que o Acrobat 8.0 e posterior deve ser executado no modo certificado ao abrir documentos protegidos com a política. Quando o Acrobat é executado no modo certificado, ele não carrega plug-ins de terceiros.

Selecione essa opção se estiver preocupado com a gravação de plug-in por um recipient de documento que pode contornar qualquer proteção de documento no Acrobat 8.0 e posteriores. Não selecione essa opção se os recipients do seu documento precisarem usar plug-ins de terceiros no Acrobat para interagir com documentos.

Essa opção ativa somente o modo certificado no Acrobat 8.0 ou posterior; o administrador deve desativar o acesso para o Acrobat 7.0.

(Consulte [Configurar o servidor de segurança de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Essa opção não se aplica ao Adobe Reader.

**Mensagem de Erro de Acesso Negado:** Uma mensagem que aparece para qualquer pessoa que tenta abrir um documento protegido por política sem permissão. Esta mensagem é exibida no Acrobat. Os clientes que não puderem exibir essa mensagem exibirão uma mensagem padrão para indicar que o acesso foi negado.

### Configurações avançadas inalteráveis {#unchangeable-advanced-settings}

A área Configurações avançadas inalteráveis contém as seguintes configurações. Não é possível alterar essas configurações após salvar a política.

**Algoritmo de Criptografia e Tamanho da Chave:** Usado para proteger seus documentos. Você pode escolher entre estas opções:

* AES de 128 bits
* AES de 256 bits. Somente o Acrobat 9.0 e posterior é compatível com essa opção. Para usar a criptografia AES 256 para arquivos PDF, obtenha e instale os arquivos de Política de Jurisdição de Força Ilimitada Java Cryptography Extension (JCE). Esses arquivos substituem os arquivos local_policy.jar e US_export_policy.jar na [pasta JAVE_HOME]/lib/security. Por exemplo, se você estiver usando o Sun JDK 1.6, copie os arquivos baixados para a pasta [dep root]/Java/jdk1.6.0_26/lib/security. Você pode baixar esses arquivos em [Downloads do Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Sem criptografia. Atualmente, o Acrobat 9.0 e versões posteriores oferecem suporte a essa opção. Se você selecionar essa opção, as opções de Restrições de documento serão desativadas. Essa opção pode ser útil se você quiser usar a segurança de documentos para auditoria de documentos ou controle de versão, mas não quiser criptografar o documento.

**Restrições de Documento:** Selecione os componentes do documento de PDF a serem criptografados. Outros aplicativos clientes criptografam todo o documento, mas não os arquivos vinculados ou incorporados. Você pode escolher entre estas opções:

* O documento inteiro, incluindo anexos e metadados. *Metadados* são informações sobre o documento e seu conteúdo que podem ser exibidas na caixa de diálogo Propriedades do documento ou no menu Avançado do Acrobat. No Acrobat, é possível anexar arquivos de diferentes tipos (por exemplo, arquivos de texto, áudio e vídeo) a documentos PDF.
* O documento e seus anexos, mas não os metadados.
* Somente os anexos do documento. Você pode criptografar os anexos para um arquivo PDF sem criptografar o conteúdo do documento.

## Habilitar ou desabilitar políticas compartilhadas {#enable-or-disable-shared-policies}

Para disponibilizar uma política compartilhada, o administrador ou o coordenador de definições de políticas deve ativá-la. Você pode ativar novas políticas ou políticas desativadas anteriormente. Uma política compartilhada que você desativa ainda é imposta para documentos que estão protegidos com essa política.

Um X vermelho é exibido ao lado de uma política desativada.

>[!NOTE]
>
>Os administradores não podem desativar políticas pessoais e os usuários não podem ativar e desativar suas próprias políticas.

1. Na página Segurança de documentos, clique em Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Clique no nome do conjunto de políticas apropriado e clique na guia Políticas.
1. Marque a caixa de seleção ao lado da política apropriada, clique em Ativar ou Desativar e, em seguida, clique em OK.

## Exibir informações sobre uma política {#view-information-about-a-policy}

Usando a guia Minhas políticas, você pode pesquisar políticas pessoais.

Os conjuntos de políticas criados pelos administradores são listados na guia Conjuntos de Políticas da página Políticas. Eles contêm informações sobre o conjunto de políticas, incluindo seu nome, a data de criação e modificação e uma descrição. Clique no nome de um conjunto de políticas para ver os detalhes. Os coordenadores de definições de políticas que têm permissão para gerenciar políticas podem criar políticas compartilhadas em um conjunto de políticas específico.

Quando você cria ou edita uma política, é exibida uma página onde é possível configurar o nome da política, os níveis de permissão, as configurações de confidencialidade e os destinatários a serem incluídos na política.

O administrador pode definir as seguintes configurações de confidencialidade para uma política:

* Opções gerais de confidencialidade de documentos, como o período de validade do documento e o período de concessão offline
* Os usuários autorizados e as restrições e privilégios de documento para cada um desses usuários
* Opções avançadas de confidencialidade de documentos, incluindo marcas d&#39;água dinâmicas e criptografia de documentos

Os usuários podem visualizar as políticas que criaram e quaisquer políticas compartilhadas às quais tenham acesso. Os administradores podem exibir todas as políticas pessoais e compartilhadas que estão na segurança de documentos.

Você pode exibir informações mais detalhadas sobre uma política que aparece na lista, incluindo os usuários ou grupos incluídos na política e as configurações de confidencialidade especificadas para esses usuários.

>[!NOTE]
>
>As políticas geradas automaticamente pelo Acrobat para os destinatários de documentos anexados a mensagens de email no Microsoft Outlook não aparecem na lista de políticas. Você pode exibir essas políticas somente abrindo a página Detalhes do documento do documento associado.

1. Na página Segurança de documentos, clique em Políticas e, em seguida, clique na guia Minhas políticas.
1. Preencha as informações de pesquisa para poder pesquisar por políticas pessoais.
1. Selecione a política apropriada na lista.
1. Na página Detalhes da política, você pode ver detalhes sobre a política, editar a política ou exibir eventos relacionados à política.

## Pesquisar por políticas {#search-for-policies}

Os administradores podem pesquisar por políticas compartilhadas e por políticas pessoais que foram criadas por outros usuários.

1. Para pesquisar uma política compartilhada, clique em Políticas e, em seguida, clique na guia Conjuntos de políticas. Clique em um conjunto de políticas na lista e, em seguida, clique na guia Políticas.

   Para pesquisar uma política pessoal, na página de segurança de documentos, clique em Políticas e, em seguida, clique na guia Minhas Políticas.

1. Na lista Localizar, selecione uma destas opções:

   **ID da Política:** o número de identificação da política gerado quando o usuário cria a política. Digite a ID exata da política.

   **Nome da Política:** O nome da política. Você pode pesquisar parte do nome da política ou todo ele.

1. Na caixa de texto, digite o valor correspondente. Por exemplo, se você selecionou Nome da política, digite o nome da política que você está procurando.
1. Na lista Exibir, selecione o número de resultados a serem exibidos e clique em Localizar. Os resultados da pesquisa são exibidos.
1. (Opcional) Para exibir detalhes da política, clique na política.

## Copiar uma política {#copy-a-policy}

Você pode copiar uma política existente e salvá-la com um novo nome e descrição. Copiar políticas é uma maneira eficiente de criar políticas usando as configurações existentes.

Usuários externos podem copiar políticas somente se o administrador habilitar esse recurso. Se não for possível criar políticas, a opção Copiar não estará disponível.

1. Na página Segurança de documentos, clique em Políticas e, em seguida, clique na guia Minha política.
1. Selecione a política apropriada na lista.
1. Na página Detalhes da política, clique em Copiar.
1. Na caixa Nome da nova política, digite o nome da nova política. Opcionalmente, digite uma nova Descrição.

   Os caracteres a seguir não podem ser usados no nome ou na descrição:

   * sinal de menor que (&lt;)
   * sinal de maior que (>)
   * E comercial (&amp;)
   * aspas simples (&#39;)
   * aspas duplas (&quot;)
   * barra invertida (\)
   * barra (/)

   Se você usou o seguinte caractere no nome ou na descrição, eles serão convertidos em espaços:

   * retorno de carro (caractere ASCII 13)
   * nova linha (caractere ASCII 10).

   >[!NOTE]
   >
   >É possível criar um nome de política que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot;, são considerados iguais. Quando alguém cria uma política, é feita uma comparação para verificar se existe uma política com o mesmo nome. A comparação não pode distinguir entre nomes que são iguais, exceto para caracteres acentuados. Pressupõe-se que a política já esteja adicionada ao banco de dados e a nova não esteja adicionada.

1. Clique em OK.

## Excluir uma política {#delete-a-policy}

É possível excluir políticas que você criou. Os administradores podem excluir políticas que qualquer usuário criou. Os coordenadores de definições de políticas podem excluir políticas em seus conjuntos de políticas. Uma política que você exclui ainda é imposta para documentos protegidos com essa política. É possível excluir mais de uma política de cada vez.

Os usuários convidados só poderão excluir políticas se o administrador habilitar esse recurso. Se não for possível excluir políticas, a opção de exclusão não estará disponível.

1. Na página Segurança de documentos, clique em Políticas.
1. Clique na guia Minha política.
1. Para excluir uma política compartilhada, clique na guia Conjuntos de políticas e clique no nome apropriado do conjunto de políticas.
1. Marque a caixa de seleção ao lado da política apropriada e clique em Excluir e, em seguida, clique em OK.

>[!NOTE]
>
>Use o aplicativo cliente para remover políticas de documentos. (Consulte a Ajuda do Acrobat ou a Ajuda das extensões adequadas do Acrobat Reader DC.)

## Classificar a lista de políticas {#sort-the-policy-list}

Você pode classificar a lista de políticas por cabeçalho de coluna para encontrar políticas mais facilmente. Um ícone de triângulo ao lado do cabeçalho da coluna indica qual coluna está sendo usada no momento para classificação. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Na página Segurança de documentos, clique em Políticas e clique na guia Conjunto de políticas.
1. Selecione um conjunto de políticas e clique na guia Políticas.
1. Clique no cabeçalho de coluna apropriado.
1. Para alterar a ordem de classificação, clique na coluna novamente.
