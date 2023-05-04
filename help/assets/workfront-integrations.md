---
title: '[!DNL Experience Manager Assets] integração com [!DNL Adobe Workfront]'
description: Introdução à integração entre [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] integração com [!DNL Adobe Workfront] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Este artigo |

O [!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração entre [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] permite que as organizações melhorem a velocidade do conteúdo e o tempo de comercialização, conectando intrinsecamente o trabalho e o gerenciamento de ativos digitais. No contexto do gerenciamento de seu trabalho no Workfront, os usuários têm acesso aos documentos e imagens necessários.

O [!DNL Workfront for Experience Manager enhanced connector] permite processos de negócios aprimorados com fluxos de trabalho completos e fornece experiências personalizadas de cliente completo e armazenamento central. O Adobe oferece um conector padrão e um conector avançado para integrar as duas soluções. Veja os recursos compatíveis abaixo para uma comparação e consulte [novidades da [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permite que sua organização:

* Crie pastas de Experience Manager vinculadas automaticamente no Workfront e organize as pastas com base em Portfolio, programas e projetos da Workfront.
* Sincronize os metadados do projeto Workfront com as pastas de Experience Manager vinculadas.
* Atualizações de metadados de Experience Manager com novas versões.
* Defina os status do objeto Workfront com base nas condições configuráveis usando workflows do Experience Manager.
* Publique ativos no ambiente de publicação do Experience Manager ou no Brand Portal.

Consulte o suporte da plataforma e [pré-requisitos para o conector aprimorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam redundante este conector; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.
>
>* O Adobe oferece suporte ao conector avançado versões 1.7.4 e superior. Não há suporte para pré-lançamento e versões personalizadas anteriores. Para verificar a versão do conector aprimorado, navegue até a `digital.hoodoo` disponível no painel esquerdo em [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR).
>
>* Consulte [Exame de certificação de parceiro para Workfront para conector aprimorado Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia de exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Comparar diferentes integrações entre [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Veja a seguir os detalhes das funcionalidades disponíveis por meio de vários tipos de integrações entre [!DNL Assets] e [!DNL Workfront].

| Destaque | Descrição | [!DNL Workfront] e [!DNL Assets Essentials] *Sem conector (OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Requer conector* | Workfront e [!DNL Experience Manager as a Cloud Service] *Sem conector (OOTB)* |
|----|----|----|-----|-----|
| Métodos de implantação | Adequado [!DNL Assets] oferta. | Assets Essentials | Adobe Managed Services, no local | Serviço em nuvem |
| **Geral** |
| Enviar arquivos digitais de [!DNL Workfront] para [!DNL Assets] | A versão mais recente de um documento WF pode ser carregada para o AEM Assets, que será vinculada como uma nova versão do documento. | ✓ | ✓ | ✓ |
| Vincular manualmente AEM pastas a objetos Workfront | As pastas AEM existentes podem ser vinculadas como uma pasta Workfront e seus ativos filhos são vinculados como novos documentos Workfront. | ✓ | ✓ | ✓ |
| Link [!DNL Assets] para objetos Workfront | Os ativos existentes no AEM podem ser vinculados a um novo documento do Workfront ou como uma nova versão de um documento existente. | ✓ | ✓ | ✓ |
| Os ativos adicionados às pastas vinculadas são enviados automaticamente para AEM | Se um documento for adicionado a uma pasta vinculada, o ativo associado será carregado automaticamente no AEM Assets como um novo ativo. | ✓ | ✓ | ✓ |
| Baixar o Linked AEM Assets no Workfront | Quando um ativo é vinculado no Workfront, o usuário pode baixar os bytes do ativo. | ✓ | ✓ | ✓ |
| Pesquisar AEM Assets no Workfront | O seletor AEM Assets no Workfront permite pesquisas em texto completo de ativos. | ✓ | ✓ | ✓ |
| Pesquisar AEM pastas no Workfront | O seletor AEM Assets no Workfront permite pesquisas de texto completo para pastas. | ✓ | ✓ | ✓ |
| Exibir e navegar AEM Hierarquia de Pastas no Workfront | O seletor do AEM Assets no Workfront permite navegar pela hierarquia do AEM Assets limitada pelos controles de acesso associados do usuário e pelas permissões definidas no AEM. | ✓ | ✓ | ✓ |
| Rastrear versões de ativos em AEM linhas do tempo | Manter histórico de versão do documento entre o Workfront e o AEM. | ✓ | ✓ | ✓ |
| Desvincular ativos da AEM Assets no Workfront | Um ativo vinculado existente do AEM pode ser desvinculado do documento do Workfront associado. Isso não exclui o ativo original dentro do AEM. | ✓ | ✓ | ✓ |
| Adicionar ativo com versão recente ao AEM Assets a partir do Workfront | Quando uma versão recém adicionada é adicionada em um documento no Workfront, um usuário pode enviar a nova versão para AEM para substituir a versão existente. | ✓ | ✓ | ✓ |
| Ativos vinculados no Workfront quando clicados em Usuário direto para AEM | Os usuários são direcionados ao AEM para visualizar um ativo vinculado no Workfront. | ✓ | ✓ | Em breve |
| Criar automaticamente pastas de AEM vinculadas no Workfront | Criar automaticamente pastas de AEM vinculadas no Workfront usando os status do projeto. Configure automaticamente AEM pastas com base em Portfolio, programas e projetos da Workfront. | Não | ✓ | Não |
| Navegue diretamente para AEM repositórios do Workfront | Permita que os usuários naveguem até repositórios AEM disponíveis configurados no Workfront. | ✓ | Não | ✓ |
| Criar pastas de AEM vinculadas no Workfront | Crie manualmente AEM pastas vinculadas no Workfront usando a opção disponível na guia Documents . | ✓ | Não | ✓ |
| Sincronização de comentários | Sincronizar automaticamente comentários de ativos do [!DNL Workfront] para [!DNL Assets] | Não | ✓ | Não |
| Suporte para vários ambientes Workfront conectando-se a um único ambiente de AEM | Os usuários de vários ambientes Workfront podem se conectar a um único ambiente de AEM. | ✓ | Não | ✓ |
| Oferecem suporte a vários ambientes AEM conectados a um único ambiente Workfront | Os usuários em um único ambiente do Workfront podem enviar ou vincular ativos entre vários ambientes de AEM. | ✓ | ✓ | ✓ |
| **Metadados** |
| Mapear metadados de ativos do Workfront para o AEM Assets | As propriedades de objeto e formulário personalizado do Workfront podem ser mapeadas para AEM propriedades de metadados de ativos. Os valores serão enviados no upload/link inicial. | ✓ | ✓ | ✓ |
| Criar automaticamente Forms personalizada de documentos no Workfront | Anexe formulários personalizados a documentos, tarefas e problemas do Workfront usando fluxos de trabalho AEM. | Não | ✓ | Não |
| Atualização automática bidirecional de metadados entre o AEM Assets e a Workfront | Atualizar automaticamente metadados entre o AEM Assets e o Workfront. Inicialmente, o ativo deve ser enviado do Workfront para o AEM e os metadados do ativo do Workfront devem ser mapeados para AEM ativos para que as atualizações de metadados bidirecionais funcionem adequadamente. | Não | ✓ | Não |
| Exibição em tempo real no Workfront para metadados mapeados para AEM | Visualize os metadados mapeados atualizados para AEM nos painéis Detalhes do documento e Resumo do documento da Workfront. | ✓ | Não | ✓ |
| Push em tempo real de metadados atualizados do Workfront para AEM | Atualizar automaticamente os metadados do Workfront mapeados para AEM sem retornar um ativo ou uma nova versão de um ativo. | ✓ | Não | ✓ |
| Mapear metadados do Workfront para pastas do AEM Assets | Sincronize os metadados do projeto Workfront com as pastas de AEM vinculadas. | Não | ✓ | ✓ |
| AEM atualizações de metadados com novas versões | Uma configuração no AEM pode ser feita para determinar se um ativo recém-versionado no Workfront também envia alterações para seus metadados. | Não | ✓ | Não |
| Atualizar automaticamente metadados AEM em alterações no Forms personalizado no Workfront | AEM permite assinar as atualizações para os formulários de documento no Workfront. Como resultado, qualquer atualização nos metadados de formulário personalizados do documento Workfront modifica os valores dos campos de metadados AEM mapeados. | Não | ✓ | Não |
| **Fluxos de trabalho (prontos para uso)** |
| Criar nova versão de prova em ativos vinculados | Ao vincular um ativo no Workfront, uma prova pode ser gerada automaticamente. | Não | Personalizado | Não |
| Definir status em objetos Workfront | Definir status de objeto do Workfront com base em condições configuráveis usando workflows AEM | Não | ✓ | Em breve |
| Publicar ativos no ambiente de publicação do AEM ou no Brand Portal | Dê aos usuários do Workfront a opção de publicar automaticamente ativos vinculados em um ambiente de publicação do AEM ou no Brand Portal. | Não | ✓ | Em breve |
