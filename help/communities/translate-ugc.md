---
title: Tradução de conteúdo gerado pelo usuário
description: Saiba como a tradução de conteúdo UGC permite que visitantes e membros do site experimentem uma comunidade global ao remover barreiras de idioma.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: ac54f06e-1545-44bb-9f8f-970f161ebb72
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Tradução de conteúdo gerado pelo usuário {#translating-user-generated-content}

O recurso de tradução das Comunidades Adobe Experience Manager (AEM) estende o conceito de [tradução do conteúdo da página](../../help/sites-administering/translation.md) para o conteúdo gerado pelo usuário (UGC) postado nos sites da comunidade usando [componentes de estrutura de componente social (SCF)](scf.md).

A tradução do UGC permite que visitantes e membros do site experimentem uma comunidade global ao remover barreiras de idioma.

Por exemplo, suponha que:

* Um membro da França posta uma receita em francês no fórum comunitário de um site multinacional de culinária.
* Outro membro do Japão usa o recurso de tradução para acionar a tradução da fórmula do francês para o japonês.
* Depois de ler a receita em japonês, o membro japonês então posta um comentário em japonês.
* O membro da França usa o recurso de tradução para traduzir o comentário japonês para o francês.
* Comunicação global.

## Visão geral {#overview}

Esta seção discute especificamente como o serviço de tradução funciona com o UGC. Ele também pressupõe que você tenha uma compreensão de como conectar o AEM a um [provedor de serviços de tradução](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e integrar esse serviço a um site configurando uma [estrutura de integração de tradução](../../help/sites-administering/tc-tic.md).

Quando um provedor de serviços de tradução é associado ao site, cada cópia de idioma do site mantém seus próprios threads de UGC publicados por meio de componentes SCF, como comentários.

Quando uma integração de tradução é configurada além do provedor de serviços de tradução, é possível que cada cópia de idioma do site compartilhe um único thread de UGC, fornecendo comunicação global entre cópias de idioma. Em vez de uma thread de discussão segregada por idioma, o [armazenamento global compartilhado](#global-translation-of-ugc) configurado permite que a thread inteira fique visível, independentemente da cópia de idioma que está sendo exibida. Além disso, várias configurações de integração de tradução podem ser configuradas, especificando diferentes lojas globais compartilhadas para um agrupamento lógico de participantes globais, como por regiões.

## O serviço de tradução padrão {#the-default-translation-service}

O AEM Communities inclui uma [licença de avaliação](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) para um [serviço de tradução padrão](../../help/sites-administering/tc-msconf.md) habilitado para vários idiomas.

Ao [criar um site de comunidade](sites-console.md), o serviço de tradução padrão é habilitado quando `Allow Machine Translation` é verificado no subpainel [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>O serviço de tradução padrão é somente para demonstração.
>
>Para um sistema de produção, é necessário um serviço de tradução licenciado. Se não for licenciado, o serviço de tradução padrão deve ser [desativado](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Tradução global do UGC {#global-translation-of-ugc}

Quando um site tem várias [cópias de idioma](../../help/sites-administering/tc-prep.md), o serviço de tradução padrão não reconhece que o UGC inserido em um site pode estar relacionado ao UGC inserido em outro. Isso é verdade quando o UGC é gerado pelo mesmo componente (a cópia de idioma da página que contém o componente).

É semelhante a grupos de pessoas que discutem um tópico. Eles não estão cientes dos comentários que são feitos em grupos que não os seus, em comparação com todos os que participam de um grande grupo em uma conversa.

Se desejar &quot;uma conversa em grupo&quot;, é possível habilitar a tradução global em um site com várias cópias de idioma, de modo que a thread inteira fique visível, independentemente da cópia de idioma que está sendo visualizada.

Por exemplo, se um fórum foi estabelecido no site base, cópias de idioma criadas e a tradução global foi ativada, um tópico postado no fórum feito em uma cópia de idioma será exibido em todas as cópias de idioma. O mesmo se aplica a todas as respostas, independentemente de qual cópia de idioma foi inserida. O resultado seria que o tópico e todo o seu encadeamento de respostas ficariam visíveis, independentemente de qual cópia de idioma o tópico está sendo visualizado.

>[!CAUTION]
>
>Qualquer UGC que existia antes da tradução global não é mais visível.
>
>Embora a UGC ainda esteja no [repositório comum](working-with-srp.md), ela está localizada no local do UGC específico do idioma, enquanto o novo conteúdo, adicionado após a configuração da tradução global, está sendo recuperado do local do repositório compartilhado global.
>
>Não há ferramenta de migração para mover ou mesclar conteúdo específico de idioma no armazenamento global compartilhado.

### Configuração da integração da tradução {#translation-integration-configuration}

Para criar uma Integração de tradução, que integra um conector do Serviço de tradução ao site na instância do autor:

* Fazer logon como administrador
* No [menu principal](http://localhost:4502/)
* Selecionar **[!UICONTROL Ferramentas]**
* Selecionar **[!UICONTROL Operações]**
* Selecionar **[!UICONTROL Nuvem]**
* Selecionar **[!UICONTROL Cloud Service]**
* Role para baixo até **[!UICONTROL Integração de tradução]**

  ![integração-tradução](assets/translation-integration.png)

* Selecione **[!UICONTROL Mostrar configurações]**

  ![configuração de exibição](assets/translation-integration1.png)

* Selecione o ícone `[+]` ao lado de **[!UICONTROL Configurações Disponíveis]** para que você possa criar uma configuração.

#### Caixa de diálogo Criar configuração {#create-configuration-dialog}

![criar-configuração](assets/translation-integration2.png)

* **[!UICONTROL Configuração pai]**

  (Obrigatório) Normalmente, deixa como padrão. O padrão é `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**

  (Obrigatório) Insira um título de exibição de sua escolha. Nenhum valor padrão.

* **[!UICONTROL Nome]**

  (Opcional) Insira um nome para a configuração. O padrão é um nome de nó com base no Título.

* Selecionar **[!UICONTROL Criar]**

#### Caixa de diálogo de configuração de tradução {#translation-config-dialog}

![caixa de diálogo de configuração](assets/translation-integration3.png)

Para obter instruções detalhadas, consulte [Criando uma Configuração de Integração de Tradução](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* Guia **[!UICONTROL Sites]**: pode deixar como padrão.

* Guia **[!UICONTROL Comunidades]**:
   * **[!UICONTROL Provedor de tradução]**
Selecione o provedor de tradução na lista suspensa. O padrão é `microsoft`, o serviço de avaliação.

   * **[!UICONTROL Categoria de conteúdo]**
Selecione uma categoria que descreva o conteúdo que está sendo traduzido. O padrão é `General.`

   * **[!UICONTROL Escolher Uma Localidade...]**
(Opcional) Ao selecionar um local para armazenar UGC, as publicações de todas as cópias de idioma aparecem em uma conversa global. Por convenção, escolha a localidade para o [idioma base](sites-console.md#translation) do site. Escolher `No Common Store` desabilita a tradução global. Por padrão, a tradução global está desativada.

* Guia **[!UICONTROL Assets]**: pode deixar como padrão.
* Selecione **[!UICONTROL OK]**

#### Ativação {#activation}

O novo serviço de nuvem da integração de tradução deve ser ativado para o ambiente do Publish. Quando associado a um site, se ainda não estiver ativado, o fluxo de trabalho de ativação solicitará a publicação dessa configuração do Cloud Service quando a página com a qual ele está associado for publicada.

## Gerenciamento de configurações de tradução {#managing-translation-settings}

>[!NOTE]
>
>**Idioma Preferencial**
>
>Ao detectar se a publicação está em um idioma diferente do idioma preferencial, o idioma preferencial do visitante do site deve ser estabelecido.
>
>O idioma preferencial é a preferência de idioma definida no perfil de um usuário, quando o visitante do site está conectado e especificou uma preferência de idioma.
>
>Quando o visitante do site é anônimo ou não especificou uma preferência de idioma em seu perfil, o idioma preferencial é o idioma base do modelo de página.

### Preferência do usuário {#user-preference}

#### Perfil de usuário {#user-profile}

Todos os Sites de comunidades fornecem um perfil de usuário que os membros conectados podem editar para se identificarem na comunidade e definirem suas preferências.

Uma dessas configurações é sempre exibir o conteúdo da comunidade no idioma de sua preferência. Por padrão, a configuração não é definida e o padrão é a configuração do sistema. O usuário pode alterar a configuração para Ligado ou Desligado para substituir a configuração do sistema.

Quando as páginas são traduzidas automaticamente para o idioma preferencial do usuário, a interface do usuário para mostrar o texto original e melhorar a tradução ainda é disponibilizada.

![perfil-usuário](assets/translation-integration4.png)

### Configuração do site da comunidade {#community-site-setting}

Quando um site da comunidade é criado, a opção de tradução pode ser ativada e configurada. A configuração de tradução está em vigor para o conteúdo que os visitantes do site podem visualizar, mas é substituída pela configuração de perfil do usuário.
