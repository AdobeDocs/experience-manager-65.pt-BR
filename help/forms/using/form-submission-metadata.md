---
title: Adicionar informações dos dados do usuário aos metadados de envio do formulário
seo-title: Adicionar informações dos dados do usuário aos metadados de envio do formulário
description: 'Saiba como adicionar informações aos metadados de um formulário enviado com dados fornecidos pelo usuário. '
seo-description: 'Saiba como adicionar informações aos metadados de um formulário enviado com dados fornecidos pelo usuário. '
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Adicionar informações dos dados do usuário aos metadados de envio do formulário{#adding-information-from-user-data-to-form-submission-metadata}

É possível usar valores inseridos em um elemento do formulário para calcular campos de metadados de um rascunho ou envio de um formulário. Os metadados permitem que você filtre o conteúdo com base nos dados do usuário. Por exemplo, um usuário digita John Doe no campo de nome do formulário. Você pode usar essas informações para calcular metadados que podem categorizar esse envio sob as iniciais JD.

Para calcular campos de metadados com valores digitados pelo usuário, adicione elementos do formulário nos metadados. Quando um usuário digita um valor nesse elemento, um script usa o valor para calcular as informações. Essas informações são adicionadas aos metadados. Quando você adiciona um elemento como um campo de metadados, fornece uma chave para ele. A chave é adicionada como um campo nos metadados e as informações calculadas são registradas em relação a ela.

Por exemplo, uma empresa de seguros de saúde publica um formulário. Neste formulário, um campo captura a idade dos usuários finais. O cliente deseja verificar todos os envios em uma faixa etária específica depois que vários usuários enviarem o formulário. Em vez de percorrer todos os dados que se complicam com o número crescente de formulários, metadados adicionais ajudam o cliente. O autor do formulário pode configurar quais propriedades/dados preenchidos pelo usuário final são armazenados no nível superior para que a pesquisa seja mais fácil. Metadados adicionais são informações preenchidas pelo usuário armazenadas no nível superior do nó de metadados, conforme configurado pelo autor.

Considere outro exemplo de um formulário que captura a ID de e-mail e o número de telefone. Quando um usuário visita esse formulário anonimamente e abandona o formulário, o autor pode configurar o formulário para salvar automaticamente a ID do email e o número de telefone. Este formulário é salvo automaticamente e o número de telefone e a ID de email são armazenados no nó de metadados do rascunho. Um caso de uso dessa configuração é o painel de gerenciamento de lead.

## Adicionar elementos de formulário aos metadados {#adding-form-elements-to-metadata}

Execute as seguintes etapas para adicionar um elemento nos metadados:

1. Abra o formulário adaptável no modo de edição.\
   Para abrir o formulário no modo de edição, no Gerenciador de formulários, selecione o formulário e toque em **Abrir**.
1. No modo de edição, selecione um componente, toque em ![field-level](assets/field-level.png) > **Container de formulário adaptável** e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, clique em **Metadados**.
1. Na seção Metadados, clique em **Adicionar**.
1. Use o campo Valor da guia Metadados para adicionar scripts. Os scripts adicionados coletam dados de elementos no formulário e calculam valores que são alimentados para os metadados.

   Por exemplo, **true** é registrado nos metadados se a idade digitada for maior que 21, e **false** é registrado se for menor que 21. Digite o seguinte script na guia Metadados:

   `(agebox.value >= 21) ? true : false`

   ![Script de metadados](assets/add-element-metadata.png)

   Script inserido na guia Metadados

1. Clique em **OK**.

Depois que um usuário digita dados no elemento selecionado como um campo de metadados, as informações calculadas são registradas nos metadados. Você pode ver os metadados no repositório configurado para armazenar metadados.

## Visualizando metadados atualizados de envio de formulário: {#seeing-updated-form-nbsp-submission-metadata}

No exemplo acima, os metadados são armazenados no repositório CRX. Os metadados se parecem com:

![Metadados](assets/metadata_entry_new.png)

Se você adicionar um elemento de caixa de seleção nos metadados, os valores selecionados serão armazenados como uma sequência separada por vírgulas. Por exemplo, adicione um componente de caixa de seleção no formulário e especifique seu nome como `checkbox1`. Nas propriedades do componente da caixa de seleção, adicione os itens Licença de condução, Número de Segurança Social e Passaporte para os valores 0, 1 e 2.

![Armazenamento de vários valores de uma caixa de seleção](assets/checkbox-metadata.png)

Você seleciona um container de formulário adaptável e, nas propriedades do formulário, adiciona uma chave de metadados `cb1` que armazena `checkbox1.value` e publica o formulário. Quando um cliente preenche o formulário, o cliente seleciona as opções de Passaporte e Número do Seguro Social no campo da caixa de seleção. Os valores 1 e 2 são armazenados como 1, 2 no campo cb1 dos metadados de envio.

![Entrada de metadados para vários valores selecionados em um campo de caixa de seleção](assets/metadata-entry.png)

>[!NOTE]
>
>O exemplo acima é apenas para fins de aprendizagem. Certifique-se de procurar metadados no local correto, conforme configurado na implementação do AEM Forms.

