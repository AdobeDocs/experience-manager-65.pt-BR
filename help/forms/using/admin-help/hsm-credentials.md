---
title: Gerenciamento de credenciais do HSM
seo-title: Gerenciamento de credenciais do HSM
description: Saiba como gerenciar as credenciais do HSM.
seo-description: Saiba como gerenciar as credenciais do HSM.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gerenciamento de credenciais do HSM {#managing-hsm-credentials}

Na página Gerenciamento de armazenamento confiável, é possível gerenciar as credenciais do Módulo de segurança de hardware (HSM). Um HSM é um dispositivo PKCS#11 de terceiros que pode ser usado para gerar e armazenar com segurança chaves privadas. O HSM protege fisicamente o acesso e o uso das chaves privadas.

O software cliente é necessário para se comunicar com o HSM. O software cliente HSM deve ser instalado e configurado no mesmo computador que os formulários AEM.

Formulários AEM Assinaturas digitais podem usar credenciais armazenadas em um HSM para aplicar assinaturas digitais do lado do servidor. Siga as instruções nesta seção para criar um alias para cada credencial HSM que o Digital Signatures usará. O alias contém todos os parâmetros exigidos pelo HSM.

>[!NOTE]
>
>Após alterar a configuração do HSM, reinicie o servidor de formulários do AEM.

## Crie um alias para uma credencial HSM quando o dispositivo HSM estiver online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM e clique em Adicionar.
1. Na caixa Nome do perfil, digite uma string usada para identificar o alias. Esse valor é usado como uma propriedade para algumas operações do Digital Signatures, como a operação Assinar campo de assinatura.
1. Na caixa Biblioteca PKCS11, digite o caminho totalmente qualificado da biblioteca do cliente HSM no servidor. Por exemplo, `c:\Program Files\LunaSA\cryptoki.dll`. Em um ambiente clusterizado, esse caminho deve ser idêntico para todos os servidores do cluster.
1. Clique em Testar conectividade HSM. Se os formulários AEM conseguirem se conectar ao dispositivo HSM, uma mensagem será exibida informando que o HSM está disponível. Clique emAvançar.
1. Use o Nome do token, a ID do slot ou o Índice da lista de slot para identificar onde as credenciais são armazenadas no HSM.

   * **** Nome do token: Corresponde ao nome da partição HSM a ser usada (por exemplo, HSMPART1).
   * **** ID do slot: A ID do slot é um identificador de slot do tipo de dados long.
   * **** Índice da lista de slots: Se você selecionar Índice da lista de slots, defina as Informações do slot para um número inteiro que corresponda ao slot. Este é um índice baseado em 0, o que significa que se o cliente for registrado na partição HSMPART1 primeiro, HSMPART1 será referenciado usando o valor 0 de SlotListIndex.

1. Na caixa Pino do token, digite a senha necessária para acessar a chave HSM e clique em Avançar.
1. Na caixa Credenciais, selecione uma credencial. Clique em Salvar.

## Criar um alias para uma credencial HSM quando o dispositivo HSM estiver offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM e clique em Adicionar.
1. Na caixa Nome do perfil, digite uma string usada para identificar o alias. Esse valor é usado como uma propriedade para algumas operações do Digital Signatures, como a operação Assinar campo de assinatura.
1. Na caixa Biblioteca PKCS11, digite o caminho totalmente qualificado da biblioteca do cliente HSM no servidor. Por exemplo, `c:\Program Files\LunaSA\cryptoki.dll`. Em um ambiente clusterizado, esse caminho deve ser idêntico para todos os servidores do cluster.
1. Marque a caixa de seleção Criação de perfil offline. Clique emAvançar.
1. Na lista Dispositivo HSM, selecione o fabricante do dispositivo HSM no qual a credencial está armazenada.
1. Na lista Tipo de slot, selecione Id do slot, Índice de slot ou Nome do token e especifique um valor na caixa Informações do slot. Os formulários AEM usam essas configurações para determinar onde as credenciais são armazenadas no HSM.

   * **** Nome do token: Corresponde a um nome de partição (por exemplo, HSMPART1).
   * **** ID do slot: A ID do slot é um número inteiro que corresponde ao slot, que por sua vez corresponde a uma partição. Por exemplo, o cliente (servidor de formulários) registrado com a partição HSMPART1 primeiro. Isso mapeia o slot 1 para a partição HSMPART1, para este cliente. Como HSMPART1 é a primeira partição registrada, a ID do slot é 1 e você definiria Informações do slot como 1.

      A ID do slot é definida cliente a cliente. Se você registrou um segundo computador em uma partição diferente (por exemplo, HSMPART2 no mesmo dispositivo HSM), então o slot 1 seria associado à partição HSMPART2 para esse cliente.

   * **** Índice de Slot: Se você selecionar Índice de slot, defina as Informações do slot para um número inteiro que corresponda ao slot. Este é um índice baseado em 0, o que significa que se o cliente for registrado com a partição HSMPART1 primeiro, o slot 1 será mapeado para o HSMPART1 desse cliente. Como HSMPART1 é a primeira partição registrada, o Índice de Slot é 0.

1. Selecione uma destas opções e forneça o caminho:

   * **Certificado**: (Não necessário se estiver usando SHA1) Clique em Procurar e localize o caminho para a chave pública para a credencial que você está usando.
   * **** Certificado SHA1: (Não é necessário se estiver usando um certificado físico) Digite o valor SHA1 (impressão digital) do arquivo de chave pública (.cer) para a credencial que você está usando. Verifique se não há espaços usados no valor SHA1.

1. Na caixa Password (Senha), digite a senha necessária para acessar a chave HSM para obter as informações do slot e clique em Save (Salvar).

## Exibir propriedades de alias de credenciais HSM {#view-hsm-credential-alias-properties}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM.
1. Clique no nome do alias do alias de credencial para exibir as propriedades e clique em OK.

## Verifique o status de uma credencial HSM {#check-the-status-of-an-hsm-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM.
1. Clique na caixa de seleção ao lado da credencial que deseja marcar e clique em Verificar status.

A coluna Status reflete o status atual da credencial. Em caso de falha, um X vermelho é exibido na coluna Status. Passe o mouse sobre o X para exibir uma dica de ferramenta contendo o motivo da falha.

## Atualizar propriedades de alias de credenciais HSM {#update-hsm-credential-alias-properties}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM.
1. Clique no nome do alias do alias de credencial.
1. Clique em Atualizar credencial e atualize as configurações conforme necessário.

## Redefinir todas as conexões HSM {#reset-all-hsm-connections}

Redefina as conexões abertas com um dispositivo HSM após qualquer interrupção na sessão de rede entre o servidor de formulários e o dispositivo HSM. Por exemplo, as interrupções podem ocorrer devido a uma interrupção de rede ou o dispositivo HSM sendo colocado offline para uma atualização de software. Após uma interrupção, as conexões existentes são obsoletas e todas as solicitações de assinatura contra essas conexões falham. Usar a opção Redefinir todas as conexões HSM limpa as conexões antigas.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM.
1. Clique em Redefinir todas as conexões HSM.

## Excluir um alias de credencial HSM {#delete-an-hsm-credential-alias}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais HSM.
1. Marque as caixas de seleção das credenciais HSM que deseja excluir, clique em Excluir e, em seguida, clique em OK.

## Configurar suporte remoto a HSM {#configure-remote-hsm-support}

Os formulários AEM usam um mecanismo IPC/RPC baseado em Serviços da Web. Esse mecanismo permite que os formulários AEM usem um HSM instalado em um computador remoto. Para usar essa funcionalidade, instale o serviço da Web no computador remoto onde o HSM está instalado. Consulte [Configuração do suporte HSM para formulários AEM ES usando Sun JDK na](https://kb2.adobe.com/cps/808/cpsid_80835.html)plataforma Windows de 64 bits para obter mais informações.

Este mecanismo não suporta a criação on-line de perfis HSM ou verificações de status. No entanto, há duas maneiras de criar perfis HSM e executar verificações de status:

* Crie uma credencial de cliente de formulários AEM, transmitindo-a para o Certificado do assinante. Siga as etapas em [Configurar o suporte de HSM para formulários AEM ES usando o Sun JDK na plataforma](https://kb2.adobe.com/cps/808/cpsid_80835.html)Windows de 64 bits. O local do serviço da Web é passado como uma propriedade de Credencial. Os perfis HSM offline criados usando o certificado der ou o certificado SHA-1 hex também são suportados. No entanto, se você tiver atualizado para formulários AEM de uma versão anterior dos formulários AEM, faça alterações no cliente porque a credencial continha informações de certificado e serviço da Web.
* O local do serviço Web é especificado no console de administração do serviço de assinatura. (Consulte Configurações [do serviço de](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)assinatura.) Aqui, o cliente carregava somente o alias do perfil HSM no repositório de confiança. É possível usar essa opção sem alterações de cliente, mesmo se você tiver atualizado para formulários AEM de uma versão anterior dos formulários AEM. Esta opção não suporta perfis HSM usando o certificado SHA-1.

