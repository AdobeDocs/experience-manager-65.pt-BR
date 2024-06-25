---
title: Como gerar e trabalhar com hashes em PDF forms dinâmicos?
description: Gerar e trabalhar com hashes em PDF forms dinâmicos.
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Gerar e trabalhar com hashes em PDF forms dinâmicos {#generate-work-with-hashes-dynamic-pdf-forms}

## Conhecimento de pré-requisito {#prerequisite-knowledge}

É necessária alguma experiência com o AEM Forms no JEE Designer, assim como a capacidade de acessar e chamar funções em objetos de script.

## Nível do usuário {#user-level}

Início

Quando quiser ocultar uma senha no formulário PDF e não quiser que ela fique em texto não criptografado dentro do código-fonte ou em qualquer outro lugar no documento PDF, é importante saber como gerar e trabalhar com hashes MD4, MD5, SHA-1 e SHA-256.

A ideia é ofuscar a senha gerando um hash exclusivo e armazenando esse hash no documento PDF. Esse hash exclusivo pode ser gerado por diferentes funções de hash e, neste artigo, é mostrado como gerá-los dentro do formulário PDF e como trabalhar com eles.

Uma função hash pega uma longa string (ou mensagem) de qualquer comprimento como entrada e produz uma string de comprimento fixo como saída, às vezes chamada de resumo da mensagem ou impressão digital.

O AEM Forms no JEE Designer permite implementar as diferentes funções de hash em objetos de script como JavaScript e executá-las dentro de um documento PDF dinâmico. Os PDF de de exemplo incluídos nos arquivos de amostra deste artigo usam implementações de código aberto das seguintes funções de hash:

* MD4 e MD5 - projetados por Ronald Rivest

* SHA-1 e SHA-256 - como são definidos pelo NIST

O maior benefício de usar hashes é que você não precisa comparar senhas diretamente comparando strings de texto claras; em vez disso, você pode comparar os dois hashes das duas senhas. Como é improvável que duas strings diferentes tenham o mesmo hash, se ambos os hashes forem idênticos, você pode supor que as strings comparadas (nesse caso, as senhas) também sejam idênticas.

>[!NOTE]
>
>Existem alguns problemas de segurança bem conhecidos (as chamadas colisões de hash) com MD4 ou MD5. Devido a essas colisões de hash e outros hacks SHA-1 (incluindo tabelas de arco-íris), decidi me concentrar na função hash SHA-256 na segunda amostra. Para obter mais informações, consulte [Colisão](https://en.wikipedia.org/wiki/Hash_collision) e [Tabela de Arco-íris](https://en.wikipedia.org/wiki/Rainbow_table) páginas da Wikipédia.

## Examinando os objetos de script {#examining-script-objects}

Ao abrir uma das duas amostras fornecidas no AEM Forms no JEE Designer, você encontrará os quatro objetos de script na paleta Hierarquia (consulte a Figura abaixo).

![Variáveis](assets/variables.jpg)

Para ver a implementação JavaScript das funções de hash nesses objetos de script, selecione o objeto de script e explore o código no Editor de scripts. Você pode ver como cada uma das seguintes funções de hash foi implementada:

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

Como você pode ver nessa lista, há diferentes funções disponíveis para os diferentes tipos de saída do hash. Você pode escolher entre `hex_` para dígitos hexadecimais, `b64_` para saída codificada em Base64, ou `str_` para codificação de sequência simples.

Dependendo da função de hash escolhida, o comprimento do hash varia:

* MD4: 128 bits
* MD5: 128 bits
* SHA-1: 160 bits
* SHA-256: 256 bits

## Experimentar os PDF forms de amostra {#try-sample-pdf-forms}

Os arquivos de exemplo deste artigo incluem dois PDF forms. A primeira amostra permite digitar uma cadeia de caracteres e gerar valores de hash MD4, MD5, SHA-1 e SHA-256 para a cadeia de caracteres. O segundo exemplo é um formulário simples que desbloqueia campos de texto se uma senha correta for inserida.

### Exemplo 1: geração de hashes {#generating-dashes}

Siga as etapas abaixo para experimentar a primeira amostra:

1. Depois de baixar e descompactar os arquivos de amostra, abra hashing_forms_sample1.pdf com o AEM Forms no JEE Designer. Como alternativa, você pode usar o Adobe Reader ou o Adobe Acrobat Professional para abrir e exibir a amostra, mas não é possível ver o código-fonte.
1. No campo de texto rotulado [!UICONTROL limpar texto] digite uma senha ou qualquer outra mensagem que você deseja que seja transformada em hash.
1. Clique em um dos quatro botões para gerar o hash MD4, MD5, SHA-1 ou SHA-256. Dependendo do botão pressionado, uma das quatro funções de hash que produzem saída hexadecimal é chamada e a cadeia de caracteres ou mensagem é transformada em hash.

O resultado da operação de hash é exibido no campo [!UICONTROL hash]. O comprimento do hash varia dependendo da função de hash escolhida.

Todas as amostras usam dígitos hexadecimais como tipo de saída. Você pode usar o Editor de scripts para modificar as amostras e alterar o tipo de saída para Base64 ou String simples.

### Exemplo 2: senhas correspondentes {#matching-passwords}

A segunda amostra demonstra como os hashes são comparados em segundo plano, sem precisar revelar a senha real. A senha digitada está com hash. A senha real, que é armazenada em um campo invisível, também tem hash. A senha é segura não porque está invisível, mas porque foi transformada em hash. Como é impossível reconstruir a senha a partir do valor com hash, é seguro expor a senha no formato com hash. A comparação é feita somente entre os hashes, não entre as senhas em texto não criptografado. Se os dois hashes forem os mesmos, você poderá supor que as senhas sejam idênticas.

Siga as etapas abaixo para experimentar a segunda amostra:

1. Abertura `hashing_forms_sample2.pdf` com o AEM Forms no JEE Designer. Como alternativa, você pode usar o Adobe Reader ou o Adobe Acrobat Professional para abrir e exibir a amostra, mas não é possível ver o código-fonte.
1. Escolha um dos dois campos de senha [!UICONTROL Senha MAN] ou [!UICONTROL Senha WOMAN] e digite as senhas:
   1. A senha do homem é `bob`
   1. A senha da mulher é `alice`
1. Quando você move o foco para fora dos campos de senha ou pressiona a tecla Enter, o hash da senha que você digitou é gerado automaticamente e é comparado com o hash armazenado da senha correta em segundo plano. As senhas corretas com hash são armazenadas nos campos de texto invisíveis rotulados `passwd_man_hashed` e `passwd_woman_hashed`. Se você digitar a senha correta para o manual, os campos de texto rotulados `Man 1` e `Man 2` ficam acessíveis para que você possa digitar texto neles. O mesmo se aplica aos campos da mulher.
1. Como opção, você pode clicar no botão &quot;excluir senhas&quot;, que desativará os campos de texto e alterará sua borda.

O código para comparar os dois valores com hash e habilitar os campos de texto é simples:

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Aonde ir daqui {#next-steps}

Onde você precisaria de algo assim? Considere um formulário PDF que tenha campos que só devem ser preenchidos por indivíduos autorizados. Protegendo esses campos com uma senha, que não pode ser vista em texto não criptografado em nenhum lugar do documento, como em Sample_2.pdf, você pode garantir que esses campos estejam acessíveis somente para usuários que conhecem a senha.

Recomendo que você continue explorando os dois arquivos PDF de amostra.  Você pode gerar novos valores de hash com Sample_1.pdf e usar os valores gerados para alterar a senha ou a função de hash usada em Sample_2.pdf.  Os recursos listados na seção Atribuições também fornecem informações adicionais sobre hash e as implementações específicas do JavaScript usadas neste artigo.

## Atribuições {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Colisão de hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Tabela de arco-íris](https://en.wikipedia.org/wiki/Rainbow_table)
* [Página inicial do projeto JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [Página inicial do projeto jsSHA2](https://anmar.eu.org/projects/jssha2/)
