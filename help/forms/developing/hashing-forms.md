---
title: Como gerar e trabalhar com hashes em PDF forms dinâmicos?
description: Gerar e trabalhar com hash em PDF forms dinâmicas
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Gerar e trabalhar com hash em PDF forms dinâmicas {#generate-work-with-hashes-dynamic-pdf-forms}


## Conhecimento pré-requisito {#prerequisite-knowledge}

É necessária alguma experiência com o AEM Forms no JEE Designer, assim como a capacidade de acessar e chamar funções em objetos de script.

## Nível do usuário {#user-level}

Início

Quando quiser ocultar uma senha em seu formulário PDF e não quiser que ela fique em um texto claro no código fonte ou em qualquer outro lugar no documento PDF, saber como gerar e trabalhar com hashes MD4, MD5, SHA-1 e SHA-256 é fundamental.

A ideia é ofuscar a senha gerando um hash exclusivo e armazenar esse hash no documento PDF. Esse hash exclusivo pode ser gerado por diferentes funções de hash, e neste artigo mostrarei como gerá-las dentro do formulário PDF e como trabalhar com elas.

Uma função de hash utiliza uma longa string (ou mensagem) de qualquer comprimento como entrada e produz uma string de comprimento fixo como saída, às vezes chamada de resumo de mensagem ou impressão digital.

O AEM Forms no JEE Designer permite implementar as diferentes funções de hash em objetos de script como JavaScript e executá-las dentro de um documento PDF dinâmico. Os PDF de exemplo incluídos com os arquivos de amostra para este artigo usam implementações de código aberto das seguintes funções de hash:

* MD4 e MD5 - projetado por Ronald Rivest

* SHA-1 e SHA-256 - conforme definido pelo NIST

O maior benefício de usar hashes é que você não precisa comparar senhas diretamente ao comparar strings de texto claras; em vez disso, você pode comparar os dois hashes das duas senhas. Como é muito improvável que duas strings diferentes tenham o mesmo hash, se ambos os hashes forem idênticos, você poderá assumir que as strings comparadas (nesse caso, as senhas) também são idênticas.

>[!NOTE]
>
>Há alguns problemas de segurança conhecidos (chamados colisões de hash) com MD4 ou MD5. Devido a essas colisões de hash e outros hacks SHA-1 (incluindo mesas de arco-íris), decidi concentrar-me na função de hash SHA-256 na segunda amostra.  Para obter mais informações, consulte o [Colisão](https://en.wikipedia.org/wiki/Hash_collision) e [Tabela de arco-íris](https://en.wikipedia.org/wiki/Rainbow_table) páginas da Wikipédia.

## Exame dos objetos de script {#examining-script-objects}

Ao abrir uma das duas amostras fornecidas no AEM Forms no JEE Designer, você encontrará os quatro objetos de script na paleta Hierarquia (veja a Figura abaixo).

![Variáveis](assets/variables.jpg)

Para ver a implementação do JavaScript das funções de hash nesses objetos de script, selecione o objeto de script e explore o código no Editor de scripts.  Você pode ver como cada uma das seguintes funções de hash foi implementada:

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

Como você pode ver nesta lista, há diferentes funções disponíveis para os diferentes tipos de saída do hash. Você pode escolher entre `hex_` para dígitos hexadecimais, `b64_` para saída codificada em Base64, ou `str_` para codificação de sequência simples.

Dependendo da função de hash escolhida, o comprimento do hash varia:

* MD4: 128 bits
* MD5: 128 bits
* SHA-1: 160 bits
* SHA-256: 256 bits

## Tentar os PDF forms de amostra {#try-sample-pdf-forms}

Os arquivos de amostra para este artigo incluem duas PDF forms. A primeira amostra permite digitar uma string e gerar valores de hash MD4, MD5, SHA-1 e SHA-256 para a string.  A segunda amostra é um formulário simples que desbloqueia campos de texto se uma senha correta for inserida.

### Exemplo 1: geração de hashes {#generating-dashes}

Siga as etapas abaixo para tentar a primeira amostra:

1. Após baixar e descompactar os arquivos de amostra, abra o hashing_forms_sample1.pdf com AEM Forms no JEE Designer. Como alternativa, você pode usar o Adobe Reader ou o Adobe Acrobat Professional para abrir e exibir a amostra, mas não poderá ver o código-fonte.
1. No campo de texto rotulado [!UICONTROL limpar texto] digite uma senha ou qualquer outra mensagem com hash.
1. Clique em um dos quatro botões para gerar o hash MD4, MD5, SHA-1 ou SHA-256. Dependendo do botão pressionado, uma das quatro funções de hash que produzem saída hexadecimal é chamada e sua string ou mensagem é colocada em hash.

O resultado da operação de hash é exibido no campo rotulado [!UICONTROL hash]. O comprimento do hash varia dependendo da função de hash escolhida.

Todas as amostras usam dígitos hexadecimais como tipo de saída. Você pode usar o Editor de scripts para modificar as amostras e alterar o tipo de saída para Base64 ou String simples.

### Exemplo 2: senhas correspondentes {#matching-passwords}

A segunda amostra demonstra como os hashes são comparados em segundo plano, sem precisar revelar a senha real. A senha digitada tem hash. A senha real, que é armazenada em um campo invisível, também tem hash. A senha é segura não porque é invisível, mas porque foi hash. Como é impossível reconstruir a senha a partir do valor com hash, é seguro expor a senha em forma com hash. A comparação é feita apenas entre os hashes, não entre as senhas em um texto claro. Se ambos os hashes forem iguais, você poderá assumir que as senhas são idênticas.

Siga as etapas abaixo para tentar a segunda amostra:

1. Abrir `hashing_forms_sample2.pdf` com o AEM Forms no JEE Designer. Como alternativa, você pode usar o Adobe Reader ou o Adobe Acrobat Professional para abrir e exibir a amostra, mas não poderá ver o código-fonte.
1. Escolha um dos dois campos de senha rotulados [!UICONTROL Senha] ou [!UICONTROL Senha MULHER] e digite as senhas:
   1. A senha do homem é `bob`
   1. A senha da mulher é `alice`
1. Quando você move o foco para fora dos campos de senha ou pressiona a tecla Enter, o hash da senha inserida é gerado automaticamente e é comparado ao hash armazenado da senha correta em segundo plano. As senhas com hash corretas são armazenadas nos campos de texto invisíveis rotulados `passwd_man_hashed` e `passwd_woman_hashed`. Se você digitar a senha correta para o homem, os campos de texto serão rotulados `Man 1` e `Man 2` são acessíveis para que você possa digitar o texto neles. O mesmo se aplica aos campos femininos.
1. Como opção, você pode clicar no botão chamado &quot;excluir senhas&quot;, que desativará os campos de texto e alterará sua borda.

O código para comparar os dois valores com hash e ativar os campos de texto é simples:

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Onde ir daqui {#next-steps}

Onde você precisaria de algo assim? Considere um formulário PDF que tenha campos que devem ser preenchidos apenas por indivíduos autorizados. Ao proteger esses campos com uma senha, que não pode ser vista em texto nítido em qualquer lugar do documento como em Sample_2.pdf, você pode garantir que esses campos sejam acessíveis somente para usuários que conhecem a senha.

Eu encorajo você a continuar explorando os dois arquivos PDF de amostra.  Você pode gerar novos valores de hash com Sample_1.pdf e usar os valores gerados para alterar a senha ou a função de hash usada em Sample_2.pdf.  Os recursos listados na seção Atribuições também fornecem informações adicionais sobre o hash e as implementações específicas do JavaScript usadas neste artigo.

## Atribuições {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Colisão de hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Mesa-arco-íris](https://en.wikipedia.org/wiki/Rainbow_table)
* [Página inicial do projeto JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [página inicial do projeto jsSHA2](https://anmar.eu.org/projects/jssha2/)
