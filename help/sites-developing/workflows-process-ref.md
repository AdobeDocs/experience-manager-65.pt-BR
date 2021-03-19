---
title: Referência do processo de fluxo de trabalho
seo-title: Referência do processo de fluxo de trabalho
description: Referência do processo de fluxo de trabalho
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---


# Referência do processo de fluxo de trabalho{#workflow-process-reference}

O AEM fornece várias etapas do processo que podem ser usadas para criar modelos de fluxo de trabalho. As etapas do processo personalizado também podem ser adicionadas para tarefas não abordadas pelas etapas internas (consulte [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md)).

## Características do Processo {#process-characteristics}

Para cada etapa do processo, as características a seguir são descritas.

### Classe Java ou caminho ECMA {#java-class-or-ecma-path}

As etapas do processo são definidas por uma classe Java ou um ECMAScript.

* Para os processos da classe Java, o nome da classe totalmente qualificado é fornecido.
* Para o ECMAScript, o caminho para o script é fornecido.

### Carga {#payload}

A carga é a entidade sobre a qual uma instância de fluxo de trabalho atua. A carga é selecionada implicitamente pelo contexto no qual uma instância de workflow é iniciada.

Por exemplo, se um workflow for aplicado a uma página AEM *P*, *P* será passado de etapa para etapa à medida que o workflow avança, com cada etapa agindo opcionalmente em *P* de alguma forma.

No caso mais comum, a carga é um nó JCR no repositório (por exemplo, uma página AEM ou ativo). Uma carga do Nó JCR é passada como uma string que é um caminho JCR ou um identificador JCR (UUID). Em alguns casos, a carga pode ser uma propriedade JCR (passada como um caminho JCR), um URL, um objeto binário ou um objeto Java genérico. As etapas de processo individuais que atuam na carga normalmente esperam uma carga de um determinado tipo ou agem de forma diferente dependendo do tipo de carga. Para cada processo descrito abaixo, o tipo de carga esperado, se houver, é descrito.

### Argumentos {#arguments}

Alguns processos de fluxo de trabalho aceitam argumentos que o administrador especifica ao configurar a etapa do fluxo de trabalho.

Os argumentos são inseridos como uma única string na propriedade **Process Arguments** no painel **Properties** do editor de workflow. Para cada processo descrito abaixo, o formato da string do argumento é descrito em uma gramática EBNF simples. Por exemplo, o seguinte indica que a cadeia de caracteres do argumento consiste em um ou mais pares delimitados por vírgulas, onde cada par consiste de um nome (que é uma cadeia de caracteres) e um valor, separados por dois pontos:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Tempo limite {#timeout}

Após esse período de tempo limite, a etapa do fluxo de trabalho não estará mais operacional. Alguns processos de workflow respeitam o tempo limite, enquanto outros não se aplicam e são ignorados.

### Permissões  {#permissions}

A sessão passada para `WorkflowProcess` é apoiada pelo usuário do serviço para o serviço de processo do fluxo de trabalho, que tem as seguintes permissões na raiz do repositório:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se esse conjunto de permissões não for suficiente para sua implementação `WorkflowProcess`, ele deverá usar uma sessão com as permissões necessárias.

A maneira recomendada para fazer isso é usar um usuário de serviço criado com o subconjunto necessário, mas mínimo, de permissões.

>[!CAUTION]
>
>Se estiver atualizando de uma versão anterior ao AEM 6.2, talvez seja necessário atualizar sua implementação.
>
>Em versões anteriores, a sessão do administrador era passada para as implementações `WorkflowProcess` e podia ter acesso total ao repositório sem precisar definir ACLs específicas.
>
>As permissões agora são definidas como acima ([Permissões](#permissions)). Como é o método recomendado para atualizar sua implementação.
>
>Uma solução de curto prazo também está disponível para fins de compatibilidade retroativa quando as alterações de código não são viáveis:
>
>* Usando o Console da Web ( `/system/console/configMgr` localize o **Adobe Granite Workflow Configuration Service**
   >
   >
* habilite o **Modo Herdado do Processo de Fluxo de Trabalho**
>
>
Isso reverterá para o comportamento antigo de fornecer uma sessão de administrador à implementação `WorkflowProcess` e fornecerá acesso irrestrito à totalidade do repositório mais uma vez.

## Processos de controle de workflow {#workflow-control-processes}

Os seguintes processos não executam nenhuma ação no conteúdo. Eles servem para controlar o comportamento do próprio workflow.

### AbsoluteTimeAutoAdvancer (Avançador Automático de Tempo Absoluto) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

O processo `AbsoluteTimeAutoAdvancer` (Avanço Automático de Tempo Absoluto) se comporta de forma idêntica a **AutoAdvancer**, exceto que expira em um determinado momento e data, em vez de após um determinado período.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Carga**: Nenhum.
* **Argumentos**: Nenhum.
* **Tempo limite**: O processo expira quando a hora e a data definidas são atingidas.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

O processo `AutoAdvancer` avança automaticamente o workflow para a próxima etapa. Se houver mais de uma próxima etapa possível (por exemplo, se houver uma divisão OR), esse processo avançará o workflow ao longo da *rota padrão*, se uma tiver sido especificada, caso contrário, o workflow não será avançado.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Carga**: Nenhum.
* **Argumentos**: Nenhum.
* **Tempo limite**: O processo expira após a duração definida.

### ProcessAssembler (Assembler do Processo) {#processassembler-process-assembler}

O processo `ProcessAssembler` executa vários subprocessos sequencialmente em uma única etapa do fluxo de trabalho. Para usar o `ProcessAssembler`, crie uma única etapa desse tipo no workflow e defina seus argumentos para indicar os nomes e argumentos dos subprocessos que deseja executar.

* **Classe** Java:  `com.day.cq.workflow.impl.process.ProcessAssembler`

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
* Crie uma imagem JPEG a partir do ativo, supondo que o ativo não seja originalmente um GIF ou um PNG (nesse caso, nenhum JPEG é criado).
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
>Você ***não deve*** alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

### delete {#delete}

O item no caminho especificado é excluído.

* **Caminho** ECMAScript:  `/libs/workflow/scripts/delete.ecma`

* **Carga**: Caminho JCR
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### noop {#noop}

Este é o processo nulo. Ele não executa nenhuma operação, mas registra uma mensagem de depuração.

* **Caminho** ECMAScript:  `/libs/workflow/scripts/noop.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### rule-false {#rule-false}

Este é um processo nulo que retorna `false` no método `check()`.

* **Caminho** ECMAScript:  `/libs/workflow/scripts/rule-false.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### exemplo {#sample}

Este é um exemplo de processo ECMAScript.

* **Caminho** ECMAScript:  `/libs/workflow/scripts/sample.ecma`

* **Carga**: Nenhum
* **Argumentos**: Nenhum
* **Tempo limite**: Ignorado

### urlcaller {#urlcaller}

Este é um processo de fluxo de trabalho simples que chama o URL especificado. Normalmente, o URL será uma referência a um JSP (ou outro servlet equivalente) que executa uma tarefa simples. Esse processo deve ser usado apenas durante o desenvolvimento e as demonstrações e não em um ambiente de produção. Os argumentos especificam o URL, o login e a senha.

* **Caminho** ECMAScript:  `/libs/workflow/scripts/urlcaller.ecma`

* **Carga**: Nenhum
* **Argumentos**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

Por exemplo: `http://localhost:4502/my.jsp, mylogin, mypassword`

* **Tempo limite**: Ignorado

### LockProcess {#lockprocess}

Bloqueia a carga do fluxo de trabalho.

* **Classe Java:** `com.day.cq.workflow.impl.process.LockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo limite:** ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está bloqueada
* O nó payload não contém um nó filho jcr:content

### UnlockProcess {#unlockprocess}

Desbloqueia a carga do fluxo de trabalho.

* **Classe Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Carga:** JCR_PATH e JCR_UUID
* **Argumentos:** Nenhum
* **Tempo limite:** ignorado

A etapa não tem efeito nas seguintes circunstâncias:

* A carga já está desbloqueada
* O nó payload não contém um nó filho jcr:content

## Processos de controle de versão {#versioning-processes}

O processo a seguir executa uma tarefa relacionada à versão.

### CreateVersionProcess {#createversionprocess}

Cria uma nova versão da carga do fluxo de trabalho (página de AEM ou ativo DAM).

* **Classe** Java:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Carga**: Um caminho JCR ou UUID que se refere a uma página ou ativo DAM
* **Argumentos**: Nenhum
* **Tempo limite**: Respeitado

