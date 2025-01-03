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
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '179'
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
