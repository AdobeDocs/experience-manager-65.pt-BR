---
title: Configurar autenticação baseada em certificado
seo-title: Configuring certificate-based authentication
description: Importe um certificado da autoridade de certificação (CA) para o armazenamento de confiança e crie um mapeamento de certificado para autenticação baseada em certificado.
seo-description: Import a Certificate Authority (CA) certificate into the Trust Store and create a certificate mapping for certificate-based authentication.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Configurar autenticação baseada em certificado {#configuring-certificate-based-authentication}

O Gerenciamento de usuários geralmente realiza autenticação usando um nome de usuário e senha. O Gerenciamento de usuários também oferece suporte à autenticação por certificado, que pode ser usada para autenticar usuários por meio do Acrobat ou para autenticar usuários de forma programática. Para obter detalhes sobre a autenticação de usuários programática, consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Para usar a autenticação baseada em certificado, importe um certificado da Autoridade de certificação (CA) confiável no Armazenamento de confiança e crie um mapeamento de certificado.

## Importe o certificado CA {#import-the-ca-certificate}

Ao importar o certificado, selecione as opções Confiança para Autenticação de Certificado e Confiança para Identidade e quaisquer outras opções necessárias. Para obter detalhes sobre a importação de certificados, consulte [Gerenciar certificados](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configuração do mapeamento de certificado {#configuring-certificate-mapping}

Para ativar a autenticação baseada em certificado para usuários, crie um mapeamento de certificado. A *mapeamento de certificado* define um mapa entre os atributos de um certificado e os atributos dos usuários em um domínio. Você pode mapear mais de um certificado para o mesmo domínio.

Ao testar um certificado, o Gerenciamento de usuários faz upload do certificado para garantir que ele atenda aos seguintes requisitos:

* O certificado é válido.
* O Emissor especificado pode verificar o certificado.
* O certificado contém o atributo necessário para o mapeamento.
* O mapeamento especificado mapeia o certificado para apenas um usuário no banco de dados de formulários AEM. Os usuários atuais e obsoletos (excluídos) são verificados para determinar se correspondem aos critérios de mapeamento. Portanto, o teste de certificado falhará se mais de um usuário, incluindo usuários obsoletos, tiver o valor do atributo sendo considerado.

>[!NOTE]
>
>Não é possível editar um mapeamento de certificado existente.

**Adicionar um mapeamento de certificado**

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Mapeamento de certificados.
1. Clique em Novo mapeamento de certificado e, na lista Por emissor, selecione o alias do certificado conforme configurado no Gerenciamento de armazenamento de confiança.
1. Mapeie um dos atributos do certificado para o atributo de um usuário. Por exemplo, você pode mapear o nome comum do certificado para a ID de logon do usuário.

   Se o conteúdo do atributo no certificado for diferente do conteúdo no atributo do usuário no banco de dados de Gerenciamento de usuários, você poderá usar uma Expressão regular Java (regex) para corresponder aos dois atributos. Por exemplo, se os nomes comuns dos certificados forem nomes como *Alex Pink (Autenticação)* e *Alex Pink (Assinatura)* e o nome comum no banco de dados Gerenciamento de usuários é *Alex Pink*, use um regex para extrair a parte necessária do atributo certificate (neste exemplo, *Alex Pink*.) A expressão regular especificada deve estar em conformidade com a especificação regex do Java.

   Você pode transformar a expressão especificando a ordem dos grupos na caixa Ordem personalizada. A ordem personalizada é usada com a variável `java.util.regex.Matcher.replaceAll()` método . O comportamento visto corresponderá ao comportamento desse método e a string de entrada (a ordem personalizada) deverá ser especificada adequadamente.

   Para testar o regex, digite um valor na caixa Test Parameter e clique em Test.

   Você pode usar os seguintes caracteres no regex:

   * . (qualquer caractere)
   * &amp;ast; (0 ou mais ocorrências)
   * () (especifique o grupo entre parênteses)
   * \ (usado para escapar de um caractere regex para um caractere regular)
   * $n (usado para se referir ao enésimo grupo)

   Exemplos de expressões regulares:

   * Para extrair &quot;Alex Pink&quot; de &quot;Alex Pink (Autenticação)&quot;

      **Regex:** (.&amp;ast;) \(Autenticação\)

   * Para extrair &quot;Alex Pink&quot; de &quot;Alex (Autenticação) Pink&quot;

      **Regex:** (.&amp;ast;)\(Autenticação\) (.&amp;ast;)

   * Para extrair &quot;Alex rosa&quot; de &quot;Alex (Autenticação) rosa&quot;

      **Regex:** (.&amp;ast;)\(Autenticação\) (.&amp;ast;)

      Ordem personalizada: $2 $1 (retornar o segundo grupo, concatenado ao primeiro grupo, capturado pelo caractere de espaço em branco)

   * Para extrair &quot;apink@sampleorg.com&quot; de &quot;smtp:apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   Para obter detalhes sobre o uso de expressões regulares, consulte [Tutorial em Java sobre expressões regulares](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Na lista Para domínio, selecione o domínio do usuário.
1. Para testar essa configuração, clique em Procurar para carregar um certificado de usuário de amostra, clique em Testar certificado e, se a configuração estiver correta, clique em OK.

**Editar um mapeamento de certificado existente**

1. No Console de Administração, clique em Configurações > Gerenciamento de Usuário > Configuração.
1. Clique em Mapeamento de certificados.
1. Selecione o mapeamento de certificado para editar e editar sua configuração. Você pode atualizar a expressão regular e a ordem personalizada.
1. Para testar suas alterações, clique em Procurar para carregar um certificado de amostra, clique em Testar certificado e em OK.

**Excluir um mapeamento de certificado**

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Mapeamento de certificados.
1. Marque a caixa de seleção do mapeamento de certificado a ser excluído, clique em Excluir e em OK.
