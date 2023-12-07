---
title: Remover os sites do Geometrixx
description: Saiba como remover o conteúdo de Geometrixx de exemplo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Remover os sites do Geometrixx{#removing-the-geometrixx-sites}

O AEM vem com um conjunto de exemplos de sites de Geometrixx. Você pode remover esse conteúdo de amostra por meio da **Gerenciador de pacotes**.

Os pacotes individuais relacionados ao geometrixx são:

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

Este pacote inclui todos os pacotes individuais acima. Para remover todo o conteúdo relacionado ao geometrixx de uma só vez, clique em **Desinstalar** neste pacote. O superpacote entra no estado desinstalado e todos os pacotes individuais desaparecem da exibição do Gerenciador de pacotes.

Agora você tem uma instância &quot;vazia&quot; do AEM sem nenhum site de demonstração.

>[!NOTE]
>
>Ao atualizar, os sites do Geometrixx são automaticamente reinstalados. Remova os sites do Geometrixx depois da atualização se não quiser essas amostras.

