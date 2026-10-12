---
title: Configuração das extensões do Acrobat Reader DC para captura de dados
description: Saiba como configurar as extensões do Acrobat Reader DC para captura de dados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%
---
# Configuração das extensões do Acrobat Reader DC para captura de dados {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Se os usuários da instalação do AEM Forms usarem a funcionalidade de captura de dados do Content Services (Obsoleto), será recomendável criar uma função com acesso somente leitura para esses usuários.

***Observação &#x200B;**: o Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários projetem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Content Services (obsoleto) termina em 31/12/2014. Consulte o [documento sobre o ciclo de vida do produto Adobe](https://helpx.adobe.com/br/support/programs/eol-matrix.html).*

A captura de dados exige que você atribua uma função de usuário para acessar SampleReaderExtensionsCredential. Você pode atribuir a função Administrador Confiável padrão. No entanto, considere que essa função oferece privilégios gerais de administrador de usuários não administrativos que controlam as configurações de Confiança da PKI e gerenciam Credenciais da PKI, o que pode comprometer a segurança da instalação dos AEM Forms em um ambiente de produção. Recomenda-se que o administrador do sistema do AEM Forms crie uma função que conceda somente leitura ao Armazenamento de confiança e atribua essa nova função a usuários não administradores que usam captura de dados.

## Criar uma função para usuários de captura de dados {#create-a-role-for-data-capture-users}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Insira o nome da função (por exemplo, Usuário da Captura de Dados) e a descrição nos campos apropriados, depois clique em Próximo.
1. Na tela Permissões de função, clique em Localizar permissões e selecione Leitura de credencial na lista de permissões disponíveis.
1. Clique em OK e em Finish.

## Atribuir a função de captura de dados {#assign-the-data-capture-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e clique em Localizar.
1. Clique na função de usuário de captura de dados criada.
1. Na guia Usuários/Grupos de função, clique em Localizar usuários/grupos.
1. Na tela Localizar usuários e grupos, clique em Localizar, selecione os usuários que requerem a função de usuário de captura de dados e clique em OK.
1. Na tela Editar função, clique em Salvar.
