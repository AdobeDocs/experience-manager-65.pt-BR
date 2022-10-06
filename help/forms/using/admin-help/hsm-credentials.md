---
title: Gerenciando credenciais do HSM
seo-title: Managing HSM credentials
description: Saiba como gerenciar credenciais do HSM.
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# Gerenciando credenciais do HSM {#managing-hsm-credentials}

Na página Gerenciamento de armazenamento de confiança, é possível gerenciar as credenciais do Módulo de segurança de hardware (HSM). Um HSM é um dispositivo PKCS#11 de terceiros que pode ser usado para gerar e armazenar chaves privadas com segurança. O HSM protege fisicamente o acesso e o uso das chaves privadas.

O software cliente é necessário para se comunicar com o HSM. O software cliente HSM deve ser instalado e configurado no mesmo computador que os formulários AEM.

AEM formulários O Digital Signatures pode usar credenciais armazenadas em um HSM para aplicar assinaturas digitais do lado do servidor. Siga as instruções desta seção para criar um alias para cada credencial do HSM que o Digital Signatures usará. O alias contém todos os parâmetros exigidos pelo HSM.

>[!NOTE]
>
>Depois de alterar a configuração do HSM, reinicie o servidor de formulários AEM.

## Crie um alias para uma credencial do HSM quando o dispositivo HSM estiver online {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM e, em seguida, clique em Adicionar.
1. Na caixa Nome do perfil, digite uma string usada para identificar o alias. Esse valor é usado como uma propriedade de algumas operações do Digital Signatures, como a operação Sign Signature Field .
1. Na caixa Biblioteca PKCS11, digite o caminho totalmente qualificado da biblioteca do cliente HSM no servidor. Por exemplo, `c:\Program Files\LunaSA\cryptoki.dll`. Em um ambiente em cluster, esse caminho deve ser idêntico para todos os servidores no cluster.
1. Clique em Testar conectividade HSM. Se AEM formulários conseguir se conectar ao dispositivo HSM, será exibida uma mensagem informando que o HSM está disponível. Clique em Avançar.
1. Use o Nome do token, a ID do slot ou o Índice da lista de slots para identificar onde as credenciais são armazenadas no HSM.

   * **Nome do token:** Corresponde ao nome da partição HSM a ser usada (por exemplo, HSMPART1).
   * **Id Do Slot:** A ID de slot é um identificador de slot do tipo de dados longo.
   * **Índice da lista de slots:** Se você selecionar Índice de lista de slots, defina as Informações do slot para um número inteiro que corresponda ao slot. Este é um índice baseado em 0, o que significa que se o cliente for registrado na partição HSMPART1 primeiro, HSMPART1 será chamado para usar o valor 0 SlotListIndex.

1. Na caixa Pino do token, digite a senha necessária para acessar a chave do HSM e clique em Avançar.
1. Na caixa Credenciais , selecione uma credencial. Clique em Salvar.

## Crie um alias para uma credencial do HSM quando o dispositivo HSM estiver offline {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM e, em seguida, clique em Adicionar.
1. Na caixa Nome do perfil, digite uma string usada para identificar o alias. Esse valor é usado como uma propriedade de algumas operações do Digital Signatures, como a operação Sign Signature Field .
1. Na caixa Biblioteca PKCS11, digite o caminho totalmente qualificado da biblioteca do cliente HSM no servidor. Por exemplo, `c:\Program Files\LunaSA\cryptoki.dll`. Em um ambiente em cluster, esse caminho deve ser idêntico para todos os servidores no cluster.
1. Marque a caixa de seleção Criação de perfil offline. Clique em Avançar.
1. Na lista Dispositivo HSM, selecione o fabricante do dispositivo HSM no qual a credencial está armazenada.
1. Na lista Tipo de slot, selecione Id de slot, Índice de slot ou Nome de token e especifique um valor na caixa Informações do slot. AEM formulários usa essas configurações para determinar onde as credenciais são armazenadas no HSM.

   * **Nome do token:** Corresponde a um nome de partição (por exemplo, HSMPART1).
   * **Id Do Slot:** A ID do slot é um número inteiro que corresponde ao slot, que, por sua vez, corresponde a uma partição. Por exemplo, o cliente (servidor de formulários) registrado com a partição HSMPART1 primeiro. Isso mapeia o slot 1 para a partição HSMPART1, para este cliente. Como HSMPART1 é a primeira partição registrada, a ID do slot é 1 e você define Informações do slot como 1.

      A ID do slot é definida cliente a cliente. Se você registrou uma segunda máquina em uma partição diferente (por exemplo, HSMPART2 no mesmo dispositivo HSM), então o slot 1 seria associado à partição HSMPART2 para esse cliente.

   * **Índice de slots:** Se você selecionar Índice de slots, defina as Informações do slot para um número inteiro que corresponda ao slot. Este é um índice baseado em 0, o que significa que se o cliente estiver registrado na partição HSMPART1 primeiro, o slot 1 será mapeado para HSMPART1 desse cliente. Como HSMPART1 é a primeira partição registrada, o Índice de Slot é 0.

1. Selecione uma dessas opções e forneça o caminho:

   * **Certificado**: (Não é necessário se estiver usando o SHA1) Clique em Procurar e localize o caminho para a chave pública da credencial que você está usando.
   * **Certificado SHA1:** (Não é necessário se estiver usando um certificado físico) Digite o valor SHA1 (impressão digital) do arquivo de chave pública (.cer) para a credencial que você está usando. Certifique-se de que não haja espaços usados no valor SHA1.

1. Na caixa Senha, digite a senha necessária para acessar a chave do HSM para obter as informações do slot e clique em Salvar.

## Exibir propriedades de alias de credenciais do HSM {#view-hsm-credential-alias-properties}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM.
1. Clique no nome do alias do alias da credencial para exibir as propriedades e clique em OK.

## Verifique o status de uma credencial do HSM {#check-the-status-of-an-hsm-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM.
1. Clique na caixa de seleção ao lado da credencial que deseja marcar e clique em Verificar status.

A coluna Status reflete o status atual da credencial. Em caso de falha, um X vermelho é exibido na coluna Status . Passe o mouse sobre o X para exibir uma dica de ferramenta contendo o motivo da falha.

## Atualizar propriedades de alias de credencial do HSM {#update-hsm-credential-alias-properties}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM.
1. Clique no nome do alias do alias da credencial.
1. Clique em Atualizar Credencial e atualize as configurações conforme necessário.

## Redefinir todas as conexões do HSM {#reset-all-hsm-connections}

Redefina as conexões abertas para um dispositivo HSM após qualquer interrupção na sessão de rede entre o servidor de formulários e o dispositivo HSM. Por exemplo, as interrupções podem ocorrer devido a uma interrupção da rede ou ao dispositivo HSM sendo colocado offline para uma atualização de software. Após uma interrupção, as conexões existentes são obsoletas e qualquer solicitação de assinatura em relação a essas conexões falha. Usar a opção Redefinir todas as conexões HSM limpa as conexões antigas.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM.
1. Clique em Redefinir todas as conexões do HSM.

## Excluir um alias de credencial do HSM {#delete-an-hsm-credential-alias}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais do HSM.
1. Marque as caixas de seleção das credenciais do HSM que deseja excluir, clique em Excluir e em OK.

## Configurar suporte remoto a HSM {#configure-remote-hsm-support}

O AEM forms usa um mecanismo IPC/RPC baseado em Serviços da Web. Esse mecanismo permite que AEM formulários usem um HSM instalado em um computador remoto. Para usar essa funcionalidade, instale o serviço da Web no computador remoto em que o HSM está instalado. Consulte [Configuração do suporte a HSM para formulários AEM ES usando Sun JDK na plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html)para obter mais informações.

Esse mecanismo não oferece suporte à criação on-line de perfis do HSM ou às verificações de status. No entanto, há duas maneiras de criar perfis HSM e executar verificações de status:

* Crie uma credencial de cliente do AEM forms transmitindo-a ao Certificado do Assinante. Siga as etapas em [Configuração do suporte a HSM para formulários AEM ES usando Sun JDK na plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html). O local do serviço da Web é passado como uma propriedade de Credencial. Perfis HSM offline criados usando o certificado ou o certificado SHA-1 hex também são suportados. No entanto, se você tiver atualizado para AEM formulários de uma versão anterior de AEM formulários, faça alterações no cliente porque a credencial continha informações de certificado e de serviço da Web.
* O local do serviço da Web é especificado no console de administração do serviço de assinatura. (Consulte [Configurações do serviço de assinatura](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) Aqui, o cliente carregava somente o alias do perfil do HSM no armazenamento confiável. Você pode usar essa opção sem alterações de clientes, mesmo se tiver atualizado para AEM formulários de uma versão anterior de AEM formulários. Essa opção não é compatível com perfis HSM usando o certificado SHA-1.
