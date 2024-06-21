---
title: Configurar credenciais para usar com extensões do Acrobat Reader DC
description: Saiba como configurar credenciais para usar com extensões do Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Configurar credenciais para usar com extensões do Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar direitos de uso a documentos do PDF, configure formulários AEM com uma credencial válida para extensões do Acrobat Reader DC. Uma credencial pode ter sido configurada durante a instalação de formulários AEM. Se você não tiver configurado sua credencial do Acrobat Reader DC Extensions ao executar o Configuration Manager ou se precisar importar uma credencial nova ou substituta, poderá fazê-lo usando as páginas Gerenciamento de Trust Store.

Se estiver usando uma credencial de avaliação, substitua-a por uma credencial de produção ao migrar para o ambiente de produção. Para atualizar uma credencial expirada ou de avaliações, primeiro exclua a credencial antiga de extensões do Acrobat Reader DC.

Para obter informações sobre como obter uma credencial, consulte [Preparação para instalar formulários AEM (servidor único)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

O armazenamento de confiança pode conter mais de uma credencial de extensões Acrobat Reader DC. Designe uma dessas credenciais como a credencial default de Extensões de Reader. A credencial padrão é usada quando um usuário do Workbench não consegue determinar qual credencial usar durante a criação do processo. Estas regras se aplicam às credenciais padrão:

* Se você importar uma credencial de extensões do Acrobat Reader DC e o armazenamento de confiança não contiver outras credenciais de extensões do Acrobat Reader DC, ela será definida como padrão.
* Se você importar uma credencial de extensões do Acrobat Reader DC com a opção Padrão selecionada, o tipo padrão será removido de uma credencial padrão existente. A credencial importada se torna o padrão.
* Não é possível excluir uma credencial padrão de extensões do Acrobat Reader DC. Para excluir a credencial padrão, primeiro defina outra credencial como padrão. Uma exceção a essa regra é que, se houver apenas uma credencial, você poderá excluí-la, mesmo que seja o padrão.
* Não é possível atualizar uma credencial padrão de extensões do Acrobat Reader DC.

>[!NOTE]
>
>Você também pode importar e excluir credenciais de forma programática. (Consulte [Programação com formulários AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR).)

## Importar uma credencial de extensões do Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar e, em Tipo de armazenamento de confiança, selecione Credencial de extensões do Acrobat Reader DC.
1. (Opcional) Para indicar que essa credencial é a padrão para usar com extensões do Acrobat Reader DC, selecione Padrão.
1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição da credencial nas extensões do Acrobat Reader DC. Esse alias também é usado para acessar a credencial de forma programática usando o SDK de formulários AEM.

   >[!NOTE]
   >
   >O nome do alias é convertido automaticamente em maiúsculas para fins de exibição. O nome do alias não diferencia maiúsculas de minúsculas quando você faz referência a ele em um processo.

1. Clique em Escolher Arquivo para localizar a credencial, digite a senha da credencial e clique em OK.

   Se a mensagem de erro &quot;Falha ao importar credencial devido a um formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

## Remover uma credencial de extensões do Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Selecione a credencial e clique em Excluir.

## Substituir uma credencial de extensões do Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Anote o alias da credencial existente, selecione-o e clique em Excluir.
1. Importe a nova credencial usando exatamente o mesmo nome de alias.
