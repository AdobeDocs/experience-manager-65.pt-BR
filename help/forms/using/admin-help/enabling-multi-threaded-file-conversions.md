---
title: Ativação de conversões de arquivos de vários processos
seo-title: Ativação de conversões de arquivos de vários processos
description: Saiba como ativar conversões de arquivos de vários processos.
seo-description: Saiba como ativar conversões de arquivos de vários processos.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---


# Ativação de conversões de arquivos de vários processos {#enabling-multi-threaded-file-conversions}

O Gerador de PDF fornece a capacidade de ativar conversões de arquivos de vários processos para certos tipos de arquivos. A conversão de arquivos de vários processos melhora o desempenho do Gerador de PDF ao permitir que ele execute várias conversões ao mesmo tempo.

## Habilitar conversões de arquivos de vários processos para documentos OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Por padrão, o Gerador de PDF pode converter somente um documento OpenOffice, Microsoft Word ou PowerPoint de cada vez. Se você ativar conversões de vários processos, o Gerador de PDF poderá converter mais de um dos documentos simultaneamente. O Gerador de PDF iniciará várias instâncias do OpenOffice ou do PDFMaker (usado para executar as conversões do Word e do PowerPoint).

>[!NOTE]
>
>Não há suporte para conversões de arquivos de vários processos no Microsoft Word 2003 e PowerPoint 2003. Para permitir conversões de arquivos de vários processos, atualize para o Microsoft Word 2007 e PowerPoint 2007 ou Microsoft Word 2010 e PowerPoint 2010.

>[!NOTE]
>
>Não há suporte para conversões de arquivos de vários processos no Microsoft Excel, Microsoft Visio, Microsoft Project ou Microsoft Publisher.

Cada instância do OpenOffice ou do PDFMaker é iniciada usando uma conta de usuário separada. Cada conta de usuário adicionada deve ser um usuário válido com privilégios administrativos no computador do servidor de formulários. Em um ambiente clusterizado, o mesmo conjunto de usuários deve ser válido para todos os nós do cluster.

Na página Contas de usuário no console de administração, é possível especificar quais contas de usuário serão usadas para conversões de arquivos de vários processos. Você pode adicionar contas, excluí-las ou alterar senhas de contas. Se você estiver executando o Gerador de PDF no Windows Server 2003 ou no Windows Server 2008, adicione pelo menos três contas de usuário que tenham privilégios de administrador.

Ao adicionar usuários para OpenOffice, Microsoft Word ou Microsoft PowerPoint no Windows Server 2003 ou 2008 ou para OpenOffice no Linux ou no Sun™ Solaris™, ignore as caixas de diálogo de ativação iniciais para todos os usuários.

### Adicione o direito de substituir o token de nível de processo {#add-the-right-to-replace-the-process-level-token}

Em um sistema operacional Windows, as contas de usuário administradores usadas para conversão de PDF (usuários de PDFG) precisarão substituir privilégios de token de nível de processo. Você pode adicionar esse direito usando o Editor de Diretiva de Grupo:

1. No menu Start do Windows, clique em Executar e digite gpedit.msc.
1. Clique em Política local do computador > Configuração do computador > Configurações do Windows > Configurações de segurança > Políticas locais > Atribuição de direitos de usuário. Edite a política *Substituir token* de nível de processo para incluir o grupo Administradores.
1. Adicione o usuário à entrada Substituir um token de nível de processo.

### Configuração adicional necessária para o OpenOffice, Microsoft Word e Microsoft PowerPoint no Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se você estiver executando o OpenOffice, o Microsoft Word ou o Microsoft PowerPoint no Windows Server 2008, desative o UAC para cada usuário adicionado.

1. Clique em Painel de controle do Campaign > Contas de usuário > Ativar ou desativar o controle de conta de usuário.
1. Desmarque a caixa &quot;Use User Account Control (UAC) Control (Usar controle de conta de usuário) para ajudar a proteger seu computador&quot; e clique em OK.
1. Reinicie o computador para que as configurações entrem em vigor.

### Configuração adicional necessária para o OpenOffice no Linux ou Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Adicionar contas de usuário. (Consulte [Adicionar uma conta](enabling-multi-threaded-file-conversions.md#add-a-user-account)de usuário.)
1. Em seguida, você fará alterações no arquivo /etc/sudoers. A permissão padrão para este arquivo é 440. Altere a permissão deste arquivo para gravável.
1. Adicione entradas para usuários adicionais (que não sejam o administrador que executa o servidor de formulários) no arquivo /etc/sudoers. Por exemplo, se você estiver executando formulários AEM como um usuário chamado lcadm e um servidor chamado myhost, e quiser representar user1 e user2, adicione as seguintes entradas a /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Essa configuração permite que o lcadm execute qualquer comando no host ‘myhost’ como ‘user1’ ou ‘user2’ sem solicitar senha.

   >[!NOTE]
   >
   >Verifique se você atribuiu funções de usuário do sistema e do PDFG a &quot;user1&quot; e &quot;user2&quot;. Para atribuir a função PDFG a um usuário, consulte [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Também no arquivo /etc/sudoers, localize e comente esta linha adicionando um sinal de número (#) no início da linha:

   ```shell
   Defaults requiretty
   ```

   Isso permite adicionar usuários Linux.

1. Altere a permissão para o arquivo etc/sudoers de volta para 440.
1. Permite que todos os usuários adicionados por meio da opção [Adicionar uma conta](enabling-multi-threaded-file-conversions.md#add-a-user-account) de usuário façam conexões com o servidor de formulários. Por exemplo, para permitir que um usuário local chamado user1 tenha a permissão de fazer a conexão com o servidor de formulários, use o seguinte comando

   `xhost +local:user1@`

   Para obter mais detalhes, consulte a documentação do comando xhost.

1. Reinicie o servidor.

>[!NOTE]
>
>O OpenOffice deve estar instalado em um local de diretório que todos os usuários do PDFG possam acessar. Você pode verificar isso fazendo logon como usuário do PDFG e verificando se é possível iniciar o OpenOffice sem problemas.

### Adicionar uma conta de usuário {#add-a-user-account}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique em Adicionar e digite o nome de usuário e a senha de um usuário que tenha privilégios administrativos no servidor de formulários. Se você estiver configurando usuários para o OpenOffice, ignore as caixas de diálogo iniciais de ativação do OpenOffice.

   >[!NOTE]
   >
   >Se você estiver configurando usuários para o OpenOffice, o número de instâncias do OpenOffice não poderá ser maior que o número de contas de usuário especificado nesta etapa.

1. Reinicie o servidor de formulários.

### Remova um usuário da lista usada para conversões de arquivos de vários processos {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique na caixa de seleção ao lado do usuário que você deseja remover e clique em Excluir.
1. Na página de confirmação, clique em Excluir.
1. Reinicie o servidor de formulários.

### Alterar a senha de uma conta {#change-the-password-for-an-account}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique no nome do usuário e digite e confirme a nova senha. Essa senha deve corresponder à senha do sistema do usuário.

