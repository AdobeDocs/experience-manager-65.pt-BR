---
title: Configurando a autenticação baseada em certificado
seo-title: Configurando a autenticação baseada em certificado
description: Importe um certificado da autoridade de certificação (CA) para o armazenamento de confiança e crie um mapeamento de certificado para autenticação baseada em certificado.
seo-description: Importe um certificado da autoridade de certificação (CA) para o armazenamento de confiança e crie um mapeamento de certificado para autenticação baseada em certificado.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---


# Configurando a autenticação baseada em certificado {#configuring-certificate-based-authentication}

O Gerenciamento de usuários geralmente realiza a autenticação usando um nome de usuário e senha. O Gerenciamento de usuários também oferece suporte à autenticação baseada em certificados, que você pode usar para autenticar usuários por meio do Acrobat ou para autenticar usuários de forma programática. Para obter detalhes sobre a autenticação programática de usuários, consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Para usar autenticação baseada em certificado, importe um certificado da autoridade de certificação (CA) confiável no armazenamento confiável e crie um mapeamento de certificado.

## Importar o certificado CA {#import-the-ca-certificate}

Ao importar o certificado, selecione as opções Confiar na autenticação do certificado e Confiar na identidade e quaisquer outras opções necessárias. Para obter detalhes sobre como importar certificados, consulte [Gerenciar certificados](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurando o mapeamento de certificado {#configuring-certificate-mapping}

Para ativar a autenticação baseada em certificados para usuários, crie um mapeamento de certificado. Um *mapeamento de certificado* define um mapa entre os atributos de um certificado e os atributos de usuários em um domínio. É possível mapear mais de um certificado para o mesmo domínio.

Ao testar um certificado, o Gerenciamento de usuários carrega as verificações do certificado para garantir que ele atenda aos seguintes requisitos:

* O certificado é válido.
* O Emissor especificado pode verificar o certificado.
* O certificado contém o atributo necessário para mapeamento.
* O mapeamento especificado mapeia o certificado para apenas um usuário no banco de dados de formulários AEM. Os usuários atuais e obsoletos (excluídos) são verificados para determinar se correspondem aos critérios de mapeamento. Portanto, o teste de certificado falhará se mais de um usuário, incluindo usuários obsoletos, tiver o valor do atributo sendo considerado.

>[!NOTE]
>
>Não é possível editar um mapeamento de certificado existente.

**Adicionar um mapeamento de certificado**

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Mapeamento de certificados.
1. Clique em Novo mapeamento de certificado e, na lista Para emissor, selecione o alias de certificado conforme configurado no Gerenciamento de armazenamento de confiança.
1. Mapeie um dos atributos do certificado para o atributo do usuário. Por exemplo, é possível mapear o nome comum do certificado para a ID de logon do usuário.

   Se o conteúdo do atributo no certificado for diferente do conteúdo no atributo do usuário no banco de dados Gerenciamento de usuários, você poderá usar uma Expressão regular Java (regex) para corresponder aos dois atributos. Por exemplo, se os nomes comuns dos certificados forem nomes como *Alex Pink (Autenticação)* e *Alex Pink (Assinatura)* e o nome comum no banco de dados Gerenciamento de usuários for *Alex Pink*, você usará um regex para extrair a parte necessária do atributo de certificado (neste exemplo, *Alex Pink*.) A expressão regular especificada deve estar em conformidade com a especificação regex do Java.

   É possível transformar a expressão especificando a ordem dos grupos na caixa Ordem personalizada. A ordem personalizada é usada com o método `java.util.regex.Matcher.replaceAll()`. O comportamento que é visto corresponderá ao comportamento desse método, e a string de entrada (a ordem personalizada) deve ser especificada de acordo.

   Para testar o regex, digite um valor na caixa Parâmetro de teste e clique em Testar.

   Você pode usar os seguintes caracteres no regex:

   * . (qualquer caractere)
   * &amp;ast; (0 ou mais ocorrências)
   * () (especificar o grupo entre parênteses)
   * \ (usado para escapar de um caractere regex para um caractere regular)
   * $n (usado para se referir ao enésimo grupo)

   Exemplos de expressões regulares:

   * Para extrair &quot;Alex Pink&quot; de &quot;Alex Pink (Autenticação)&quot;

      **Regex:** (.&amp;ast;) \(Autenticação\)

   * Para extrair &quot;Alex Pink&quot; de &quot;Alex (Autenticação) Pink&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * Para extrair &quot;Alex Rosa&quot; de &quot;Alex (Autenticação) Rosa&quot;

      **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

      Ordem personalizada: $2 $1 (retornar o segundo grupo, concatenado para o primeiro grupo, capturado pelo caractere de espaço em branco)

   * Para extrair &quot;apink@sampleorg.com&quot; de &quot;smtp:apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   Para obter detalhes sobre como usar expressões regulares, consulte [tutorial Java sobre expressões regulares](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Na lista Para domínio, selecione o domínio do usuário.
1. Para testar essa configuração, clique em Procurar para fazer upload de um certificado de usuário de amostra, clique em Testar certificado e, se a configuração estiver correta, clique em OK.

**Editar um mapeamento de certificado existente**

1. No Console de administração, clique em Configurações > Gerenciamento de usuário > Configuração.
1. Clique em Mapeamento de certificados.
1. Selecione o mapeamento do certificado para editar e editar sua configuração. Você pode atualizar a expressão regular e a ordem personalizada.
1. Para testar as alterações, clique em Procurar para carregar um certificado de amostra, clique em Testar certificado e, em seguida, clique em OK.

**Excluir um mapeamento de certificado**

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Mapeamento de certificados.
1. Marque a caixa de seleção para o mapeamento de certificado a ser excluído, clique em Excluir e, em seguida, clique em OK.

