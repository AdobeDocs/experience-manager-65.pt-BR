---
title: Referência do processo de fluxo de trabalho
seo-title: Workflow Process Reference
description: Referência do processo de fluxo de trabalho
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: cf3b739fd774bc860d9906b9884d22fd532fd5dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# Referência do processo de fluxo de trabalho{#workflow-process-reference}

O AEM fornece várias etapas do processo que podem ser usadas para criar modelos de fluxo de trabalho. As etapas do processo personalizado também podem ser adicionadas para tarefas não abordadas pelas etapas internas (consulte [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md)).

## Características do processo {#process-characteristics}

Para cada etapa do processo, as características a seguir são descritas.

### Classe Java ou caminho ECMA {#java-class-or-ecma-path}

As etapas do processo são definidas por uma classe Java ou um ECMAScript.

* Para os processos da classe Java, o nome da classe totalmente qualificado é fornecido.
* Para o ECMAScript, o caminho para o script é fornecido.

### Carga {#payload}

A carga é a entidade sobre a qual uma instância de fluxo de trabalho atua. A carga é selecionada implicitamente pelo contexto no qual uma instância de workflow é iniciada.

Por exemplo, se um fluxo de trabalho for aplicado a uma página de AEM *P* then *P* é transmitido de etapa para etapa, à medida que o fluxo de trabalho avança, com cada etapa agindo opcionalmente sobre *P* de alguma forma.

No caso mais comum, a carga é um nó JCR no repositório (por exemplo, uma página AEM ou ativo). Uma carga do Nó JCR é passada como uma string que é um caminho JCR ou um identificador JCR (UUID). Em alguns casos, a carga pode ser uma propriedade JCR (passada como um caminho JCR), um URL, um objeto binário ou um objeto Java genérico. As etapas de processo individuais que atuam na carga normalmente esperam uma carga de um determinado tipo ou agem de forma diferente dependendo do tipo de carga. Para cada processo descrito abaixo, o tipo de carga esperado, se houver, é descrito.

### Argumentos {#arguments}

Alguns processos de fluxo de trabalho aceitam argumentos que o administrador especifica ao configurar a etapa do fluxo de trabalho.

Os argumentos são inseridos como uma única string na variável **Argumentos do processo** na **Propriedades** painel do editor de fluxo de trabalho. Para cada processo descrito abaixo, o formato da string do argumento é descrito em uma gramática EBNF simples. Por exemplo, o seguinte indica que a cadeia de caracteres do argumento consiste em um ou mais pares delimitados por vírgulas, onde cada par consiste de um nome (que é uma cadeia de caracteres) e um valor, separados por dois pontos:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Tempo limite {#timeout}

Após esse período de tempo limite, a etapa do fluxo de trabalho não estará mais operacional. Alguns processos de workflow respeitam o tempo limite, enquanto outros não se aplicam e são ignorados.

### Permissões {#permissions}

A sessão passada para a `WorkflowProcess` é respaldado pelo usuário do serviço do processo do fluxo de trabalho, que tem as seguintes permissões na raiz do repositório:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se esse conjunto de permissões não for suficiente para sua `WorkflowProcess` , então deve usar uma sessão com as permissões necessárias.

A maneira recomendada para fazer isso é usar um usuário de serviço criado com o subconjunto necessário, mas mínimo, de permissões.

>[!CAUTION]
>
>Se estiver atualizando de uma versão anterior ao AEM 6.2, talvez seja necessário atualizar sua implementação.
>
>Em versões anteriores, a sessão do administrador era passada para o `WorkflowProcess` implementações e poderiam ter acesso total ao repositório sem a necessidade de definir ACLs específicas.
>
>As permissões agora são definidas como acima ([Permissões](#permissions)). Como é o método recomendado para atualizar sua implementação.
>
>Uma solução de curto prazo também está disponível para fins de compatibilidade retroativa quando as alterações de código não são viáveis:
>
>* Uso do Console da Web ( `/system/console/configMgr` localize o **Serviço de configuração de fluxo de trabalho do Adobe Granite**
>
>* habilite o **Modo Legado do Processo de Fluxo de Trabalho**
>
>Isso reverterá para o comportamento antigo de fornecer uma sessão de administrador ao `WorkflowProcess` e fornecer acesso irrestrito a todo o repositório mais uma vez.

## Processos de Controle de Workflow {#workflow-control-processes}

Os seguintes processos não executam nenhuma ação no conteúdo. Eles servem para controlar o comportamento do próprio workflow.

### AbsoluteTimeAutoAdvancer (Avançador Automático de Tempo Absoluto) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

O `AbsoluteTimeAutoAdvancer` O processo (Advancer automático em tempo absoluto) se comporta de forma idêntica a **AutoAdvancer**, exceto que expira em um determinado horário e data, em vez de após um determinado período.

* **Classe Java**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Carga**: Nenhum.
* **Argumentos**: Nenhum.
* **Tempo limite**: O processo expira quando a hora e a data definidas são atingidas.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

O `AutoAdvancer` O processo avança automaticamente o fluxo de trabalho para a próxima etapa. Se houver mais de uma próxima etapa possível (por exemplo, se houver uma divisão OR), esse processo avançará o fluxo de trabalho ao longo da *rota padrão*, se um tiver sido especificado, caso contrário, o fluxo de trabalho não será avançado.

* **Classe Java**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Carga**: Nenhum.
* **Argumentos**: Nenhum.
* **Tempo limite**: O processo expira após a duração definida.

### ProcessAssembler (Assembler do Processo) {#processassembler-process-assembler}

O `ProcessAssembler` O processo executa vários subprocessos sequencialmente em uma única etapa do fluxo de trabalho. Para usar o `ProcessAssembler`, crie uma única etapa desse tipo no fluxo de trabalho e defina seus argumentos para indicar os nomes e os argumentos dos subprocessos que deseja executar.

* **Classe Java**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Carga**: Um ativo DAM, AEM página ou sem carga útil (depende dos requisitos dos subprocessos).
* **Argumentos**:

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

* **Tempo limite**: Respeitado.

Por exemplo:

* Extraia os metadados do ativo.
* Crie três miniaturas dos três tamanhos especificados.
* Crie uma imagem JPEG do ativo, supondo que o ativo não seja originalmente um GIF ou um PNG (nesse caso, nenhum JPEG é criado).
* Defina a data da última modificação no ativo.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Processos básicos {#basic-processes}

Os seguintes processos executam tarefas simples ou servem como exemplos.

>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

### delete {#delete}

O item no caminho especificado é excluído.

* **Caminho ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Carga**: Caminho JCR
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### noop {#noop}

Este é o processo nulo. Ele não executa nenhuma operação, mas registra uma mensagem de depuração.

* **Caminho ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### rule-false {#rule-false}

Este é um processo nulo que retorna `false` no `check()` método .

* **Caminho ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### amostra {#sample}

Este é um exemplo de processo ECMAScript.

* **Caminho ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### BloquearProcesso {#lockprocess}

Bloqueia a carga do fluxo de trabalho.

* **Classe Java:** `com.day.cq.workflow.impl.process.LockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo limite:** Ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está bloqueada
* O nó payload não contém um nó filho jcr:content

### UnlockProcess {#unlockprocess}

Desbloqueia a carga do fluxo de trabalho.

* **Classe Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo limite:** Ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está desbloqueada
* O nó payload não contém um nó filho jcr:content

## Processos de controle de versão {#versioning-processes}

O processo a seguir executa uma tarefa relacionada à versão.

### CreateVersionProcess {#createversionprocess}

Cria uma nova versão da carga do fluxo de trabalho (página de AEM ou ativo DAM).

* **Classe Java**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Carga**: Um caminho JCR ou UUID que se refere a uma página ou ativo DAM
* **Argumentos**: Nenhum
* **Tempo limite**: Respeitado
