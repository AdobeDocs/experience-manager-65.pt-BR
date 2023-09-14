---
title: Gerenciar listas de revogação de certificados
description: Saiba como gerenciar listas de certificados revogados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# Gerenciar listas de revogação de certificados{#managing-certificate-revocationlists}

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
