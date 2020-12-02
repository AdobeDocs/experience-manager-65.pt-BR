---
title: Configuração de extensões Acrobat Reader DC para captura de dados
seo-title: Configuração de extensões Acrobat Reader DC para captura de dados
description: Saiba como configurar extensões do Acrobat Reader DC para captura de dados.
seo-description: Saiba como configurar extensões do Acrobat Reader DC para captura de dados.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Configuração de extensões Acrobat Reader DC para captura de dados {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Se os usuários da instalação de formulários AEM usarem a funcionalidade de captura de dados do Content Services (obsoleto), é recomendável criar uma função com acesso somente leitura para esses usuários.

***observação **: O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gestão de conteúdo instalado com o LiveCycle. Ela permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto do Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Para saber mais sobre a configuração do Content Services (obsoleto), consulte [Administração do Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

A captura de dados exige que você atribua uma função de usuário para acessar a SampleReaderExtensionsCredential. Você pode atribuir a função de Administrador de Confiança padrão, mas considere que essa função fornece aos usuários gerais e não administrativos privilégios poderosos de administrador que controlam as configurações de Confiança de PKI e gerenciam as Credenciais de PKI, o que pode comprometer a segurança da instalação dos formulários AEM em um ambiente de produção. É recomendável que o administrador do sistema de formulários AEM crie uma função que conceda somente acesso somente leitura ao Repositório de confiança e atribua essa nova função a usuários que não sejam administradores e que usem a captura de dados.

## Criar uma função para usuários de captura de dados {#create-a-role-for-data-capture-users}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Insira o nome da função (por exemplo, Usuário de captura de dados) e a descrição nos campos apropriados e clique em Avançar.
1. Na tela Permissões de função, clique em Localizar permissões e selecione Leitura de credenciais na lista de permissões disponíveis.
1. Clique em OK e em Concluir.

## Atribuir a função de captura de dados {#assign-the-data-capture-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e clique em Localizar.
1. Clique na função de usuário de captura de dados que você criou.
1. Na guia Usuários/grupos da função, clique em Localizar usuários/grupos.
1. Na tela Localizar usuários e grupos, clique em Localizar, selecione os usuários que exigem a função de usuário de captura de dados e clique em OK.
1. Na tela Editar função, clique em Salvar.

