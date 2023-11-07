---
title: Ativação de conversões de arquivos multithread
description: Saiba como habilitar conversões de arquivos com vários threads.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# Ativação de conversões de arquivos multithread {#enabling-multi-threaded-file-conversions}

O PDF Generator permite ativar conversões de arquivos com vários threads para determinados tipos de arquivos. A conversão de arquivos multithread melhora o desempenho do PDF Generator, permitindo que ele execute várias conversões ao mesmo tempo.

## Ativação de conversões de arquivos de várias operações para documentos OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Por padrão, o PDF Generator pode converter apenas um documento OpenOffice, Microsoft® Word ou PowerPoint por vez. Se você ativar conversões multithread, o PDF Generator poderá converter mais de um dos documentos simultaneamente. O PDF Generator inicia várias instâncias do OpenOffice ou do PDFMaker (usado para executar as conversões do Word e do PowerPoint).

>[!NOTE]
>
>Conversões de arquivos de várias operações não são suportadas com o Microsoft® Word 2003 e PowerPoint 2003. Para habilitar conversões de arquivos de múltiplos processos, atualize para o Microsoft® Word 2007 e PowerPoint 2007 ou Microsoft® Word 2010 e PowerPoint 2010.

>[!NOTE]
>
As conversões de arquivos de várias operações não são suportadas com o Microsoft® Excel, Microsoft® Visio, Microsoft® Project ou Microsoft® Publisher.

Cada instância do OpenOffice ou do PDFMaker é iniciada usando uma conta de usuário separada. Cada conta de usuário adicionada deve ser um usuário válido com privilégios administrativos no computador do Forms Server. Em um ambiente clusterizado, o mesmo conjunto de usuários deve ser válido para todos os nós do cluster.

Na página Contas de usuário do console de administração, você pode especificar quais contas de usuário utilizar para conversões de arquivos multithread. Você pode adicionar contas, excluí-las ou alterar senhas de contas. Se você estiver executando o PDF Generator no Windows Server 2003 ou no Windows Server 2008, adicione pelo menos três contas de usuário com privilégios de administrador.

Ao adicionar usuários para OpenOffice, Microsoft® Word ou Microsoft® PowerPoint no Windows Server 2003 ou 2008, ou para OpenOffice no Linux® ou Sun™ Solaris™, ignore as caixas de diálogo de ativação iniciais para todos os usuários.

### Adicionar o direito de substituir o token no nível do processo {#add-the-right-to-replace-the-process-level-token}

Em um sistema operacional Windows, as contas de usuário administrador usadas para conversão de PDF (usuários PDFG) devem substituir os privilégios de token de nível de processo. Você pode adicionar este direito usando o Editor de Diretiva de Grupo:

1. No menu Iniciar do Windows, clique em Executar e depois insira gpedit.msc.
1. Clique em Política do Computador Local > Configuração do Computador > Configurações do Windows > Configurações de Segurança > Políticas Locais > Atribuição de Direitos do Usuário. Edite o *Substituir um token de nível de processo* política para incluir o grupo Administradores.
1. Adicione o usuário à entrada Substituir um token no nível do processo.

### Configuração adicional necessária para OpenOffice, Microsoft® Word e Microsoft® PowerPoint no Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se você estiver executando o OpenOffice, o Microsoft® Word ou o Microsoft® PowerPoint no Windows Server 2008, desative o UAC para cada usuário adicionado.

1. Clique em Painel de controle > Contas de usuário > Ativar ou desativar o controle de conta de usuário.
1. Desmarque a caixa &quot;Usar UAC (Controle de conta de usuário) para ajudar a proteger seu computador&quot; e clique em OK.
1. Reinicie o computador para que as configurações sejam aplicadas.

### Configuração adicional necessária para OpenOffice no Linux® ou Solaris™ {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Adicionar contas de usuário. (Consulte [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Em seguida, você deve alterar o arquivo /etc/sudoers. A permissão padrão para esse arquivo é 440. Alterar a permissão deste arquivo para gravável.
1. Adicione entradas para usuários adicionais (além do administrador que executa o Forms Server) no arquivo /etc/sudoers. Por exemplo, se você estiver executando formulários AEM como um usuário chamado lcadm e um servidor chamado myhost e quiser representar user1 e user2, adicione as seguintes entradas em /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Essa configuração permite que o lcadm execute qualquer comando no host &quot;myhost&quot; como &quot;user1&quot; ou &quot;user2&quot; sem solicitar uma senha.

   >[!NOTE]
   >
   Verifique se você atribuiu as funções de usuário do sistema e usuário PDFG a &#39;usuário1&#39; e &#39;usuário2&#39; . Para atribuir uma função PDFG a um usuário, consulte [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Além disso, no arquivo /etc/sudoers, localize e comente esta linha adicionando um sinal numérico (#) no início da linha:

   ```shell
   Defaults requiretty
   ```

   Isso permite adicionar usuários do Linux®.

1. Altere a permissão para o arquivo etc/sudoers de volta para 440.
1. Permitir todos os usuários adicionados via [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account) para fazer conexões com o Forms Server. Por exemplo, para permitir que um usuário local chamado user1 tenha a permissão de fazer a conexão com o Forms Server, use o seguinte comando

   `xhost +local:user1@`

   Para obter mais detalhes, consulte a documentação do comando xhost.

1. Reinicie o servidor.

>[!NOTE]
>
O OpenOffice deve ser instalado em um local de diretório que todos os usuários de PDFG possam acessar. Você pode verificar isso fazendo logon como usuário PDFG e verificando se é possível iniciar o OpenOffice sem problemas.

### Adicionar uma conta de usuário {#add-a-user-account}

1. No console de administração, clique em Serviços > PDF Generator > Contas de usuário.
1. Clique em Adicionar e digite o nome de usuário e a senha de um usuário que tenha privilégios administrativos no Forms Server. Se você estiver configurando usuários para o OpenOffice, ignore as caixas de diálogo de ativação iniciais do OpenOffice.

   >[!NOTE]
   >
   Se você estiver configurando usuários para OpenOffice, o número de instâncias do OpenOffice não poderá ser maior que o número de contas de usuário especificadas nesta etapa.

1. Reinicie o servidor do Forms.

### Remover um usuário da lista usada para conversões de arquivos multithread {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. No console de administração, clique em Serviços > PDF Generator > Contas de usuário.
1. Clique na caixa de seleção ao lado do usuário que deseja remover e clique em Excluir.
1. Na página de confirmação, clique em Excluir.
1. Reinicie o servidor do Forms.

### Alterar a senha de uma conta {#change-the-password-for-an-account}

1. No console de administração, clique em Serviços > PDF Generator > Contas de usuário.
1. Clique no nome do usuário, digite e confirme a nova senha. Esta senha deve corresponder à senha do sistema do usuário.
