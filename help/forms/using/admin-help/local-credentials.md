---
title: Gerenciamento de credenciais locais
seo-title: Gerenciamento de credenciais locais
description: Saiba como gerenciar credenciais locais.
seo-description: Saiba como gerenciar credenciais locais.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Gerenciando credenciais locais {#managing-local-credentials}

As credenciais locais são credenciais de chave privada hospedadas no Gerenciamento de Armazenamento de Confiança. Uma *credencial local* identifica onde a credencial DES de um usuário é armazenada. Usando o Gerenciamento de armazenamento confiável, você pode importar e gerenciar suas credenciais locais usando, por exemplo, arquivos PFX existentes para que possa importar, editar e excluir credenciais locais.

AEM formulários oferecem suporte a credenciais RSA e DSA de até 4096 bits no formato PKCS12 padrão (arquivos .pfx e .p12).

É possível importar e exportar qualquer número de credenciais. Se quiser substituir uma credencial expirada usando o mesmo alias, exclua a credencial e importe a nova credencial com o mesmo alias.

Para obter informações e instruções relacionadas às extensões do Acrobat Reader DC, consulte [Configurar credenciais para uso com extensões do Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar uma credencial {#import-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar. Em Tipo de armazenamento confiável, selecione uma destas opções:

   * **Credencial de assinatura do documento:** uma credencial usada para emitir uma assinatura digital em um documento.
   * **Credencial de extensões do Acrobat Reader DC:** Um certificado digital específico para extensões do Acrobat Reader DC que permite que os direitos de uso do Adobe Reader sejam ativados nos documentos PDF produzidos.
   * **Padrão:** Indica que esta é a credencial padrão a ser usada com extensões do Acrobat Reader DC.

   Para obter informações sobre como obter uma credencial, consulte [Preparação para instalar formulários AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição para a credencial nas extensões do Acrobat Reader DC e no serviço de assinatura. Esse alias também é usado para acessar a credencial de forma programática usando o SDK de formulários AEM.

   >[!NOTE]
   >
   >O nome do alias é convertido automaticamente em maiúsculas para fins de exibição. O nome do alias não faz distinção entre maiúsculas e minúsculas quando você faz referência a ele em um processo.

1. Clique em Procurar para localizar a credencial, digite a senha da credencial e clique em OK.

   Se a mensagem de erro &quot;Falha ao importar credenciais devido a um formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

## Exportar uma credencial {#export-a-credential}

As credenciais são exportadas como arquivos P12 no formato PKCS#12.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que deseja exportar e clique em Exportar.
1. Na caixa Senha, digite a senha. Esta senha é nova e é usada para criptografar a credencial exportada.
1. Clique em Exportar, siga as instruções para exportar a credencial e clique em OK.

## Editar o alias ou o tipo de armazenamento de confiança de uma credencial {#edit-a-credential-s-alias-or-trust-store-type}

Depois que uma credencial é importada, você pode editar o nome do alias e o tipo de armazenamento confiável.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que deseja editar.
1. Clique em Atualizar credencial.
1. Edite o nome do alias e o tipo de armazenamento confiável, conforme necessário, e clique em OK.

## Excluir uma credencial {#delete-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Marque as caixas de seleção das credenciais a serem excluídas.
1. Clique em Excluir e em OK.

