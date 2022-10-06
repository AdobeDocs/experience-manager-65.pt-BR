---
title: Gerenciamento de credenciais locais
seo-title: Managing local credentials
description: Saiba como gerenciar credenciais locais.
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Gerenciamento de credenciais locais {#managing-local-credentials}

As credenciais locais são credenciais de chave privada hospedadas no Gerenciamento de Armazenamento de Confiança. A *credencial local* identifica onde a credencial DES de um usuário é armazenada. Usando o Gerenciamento de armazenamento de confiança, você pode importar e gerenciar suas credenciais locais usando, por exemplo, arquivos PFX existentes, para que possa importar, editar e excluir credenciais locais.

AEM formulários oferecem suporte às credenciais RSA e DSA de até 4096 bits no formato PKCS12 padrão (arquivos .pfx e .p12).

É possível importar e exportar qualquer número de credenciais. Se quiser substituir uma credencial expirada usando o mesmo alias, exclua a credencial e importe a nova credencial com o mesmo alias.

Para obter informações e instruções relacionadas às extensões do Acrobat Reader DC, consulte [Configurar credenciais para uso com extensões do Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar uma credencial {#import-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar. Em Tipo de Armazenamento de Confiança, selecione uma destas opções:

   * **Credencial de assinatura de documento:** Uma credencial usada para emitir uma assinatura digital em um documento.
   * **Credencial de extensões do Acrobat Reader DC:** Um certificado digital específico para extensões do Acrobat Reader DC que permite que direitos de uso do Adobe Reader sejam ativados nos documentos do PDF produzidos.
   * **Padrão:** Indica que esta é a credencial padrão a ser usada com as extensões do Acrobat Reader DC.

   Para obter informações sobre como obter uma credencial, consulte [Preparação para instalar formulários AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição para a credencial nas extensões do Acrobat Reader DC e no serviço de assinatura. Esse alias também é usado para acessar a credencial de forma programática usando o SDK dos formulários AEM.

   >[!NOTE]
   >
   >O nome do alias é convertido automaticamente em maiúsculas para fins de exibição. O nome do alias não diferencia maiúsculas de minúsculas quando você faz referência a ele em um processo.

1. Clique em Procurar para localizar a credencial, digite a senha da credencial e clique em OK.

   Se a mensagem de erro &quot;Falha ao importar credencial devido a um formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

## Exportar uma credencial {#export-a-credential}

As credenciais são exportadas como arquivos P12 no formato PKCS#12.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que deseja exportar e clique em Exportar.
1. Na caixa Senha, digite a senha. Essa senha é nova e é usada para criptografar a credencial exportada.
1. Clique em Exportar, siga as instruções para exportar a credencial e clique em OK.

## Editar o alias ou o tipo de armazenamento de confiança de uma credencial {#edit-a-credential-s-alias-or-trust-store-type}

Depois que uma credencial é importada, você pode editar o nome do alias e o tipo de armazenamento de confiança.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que deseja editar.
1. Clique em Atualizar Credencial.
1. Edite o nome do alias e o tipo de armazenamento de confiança conforme necessário e clique em OK.

## Excluir uma credencial {#delete-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Marque as caixas de seleção das credenciais a serem excluídas.
1. Clique em Excluir e em OK.
