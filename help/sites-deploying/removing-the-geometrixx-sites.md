---
title: Remoção dos sites da Geometrixx
seo-title: Remoção dos sites da Geometrixx
description: Saiba como remover o conteúdo do Geometrixx de amostra.
seo-description: Saiba como remover o conteúdo do Geometrixx de amostra.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Remoção dos sites da Geometrixx{#removing-the-geometrixx-sites}

O AEM vem com um conjunto de exemplos de sites da Geometrixx. É possível remover esse conteúdo de amostra por meio do Gerenciador **de pacotes**.

Os pacotes relacionados à geometrixx individuais são:

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Para remover um pacote individual, basta clicar em **Desinstalar** nesse pacote.

Há também um super-pacote:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Este pacote inclui todos os pacotes individuais acima. Para remover todo o conteúdo relacionado ao geometrixx de uma vez, clique em **Desinstalar** neste pacote. O superpacote entrará no estado desinstalado e todos os pacotes individuais desaparecerão da exibição do gerenciador de pacotes.

Agora você tem uma instância do AEM &quot;vazia&quot; sem nenhum site de demonstração.

>[!NOTE]
>
>Ao atualizar, os sites do geometrixx são reinstalados automaticamente. Talvez seja necessário remover os sites geometrixx após a atualização, caso não deseje essas amostras.

