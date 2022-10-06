---
title: Configuração das extensões do Acrobat Reader DC para captura de dados
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: Saiba como configurar extensões do Acrobat Reader DC para captura de dados.
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Configuração das extensões do Acrobat Reader DC para captura de dados {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Se os usuários da instalação do AEM forms usarem a funcionalidade de captura de dados do Content Services (obsoleto), é recomendável criar uma função com acesso somente leitura para esses usuários.

***observação **: O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados em seres humanos. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [Documento de ciclo de vida do produto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).*

A captura de dados exige que você atribua uma função de usuário para acessar a SampleReaderExtensionsCredential. Você pode atribuir a função de Administrador de Confiança padrão, mas considere que essa função fornece aos usuários gerais e não administrativos privilégios de administrador poderosos que controlam as configurações de Confiança de PKI e gerenciam as Credenciais de PKI, o que poderia comprometer a segurança da instalação dos formulários de AEM em um ambiente de produção. Recomenda-se que o administrador do sistema dos formulários AEM crie uma função que conceda somente leitura ao Armazenamento de Confiança e atribua essa nova função a usuários não administradores que usam captura de dados.

## Criar uma função para usuários de captura de dados {#create-a-role-for-data-capture-users}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Insira o nome da função (por exemplo, Usuário da captura de dados) e a descrição nos campos apropriados, em seguida, clique em Avançar.
1. Na tela Permissões de função , clique em Localizar permissões e selecione Leitura de credencial na lista de permissões disponíveis.
1. Clique em OK e depois em Concluir.

## Atribuir a função de captura de dados {#assign-the-data-capture-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Localizar.
1. Clique na função de usuário de captura de dados criada.
1. Na guia Usuários/grupos da função , clique em Localizar usuários/grupos.
1. Na tela Localizar usuários e grupos, clique em Localizar, selecione os usuários que exigem a função de usuário de captura de dados e clique em OK.
1. Na tela Editar função , clique em Salvar.
