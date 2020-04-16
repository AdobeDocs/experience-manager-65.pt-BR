---
title: Como entender os processos do AEM Forms
seo-title: Como entender os processos do AEM Forms
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Como entender os processos do AEM Forms {#understanding-aem-forms-processes}

Um caso de uso comum é para um conjunto de serviços do AEM Forms operarem em um único documento. Você pode enviar uma solicitação ao container de serviço criando um processo usando o Workbench. Um processo representa um processo de negócios que você está automatizando. Para obter informações sobre como criar processos, consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando um processo é ativado, ele se torna um serviço e pode ser chamado como outros serviços. Uma diferença entre um serviço padrão, como o Encryption Service e um serviço originado de um processo, é que este tem uma operação que executa muitas ações. Em contraste, um serviço padrão tem muitas operações. Cada operação normalmente executa uma ação, como aplicar uma política a um documento ou criptografar um documento.

Os processos podem ter vida curta ou longa. Um processo de duração curta é uma operação executada de forma síncrona e no mesmo thread de execução a partir do qual foi chamada. As operações de duração curta são comparáveis ao comportamento padrão encontrado na maioria das linguagens de programação, onde um aplicativo cliente chama um método e aguarda um valor de retorno.

No entanto, há situações em que um processo não pode ser concluído sincronicamente devido a fatores como estes:

* Um processo pode abranger uma quantidade significativa de tempo.
* Um processo pode estender-se por limites organizacionais.
* Um processo precisa de entrada externa para que seja concluído. Por exemplo, considere uma situação em que um formulário é enviado para um gerente que está fora do escritório. Nesse caso, o processo não é concluído até que o gerente retorne e preencha o formulário.

   Esses tipos de processos são conhecidos como processos duradouros. Um processo de longa duração é executado de forma assíncrona, permitindo que os sistemas interajam como os recursos permitem e permitindo o rastreamento e o monitoramento da operação. Quando um processo de longa duração é chamado, o AEM Forms cria um valor identificador de invocação como parte de um registro que acompanha o status do processo de longa duração. O registro é armazenado no banco de dados do AEM Forms. Você pode expurgar registros de processos de longa duração quando não forem mais necessários.

>[!NOTE]
>
>O AEM Forms não cria um registro quando um processo de duração curta é chamado.

Usando o valor do identificador de invocação, é possível rastrear o status do processo de longa duração. Por exemplo, você pode usar o valor do identificador de invocação do processo para executar operações do Process Manager, como encerrar uma instância de processo em execução.

**Exemplo de processo de duração curta**

A ilustração a seguir é um exemplo de um processo de duração curta chamado *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Esse processo não se baseia em um processo de formulários AEM existente. Para acompanhar os exemplos de código que discutem como invocar esse processo, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo de duração curta é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo como um valor de entrada.
1. Criptografa o documento PDF com uma senha. O nome do parâmetro de entrada para esse processo é `inDoc` e o tipo de dados é documento.
1. Salva o documento PDF criptografado por senha como um arquivo PDF no sistema de arquivos local. Esse processo retorna o documento PDF criptografado como um valor de saída. O nome do parâmetro de saída para esse processo é `outDoc` e o tipo de dados é documento.

   Esse processo é concluído sincronicamente no mesmo thread de execução a partir do qual foi chamado. O nome desse processo de curta duração é `MyApplication/EncryptDocument`e sua operação é `invoke`.

   >[!NOTE]
   >
   >Normalmente, um processo de duração curta consiste em mais de três ações. Você cria um processo usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *A programação com* formulários AEM descreve as seguintes maneiras nas quais você pode chamar programaticamente esse processo de curta duração:

   * [Invocar um processo de duração curta transmitindo um documento não seguro usando o AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (usando um aplicativo Flex)
   * [Invocando um processo de duração curta usando a API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) de chamada (API de chamada Java)
   * [Invocar o AEM Forms usando a codificação](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) Base64 (exemplo de serviço da Web)
   * [Invocar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (exemplo de serviço da Web)
   * [Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (exemplo de serviço da Web)
   * [Invocar o AEM Forms usando dados BLOB em HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (exemplo de serviço da Web)
   * [Invocar o AEM Forms usando DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (exemplo de serviço da Web)
   * [Chamada do processo MyApplication/EncryptDocument usando REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Exemplo de processo de longa duração**

A ilustração a seguir é um exemplo de um processo de longa duração.

Este processo é invocado quando um candidato submete um formulário de empréstimo. O processo não está concluído até que um agente de empréstimo aprove ou rejeite o pedido de empréstimo. O nome desse processo de longa duração é *FirstAppSolution/PreLoanProcess* e sua operação é `invoke_Async`. Este processo deve ser invocado de forma assíncrona. Para obter informações sobre como invocar programaticamente esse processo de longa duração, consulte [Invocando Processos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)de Vida Longa Centrados em Humanos.

>[!NOTE]
>
>Esse processo pode ser criado seguindo o tutorial especificado em [Criar seu primeiro aplicativo](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)AEM Forms.