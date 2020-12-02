---
title: Criação de mapeamentos de formulário personalizados
seo-title: Criação de mapeamentos de formulário personalizados
description: Ao criar uma tabela personalizada no Adobe Campaign, talvez você queira criar um formulário no AEM que mapeie para essa tabela personalizada
seo-description: Ao criar uma tabela personalizada no Adobe Campaign, talvez você queira criar um formulário no AEM que mapeie para essa tabela personalizada
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 4%

---


# Criação de mapeamentos de formulário personalizados{#creating-custom-form-mappings}

Ao criar uma tabela personalizada no Adobe Campaign, talvez você queira criar um formulário no AEM que mapeie para essa tabela personalizada.

Este documento descreve como criar mapeamentos de formulário personalizados. Quando você concluir as etapas neste documento, você fornecerá aos usuários uma página de evento na qual eles poderão se inscrever para um evento futuro. Em seguida, você acompanha esses usuários via Adobe Campaign.

## Pré-requisitos {#prerequisites}

É necessário ter o seguinte instalado:

* Adobe Experience Manager
* Adobe Campaign Classic

Consulte [Integração de AEM com o Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) para obter mais informações.

## Criação de mapeamentos de formulário personalizados {#creating-custom-form-mappings-2}

Para criar mapeamentos de formulário personalizados, é necessário seguir essas etapas de alto nível, descritas detalhadamente nas seguintes seções:

1. Crie uma tabela personalizada.
1. Estende a tabela **semente**.
1. Crie um mapeamento personalizado.
1. Crie um delivery com base no mapeamento personalizado.
1. Crie o formulário no AEM, que usará o delivery criado.
1. Envie o formulário para testá-lo.

### Criação da tabela personalizada no Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Start criando uma tabela personalizada no Adobe Campaign. Neste exemplo, estamos usando a seguinte definição para criar uma tabela de eventos:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Depois de criar a tabela de eventos, execute o **Assistente para Atualizar a estrutura do banco de dados** para criar a tabela.

### Extensão da Tabela de Sementes {#extending-the-seed-table}

No Adobe Campaign, toque/clique em **Adicionar** para criar uma nova extensão da tabela **Seeds addresses (nms)**.

![chlimage_1-194](assets/chlimage_1-194.png)

Agora, use os campos da tabela **evento** para estender a tabela **semente**:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Depois disso, execute **Assistente de atualização de banco de dados** para aplicar as alterações.

### Criando Target mapping Personalizado {#creating-custom-target-mapping}

Em **Gerenciamento de administração/Campanha** t, vá para **Target mapping** e adicione um novo Mapeamento de T **destino.**

>[!NOTE]
>
>Certifique-se de usar um nome significativo para **Nome interno**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Criando um Template do delivery personalizado {#creating-a-custom-delivery-template}

Nesta etapa, você está adicionando um template do delivery que usa o Target mapping **criado**.

Em **Resources/Templates**, navegue até o Template do delivery e duplicado o delivery AEM existente. Ao clicar em **To**, selecione o evento create **Target mapping**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Criação do formulário em AEM {#building-the-form-in-aem}

No AEM, certifique-se de ter configurado um Cloud Service em **Propriedades da página**.

Em seguida, na guia **Adobe Campaign**, selecione o delivery que foi criado em [Criação de um Template do delivery personalizado](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Ao configurar os campos, especifique nomes de elemento exclusivos para os campos de formulário.

Depois que os campos forem configurados, é necessário alterar manualmente o mapeamento.

No CRXDE-lite, vá para o nó **jcr:content** (da página) e altere o valor **acMapping** para o nome interno do Target mapping **a5/>.**

![chlimage_1-198](assets/chlimage_1-198.png)

Na configuração do formulário, marque a caixa de seleção para criar se não existir

![chlimage_1-199](assets/chlimage_1-199.png)

### Enviando o formulário {#submitting-the-form}

Agora é possível enviar o formulário e validar no Adobe Campaign se os valores são salvos.

![chlimage_1-200](assets/chlimage_1-200.png)

## Resolução de problemas {#troubleshooting}

**&quot;Tipo inválido para o valor &#39;02/02/2015&#39; do elemento &#39;@eventdate&#39; (documento do tipo &#39;Evento ([adb:evento])&#39;)&quot;**

Ao enviar o formulário, esse erro é registrado em **error.log** no AEM.

Isso ocorre devido a um formato inválido para o campo de data. A solução alternativa é fornecer **aaaa-mm-dd** como o valor.

