---
title: O que é segurança de documentos?
description: Saiba como criar, armazenar e aplicar configurações de confidencialidade predefinidas e distribuir suas informações com segurança usando a segurança de documentos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: 0cdc9ee3-0172-43be-9b62-ed768534c074
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '3219'
ht-degree: 0%

---

# Sobre a segurança de documentos {#about-document-security}

A segurança de documentos garante que somente usuários autorizados possam usar seus documentos. Com a segurança de documentos, você pode distribuir com segurança qualquer informação que tenha sido salva em um formato compatível. Os formatos de arquivo compatíveis incluem:

* Arquivos do Adobe PDF
* Arquivos do Microsoft® Word, Excel e PowerPoint

Para obter mais informações sobre como as políticas protegem os tipos de arquivos compatíveis, consulte [mais informações de segurança de documentos](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-security/document-security-offerings.html?lang=en).

Usando a segurança de documentos, você pode criar, armazenar e aplicar facilmente configurações de confidencialidade predefinidas a seus documentos. Para evitar que as informações se espalhem além do seu alcance, você também pode monitorar e controlar como os recipients usam seus documentos depois de distribuí-los.

Você pode proteger documentos usando políticas. Uma *política* é uma coleção de informações que inclui configurações de confidencialidade e uma lista de usuários autorizados. As configurações de confidencialidade especificadas em uma política determinam como um destinatário pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

Os usuários da segurança de documentos criam políticas por meio das páginas da Web do usuário final. Os administradores usam as páginas da Web de segurança de documentos para criar conjuntos de políticas que contenham políticas compartilhadas disponíveis para todos os usuários autorizados.

Embora as políticas sejam armazenadas na segurança de documentos, elas podem ser aplicadas a documentos por meio do aplicativo cliente. Como aplicar políticas a documentos do PDF é descrito detalhadamente em *Ajuda do Acrobat*. A aplicação de políticas usando outros aplicativos, como o Microsoft® Office, está documentada na *Ajuda das extensões do Acrobat Reader DC* para o aplicativo.

Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações contidas no documento. As configurações de confidencialidade também protegem todos os arquivos (texto, áudio ou vídeo) de um documento PDF. Você pode distribuir o documento protegido por política para recipients autorizados pela política.

**Auditoria e controle de acesso a documentos**

Usar uma política para proteger um documento oferece controle contínuo sobre esse documento, mesmo depois de distribuí-lo. Você pode monitorar o documento, alterar a política, impedir que os usuários continuem acessando o documento e alternar a política aplicada ao documento.

Por meio da segurança de documentos, é possível monitorar documentos protegidos por política e rastrear eventos, como quando um usuário autorizado ou não autorizado tenta abrir o documento.

**Componentes**

A segurança de documentos consiste em um servidor e uma interface de usuário:

**Servidor:** O componente central por meio do qual a segurança de documentos realiza transações, como autenticação de usuários, gerenciamento de políticas em tempo real e aplicação de confidencialidade. O servidor também fornece um repositório central para políticas, registros de auditoria e outras informações relacionadas.

**Páginas da Web:** A interface em que você cria políticas, gerencia documentos protegidos por política e monitora eventos associados a documentos protegidos por política. Os administradores também podem configurar opções globais, como autenticação de usuário, auditoria e mensagens para usuários convidados, e gerenciar contas de usuários convidados.

![rm_psworkflow](assets/rm_psworkflow.png)

As etapas na ilustração são as seguintes:

1. O proprietário do documento cria políticas usando as páginas da Web. Os proprietários de documentos podem criar políticas pessoais acessíveis apenas para eles. Os administradores e coordenadores de definições de políticas podem criar políticas compartilhadas em conjuntos de políticas acessíveis a usuários autorizados.
1. O proprietário do documento aplica a política, salva e distribui o documento. O documento pode ser distribuído por email, por uma pasta de rede ou em um site.
1. O recipient abre o documento no aplicativo cliente apropriado. O recipient pode usar o documento de acordo com sua política.
1. O proprietário do documento, o coordenador do conjunto de políticas ou o administrador podem rastrear documentos e modificar o acesso a eles usando as páginas da Web.

## Sobre usuários de segurança de documentos {#about-document-security-users}

Vários tipos de usuários trabalham com segurança de documentos para realizar tarefas diferentes:

* O administrador do sistema ou outra pessoa do sistema de informações (IS) instala e configura a segurança de documentos. Essa pessoa também pode ser responsável por definir configurações globais para o servidor, páginas da Web, políticas e documentos.

  Essas configurações podem incluir, por exemplo, um URL de segurança do documento base, notificações de auditoria e privacidade, avisos de registro de usuário convidado e períodos de concessão offline padrão.

* Os administradores de segurança de documentos criam políticas e conjuntos de políticas e gerenciam documentos protegidos por políticas para os usuários, conforme necessário. Eles também criam contas de usuários convidados e monitoram eventos do sistema, de documentos, de usuários, de políticas, de definições de políticas e personalizados. Eles também podem ser responsáveis pela configuração do servidor global, da página da Web e das configurações de política com um administrador do sistema.

  Os administradores podem atribuir aos usuários as seguintes funções na área Gerenciamento de usuários do console de administração. Os usuários com essas funções atribuídas executam suas tarefas na área de interface de usuário de segurança de documentos do console de administração.

  **Superadministrador de segurança de documentos**

  Os usuários com essa função têm acesso a todas as configurações de segurança de documentos no console de administração. Estas permissões estão associadas à função:

   * Gerenciar configuração
   * Gerenciar política
   * Gerenciar conjuntos de políticas
   * Gerenciar documentos
   * Gerenciar editores de documento
   * Gerenciar usuários convidados e locais
   * Exibir eventos
   * Delegar
   * Convidar usuários externos

  **Administrador de segurança de documentos**

  Os usuários com essa função podem configurar o servidor de segurança de documentos, usando a página Configuração na seção Segurança de documentos do console de administração. Esta permissão está associada à função Gerenciar configuração.

  >[!NOTE]
  >
  >Os usuários com essa função também devem ter a função Usuário do console de administração para poderem fazer logon no console de administração e editar quaisquer configurações relacionadas.

  **Administrador do conjunto de políticas de segurança de documentos**

  Os usuários com essa função podem usar a seção de segurança de documentos do console de administração para editar as políticas de outros usuários e para criar, editar e excluir conjuntos de políticas. Quando um administrador de conjunto de políticas cria um conjunto de políticas, ele pode atribuir um coordenador de conjunto de políticas a esse conjunto de políticas. Estas permissões estão associadas à função:

   * Gerenciar política
   * Gerenciar conjuntos de políticas
   * Gerenciar documentos
   * Gerenciar editores de documento
   * Exibir eventos
   * Delegar

  >[!NOTE]
  >
  >Os usuários com essa função também devem ter a função Usuário do console de administração para poderem fazer logon no console de administração e editar quaisquer configurações relacionadas.

  **A segurança de documentos gerencia usuários convidados e locais**

  Os usuários com essa função podem executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas da Web de segurança de documentos relevantes. Estas permissões estão associadas à função:

   * Gerenciar usuários convidados e locais
   * Convidar usuários externos
   * Acessar páginas da Web do usuário final

  >[!NOTE]
  >
  >Os usuários com essa função também devem ter a função Usuário do console de administração para poderem fazer logon no console de administração e editar quaisquer configurações relacionadas.

  **Usuário de convite de segurança de documentos**

  Os usuários com essa função podem convidar usuários. Estas permissões estão associadas à função:

   * Convidar usuários externos
   * Acessar páginas da Web do usuário final

  **Usuário final de segurança de documentos**

  Os usuários com essa função podem acessar páginas da Web do usuário final de segurança de documentos. Essa função também pode ser atribuída aos administradores para permitir que eles criem políticas usando as páginas de usuário final. Essa permissão está associada à função Acessar páginas da Web do usuário final.

* Os usuários da organização que têm contas válidas de segurança de documentos criam suas próprias políticas, usam políticas para proteger documentos, rastrear e gerenciar seus documentos protegidos por política e monitorar eventos relacionados a seus documentos.
* Os coordenadores de definições de políticas gerenciam documentos, exibem eventos e gerenciam outros coordenadores de definições de políticas (com base em suas permissões). Os administradores designam os usuários como coordenadores de definições de políticas para definições de políticas específicas.
* Os usuários externos à sua organização (por exemplo, um parceiro comercial) podem usar documentos protegidos por política se estiverem no diretório de segurança de documentos, se o administrador criar uma conta para eles ou se se registrarem com a segurança de documentos por meio de um processo automatizado de convite por email. Dependendo de como o administrador ativar as configurações de acesso, os usuários convidados também poderão ter permissão para aplicar políticas a documentos, criar, modificar e excluir suas políticas e convidar outros usuários externos a usar seus documentos protegidos por política.
* Os desenvolvedores usam o SDK do AEM Forms para integrar aplicativos personalizados com segurança de documentos.

Os administradores de segurança de documentos podem criar funções personalizadas usando as seguintes permissões no Gerenciamento de usuários:

* Segurança de documentos - Gerenciar configuração
* Segurança de documentos Gerenciar usuários convidados e locais
* Segurança de documentos Gerenciar conjuntos de políticas
* Segurança de documentos Gerenciar conjuntos de políticas
* Eventos do Servidor de Exibição de Segurança de Documentos
* Proprietário da Política de Alteração de Segurança de Documentos

## Políticas e documentos protegidos por política {#policies-and-policy-protected-documents}

A *política* define um conjunto de configurações de confidencialidade e usuários que podem acessar um documento ao qual a política é aplicada. Uma política também permite que as permissões em um documento sejam alteradas dinamicamente. Ele dá à pessoa que protege o documento permissão para alterar as configurações de confidencialidade para revogar o acesso ao documento ou para alternar a política.

A proteção por política pode ser aplicada a um documento PDF usando Adobe Acrobat® Pro e Acrobat Standard. A proteção por política pode ser aplicada a outros tipos de arquivos, como arquivos do Microsoft® Word, Excel e PowerPoint, usando o aplicativo cliente com as extensões adequadas do Acrobat Reader DC instaladas.

### Como as políticas funcionam {#how-policies-work}

As políticas contêm informações sobre os usuários autorizados e as configurações de confidencialidade a serem aplicadas aos documentos. Os usuários podem ser qualquer pessoa da sua organização e pessoas externas à organização que têm uma conta. Se o administrador ativar o recurso de convite de usuário, é possível até mesmo adicionar novos usuários às políticas, iniciando, portanto, um processo de email de convite de registro.

As configurações de confidencialidade em uma política determinam como os recipients podem usar o documento. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, fazer alterações ou adicionar assinaturas e comentários a documentos protegidos. A mesma política também pode especificar configurações de confidencialidade diferentes para usuários específicos.

>[!NOTE]
>
>As configurações de confidencialidade aplicadas por meio de uma política substituem quaisquer configurações que possam ter sido aplicadas a um documento PDF no Acrobat usando as opções de segurança de senha ou certificado. (Consulte a Ajuda do Acrobat para obter mais informações.)

Usuários e administradores criam políticas por meio das páginas da Web de segurança de documentos. Somente uma política por vez pode ser aplicada a um documento. Você pode aplicar uma política usando um destes métodos:

* Abra o documento no Acrobat ou em outro aplicativo cliente e selecione uma política para proteger o documento.
* Envie um documento como um anexo de email no Microsoft® Outlook. Nesse caso, você pode selecionar uma política em uma lista de políticas. Ou você pode selecionar uma política gerada automaticamente que o Acrobat cria com um conjunto padrão de configurações de confidencialidade para proteger o documento somente para os destinatários de mensagem de email.

Uma política pode ser removida de um documento usando o aplicativo cliente.

![rm_psonline_policy](assets/rm_psonline_policy.png)

As etapas do diagrama são as seguintes:

1. O proprietário do documento protege o documento de um aplicativo cliente compatível com uma política que permite o uso online.
1. A Segurança de documentos cria uma licença de documento e chaves de documento e criptografa a política. A licença do documento, a política criptografada e a chave do documento são retornadas ao aplicativo cliente.
1. O documento é criptografado com a chave de documento, e a chave de documento é descartada. O documento agora incorpora a licença e a política. Essas tarefas são executadas no aplicativo cliente compatível.

Quando você aplica uma política a um documento, as informações contidas nele, incluindo quaisquer arquivos contidos (texto, áudio ou vídeo) em documentos PDF, são protegidas pelas configurações de confidencialidade especificadas na política. A Segurança de documentos gera uma licença e informações de criptografia que são incorporadas ao documento. Ao distribuir o documento, a segurança de documentos pode autenticar os recipients que tentarem abrir o documento e autorizar o acesso de acordo com os privilégios especificados na política.

Se o uso offline estiver ativado, os recipients também poderão usar documentos protegidos por política offline (sem uma conexão ativa com a Internet ou com uma rede) pelo período especificado na política.

### Como documentos protegidos por política funcionam {#how-policy-protected-documents-work}

Para abrir e usar documentos protegidos por política, a política deve incluir seu nome como um recipient e você deve ter uma conta de segurança de documentos válida. Para documentos PDF, você precisa do Acrobat ou Adobe Reader®. Para outros tipos de arquivos, é necessário o aplicativo apropriado para o arquivo com as extensões do Acrobat Reader DC instaladas.

Ao abrir um documento protegido por política, o Acrobat, o Adobe Reader ou as extensões do Acrobat Reader DC se conectam à segurança de documentos para autenticar você. Em seguida, prossiga para o logon. Se o uso do documento estiver sendo auditado, uma mensagem de notificação será exibida. Depois que a segurança de documentos determina quais permissões de documento conceder, ela gerencia a descriptografia do documento. Você poderá então usar o documento de acordo com as configurações de confidencialidade da política.

![rm_psopen_online](assets/rm_psopen_online.png)

As etapas do diagrama são as seguintes:

1. O usuário do documento abre o documento em um aplicativo cliente compatível e se autentica no servidor. O identificador do documento é enviado ao servidor de segurança de documentos.
1. A segurança de documentos autentica os usuários, verifica a política de autorização e cria um voucher. O voucher (que contém a chave do documento e as permissões) é retornado ao aplicativo cliente.
1. O documento é descriptografado com a chave de documento, e a chave de documento é descartada. O documento pode ser usado de acordo com as configurações de confidencialidade da política. Essas tarefas são executadas no aplicativo cliente compatível.

Você pode continuar a usar um documento sob estas condições:

* Indefinidamente ou pelo período de validade especificado na política
* Até que o administrador ou a pessoa que aplicou a política revogue o acesso ao documento ou altere a política

Você também pode usar documentos protegidos por política offline (sem uma conexão com a Internet ou com uma rede) se a política permitir acesso offline. Primeiro logon na segurança de documentos para sincronizar o documento. Você pode usar o documento durante o período de concessão offline especificado na política.

Quando o período de concessão offline terminar, sincronize o documento com a segurança de documentos novamente, entrando online e abrindo um documento protegido por política ou usando um comando no aplicativo cliente. Consulte *Ajuda do Acrobat* ou o apropriado *Ajuda das extensões do Acrobat Reader DC* para obter detalhes.

Se você salvar uma cópia de um documento protegido por política usando o comando de menu Salvar ou Salvar como, a política será automaticamente aplicada e imposta para o novo documento. Eventos como tentativas de abrir o novo documento também são auditados e registrados para o documento original.

## Conjuntos de políticas {#policy-sets}

*Conjuntos de políticas* são usados para agrupar um conjunto de políticas que têm um objetivo comercial comum. Esses conjuntos de políticas são então disponibilizados a um subconjunto de usuários no sistema.

Cada conjunto de políticas pode ter um ou mais coordenadores de definições de políticas associados. O coordenador do conjunto de políticas é um administrador ou um usuário que tem mais permissões. A variável *coordenador de conjunto de políticas* O geralmente é um especialista na organização que pode criar melhor as políticas em um conjunto de políticas específico.

Os coordenadores de definições de políticas podem executar estas tarefas:

* Criar políticas
* Editar e excluir qualquer política no conjunto de políticas
* Editar configurações do conjunto de políticas
* Adicionar e remover coordenadores de definição de políticas
* Exibir eventos de política e documento para qualquer política ou documento no conjunto de políticas
* Revogar acesso a documentos
* Alternar políticas para o documento.

>[!NOTE]
>
>Você pode recuperar no máximo 1000 nomes de conjuntos de políticas do banco de dados usando `getAllPolicysetnames()` API.

Os conjuntos de políticas são criados e excluídos nas páginas da Web de administração de segurança de documentos por administradores e coordenadores de definições de políticas que têm permissão para fazer isso.

Os conjuntos de políticas são disponibilizados para um número limitado de usuários especificando quais usuários ou grupos em um domínio podem usar as políticas do conjunto de políticas para proteger documentos.

Quando a segurança de documentos é instalada, um conjunto de políticas padrão é criado, chamado *Conjunto de Políticas Globais*. O administrador que instalou o software gerencia este conjunto de políticas.

## Práticas recomendadas {#best-practices}

As políticas são conjuntos reutilizáveis de permissões e grupos de usuários que podem ser aplicados a vários documentos. Para os documentos protegidos. Essas políticas garantem que somente usuários autorizados possam usar os recursos permitidos. Espera-se que o número de políticas e conjuntos de políticas aumente com um aumento em diferentes funções de usuário e documentos em um departamento. Para criar e gerenciar políticas, veja a seguir algumas considerações e práticas recomendadas:

* **Criar políticas reutilizáveis:** O Adobe recomenda reutilizar políticas em vários documentos. Isso ajuda a manter o número de políticas no mínimo, fornece o desempenho ideal e facilita o gerenciamento de políticas. Para criar uma política reutilizável:

1. Identificar e definir os requisitos de controle de acesso em nível de departamentos e organizações.

1. Crie grupos de usuários e adicione usuários a esses grupos.

1. Criar um conjunto de políticas.

1. Abra o conjunto de políticas e crie uma política. Adicionar grupos de usuários e definir configurações de confidencialidade (controle de acesso) para a política.

Adicione grupos de usuários a políticas em vez de usuários individuais. Isso facilita o gerenciamento e a aplicação de políticas a muitos usuários.

* **Criar conjuntos de políticas personalizados:** Um conjunto de políticas combina várias políticas em uma entidade gerenciável. Crie conjuntos de políticas personalizados para sua organização ou departamento, use-os para agrupar políticas relacionadas e disponibilizá-los a um subconjunto de usuários no sistema.

  Usar conjuntos de políticas facilita a atribuição e o gerenciamento de políticas relacionadas a usuários específicos em uma organização ou departamento. Por exemplo, conjuntos de políticas separados para o departamento de finanças e recursos humanos podem ajudar a gerenciar e aplicar políticas relacionadas facilmente a documentos designados para departamentos correspondentes.

* **Usar um autorizador externo para aplicar permissões dinamicamente:** Você pode usar [autorizador externo](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html) para avaliar e aplicar dinamicamente permissões com base na condição externa. Quando as permissões são avaliadas dinamicamente, com base na condição externa, você pode:

   * Forneça controle de acesso centralizado para documentos em sua organização.

   * Controlar o acesso a documentos protegidos por política determinando dinamicamente se um usuário pode acessar um documento protegido por política. Por exemplo, decide dinamicamente se um usuário pode imprimir um documento protegido por política.

   * Use um mecanismo de controle de acesso que seu sistema de gerenciamento de conteúdo usa, além do processo padrão de avaliação de políticas. Por exemplo, quando o serviço determina se um usuário pode imprimir um documento protegido por política, ele pode usar o processo padrão de avaliação de política. E também pode usar o mecanismo de controle de acesso que seu sistema de gerenciamento de conteúdo usa.

  Embora seja possível substituir completamente o processo de avaliação de política de Segurança de documentos por um manipulador de autorização externo, é recomendável usar um manipulador de autorização externo com o processo de avaliação de política. Como resultado, o acesso aos documentos pode ser controlado pelo mesmo mecanismo de controle que seu sistema de gerenciamento de conteúdo usa. Por exemplo, quando o serviço de Segurança de documentos determina se um usuário pode imprimir um documento protegido por política, ele usa o processo padrão de avaliação de política. Ele também usa o mecanismo de controle de acesso que seu sistema de gerenciamento de conteúdo usa. Para obter mais informações, consulte [Criando manipuladores de autorização externos](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html).

* **Mantenha os conjuntos de políticas em um número limitado:** Vários fatores conduzem a um crescimento constante das políticas e dos conjuntos de políticas. Alguns fatores comuns são:

   * Aumento nas funções de usuário, departamentos e documentos em uma organização durante um período.
   * Os departamentos de uma organização trabalham isoladamente e mantêm um controle rígido sobre as políticas específicas do departamento. Ele leva a políticas idênticas dentro de uma organização.

  A Adobe recomenda manter o número mínimo de políticas e conjuntos de políticas. Ele ajuda a gerenciar facilmente políticas e conjuntos de políticas e a fornecer melhor desempenho. Para manter o número no mínimo:

   * Criar políticas reutilizáveis. Essas políticas podem ser compartilhadas em vários departamentos.
   * Considere criar conjuntos de políticas em toda a organização, se algumas políticas se aplicarem a vários departamentos em vez de um conjunto de políticas individual para cada departamento.
   * Políticas relacionadas a grupos em um conjunto de políticas. Não crie um conjunto de políticas separado para cada política.
   * Use um autorizador externo para controlar dinamicamente as permissões do usuário.

  >[!NOTE]
  >
  >Você pode usar o [getAllPolicysetnames()](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/PolicyManager.html) API para recuperar um máximo de 1000 nomes de conjuntos de políticas. Internamente, a API recupera um máximo de 1000 políticas para as quais o chamador da API tem permissão de editor de documentos e, em seguida, cria e retorna uma lista de nomes de conjuntos de políticas exclusivos associados às políticas recuperadas para você. Por exemplo, quando a API recupera 1000 políticas e as políticas recuperadas são associadas a 200 conjuntos de políticas no total, a API retorna apenas 200 nomes de conjuntos de políticas.
