---
title: Remover os sites do Geometrixx
seo-title: Removing the Geometrixx Sites
description: Saiba como remover o conteúdo de amostra do Geometrixx.
seo-description: Learn how to remove the sample Geometrixx content.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Remover os sites do Geometrixx{#removing-the-geometrixx-sites}

AEM vem com um conjunto de sites de exemplo do Geometrixx. Você pode remover esse conteúdo de amostra por meio do **Gerenciador de pacotes**.

Os pacotes relacionados ao geometrixx individuais são:

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Para remover um pacote individual, clique com o botão **Desinstalar** nesse pacote.

Há também um super pacote:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Este pacote inclui todos os pacotes individuais acima. Para remover todo o conteúdo relacionado ao geometrixx de uma só vez, clique em **Desinstalar** neste pacote. O super-pacote entrará no estado desinstalado e todos os pacotes individuais desaparecerão da visualização do gerenciador de pacotes.

Agora você tem uma instância de AEM &quot;vazia&quot; sem nenhum site de demonstração.

>[!NOTE]
>
>Ao atualizar, os sites geometrixx são reinstalados automaticamente. Talvez seja necessário remover sites geometrixx após a atualização, caso não queira essas amostras.

