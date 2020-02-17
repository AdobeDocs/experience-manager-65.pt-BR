---
title: Configurar credenciais para uso com extensões do Acrobat Reader DC
seo-title: Configurar credenciais para uso com extensões do Acrobat Reader DC
description: Saiba como configurar credenciais para uso com extensões do Acrobat Reader DC.
seo-description: Saiba como configurar credenciais para uso com extensões do Acrobat Reader DC.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar credenciais para uso com extensões do Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar direitos de uso a documentos PDF, configure formulários AEM com uma credencial válida para extensões do Acrobat Reader DC. Uma credencial pode ter sido configurada durante a instalação dos formulários AEM. Se você não configurou a credencial de extensões do Acrobat Reader DC ao executar o Configuration Manager ou se precisar importar uma credencial nova ou de substituição, poderá fazê-lo usando as páginas de Gerenciamento de armazenamento de confiança.

Se você estiver usando uma credencial de avaliação, substitua-a por uma credencial de produção ao mudar para o ambiente de produção. Para atualizar uma credencial expirada ou de avaliações, primeiro exclua a credencial antiga de extensões do Acrobat Reader DC.

Para obter informações sobre como obter uma credencial, consulte [Preparação para instalar formulários AEM (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

O Armazenamento de confiança pode conter mais de uma credencial de extensões do Acrobat Reader DC. Você deve designar uma dessas credenciais como a credencial padrão do Reader Extensions. A credencial padrão é usada quando um usuário do Workbench não consegue determinar qual credencial usar durante a criação do processo. Essas regras se aplicam às credenciais padrão:

* Se você importar uma credencial de extensões do Acrobat Reader DC e o Trust Store não contiver outras credenciais de extensões do Acrobat Reader DC, ela será definida como padrão.
* Se você importar uma credencial de extensões do Acrobat Reader DC com a opção Padrão selecionada, o tipo padrão será removido de uma credencial padrão existente. A credencial importada se torna o padrão.
* Não é possível excluir uma credencial padrão de extensões do Acrobat Reader DC. Para excluir a credencial padrão, primeiro defina outra credencial como padrão. Uma exceção a essa regra é que se houver apenas uma credencial, você poderá excluí-la mesmo que ela seja o padrão.
* Não é possível atualizar uma credencial de extensões padrão do Acrobat Reader DC.

>[!NOTE]
>
>Também é possível importar e excluir credenciais de forma programática. (Consulte [Programação com formulários](https://www.adobe.com/go/learn_aemforms_programming_63)AEM.)

## Importar uma credencial de extensões do Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Clique em Importar e, em Tipo de armazenamento confiável, selecione Credencial de extensões do Acrobat Reader DC.
1. (Opcional) Para indicar que essa credencial é a credencial padrão a ser usada com extensões do Acrobat Reader DC, selecione Padrão.
1. Na caixa Alias, digite um identificador para a credencial. Esse identificador é usado como o nome de exibição para a credencial nas extensões do Acrobat Reader DC. Esse alias também é usado para acessar a credencial de forma programática usando o SDK de formulários do AEM.

   >[!NOTE]
   >
   >O nome do alias é convertido automaticamente em maiúsculas para fins de exibição. O nome do alias não faz distinção entre maiúsculas e minúsculas quando você faz referência a ele em um processo.

1. Clique em Escolher arquivo para localizar a credencial, digite a senha da credencial e clique em OK.

   Se a mensagem de erro &quot;Falha ao importar credenciais devido ao formato de arquivo incorreto ou senha incorreta&quot; for exibida, verifique se a senha é válida.

## Remover uma credencial de extensões do Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Selecione a credencial e clique em Excluir.

## Substituir uma credencial de extensões do Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Credenciais locais.
1. Anote o alias da credencial existente e selecione-o e clique em Excluir.
1. Importe a nova credencial usando exatamente o mesmo nome de alias.

