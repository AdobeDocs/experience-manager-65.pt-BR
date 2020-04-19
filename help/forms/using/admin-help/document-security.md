---
title: 'Sobre a segurança do documento '
seo-title: 'Sobre a segurança do documento '
description: Saiba como criar, armazenar e aplicar configurações de confidencialidade predefinidas e distribuir suas informações com segurança usando a segurança do documento.
seo-description: Saiba como criar, armazenar e aplicar configurações de confidencialidade predefinidas e distribuir suas informações com segurança usando a segurança do documento.
uuid: e4fba2a4-f3c1-4b20-8e05-8e241b40ebd0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1820cb38-ba70-4cce-8895-290524bdd9bf
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Sobre a segurança do documento {#about-document-security}

A segurança do Documento garante que somente usuários autorizados possam usar seus documentos. Usando a segurança do documento, é possível distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem:

* Arquivos Adobe PDF
* Arquivos do Microsoft® Word, Excel e PowerPoint

Para obter mais informações sobre como as políticas protegem os tipos de arquivos suportados, consulte Informações [](https://www.adobe.com/go/learn_aemforms_doc_security_63)adicionais de segurança do documento.

Usando a segurança do documento, você pode criar, armazenar e aplicar facilmente configurações de confidencialidade predefinidas a seus documentos. Para evitar que as informações se espalhem além do seu alcance, você também pode monitorar e controlar como os recipient usam seus documentos depois de distribuí-los.

É possível proteger documentos usando políticas. Uma *política* é uma coleção de informações que inclui configurações de confidencialidade e uma lista de usuários autorizados. As configurações de confidencialidade especificadas em uma política determinam como um recipient pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os recipient podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

Os usuários de segurança do Documento criam políticas por meio das páginas da Web do usuário final. Os administradores usam as páginas da Web de segurança do documento para criar conjuntos de políticas que contêm políticas compartilhadas disponíveis para todos os usuários autorizados.

Embora as políticas sejam armazenadas na segurança do documento, você as aplica a documentos por meio do aplicativo cliente. Como aplicar políticas a documentos PDF é descrito detalhadamente na Ajuda *do* Acrobat. A aplicação de políticas usando outros aplicativos, como o Microsoft Office, está documentada na Ajuda *das extensões do* Acrobat Reader DC para o aplicativo.

Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. As configurações de confidencialidade também protegem quaisquer arquivos (texto, áudio ou vídeo) dentro de um documento PDF. É possível distribuir o documento protegido por política para recipient autorizados pela política.

**Documento e auditoria**

Usar uma política para proteger um documento dá a você controle contínuo sobre esse documento, mesmo depois de distribuí-lo. Você pode monitorar o documento, fazer alterações na política, impedir que os usuários continuem acessando o documento e alterar a política aplicada ao documento.

Por meio da segurança do documento, você pode monitorar documentos protegidos por política e rastrear eventos, como quando um usuário autorizado ou não-autorizado tenta abrir o documento.

**Componentes**

A segurança do Documento consiste em uma interface do servidor e do usuário:

**Servidor:** O componente central através do qual a segurança do documento realiza transações como autenticação do usuário, gerenciamento em tempo real de políticas e aplicação de confidencialidade. O servidor também fornece um repositório central para políticas, registros de auditoria e outras informações relacionadas.

**Páginas da Web:** A interface onde você cria políticas, gerencia seus documentos protegidos por política e monitora eventos associados a documentos protegidos por política. Os administradores também podem configurar opções globais, como autenticação de usuário, auditoria e mensagens para usuários convidados, e gerenciar contas de usuários convidados.

![rm_psworkflow](assets/rm_psworkflow.png)

As etapas na ilustração são as seguintes:

1. O proprietário do documento cria políticas usando as páginas da Web. Os proprietários de Documentos podem criar políticas pessoais que só podem ser acessadas por eles. Os administradores e os coordenadores de definição de política podem criar políticas compartilhadas em conjuntos de políticas acessíveis aos usuários autorizados.
1. O proprietário do documento aplica a política e, em seguida, salva e distribui o documento. O documento pode ser distribuído por email, por uma pasta de rede ou em um site.
1. O recipient abre o documento no aplicativo cliente apropriado. O recipient pode usar o documento de acordo com sua política.
1. O proprietário do documento, o coordenador do conjunto de políticas ou o administrador pode rastrear documentos e modificar o acesso a eles usando as páginas da Web.

## Sobre usuários de segurança do documento {#about-document-security-users}

Vários tipos de usuários trabalham com segurança de documento para realizar tarefas diferentes:

* O administrador do sistema ou outra pessoa do IS (Information System, sistema de informações) instala e configura a segurança do documento. Essa pessoa também pode ser responsável por definir configurações globais para o servidor, páginas da Web e políticas e documentos.

   Essas configurações podem incluir, por exemplo, um URL de segurança de documento básico, notificações de auditoria e privacidade, avisos de registro de usuário convidados e períodos padrão de empréstimo offline.

* Os administradores de segurança do Documento criam políticas e conjuntos de políticas e gerenciam documentos protegidos por política para usuários, conforme necessário. Eles também criam contas de usuários convidados e monitoram sistemas, documentos, usuários, políticas, conjuntos de políticas e eventos personalizados. Eles também podem ser responsáveis pela configuração do servidor global, da página da Web e das configurações de política em conjunto com um administrador do sistema.

   Os administradores podem atribuir aos usuários as seguintes funções na área Gerenciamento de usuários do console de administração. Os usuários aos quais essas funções são atribuídas executam suas tarefas na área da interface de usuário de segurança do documento do console de administração.

   **Superadministrador de segurança do Documento**

   Os usuários com essa função têm acesso a todas as configurações de segurança do documento no console de administração. Essas permissões estão associadas à função:

   * Gerenciar configuração
   * Gerenciar política
   * Gerenciar conjuntos de políticas
   * Gerenciar documentos
   * Gerenciar editores de documentos
   * Gerenciar usuários convidados e locais
   * eventos Visualizações
   * Delegar
   * Convidar usuários externos
   **Administrador de segurança do Documento**

   Os usuários com essa função podem configurar o servidor de segurança do documento, usando a página Configuração na seção de segurança do documento do console de administração. Essa permissão está associada à função Gerenciar configuração.

   >[!NOTE]
   >
   >Os usuários com essa função também devem ter a função Usuário do console de administração para poder fazer logon no console de administração e editar qualquer configuração relacionada.

   **administrador do conjunto de políticas de segurança do Documento**

   Os usuários com essa função podem usar a seção de segurança do documento do console de administração para editar as políticas de outros usuários e para criar, editar e excluir conjuntos de políticas. Quando um administrador de conjunto de políticas cria um conjunto de políticas, ele pode atribuir um coordenador de conjunto de políticas a esse conjunto de políticas. Essas permissões estão associadas à função:

   * Gerenciar política
   * Gerenciar conjuntos de políticas
   * Gerenciar documentos
   * Gerenciar editores de documentos
   * eventos Visualizações
   * Delegar
   >[!NOTE]
   >
   >Os usuários com essa função também devem ter a função Usuário do console de administração para poder fazer logon no console de administração e editar qualquer configuração relacionada.

   **Usuários convidados e locais gerenciam a segurança do Documento**

   Os usuários com essa função podem executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas da Web relevantes de segurança do documento. Essas permissões estão associadas à função:

   * Gerenciar usuários convidados e locais
   * Convidar usuários externos
   * Acessar páginas da Web de usuários finais
   >[!NOTE]
   >
   >Os usuários com essa função também devem ter a função Usuário do console de administração para poder fazer logon no console de administração e editar qualquer configuração relacionada.

   **usuário convidado de segurança do Documento**

   Os usuários com essa função podem convidar usuários. Essas permissões estão associadas à função:

   * Convidar usuários externos
   * Acessar páginas da Web de usuários finais
   **Usuário final de segurança do Documento**

   Os usuários com essa função podem acessar as páginas da Web de usuários finais de segurança do documento. Essa função também pode ser atribuída aos administradores para permitir que eles criem políticas usando as páginas de usuário final. Essa permissão está associada à função Acessar páginas da Web de usuários finais.

* Os usuários na organização que têm contas de segurança de documento válidas criam suas próprias políticas, usam políticas para proteger documentos, rastreiam e gerenciam documentos protegidos por política e monitoram eventos relacionados a seus documentos.
* Os coordenadores de definição de política gerenciam documentos, eventos de visualização e outros coordenadores de definição de política (com base em suas permissões). Os administradores designam usuários como coordenadores de conjunto de políticas para conjuntos de políticas específicos.
* Os usuários externos à sua organização (por exemplo, um parceiro comercial) podem usar documentos protegidos por política se estiverem no diretório de segurança do documento de segurança do documento, se o administrador criar uma conta para eles ou se se registrarem com segurança do documento por meio de um processo de convite por email automatizado. Dependendo de como o administrador habilita as configurações de acesso, os usuários convidados também podem ter permissão para aplicar políticas a documentos, criar, modificar e excluir suas políticas e convidar outros usuários externos a usar seus documentos protegidos por política.
* Os desenvolvedores usam o SDK de formulários AEM para integrar aplicativos personalizados à segurança do documento.

Os administradores de segurança do Documento podem criar funções personalizadas usando as seguintes permissões no Gerenciamento de usuários:

* Configuração do gerenciador de segurança do Documento
* Usuários convidados e locais do Documento security Manage
* Conjuntos de políticas de gerenciamento de segurança do Documento
* Conjuntos de políticas de gerenciamento de segurança do Documento
* Eventos do servidor de Visualização de segurança do Documento
* Proprietário da Política de Alteração de Segurança do Documento

## Políticas e documentos protegidos por política {#policies-and-policy-protected-documents}

Uma *política* define um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Uma política também permite que as permissões em um documento sejam alteradas dinamicamente. Ele concede à pessoa que protege o documento permissão para alterar as configurações de confidencialidade para revogar o acesso ao documento ou para alterar a política.

A proteção por política pode ser aplicada a um documento PDF usando o Adobe Acrobat® Pro e o Acrobat Standard. A proteção por política pode ser aplicada a outros tipos de arquivos, como Microsoft Word, Excel e PowerPoint, usando o aplicativo cliente com as extensões apropriadas do Acrobat Reader DC instaladas.

### Como as políticas funcionam {#how-policies-work}

As políticas contêm informações sobre os usuários autorizados e as configurações de confidencialidade a serem aplicadas aos documentos. Os usuários podem ser qualquer pessoa em sua organização, assim como pessoas externas à sua organização que tenham uma conta. Se o administrador ativar o recurso de convite do usuário, será possível adicionar novos usuários às políticas, iniciando, portanto, um processo de convite de registro por email.

As configurações de confidencialidade em uma política determinam como os recipient podem usar o documento. Por exemplo, você pode especificar se os recipient podem imprimir ou copiar texto, fazer alterações ou adicionar assinaturas e comentários a documentos protegidos. A mesma política também pode especificar configurações de confidencialidade diferentes para usuários específicos.

>[!NOTE]
>
>As configurações de confidencialidade aplicadas por meio de uma política substituem quaisquer configurações que possam ter sido aplicadas a um documento PDF no Acrobat usando as opções de segurança de senha ou certificado. (Consulte a Ajuda do Acrobat para obter mais informações.)

Os usuários e administradores criam políticas por meio das páginas da Web de segurança do documento. Somente uma política de cada vez pode ser aplicada a um documento. É possível aplicar uma política usando um destes métodos:

* Abra o documento no Acrobat ou em outro aplicativo cliente e selecione uma política para proteger o documento.
* Envie um documento como anexo de email no Microsoft Outlook. Nesse caso, você pode selecionar uma política de uma lista de políticas ou selecionar uma política gerada automaticamente que o Acrobat crie com um conjunto padrão de configurações de confidencialidade para proteger o documento somente para os recipient de mensagem de email.

Uma política pode ser removida de um documento usando o aplicativo cliente.

![rm_psonline_policy](assets/rm_psonline_policy.png)

As etapas no diagrama são as seguintes:

1. O proprietário do documento protege o documento de um aplicativo cliente suportado com uma política que permite o uso on-line.
1. A segurança do Documento cria uma licença do documento e chaves do documento, além de criptografar a política. A licença do documento, a política criptografada e a chave do documento são retornadas ao aplicativo cliente.
1. O documento é criptografado com a chave do documento e a chave do documento é descartada. O documento agora incorpora a licença e a política. Essas tarefas são executadas no aplicativo cliente suportado.

Quando você aplica uma política a um documento, as informações que o documento contém, incluindo quaisquer arquivos contidos (texto, áudio ou vídeo) em documentos PDF, são protegidas pelas configurações de confidencialidade especificadas na política. A segurança do Documento gera informações de licença e criptografia que são incorporadas ao documento. Quando você distribui o documento, a segurança do documento pode autenticar os recipient que tentam abrir o documento e autorizar o acesso de acordo com os privilégios especificados na política.

Se o uso offline estiver ativado, os recipient também poderão usar documentos offline protegidos por política (sem uma conexão ativa com a Internet ou a rede) pelo período especificado na política.

### Como funcionam os documentos protegidos por política {#how-policy-protected-documents-work}

Para abrir e usar documentos protegidos por política, a política deve incluir seu nome como um recipient e você deve ter uma conta de segurança de documento válida. Para documentos PDF, você precisa do Acrobat ou do Adobe Reader®. Para outros tipos de arquivos, é necessário o aplicativo apropriado para o arquivo com as extensões do Acrobat Reader DC instaladas.

Quando você tenta abrir um documento protegido por política, o Acrobat, o Adobe Reader ou as extensões do Acrobat Reader DC se conectam à segurança do documento para autenticá-lo. Em seguida, você pode continuar a fazer logon. Se o uso do documento estiver sendo auditado, uma mensagem de notificação será exibida. Depois que a segurança do documento determinar quais permissões de documento conceder, ele gerenciará a descriptografia do documento. Em seguida, você pode usar o documento de acordo com as configurações de confidencialidade da política.

![rm_psopen_online](assets/rm_psopen_online.png)

As etapas no diagrama são as seguintes:

1. O usuário do documento abre o documento em um aplicativo cliente suportado e é autenticado no servidor. O identificador do documento é enviado para o servidor de segurança do documento.
1. A segurança do Documento autentica os usuários, verifica a política para obter autorização e cria um comprovante. O comprovante (que contém a chave do documento e as permissões) é retornado ao aplicativo cliente.
1. O documento é descriptografado com a chave do documento e a chave do documento é descartada. O documento pode então ser usado de acordo com as configurações de confidencialidade da política. Essas tarefas são executadas no aplicativo cliente suportado.

Você pode continuar usando um documento sob estas condições:

* Indefinidamente ou pelo período de validade especificado na política
* Até que o administrador ou a pessoa que aplicou a política revogue o acesso ao documento ou altere a política

Você também pode usar documentos offline protegidos por política (sem uma conexão com a Internet ou com a rede) se a política permitir o acesso offline. Primeiro, você deve fazer logon na segurança do documento para sincronizar o documento. Você pode usar o documento pela duração do período de empréstimo offline especificado na política.

Quando o período de empréstimo offline terminar, você deverá sincronizar o documento com a segurança do documento novamente, entrando online e abrindo um documento protegido por política ou usando um comando no aplicativo cliente. (Consulte a Ajuda *do* Acrobat ou a Ajuda *das extensões apropriadas do* Acrobat Reader DC para obter detalhes.)

Se você salvar uma cópia de um documento protegido por política usando o comando de menu Salvar ou Salvar como, a política será automaticamente aplicada e imposta para o novo documento. Eventos como tentativas de abrir o novo documento também são auditados e registrados para o documento original.

## Conjuntos de políticas {#policy-sets}

*Os conjuntos* de políticas são usados para agrupar um conjunto de políticas que têm um objetivo comercial comum. Esses conjuntos de políticas são disponibilizados para um subconjunto de usuários no sistema.

Cada conjunto de políticas pode ter um ou mais coordenadores de conjunto de políticas associados. O coordenador do conjunto de políticas é um administrador ou um usuário com permissões adicionais. O coordenador *do conjunto de* políticas é tipicamente um especialista na organização que pode melhor criar as políticas num conjunto de políticas específico.

Os coordenadores de conjuntos de políticas podem executar estas tarefas:

* Criar novas políticas
* Editar e excluir qualquer política no conjunto de políticas
* Editar configurações de conjunto de políticas
* Adicionar e remover coordenadores de conjunto de políticas
* Política de Visualização e eventos de documento para qualquer política ou documento dentro do conjunto de políticas
* Revogar acesso a documentos
* Alternar políticas para o documento.

Os conjuntos de políticas são criados e excluídos nas páginas da Web de administração de segurança do documento pelos administradores e coordenadores de conjuntos de políticas que têm permissão para isso.

Os conjuntos de políticas geralmente são disponibilizados a um número limitado de usuários, especificando quais usuários ou grupos dentro de um domínio podem usar as políticas do conjunto de políticas para proteger documentos.

Quando a segurança do documento é instalada, um conjunto de políticas padrão é criado chamado Conjunto *de Políticas* Globais. O administrador que instalou o software gerencia esse conjunto de políticas.
