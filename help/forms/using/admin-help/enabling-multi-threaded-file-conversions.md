---
title: Ativar conversões de arquivos de vários segmentos
seo-title: Enabling multi-threaded file conversions
description: Saiba como ativar conversões de arquivos de vários segmentos.
seo-description: Learn how to enable multi-threaded file conversions.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Ativar conversões de arquivos de vários segmentos {#enabling-multi-threaded-file-conversions}

O Gerador de PDF oferece a capacidade de ativar conversões de arquivos de vários processos para determinados tipos de arquivos. A conversão de arquivos de vários segmentos melhora o desempenho do Gerador de PDF, permitindo que ele execute várias conversões ao mesmo tempo.

## Ativando conversões de arquivos de vários segmentos para documentos OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Por padrão, o PDF Generator pode converter apenas um documento OpenOffice, Microsoft Word ou PowerPoint de cada vez. Se você ativar conversões de vários segmentos, o Gerador de PDF poderá converter mais de um dos documentos simultaneamente. O PDF Generator iniciará várias instâncias do OpenOffice ou do PDFMaker (usado para executar as conversões do Word e do PowerPoint).

>[!NOTE]
>
>Não há suporte para conversões de arquivos de vários segmentos com o Microsoft Word 2003 e o PowerPoint 2003. Para permitir conversões de arquivos de vários segmentos, atualize para o Microsoft Word 2007 e PowerPoint 2007 ou Microsoft Word 2010 e PowerPoint 2010.

>[!NOTE]
>
>As conversões de arquivos de vários segmentos não são compatíveis com o Microsoft Excel, Microsoft Visio, Microsoft Project ou Microsoft Publisher.

Cada instância do OpenOffice ou do PDFMaker é iniciada usando uma conta de usuário separada. Cada conta de usuário adicionada deve ser um usuário válido com privilégios administrativos no computador do servidor de formulários. Em um ambiente em cluster, o mesmo conjunto de usuários deve ser válido para todos os nós do cluster.

Na página Contas de usuário no console de administração, é possível especificar quais contas de usuário usar para conversões de arquivos de vários segmentos. Você pode adicionar contas, excluí-las ou alterar senhas de conta. Se você estiver executando o PDF Generator no Windows Server 2003 ou no Windows Server 2008, adicione pelo menos três contas de usuário que tenham privilégios de administrador.

Ao adicionar usuários para OpenOffice, Microsoft Word ou Microsoft PowerPoint no Windows Server 2003 ou 2008, ou para OpenOffice no Linux ou Sun™ Solaris™, ignore as caixas de diálogo de ativação inicial para todos os usuários.

### Adicionar o direito de substituir o token no nível do processo {#add-the-right-to-replace-the-process-level-token}

Em um sistema operacional Windows, as contas de usuário de administrador usadas para conversão de PDF (usuários de PDFG) precisarão substituir privilégios de token de nível de processo. Você pode adicionar este direito usando o Editor de Política de Grupo:

1. No menu Iniciar do Windows, clique em Executar e digite gpedit.msc.
1. Clique em Política de Computador Local > Configuração do Computador > Configurações do Windows > Configurações de Segurança > Políticas Locais > Atribuição de Direitos de Usuário. Edite o *Substituir um token de nível de processo* política para incluir o grupo Administradores.
1. Adicione o usuário à entrada Substituir um token de nível de processo .

### Configuração adicional necessária para OpenOffice, Microsoft Word e Microsoft PowerPoint no Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se estiver executando o OpenOffice, Microsoft Word ou Microsoft PowerPoint no Windows Server 2008, desative o UAC para cada usuário adicionado.

1. Clique em Painel de controle > Contas de usuário > Ativar ou desativar o Controle de conta de usuário.
1. Desmarque a caixa &quot;Usar controle de conta de usuário (UAC) para ajudar a proteger seu computador&quot; e clique em OK.
1. Reinicie o computador para que as configurações entrem em vigor.

### Configuração adicional necessária para OpenOffice no Linux ou Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Adicionar contas de usuário. (Consulte [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Em seguida, você fará alterações no arquivo /etc/sudoers . A permissão padrão para este arquivo é 440. Altere a permissão deste arquivo para gravável.
1. Adicione entradas para usuários adicionais (diferente do administrador que executa o servidor de formulários) no arquivo /etc/sudoers. Por exemplo, se você estiver executando AEM formulários como um usuário chamado lcadm e um servidor chamado myhost e quiser representar user1 e user2, adicione as seguintes entradas em /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Essa configuração permite que o lcadm execute qualquer comando no host ‘myhost’ como ‘user1’ ou ‘user2’ sem solicitar a senha.

   >[!NOTE]
   >
   >Certifique-se de ter atribuído funções de usuário do sistema e do usuário PDFG a &quot;usuário1&quot; e &quot;usuário2&quot;. Para atribuir a função PDFG a um usuário, consulte [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Além disso, no arquivo /etc/sudoers , localize e comente essa linha adicionando um sinal de número (#) no início da linha:

   ```shell
   Defaults requiretty
   ```

   Isso permite adicionar usuários Linux.

1. Altere a permissão para o arquivo etc/sudoers de volta para 440.
1. Permitir todos os usuários adicionados por meio de [Adicionar uma conta de usuário](enabling-multi-threaded-file-conversions.md#add-a-user-account) para fazer conexões com o servidor de formulários. Por exemplo, para permitir que um usuário local chamado user1 tenha a permissão de fazer a conexão com o servidor de formulários, use o seguinte comando

   `xhost +local:user1@`

   Para obter mais detalhes, consulte a documentação de comando xhost.

1. Reinicie o servidor.

>[!NOTE]
>
>O OpenOffice deve ser instalado em um local de diretório que todos os usuários do PDFG possam acessar. Você pode verificar isso fazendo logon como usuário do PDFG e verificando se pode iniciar o OpenOffice sem problemas.

### Adicionar uma conta de usuário {#add-a-user-account}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique em Adicionar e insira o nome de usuário e a senha de um usuário que tenha privilégios administrativos no servidor de formulários. Se você estiver configurando usuários para o OpenOffice, descarte as caixas de diálogo de ativação do OpenOffice iniciais.

   >[!NOTE]
   >
   >Se você estiver configurando usuários para o OpenOffice, o número de instâncias do OpenOffice não poderá ser maior do que o número de contas de usuário especificadas nesta etapa.

1. Reinicie o servidor de formulários.

### Remover um usuário da lista usada para conversões de arquivos de vários segmentos {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique na caixa de seleção ao lado do usuário que você deseja remover e clique em Excluir.
1. Na página de confirmação, clique em Excluir.
1. Reinicie o servidor de formulários.

### Alterar a senha de uma conta {#change-the-password-for-an-account}

1. No console de administração, clique em Serviços > Gerador de PDF > Contas de usuário.
1. Clique no nome de usuário e digite e confirme a nova senha. Essa senha deve corresponder à senha do sistema do usuário.
