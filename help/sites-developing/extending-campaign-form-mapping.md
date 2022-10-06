---
title: Criação de mapeamentos de formulário personalizados
seo-title: Creating Custom Form Mappings
description: Ao criar uma tabela personalizada no Adobe Campaign, talvez você queira criar um formulário no AEM que mapeie para essa tabela personalizada
seo-description: When you create a custom table in Adobe Campaign, you may want to build a form in AEM that maps to that custom table
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 3%

---

# Criação de mapeamentos de formulário personalizados{#creating-custom-form-mappings}

Ao criar uma tabela personalizada no Adobe Campaign, talvez você queira criar um formulário no AEM que mapeie para essa tabela personalizada.

Este documento descreve como criar mapeamentos de formulário personalizados. Ao concluir as etapas neste documento, você fornecerá aos usuários uma página de evento em que eles poderão se inscrever para um evento futuro. Em seguida, você acompanha esses usuários por meio da Adobe Campaign.

## Pré-requisitos {#prerequisites}

Você precisa ter o seguinte instalado:

* Adobe Experience Manager
* Adobe Campaign Classic

Consulte [Integração do AEM com o Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) para obter mais informações.

## Criação de mapeamentos de formulário personalizados {#creating-custom-form-mappings-2}

Para criar mapeamentos de formulário personalizados, é necessário seguir essas etapas de alto nível, descritas detalhadamente nas seguintes seções:

1. Crie uma tabela personalizada.
1. Estender o **semente** tabela.
1. Crie um mapeamento personalizado.
1. Crie um delivery com base no mapeamento personalizado.
1. Crie o formulário no AEM, que usará o delivery criado.
1. Envie o formulário para testá-lo.

### Criação da tabela personalizada no Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Comece criando uma tabela personalizada no Adobe Campaign. Neste exemplo, estamos usando a seguinte definição para criar uma tabela de eventos:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Depois de criar a tabela de eventos, execute o **Assistente para atualização da estrutura do banco de dados** para criar a tabela.

### Extensão da tabela de sementes {#extending-the-seed-table}

No Adobe Campaign, toque/clique **Adicionar** para criar uma nova extensão do **Seed addresses (nms)** tabela.

![chlimage_1-194](assets/chlimage_1-194.png)

Agora, use os campos do **evento** tabela para estender o **semente** tabela:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Depois disso, execute **Assistente para atualização do banco de dados** para aplicar as alterações.

### Criação de mapeamento de destino personalizado {#creating-custom-target-mapping}

Em **Administração/Gerenciamento de campanha** t, vá para **Mapeamentos do Target** e adicionar um novo T **Mapeamento do Target.**

>[!NOTE]
>
>Certifique-se de usar um nome significativo para **Nome interno**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Criação de um template de delivery personalizado {#creating-a-custom-delivery-template}

Nesta etapa, você está adicionando um template do delivery que usa o **Target mapping**.

Em **Recursos/modelos**, navegue até o Modelo de entrega e duplique o delivery AEM existente. Ao clicar em **Para**, selecione criar evento **Target mapping**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Criação do formulário no AEM {#building-the-form-in-aem}

No AEM, verifique se você configurou um Cloud Service in **Propriedades da página**.

Em seguida, no **Adobe Campaign** selecione o delivery criado em [Criação de um template de delivery personalizado](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Ao configurar os campos, especifique nomes de elemento exclusivos para os campos de formulário.

Depois que os campos forem configurados, será necessário alterar manualmente o mapeamento.

No CRXDE-lite, acesse **jcr:content** (da página) e altere o nó **acMapping** para o nome interno da **Target mapping**.

![chlimage_1-198](assets/chlimage_1-198.png)

Na configuração do formulário, marque a caixa de seleção para criar se não existir

![chlimage_1-199](assets/chlimage_1-199.png)

### Envio do formulário {#submitting-the-form}

Agora é possível enviar o formulário e validar no lado do Adobe Campaign se os valores são salvos.

![chlimage_1-200](assets/chlimage_1-200.png)

## Resolução de problemas {#troubleshooting}

**&quot;Tipo inválido para o valor &#39;02/02/2015&#39; do elemento &#39;@eventdate&#39; (documento do tipo &#39;Event ([adb:event])&quot;**

Ao enviar o formulário, esse erro é registrado no **error.log** em AEM.

Isso ocorre devido a um formato inválido para o campo de data. A solução alternativa é fornecer **aaaa-mm-dd** como o valor.
