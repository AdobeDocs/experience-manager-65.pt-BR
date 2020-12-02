---
title: Traduzindo conteúdo gerado pelo usuário
seo-title: Traduzindo conteúdo gerado pelo usuário
description: Como o recurso de tradução funciona
seo-description: Como o recurso de tradução funciona
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
translation-type: tm+mt
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---


# Traduzindo conteúdo gerado pelo usuário {#translating-user-generated-content}

O recurso de tradução do AEM Communities estende o conceito de [tradução do conteúdo da página](../../help/sites-administering/translation.md) para o conteúdo gerado pelo usuário (UGC) postado em sites da comunidade usando [componentes do Social Component Framework (SCF)](scf.md).

A tradução do UGC permite que os visitantes do site e os membros experimentem uma comunidade global, eliminando barreiras linguísticas.

Por exemplo, suponha que:

* Um membro da França posta uma receita em francês no fórum comunitário de um site multinacional de culinária.
* Outro membro do Japão usa o recurso de tradução para acionar a tradução da receita do francês para o japonês.
* Depois de ler a receita em japonês, o membro do Japão publica um comentário em japonês.
* O membro da França usa o recurso de tradução para traduzir o comentário japonês para o francês.
* Comunicação global.

## Visão geral {#overview}

Esta seção da documentação discute especificamente como o serviço de tradução funciona com o UGC, ao mesmo tempo que assume um entendimento de como conectar AEM a um [provedor de serviço de tradução](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e integrar esse serviço em um site, configurando uma [estrutura de integração de tradução](../../help/sites-administering/tc-tic.md).

Quando um provedor de serviço de tradução é associado ao site, cada cópia de idioma do site mantém seus próprios threads do UGC publicados por componentes do SCF, como comentários.

Quando uma estrutura de integração de tradução é configurada além do provedor de serviço de tradução, é possível que cada cópia de idioma do site compartilhe um único segmento do UGC, fornecendo assim comunicação global entre cópias de idioma. Em vez de um thread de discussão segregado por idioma, o armazenamento compartilhado global configurado [permite que o thread inteiro fique visível independentemente da cópia de idioma que está sendo visualizada. ](#global-translation-of-ugc) Além disso, várias configurações de integração de tradução podem ser configuradas especificando diferentes lojas compartilhadas globais para um agrupamento lógico de participantes globais, como por regiões.

## O Serviço de Tradução Padrão {#the-default-translation-service}

A AEM Communities inclui uma [licença de avaliação](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) para um [serviço de tradução padrão](../../help/sites-administering/tc-msconf.md) ativado para vários idiomas.

Quando [criar um site da comunidade](sites-console.md), o serviço de tradução padrão é ativado quando `Allow Machine Translation` é verificado no subpainel [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>O serviço de tradução padrão é somente para demonstração.
>
>Para um sistema de produção, é necessário um serviço de tradução licenciado. Se não estiver licenciado, o serviço de tradução padrão deverá ser [desativado](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Tradução Global de UGC {#global-translation-of-ugc}

Quando um site tem várias [cópias de idioma](../../help/sites-administering/tc-prep.md), o serviço de tradução padrão não reconhece que o UGC inserido em um site pode estar relacionado ao UGC inserido em outro, como quando o UGC é, essencialmente, gerado pelo mesmo componente (a cópia de idioma da página que contém o componente).

É semelhante a grupos de pessoas que discutem um tópico desconhecendo os comentários feitos em grupos diferentes dos seus, em comparação com todos em um grande grupo que participa de uma conversa.

Se &quot;uma conversa de grupo&quot; for desejada, será possível habilitar a tradução global em um site com várias cópias de idioma, de modo que o thread inteiro esteja visível, independentemente da cópia de idioma que está sendo visualizada.

Por exemplo, se um fórum foi estabelecido no site base, as cópias de idioma criadas e a tradução global foi ativada, então um tópico publicado no fórum feito em uma cópia de idioma aparecerá em todas as cópias de idioma. O mesmo se aplica a todas as respostas, independentemente da cópia linguística da resposta. O resultado seria que o tópico e todo o seu encadeamento de respostas ficariam visíveis independentemente de qual cópia de idioma o tópico está sendo visualizado.

>[!CAUTION]
>
>Qualquer UGC que existisse antes da tradução global não é mais visível.
>
>Embora o UGC ainda esteja no [armazenamento comum](working-with-srp.md), ele está localizado no local UGC específico do idioma, enquanto o novo conteúdo, adicionado após a conversão global ter sido configurada, está sendo recuperado do local do armazenamento compartilhado global.
>
>Não há ferramenta de migração para mover ou mesclar conteúdo específico de idioma na loja compartilhada global.

### Configuração da integração da tradução {#translation-integration-configuration}

Para criar uma nova integração de tradução, que integra um conector do Serviço de tradução ao site na instância do autor:

* Fazer logon como administrador
* No menu principal [](http://localhost:4502/)
* Selecione **[!UICONTROL Ferramentas]**
* Selecione **[!UICONTROL Operações]**
* Selecionar **[!UICONTROL Nuvem]**
* Selecione **[!UICONTROL Cloud Services]**
* Role para baixo até **[!UICONTROL Integração de tradução]**

   ![integração de tradução](assets/translation-integration.png)

* Selecione **[!UICONTROL Mostrar configurações]**

   ![show-configuration](assets/translation-integration1.png)

* Selecione o ícone `[+]` ao lado de **[!UICONTROL Configurações disponíveis]** para criar uma nova configuração

#### Criar caixa de diálogo de configuração {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configuração primária]**

   (Obrigatório) Geralmente deixe como padrão. O padrão é `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**

   (Obrigatório) Insira um título de exibição de sua escolha. Nenhum valor padrão.

* **[!UICONTROL Nome]**

   (Opcional) Digite um nome para a configuração. O padrão é um nome de nó com base no Título.

* Selecione **[!UICONTROL Criar]**

#### Diálogo de configuração de tradução {#translation-config-dialog}

![diálogo de configuração](assets/translation-integration3.png)

Para obter instruções detalhadas, visite [Criando uma Configuração de Integração de Tradução](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **** Locação: pode ser deixado como padrão.

* **[!UICONTROL Disposições]** comunitárias:
   * **[!UICONTROL Provedor]**
de traduçãoSelecione o provedor de tradução na lista suspensa. O padrão é 
`microsoft`, o serviço de julgamento.

   * **[!UICONTROL Categoria]**
de conteúdoSelecione uma categoria que descreva o conteúdo que está sendo traduzido. O padrão é 
`General.`

   * **[!UICONTROL Escolher Uma Localidade...]**
(Opcional) Ao selecionar uma localidade para armazenar o UGC, as publicações de todas as cópias de idioma aparecerão em uma conversa global. Por convenção, escolha a localidade para o [idioma base](sites-console.md#translation) do site. A escolha de `No Common Store` desativará a tradução global. Por padrão, a tradução global está desativada.

* **** Ativo: pode ser deixado como padrão.
* Selecione **[!UICONTROL OK]**

#### Ativação {#activation}

O novo serviço em nuvem de integração de tradução precisará ser ativado para o ambiente de publicação. Quando associado a um site, se ainda não estiver ativado, o fluxo de trabalho da ativação solicitará a publicação dessa configuração de serviço em nuvem quando a página à qual está associada for publicada.

## Gerenciando configurações de tradução {#managing-translation-settings}

>[!NOTE]
>
>**Idioma preferencial**
>
>Para detectar se a publicação está em um idioma diferente do idioma preferencial, o idioma preferencial do visitante do site deve ser estabelecido.
>
>O idioma preferencial é a preferência de idioma definida no perfil do usuário, quando o visitante do site está conectado e especificou uma preferência de idioma.
>
>Quando o visitante do site é anônimo ou não especificou uma preferência de idioma em seu perfil, o idioma preferencial é o idioma base do modelo de página.

### Preferência do usuário {#user-preference}

#### Perfil de usuário {#user-profile}

Todos os sites das comunidades fornecem um perfil de usuário que os membros que fizeram logon podem editar para se identificar com a comunidade e definir suas preferências.

Uma dessas configurações é sempre exibir ou não o conteúdo da comunidade em seu idioma preferido. Por padrão, a configuração não está definida e será usada como padrão para a configuração do sistema. O usuário pode alterar a configuração para Ligado ou Desligado, substituindo assim a configuração do sistema.

Quando as páginas são traduzidas automaticamente para o idioma preferencial do usuário, a interface do usuário para mostrar o texto original e melhorar a tradução ainda é disponibilizada.

![perfil do usuário](assets/translation-integration4.png)

### Configuração do site da comunidade {#community-site-setting}

Quando um Site de comunidade é criado, a opção de conversão pode ser ativada e configurada. A configuração de tradução está em vigor para visitantes de site anônimos de conteúdo podem ser visualizações, mas é substituída pela configuração de perfil do usuário.
