---
title: Noções básicas sobre os processos do AEM Forms
seo-title: Noções básicas sobre os processos do AEM Forms
description: Noções básicas sobre os processos do AEM Forms
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# Noções básicas sobre os processos do AEM Forms {#understanding-aem-forms-processes}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Um caso de uso comum é um conjunto de serviços da AEM Forms operarem em um único documento. Você pode enviar uma solicitação para o contêiner de serviço criando um processo usando o Workbench. Um processo representa um processo de negócios que você está automatizando. Para obter informações sobre como criar processos, consulte [Usar Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando um processo é ativado, ele se torna um serviço e pode ser chamado como outros serviços. Uma diferença entre um serviço padrão, como o Serviço de criptografia e um serviço originado de um processo, é que o último tem uma operação que executa muitas ações. Por outro lado, um serviço padrão tem muitas operações. Cada operação normalmente executa uma ação, como aplicar uma política a um documento ou criptografar um documento.

Os processos podem ter vida curta ou longa. Um processo de duração curta é uma operação executada de forma síncrona e no mesmo thread de execução a partir da qual foi invocada. As operações de curta duração são comparáveis ao comportamento padrão encontrado na maioria das linguagens de programação, onde um aplicativo cliente chama um método e aguarda um valor de retorno.

No entanto, há situações em que um processo não pode ser concluído de forma síncrona devido a fatores como estes:

* Um processo pode abranger uma quantidade significativa de tempo.
* Um processo pode estender-se por limites organizacionais.
* Um processo precisa de entrada externa para ser concluído. Por exemplo, considere uma situação em que um formulário é enviado para um gerente que está fora do escritório. Nessa situação, o processo não é concluído até que o gerente retorne e preencha o formulário.

   Esses tipos de processos são conhecidos como processos de longa duração. Um processo de longa duração é executado de forma assíncrona, permitindo que os sistemas interajam como os recursos permitem e permitindo o rastreamento e o monitoramento da operação. Quando um processo de longa duração é chamado, o AEM Forms cria um valor de identificador de invocação como parte de um registro que rastreia o status do processo de longa duração. O registro é armazenado no banco de dados do AEM Forms. Você pode limpar registros de processos de longa duração quando não forem mais necessários.

>[!NOTE]
>
>O AEM Forms não cria um registro quando um processo de duração curta é chamado.

Usando o valor do identificador de invocação , você pode rastrear o status do processo de longa duração. Por exemplo, você pode usar o valor do identificador de invocação de processo para executar operações do Process Manager, como encerrar uma instância de processo em execução.

**Exemplo de processo de duração curta**

A ilustração a seguir é um exemplo de um processo de duração curta chamado *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para seguir junto com os exemplos de código que discutem como invocar esse processo, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo de duração curta é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não seguro passado para o processo como um valor de entrada.
1. Criptografa o documento PDF com uma senha. O nome do parâmetro de entrada para esse processo é `inDoc` e o tipo de dados é document.
1. Salva o documento PDF criptografado por senha como um arquivo PDF no sistema de arquivos local. Esse processo retorna o documento PDF criptografado como um valor de saída. O nome do parâmetro de saída para esse processo é `outDoc` e o tipo de dados é document.

   Esse processo é concluído de forma síncrona no mesmo thread de execução do qual foi chamado. O nome desse processo de duração curta é `MyApplication/EncryptDocument`e sua operação é `invoke`.

   >[!NOTE]
   >
   >Normalmente, um processo de duração curta consiste em mais de três ações. Você cria um processo usando o Workbench. (Consulte [Usando Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *A programação com formulários AEM* descreve as seguintes maneiras nas quais você pode invocar programaticamente esse processo de curta duração:

   * [Chamar um processo de duração curta transmitindo um documento inseguro usando o AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)  (usando um aplicativo Flex)
   * [Chamada de um processo de duração curta usando a API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)  de chamada (API de chamada de Java)
   * [Chamar o AEM Forms usando a codificação](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)  Base64 (exemplo de serviço da Web)
   * [Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)  (exemplo de serviço da Web)
   * [Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)  (exemplo de serviço da Web)
   * [Chamar o AEM Forms usando dados BLOB sobre HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)  (exemplo de serviço da Web)
   * [Chamada de AEM Forms usando DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime)  (exemplo de serviço da Web)
   * [Chamar o processo MyApplication/EncryptDocument usando REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Exemplo de processo de duração longa**

A ilustração a seguir é um exemplo de um processo de longa duração.

Este processo é invocado quando um candidato submete um formulário de empréstimo. O processo não está completo até que um agente de empréstimo aprove ou rejeite o pedido de empréstimo. O nome desse processo de longa duração é *FirstAppSolution/PreLoanProcess* e sua operação é `invoke_Async`. Esse processo deve ser chamado de forma assíncrona. Para obter informações sobre invocar programaticamente esse processo de longa duração, consulte [Invocando processos de longa vida centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Esse processo pode ser criado seguindo o tutorial especificado em [Criar seu primeiro aplicativo AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).