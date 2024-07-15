---
title: Referência do processo de fluxo de trabalho
description: Consulte esta referência de processo para fluxos de trabalho no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Referência do processo de fluxo de trabalho{#workflow-process-reference}

O AEM fornece várias etapas de processo que podem ser usadas para criar modelos de fluxo de trabalho. Etapas de processo personalizadas também podem ser adicionadas para tarefas não cobertas pelas etapas internas (consulte [Criação de Modelos de Fluxo de Trabalho](/help/sites-developing/workflows-models.md)).

## Características do processo {#process-characteristics}

Para cada etapa do processo, as seguintes características são descritas.

### Classe Java™ ou caminho ECMA {#java-class-or-ecma-path}

As etapas do processo são definidas por uma classe Java™ ou por um ECMAScript.

* Para os processos de classe Java™, o nome de classe totalmente qualificado é fornecido.
* Para os processos do ECMAScript, é fornecido o caminho para o script.

### Carga útil {#payload}

A carga é a entidade sobre a qual uma instância de fluxo de trabalho atua. A carga é selecionada implicitamente pelo contexto em que uma instância de fluxo de trabalho é iniciada.

Por exemplo, se um fluxo de trabalho for aplicado a uma página do AEM *P*, *P* será passado de etapa a etapa conforme o fluxo de trabalho avança, com cada etapa atuando opcionalmente sobre *P* de alguma forma.

No caso mais comum, a carga é um nó JCR no repositório (por exemplo, uma página ou ativo AEM). Uma carga de Nó JCR é passada como uma string que é um caminho JCR ou um identificador JCR (UUID). Às vezes, a carga pode ser uma propriedade JCR (passada como um caminho JCR), um URL, um objeto binário ou um objeto Java™ genérico. Etapas de processo individuais que atuam na carga normalmente esperam uma carga de um determinado tipo ou agem de forma diferente dependendo do tipo de carga. Para cada processo descrito abaixo, o tipo de carga útil esperado, se houver, é descrito.

### Argumentos {#arguments}

Alguns processos de fluxo de trabalho aceitam argumentos que o administrador especifica ao configurar a etapa do fluxo de trabalho.

Os argumentos são inseridos como uma única cadeia de caracteres na propriedade **Argumentos do Processo**, no painel **Propriedades** do editor de fluxo de trabalho. Para cada processo descrito abaixo, o formato da string do argumento é descrito em uma gramática EBNF simples. Por exemplo, o código a seguir indica que a sequência de caracteres do argumento consiste em um ou mais pares delimitados por vírgulas, em que cada par consiste em um nome (que é uma sequência de caracteres) e um valor, separados por dois-pontos duplos:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Tempo limite {#timeout}

Após esse período de tempo limite, a etapa do fluxo de trabalho não estará mais operacional. Alguns processos de fluxo de trabalho respeitam o tempo limite, enquanto outros não se aplicam e são ignorados.

### Permissões {#permissions}

A sessão passada para `WorkflowProcess` é apoiada pelo usuário do serviço para o serviço de processo de fluxo de trabalho, que tem as seguintes permissões na raiz do repositório:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se esse conjunto de permissões não for suficiente para sua implementação do `WorkflowProcess`, ele deverá usar uma sessão com as permissões necessárias.

A maneira recomendada de fazer isso é usar um serviço de usuário criado com o subconjunto de permissões necessário, mas mínimo.

>[!CAUTION]
>
>Se estiver atualizando de uma versão anterior ao AEM 6.2, talvez seja necessário atualizar sua implementação.
>
>Em versões anteriores, a sessão de administrador era passada para as implementações do `WorkflowProcess` e poderia ter acesso total ao repositório sem precisar definir ACLs específicas.
>
>As permissões agora estão definidas como acima ([Permissões](#permissions)). Como é o método recomendado para atualizar sua implementação.
>
>Uma solução de curto prazo também está disponível para fins de compatibilidade com versões anteriores quando não for possível fazer alterações no código:
>
>* Usando o Console da Web ( `/system/console/configMgr`), localize o **Serviço de Configuração de Fluxo de Trabalho do Adobe Granite**
>
>* habilitar o **Modo Herdado do Processo de Fluxo de Trabalho**
>
>Isso reverte para o comportamento antigo de fornecer uma sessão de administrador para a implementação `WorkflowProcess` e fornecer acesso irrestrito à totalidade do repositório mais uma vez.

## Processos de Controle de Workflow {#workflow-control-processes}

Os processos a seguir não executam ações no conteúdo. Eles servem para controlar o comportamento do próprio workflow.

### AbsoluteTimeAutoAdvancer (Avançador automático de horário absoluto) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

O processo `AbsoluteTimeAutoAdvancer` (Avançador automático de tempo absoluto) se comporta de forma idêntica ao **AutoAdvancer**, exceto que seu tempo limite é atingido em um determinado horário e data, e não após um determinado período.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Carga**: nenhuma.
* **Argumentos**: nenhum.
* **Tempo limite**: o processo atinge o tempo limite quando a hora e a data definidas são atingidas.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

O processo `AutoAdvancer` avança automaticamente o fluxo de trabalho para a próxima etapa. Se houver mais de uma próxima etapa possível (por exemplo, se houver uma divisão OR), esse processo avançará o fluxo de trabalho ao longo da *rota padrão*, se uma tiver sido especificada, caso contrário, o fluxo de trabalho não será avançado.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Carga**: nenhuma.
* **Argumentos**: nenhum.
* **Tempo limite**: o processo expira após o período definido.

### ProcessAssembler (Assembler de Processo) {#processassembler-process-assembler}

O processo `ProcessAssembler` executa vários subprocessos sequencialmente em uma única etapa do fluxo de trabalho. Para usar o `ProcessAssembler`, crie uma única etapa desse tipo no fluxo de trabalho e defina seus argumentos para indicar os nomes e argumentos dos subprocessos que deseja executar.

* **Classe Java™**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Carga**: um ativo DAM, uma página AEM ou nenhuma carga (depende dos requisitos dos subprocessos).
* **argumentos**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Tempo Limite**: Respeitado.

Por exemplo:

* Extraia os metadados do ativo.
* Cria três miniaturas dos três tamanhos especificados.
* Crie uma imagem de JPEG do ativo, supondo que o ativo originalmente não seja um GIF ou um PNG (caso em que nenhum JPEG é criado).
* Defina a data da última modificação no ativo.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Processos básicos {#basic-processes}

Os processos a seguir executam tarefas simples ou servem como exemplos.

>[!CAUTION]
>
>Não altere nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

### excluir {#delete}

O item no caminho fornecido é excluído.

* **Caminho do ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Carga**: caminho JCR
* **Argumentos**: nenhum
* **Tempo Limite**: Ignorado

### noop {#noop}

Este é o processo nulo. Ela não executa nenhuma operação, mas registra uma mensagem de depuração.

* **Caminho do ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Carga**: nenhuma
* **Argumentos**: nenhum
* **Tempo Limite**: Ignorado

### regra-falso {#rule-false}

Este é um processo nulo que retorna `false` no método `check()`.

* **Caminho do ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Carga**: nenhuma
* **Argumentos**: nenhum
* **Tempo Limite**: Ignorado

### amostra {#sample}

Este é um exemplo de processo do ECMAScript.

* **Caminho do ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Carga**: nenhuma
* **Argumentos**: nenhum
* **Tempo Limite**: Ignorado

### LockProcess {#lockprocess}

Bloqueia a carga do workflow.

* **Classe Java™:** `com.day.cq.workflow.impl.process.LockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo Limite:** Ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está bloqueada
* O nó de carga útil não contém um nó secundário jcr:content

### UnlockProcess {#unlockprocess}

Desbloqueia a carga do fluxo de trabalho.

* **Classe Java™:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo Limite:** Ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está desbloqueada
* O nó de carga útil não contém um nó secundário jcr:content

## Processos de controle de versão {#versioning-processes}

O processo a seguir executa uma tarefa relacionada à versão.

### CreateVersionProcess {#createversionprocess}

Cria uma versão da carga do fluxo de trabalho (página AEM ou ativo DAM).

* **Classe Java™**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Carga**: um caminho JCR ou UUID que se refere a uma página ou ativo DAM
* **Argumentos**: nenhum
* **Tempo Limite**: Respeitado
