---
title: Gerenciar listas de revogação de certificados
description: Saiba como gerenciar listas de certificados revogados. Você pode importar, editar e excluir listas de certificados revogados (CRLs) usando o Gerenciamento de Repositório de Confiança.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# Gerenciar listas de revogação de certificados{#managing-certificate-revocationlists}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Usando o Gerenciamento de Repositório de Confiança, você pode importar, editar e excluir listas de certificados revogados (CRLs). Listas de certificados revogados codificadas em Base64 e DER são suportadas.

## Importar uma CRL {#import-a-crl}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Listas de revogação de certificados e, em seguida, clique em Importar.
1. Na caixa Alias, digite um identificador para a CRL.
1. Clique em Procurar para localizar a CRL e clique em OK.

## Exportar uma CRL {#export-a-crl}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Listas de revogação de certificados.
1. Clique no nome do alias da CRL, para poder exportá-la, e clique em Exportar.
1. Siga as instruções para exportar a CRL. As CRLs são exportadas na codificação Base64.
1. Clique em OK.

## Excluir uma CRL {#delete-a-crl}

1. No console de administração, clique em Configurações > Gerenciamento de armazenamento de confiança > Listas de revogação de certificados.
1. Marque as caixas de seleção das CRLs a serem excluídas, clique em Excluir e, em seguida, clique em OK.
