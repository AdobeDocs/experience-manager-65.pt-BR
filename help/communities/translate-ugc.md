---
title: Tradução de conteúdo gerado pelo usuário
seo-title: Tradução de conteúdo gerado pelo usuário
description: Como o recurso de tradução funciona
seo-description: Como o recurso de tradução funciona
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---


# Traduzindo conteúdo gerado pelo usuário {#translating-user-generated-content}

O recurso de tradução do AEM Communities estende o conceito de [tradução do conteúdo da página](../../help/sites-administering/translation.md) para o conteúdo gerado pelo usuário (UGC) publicado em sites da comunidade usando [componentes de estrutura de componente social (SCF)](scf.md).

A tradução do UGC permite que visitantes e membros do site experimentem uma comunidade global removendo barreiras de idioma.

Por exemplo, suponha:

* Um membro da França posta uma receita em francês no fórum comunitário de um site multinacional de culinária.
* Outro membro do Japão usa o recurso de tradução para acionar a tradução da receita do francês para o japonês.
* Depois de ler a receita em japonês, o membro do Japão publica um comentário em japonês.
* O membro da França usa o recurso de tradução para traduzir o comentário japonês para francês.
* Comunicação global.

## Visão geral {#overview}

Esta seção da documentação discute especificamente como o serviço de tradução funciona com o UGC, assumindo ao mesmo tempo uma compreensão de como se conectar AEM a um [provedor de serviços de tradução](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e integrar esse serviço a um site, configurando uma [estrutura de integração de tradução](../../help/sites-administering/tc-tic.md).

Quando um provedor de serviços de tradução é associado ao site, cada cópia de idioma do site mantém seus próprios threads do UGC publicados por componentes do SCF, como comentários.

Quando uma estrutura de integração de tradução é configurada além do provedor de serviços de tradução, é possível que cada cópia de idioma do site compartilhe um único thread do UGC, fornecendo comunicação global entre cópias de idioma. Em vez de um thread de discussão segregado por idioma, o [armazenamento compartilhado global](#global-translation-of-ugc) configurado permite que todo o thread fique visível, independentemente da cópia de idioma que está sendo visualizada. Além disso, várias configurações de integração de tradução podem ser configuradas especificando diferentes lojas compartilhadas globais para um agrupamento lógico de participantes globais, como por regiões.

## O Serviço de Tradução Padrão {#the-default-translation-service}

O AEM Communities inclui uma [licença de avaliação](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) para um [serviço de tradução padrão](../../help/sites-administering/tc-msconf.md) habilitado para vários idiomas.

Quando [criar um site da comunidade](sites-console.md), o serviço de tradução padrão é ativado quando `Allow Machine Translation` é verificado no subpainel [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>O serviço de tradução padrão é somente para demonstração.
>
>Para um sistema de produção, é necessário um serviço de tradução licenciado. Se não estiver licenciado, o serviço de tradução padrão deve ser [desativado](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Tradução global do UGC {#global-translation-of-ugc}

Quando um site tem várias [cópias de idioma](../../help/sites-administering/tc-prep.md), o serviço de tradução padrão não reconhece que o UGC inserido em um site pode estar relacionado ao UGC inserido em outro, como quando o UGC é, essencialmente, gerado pelo mesmo componente (a cópia de idioma da página que contém o componente).

É semelhante a grupos de pessoas que discutem um tópico desconhecendo os comentários feitos em grupos que não o seu, em comparação com todos em um grande grupo que participa de uma conversa.

Se &quot;uma conversa em grupo&quot; for desejada, é possível habilitar a tradução global em um site com várias cópias de idioma, de modo que todo o thread esteja visível, independentemente da cópia de idioma que está sendo visualizada.

Por exemplo, se um fórum fosse estabelecido no site base, as cópias de idioma criadas e a tradução global fosse ativada, um tópico publicado no fórum feito em uma cópia de idioma apareceria em todas as cópias de idioma. O mesmo se aplica a todas as respostas, independentemente da cópia linguística da resposta. O resultado seria que o tópico e todo o seu encadeamento de respostas ficariam visíveis, independentemente de qual cópia de idioma o tópico estiver sendo visualizado.

>[!CAUTION]
>
>Qualquer UGC que existia antes da tradução global não está mais visível.
>
>Embora o UGC ainda esteja no [common store](working-with-srp.md), ele está localizado no local UGC específico do idioma, enquanto o novo conteúdo, adicionado após a configuração da tradução global, está sendo recuperado do local de armazenamento compartilhado global.
>
>Não há ferramenta de migração para mover ou mesclar conteúdo específico de idioma na loja compartilhada global.

### Configuração da integração da tradução {#translation-integration-configuration}

Para criar uma nova Integração de tradução, que integra um conector do Serviço de tradução ao site na instância do autor:

* Fazer logon como administrador
* No [menu principal](http://localhost:4502/)
* Selecione **[!UICONTROL Ferramentas]**
* Selecione **[!UICONTROL Operações]**
* Selecione **[!UICONTROL Cloud]**
* Selecione **[!UICONTROL Cloud Services]**
* Role para baixo até **[!UICONTROL Integração de tradução]**

   ![integração de tradução](assets/translation-integration.png)

* Selecione **[!UICONTROL Mostrar configurações]**

   ![show-configuration](assets/translation-integration1.png)

* Selecione o ícone `[+]` ao lado de **[!UICONTROL Configurações disponíveis]** para criar uma nova configuração

#### Criar caixa de diálogo de configuração {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configuração primária]**

   (Obrigatório) Geralmente, deixe como padrão. O padrão é `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**

   (Obrigatório) Insira um título de exibição de sua escolha. Nenhum valor padrão.

* **[!UICONTROL Nome]**

   (Opcional) Insira um nome para a configuração. O padrão é um nome de nó com base no Título.

* Selecione **[!UICONTROL Criar]**

#### Caixa de diálogo de configuração de tradução {#translation-config-dialog}

![diálogo de configuração](assets/translation-integration3.png)

Para obter instruções detalhadas, visite [Criação de uma Configuração de Integração de Tradução](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **** Local: pode ser deixado como padrão.

* **** Disposições comunitárias:
   * ****
Provedor de traduçãoSelecione o provedor de tradução na lista suspensa. O padrão é 
`microsoft`, o serviço de avaliação.

   * ****
Categoria de conteúdoSelecione uma categoria que descreve o conteúdo que está sendo traduzido. O padrão é 
`General.`

   * **[!UICONTROL Escolher Um Local...]**
(Opcional) Ao selecionar um local para armazenar o UGC, as publicações de todas as cópias de idioma serão exibidas em uma conversa global. Por convenção, escolha a localidade para o [idioma base](sites-console.md#translation) para o site. Escolher `No Common Store` desativará a tradução global. Por padrão, a tradução global está desativada.

* **** Guia do ativo: pode ser deixado como padrão.
* Selecione **[!UICONTROL OK]**

#### Ativação {#activation}

O novo serviço de nuvem de integração de tradução precisará ser ativado para o ambiente de publicação. Quando associado a um site, se ainda não estiver ativado, o fluxo de trabalho de ativação solicitará a publicação dessa configuração de serviço de nuvem quando a página à qual está associado for publicada.

## Gerenciando configurações de tradução {#managing-translation-settings}

>[!NOTE]
>
>**Idioma preferencial**
>
>Para detectar se a publicação está em um idioma diferente do idioma preferencial, o idioma preferencial do visitante deve ser estabelecido.
>
>O idioma preferencial é a preferência de idioma definida no perfil de um usuário, quando o visitante do site está conectado e especificou uma preferência de idioma.
>
>Quando o visitante do site é anônimo ou não especificou uma preferência de idioma em seu perfil, o idioma preferencial é o idioma base do modelo de página.

### Preferência do usuário {#user-preference}

#### Perfil de usuário {#user-profile}

Todos os Sites de comunidades fornecem um perfil de usuário que tenha feito logon, que pode editar para se identificar com a comunidade e definir suas preferências.

Uma dessas configurações é sempre exibir ou não o conteúdo da comunidade em seu idioma preferido. Por padrão, a configuração não está definida e será padronizada com a configuração do sistema. O usuário pode alterar a configuração para Ligado ou Desligado, substituindo assim a configuração do sistema.

Quando as páginas são traduzidas automaticamente para o idioma preferencial do usuário, a interface do usuário para mostrar o texto original e melhorar a tradução ainda é disponibilizada.

![perfil de usuário](assets/translation-integration4.png)

### Configuração do site da comunidade {#community-site-setting}

Quando um Site de comunidade é criado, a opção de tradução pode ser ativada e configurada. A configuração de tradução está em vigor para o conteúdo que os visitantes anônimos do site podem visualizar, mas é substituída pela configuração de perfil do usuário.
