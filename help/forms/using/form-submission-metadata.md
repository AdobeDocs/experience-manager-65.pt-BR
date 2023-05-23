---
title: Adição de informações de dados do usuário para metadados de envio de formulário
seo-title: Adding information from user data to form submission metadata
description: Saiba como adicionar informações aos metadados de um formulário enviado com dados fornecidos pelo usuário.
seo-description: Learn how to add information to metadata of a submitted form with user provided data.
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
feature: Adaptive Forms
exl-id: 5ca850e3-30f0-4384-b615-356dc3c2ad0d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Adição de informações de dados do usuário para metadados de envio de formulário{#adding-information-from-user-data-to-form-submission-metadata}

Você pode usar os valores inseridos em um elemento do formulário para calcular campos de metadados de um rascunho ou envio de formulário. Os metadados permitem filtrar o conteúdo com base nos dados do usuário. Por exemplo, um usuário digita João da Silva no campo de nome do formulário. É possível usar essas informações para calcular metadados que podem categorizar esse envio no JD de iniciais.

Para calcular campos de metadados com valores inseridos pelo usuário, adicione elementos do formulário nos metadados. Quando um usuário insere um valor nesse elemento, um script usa o valor para calcular as informações. Essas informações são adicionadas nos metadados. Ao adicionar um elemento como um campo de metadados, você fornece uma chave para ele. A chave é adicionada como um campo nos metadados e as informações computadas são registradas em relação a ela.

Por exemplo, uma empresa de seguros de saúde publica um formulário. Nesse formulário, um campo captura a idade dos usuários finais. O cliente deseja verificar todos os envios em uma faixa etária específica depois que vários usuários enviarem o formulário. Em vez de analisar todos os dados que se complicam com o aumento do número de formulários, os metadados adicionais ajudam o cliente. O autor do formulário pode configurar quais propriedades/dados preenchidos pelo usuário final são armazenados no nível superior para que a pesquisa seja mais fácil. Os metadados adicionais são informações preenchidas pelo usuário armazenadas no nível superior do nó de metadados, conforme configurado pelo autor.

Considere outro exemplo de um formulário que captura a ID de email e o número de telefone. Quando um usuário visita esse formulário anonimamente e abandona o formulário, o autor pode configurá-lo para salvar automaticamente a ID de email e o número de telefone. Esse formulário é salvo automaticamente e o número de telefone e a ID de email são armazenados no nó de metadados do rascunho. Um caso de uso dessa configuração é o painel de gerenciamento de clientes potenciais.

## Adição de elementos de formulário aos metadados {#adding-form-elements-to-metadata}

Execute as seguintes etapas para adicionar um elemento aos metadados:

1. Abra o formulário adaptável no modo de edição.\
   Para abrir o formulário no modo de edição, no gerenciador de formulários, selecione o formulário e toque em **Abertura**.
1. No modo de edição, selecione um componente, toque em ![nível de campo](assets/field-level.png) > **Contêiner de formulário adaptável** e toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, clique em **Metadados**.
1. Na seção Metadados, clique em **Adicionar**.
1. Use o campo Value da guia Metadata para adicionar scripts. Os scripts que você adiciona coletam dados de elementos no formulário e calculam valores que são alimentados para os metadados.

   Por exemplo, **true** é registrado nos metadados se a idade inserida for maior que 21 e **false** é registrado se for menor que 21. Digite o seguinte script na guia Metadados:

   `(agebox.value >= 21) ? true : false`

   ![Script de metadados](assets/add-element-metadata.png)

   Script inserido na guia Metadados

1. Clique em **OK**.

Depois que um usuário insere dados no elemento selecionado como um campo de metadados, as informações calculadas são registradas nos metadados. Você pode ver os metadados no repositório configurado para armazenar metadados.

## Visualização de metadados de envio de formulário atualizados: {#seeing-updated-form-nbsp-submission-metadata}

No exemplo acima, os metadados são armazenados no repositório CRX. Os metadados são como:

![Metadados](assets/metadata_entry_new.png)

Se você adicionar um elemento de caixa de seleção nos metadados, os valores selecionados serão armazenados como uma string separada por vírgulas. Por exemplo, você adiciona um componente de caixa de seleção no formulário e especifica seu nome como `checkbox1`. Nas propriedades do componente da caixa de seleção, adicione os itens Licença de condução, Número da Previdência social e Passaporte para valores 0, 1 e 2.

![Armazenamento de vários valores a partir de uma caixa de seleção](assets/checkbox-metadata.png)

Selecione o contêiner de formulário adaptável e, nas propriedades do formulário, adicione uma chave de metadados `cb1` que armazena `checkbox1.value`e publique o formulário. Quando um cliente preenche o formulário, ele seleciona as opções Passport e Social Security Number no campo da caixa de seleção. Os valores 1 e 2 são armazenados como 1, 2 no campo cb1 dos metadados de envio.

![Entrada de metadados para vários valores selecionados em um campo de caixa de seleção](assets/metadata-entry.png)

>[!NOTE]
>
>O exemplo acima é somente para fins de aprendizado. Certifique-se de procurar metadados no local correto, conforme configurado na implementação do AEM Forms.
