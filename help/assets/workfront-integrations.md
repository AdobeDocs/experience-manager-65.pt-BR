---
title: '[!DNL Experience Manager Assets] integração com  [!DNL Adobe Workfront]'
description: Introdução à integração entre [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Developer
feature: Workfront Integrations and Apps
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
solution: Experience Manager, Workfront
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 4%

---

# Integração de [!DNL Adobe Experience Manager Assets] com [!DNL Adobe Workfront] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Este artigo |

O [!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração entre o [!DNL Workfront] e o [!DNL Adobe Experience Manager Assets] permite que as organizações melhorem a velocidade do conteúdo e o prazo para comercialização, conectando intrinsecamente o gerenciamento de trabalho e de ativos digitais. No contexto do gerenciamento de trabalho no Workfront, os usuários têm acesso aos documentos e imagens necessários.

O [!DNL Workfront for Experience Manager enhanced connector] permite processos de negócios aprimorados com fluxos de trabalho completos e fornece experiências personalizadas e armazenamento central completos para o cliente. A Adobe oferece um conector padrão e um conector aprimorado para integrar as duas soluções. Consulte os recursos com suporte abaixo para obter uma comparação e consulte [novidades no [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permite que sua organização:

* Crie automaticamente pastas vinculadas do Experience Manager no Workfront e organize as pastas com base em Portfólios, Programas e Projetos do Workfront.
* Sincronizar metadados de projeto do Workfront com pastas vinculadas do Experience Manager.
* Atualizações de metadados do Experience Manager com novas versões.
* Defina os status do objeto do Workfront com base em condições configuráveis usando workflows do Experience Manager.
* Publicar ativos no ambiente de publicação do Experience Manager ou no Brand Portal.

Consulte o suporte à plataforma e os [pré-requisitos do conector aprimorado](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* A Adobe requer a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantada e configurada sem um parceiro certificado ou [!DNL Adobe Professional Services], não é suportada pela Adobe.
>
>* A Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam este conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso deste conector.
>
>* O Adobe oferece suporte às versões avançadas de conectores 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, navegue até o grupo `digital.hoodoo` disponível no painel esquerdo no [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulte [Exame de certificação de parceiro para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte o [Guia do Exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Comparar diferentes integrações entre [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

A seguir estão os detalhes das funcionalidades disponíveis por meio de vários tipos de integrações entre o [!DNL Assets] e o [!DNL Workfront].

| Destaque | Descrição | [!DNL Workfront] e [!DNL Assets Essentials] *Nenhum conector (pronto para uso)* | [!DNL Workfront for Experience Manager enhanced connector] *Requer Conector* | Workfront e [!DNL Experience Manager as a Cloud Service] *Nenhum Conector (pronto para uso)* |
|----|----|----|-----|-----|
| Métodos de implantação | Apropriado para qual oferta [!DNL Assets]. | Assets Essentials | Adobe Managed Services, no local | Cloud Service |
| **Geral** |  |  |  |  |
| Enviar arquivos digitais de [!DNL Workfront] para [!DNL Assets] | A versão mais recente de um documento WF pode ser carregada no AEM Assets, que está vinculado como uma nova versão do documento. | ✓ | ✓ | ✓ |
| Vincular manualmente pastas do AEM a objetos do Workfront | As pastas existentes do AEM podem ser vinculadas como uma pasta do Workfront e seus ativos secundários são vinculados como novos documentos do Workfront. | ✓ | ✓ | ✓ |
| Vincular [!DNL Assets] a objetos do Workfront | Os ativos existentes no AEM podem ser vinculados a um novo documento do Workfront ou como uma nova versão de um documento existente. | ✓ | ✓ | ✓ |
| O Assets adicionado às pastas vinculadas é enviado automaticamente para o AEM | Se um documento for adicionado a uma pasta vinculada, o ativo associado será carregado automaticamente no AEM Assets como um novo ativo. | ✓ | ✓ | ✓ |
| Baixar o AEM Assets vinculado no Workfront | Quando um ativo é vinculado no Workfront, o usuário pode baixar os bytes do ativo. | ✓ | ✓ | ✓ |
| Pesquisar por AEM Assets no Workfront | O seletor de AEM Assets no Workfront permite pesquisas de texto completo por ativos. | ✓ | ✓ | ✓ |
| Pesquisar pastas do AEM no Workfront | O seletor de AEM Assets no Workfront permite pesquisas de texto completo para pastas. | ✓ | ✓ | ✓ |
| Exibir e Navegar pela Hierarquia de Pastas do AEM a partir do Workfront | O seletor de AEM Assets no Workfront permite a navegação da hierarquia do AEM Assets limitada pelo   controles de acesso associados do usuário e permissões definidos no AEM. | ✓ | ✓ | ✓ |
| Rastrear as versões do ativo nas linhas do tempo do AEM | Mantenha o histórico de versões do documento entre o Workfront e o AEM. | ✓ | ✓ | ✓ |
| Desvincular o Assets do AEM Assets no Workfront | Um ativo vinculado existente do AEM pode ser desvinculado do documento associado do Workfront. Isso não exclui o ativo original no AEM. | ✓ | ✓ | ✓ |
| Adicionar ativo de nova versão do Workfront ao AEM Assets | Quando uma versão recém-adicionada é adicionada em um documento no Workfront, um usuário pode enviar a nova versão para o AEM para substituir a versão existente. | ✓ | ✓ | ✓ |
| Assets vinculada no Workfront quando clicada em Direcionar usuário para o AEM | Os usuários são direcionados ao AEM para visualizar um ativo vinculado no Workfront. | ✓ | ✓ | Próximos |
| Criar automaticamente pastas vinculadas do AEM no Workfront | Crie automaticamente pastas vinculadas do AEM no Workfront usando status de projeto. Configure automaticamente pastas do AEM com base em Portfólios, Programas e Projetos do Workfront. | Não | ✓ | Não |
| Navegar diretamente para repositórios AEM a partir do Workfront | Permitir que os usuários naveguem até os repositórios disponíveis do AEM configurados no Workfront. | ✓ | Não | ✓ |
| Criar pastas vinculadas do AEM no Workfront | Crie manualmente pastas vinculadas do AEM no Workfront usando a opção disponível na guia Documentos. | ✓ | Não | ✓ |
| Sincronização de comentários | Sincronizar comentários automaticamente para ativos de [!DNL Workfront] a [!DNL Assets] | Não | ✓ | Não |
| Suporte a vários ambientes Workfront conectados a um único ambiente AEM | Usuários de vários ambientes do Workfront podem se conectar a um único ambiente do AEM. | ✓ | Não | ✓ |
| Suporte a vários ambientes AEM conectados a um único ambiente Workfront | Os usuários em um único ambiente do Workfront podem enviar ou vincular ativos entre vários ambientes do AEM. | ✓ | ✓ | ✓ |
| **Metadados** |  |  |  |  |
| Mapear metadados de ativos do Workfront para o AEM Assets | As propriedades de objetos e formulários personalizados do Workfront podem ser mapeadas para as propriedades de metadados de ativos do AEM. Os valores são enviados no upload/link inicial. | ✓ | ✓ | ✓ |
| Criar automaticamente Forms personalizados de documentos no Workfront | Anexe formulários personalizados a documentos, tarefas e problemas do Workfront usando fluxos de trabalho do AEM. | Não | ✓ | Não |
| Atualização automática bidirecional de metadados entre o AEM Assets e o Workfront | Atualize automaticamente os metadados entre o AEM Assets e o Workfront. O ativo deve ser enviado inicialmente do Workfront para o AEM e os metadados de ativos do Workfront devem ser mapeados para ativos do AEM para que as atualizações bidirecionais de metadados funcionem adequadamente. | Não | ✓ | Não |
| Visualização em tempo real no Workfront para metadados mapeados para o AEM | Visualize os metadados mapeados atualizados para o AEM nos painéis Detalhes do documento e Resumo do documento do Workfront. | ✓ | Não | ✓ |
| Envio em tempo real de metadados atualizados do Workfront para o AEM | Atualizar automaticamente os metadados do Workfront mapeados para o AEM sem recarregar um ativo ou uma nova versão de um ativo. | ✓ | Não | ✓ |
| Mapear metadados do Workfront para pastas do AEM Assets | Sincronizar metadados de projeto do Workfront com pastas vinculadas do AEM. | Não | ✓ | ✓ |
| Atualizações de metadados do AEM com novas versões | Uma configuração no AEM pode ser feita para determinar se um ativo de versão recente no Workfront também envia com quaisquer alterações feitas nos metadados. | Não | ✓ | Não |
| Atualizar automaticamente os metadados do AEM nas alterações no Forms personalizado no Workfront | O AEM permite assinar as atualizações nos formulários de documento no Workfront. Como resultado, qualquer atualização nos metadados de formulário personalizados do documento do Workfront edita os valores dos campos de metadados do AEM mapeados. | Não | ✓ | Não |
| **Fluxos de trabalho (prontos para uso)** |  |  |  |  |
| Criar nova versão de prova no Assets vinculado | Ao vincular um ativo no Workfront, uma prova pode ser gerada automaticamente. | Não | Personalizado | Não |
| Definir status em objetos do Workfront | Definir status de objetos do Workfront com base em condições configuráveis usando workflows do AEM | Não | ✓ | Próximos |
| Publicar o Assets no ambiente de publicação do AEM ou no Brand Portal | Dê aos usuários do Workfront a opção de publicar automaticamente ativos vinculados em um ambiente de publicação do AEM ou no Brand Portal. | Não | ✓ | Próximos |
