---
title: Gerenciar credenciais locais
description: Saiba como gerenciar credenciais locais usando o Gerenciamento de armazenamento de confiança. Os formulários AEM são compatíveis com credenciais RSA e DSA no formulário PKCS12 padrão.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Gerenciar credenciais locais {#managing-local-credentials}

As credenciais locais são credenciais de chave privada hospedadas no Gerenciamento de Repositório de Confiança. A *credencial local* identifica onde a credencial DES de um usuário é armazenada. Usando o Gerenciamento de Armazenamento de Confiança, você pode importar e gerenciar suas credenciais locais usando, por exemplo, arquivos PFX existentes para poder importar, editar e excluir credenciais locais.

Os formulários AEM são compatíveis com credenciais RSA e DSA de até 4.096 bits no formato PKCS12 padrão (arquivos .pfx e .p12).

É possível importar e exportar qualquer número de credenciais. Se você quiser substituir uma credencial expirada usando o mesmo alias, exclua a credencial e importe a nova credencial com o mesmo alias.

Para obter informações e instruções relacionadas às extensões do Acrobat Reader DC, consulte [Configurar credenciais para usar com extensões do Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar uma credencial {#import-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar. Em Tipo de armazenamento de confiança, selecione uma destas opções:

   * **Credencial de assinatura de documento:** Uma credencial usada para emitir uma assinatura digital em um documento.
   * **Credencial de extensões do Acrobat Reader DC:** Um certificado digital específico para extensões do Acrobat Reader DC que permite que os direitos de uso do Adobe Reader sejam ativados nos documentos PDF produzidos.
   * **Padrão:** Indica que essa é a credencial padrão para usar com as extensões do Acrobat Reader DC.

   Para obter informações sobre como obter uma credencial, consulte [Preparação para instalar formulários AEM](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição da credencial nas Extensões da Acrobat Reader DC e no serviço de assinatura. Esse alias também é usado para acessar a credencial de forma programática usando o SDK de formulários AEM.

   >[!NOTE]
   >
   >O nome do alias é convertido automaticamente em maiúsculas para fins de exibição. O nome do alias não diferencia maiúsculas de minúsculas quando você faz referência a ele em um processo.

1. Clique em Procurar para localizar a credencial, digite a senha da credencial e clique em OK.

   Se a mensagem de erro &quot;Falha ao importar credencial devido a um formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

## Exportar uma credencial {#export-a-credential}

As credenciais são exportadas como arquivos P12 no formato PKCS#12.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que você deseja exportar e clique em Exportar.
1. Na caixa Senha, digite a senha. Essa senha é nova e é usada para criptografar a credencial exportada.
1. Clique em Exportar, siga as instruções para exportar a credencial e clique em OK.

## Editar um alias ou tipo de armazenamento de confiança da credencial {#edit-a-credential-s-alias-or-trust-store-type}

Depois que uma credencial for importada, você poderá editar seu nome de alias e tipo de armazenamento de confiança.

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique no nome do alias da credencial que deseja editar.
1. Clique em Atualizar credencial.
1. Edite o nome do alias e o tipo de armazenamento de confiança conforme necessário e clique em OK.

## Excluir uma credencial {#delete-a-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Marque as caixas de seleção das credenciais a serem excluídas.
1. Clique em Excluir e em OK.
