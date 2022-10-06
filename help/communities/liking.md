---
title: Usar curtir
seo-title: Using Liking
description: Adicionar e configurar o componente de vinculação
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# Usar curtir {#using-liking}

O `Liking` é uma ferramenta útil que permite que os usuários expressem uma opinião sobre um conteúdo específico, como um comentário em um fórum. Com o `Liking` , os membros selecionam o ícone do coração para indicar uma opinião positiva.

## Adicionar curtir a uma página {#adding-liking-to-a-page}

Para adicionar uma `Liking` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Liking`

e arraste-a para o local em uma página, como uma posição relativa ao recurso que os usuários desejam.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-liking.md#essentials-for-client-side) são incluídos, é assim que a variável `Liking` será exibido.

![componente de ligação](assets/liking-component.png)

## Configuração de curtir {#configuring-liking}

Selecione o `Liking` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

Em **[!UICONTROL Textos e rótulos]** , especifique as propriedades usadas para registrar curtidas.

![curtir a configuração](assets/configure-liking.png)

* **[!UICONTROL Rótulo de resposta positiva]**

   (*Obrigatório*) O nome da propriedade para uma resposta positiva.

* **[!UICONTROL Etiqueta de resposta negativa]**

   (*Obrigatório*) O nome da propriedade para uma resposta negativa.

* **[!UICONTROL Nome Tally]**

   (*Obrigatório*) O nome de propriedade interno e identificável para esta instância de um componente de votação.

## Experiência de visitante do site {#site-visitor-experience}

### Membros {#members}

Os deputados podem alterar a sua posição a qualquer momento.

### Anônimo {#anonymous}

A ligação anônima não é suportada. Os visitantes do site devem se registrar (se tornar um membro) e fazer logon para participar do curtidas.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Noções básicas sobre curtir](essentials-liking.md) página para desenvolvedores.
