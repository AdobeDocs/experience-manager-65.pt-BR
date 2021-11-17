---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: Introdução à integração entre [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 468a8d96153c67232524eea6f180c9ceb364d60a
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] integração com [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração entre [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] permite que as organizações melhorem a velocidade do conteúdo e o tempo de comercialização, conectando intrinsecamente o trabalho e o gerenciamento de ativos digitais. No contexto do gerenciamento de seu trabalho no Workfront, os usuários têm acesso aos documentos necessários e às imagens.

O Adobe oferece dois conectores diferentes para integrar ambas as soluções. Os conectores permitem automação empresarial complexa, configuração e fluxos de trabalho extensíveis entre [!DNL Assets] e [!DNL Workfront]. Além disso, [!DNL Assets Essentials] está disponível como um complemento desse novo [!DNL Workfront] os clientes podem comprar separadamente. Para saber mais, consulte [[!DNL Workfront] and [!DNL Assets Essentials] integração](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/integration.html).

[!DNL Workfront for Experience Manage enhanced connector] permite que sua organização:

* Colabore facilmente. As equipes criativas podem se preocupar com uma coisa a menos. Agora, quando o trabalho terminar, eles poderão enviá-lo para a AEM Assets com o clique de um botão
* Enriqueça ativos em todas as etapas. Colete novos dados em cada estágio do ciclo de vida do ativo. Da ideação à entrega, sua organização pode capturar as métricas principais para tomar decisões de negócios mais informadas sobre o desenvolvimento futuro de ativos.
* Fazer referência a ativos existentes. Localize e reutilize facilmente os ativos existentes em produção e adicione-os a novos projetos como itens de referência.
* Sincronize todos os seus metadados. Aprimore seus metadados, facilitando ao máximo a adição. Com o conector , os metadados são sincronizados bidirecionalmente entre o Workfront e o AEM Assets
* Aproveitamento [!DNL Experience Manager Assets] recursos de gerenciamento digital. Acesso a todos os seus ativos digitais diretamente no seu favorito [!DNL Creative Cloud] aplicativos. Marcação e recorte inteligentes habilitados para IA, ferramentas de pesquisa, delivery dinâmico por meio de [!DNL Dynamic Media]e muito mais.

Consulte o suporte à plataforma e outros [pré-requisitos para o conector aprimorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que torna este conector redundante; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.

## Comparar diferentes integrações entre [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Veja a seguir os detalhes das funcionalidades disponíveis por meio de vários tipos de integrações entre [!DNL Assets] e [!DNL Workfront].

| Recurso | Descrição | [!DNL Workfront] e [!DNL Assets Essentials] | [!DNL Workfront] para [!DNL Experience Manager] conector | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Métodos de implantação | Adequado [!DNL Assets] oferta. | Assets Essentials | Cloud Service, Adobe Managed Services, no local | Cloud Service, Adobe Managed Services, no local |
| Enviar arquivos digitais de [!DNL Workfront] para [!DNL Assets] | A versão mais recente de um documento WF pode ser carregada para o AEM Assets, que será vinculada como uma nova versão do documento. | Instantâneo | Instantâneo | Instantâneo |
| Vincular manualmente AEM pastas a objetos Workfront | As pastas AEM existentes podem ser vinculadas como uma pasta Workfront e seus ativos filhos são vinculados como novos documentos Workfront. | Instantâneo | Instantâneo | Instantâneo |
| Link [!DNL Assets] para objetos Workfront | Os ativos existentes no AEM podem ser vinculados a um novo documento do Workfront ou como uma nova versão de um documento existente. | Instantâneo | Instantâneo | Instantâneo |
| Os ativos adicionados às pastas vinculadas são enviados automaticamente para AEM | Se um documento for adicionado a uma pasta vinculada, o ativo associado será carregado automaticamente no AEM Assets como um novo ativo. | Instantâneo | Instantâneo | Instantâneo |
| Baixar o Linked AEM Assets no Workfront | Quando um ativo é vinculado no Workfront, o usuário pode baixar os bytes do ativo. | Instantâneo | Instantâneo | Instantâneo |
| Pesquisar AEM Assets no Workfront | O seletor AEM Assets no Workfront permite pesquisas em texto completo de ativos. | Instantâneo | Instantâneo | Instantâneo |
| Exibir e navegar AEM Hierarquia de Pastas no Workfront | O seletor do AEM Assets no Workfront permite navegar pela hierarquia do AEM Assets limitada pelos controles de acesso associados do usuário e pelas permissões definidas no AEM. | Instantâneo | Instantâneo | Instantâneo |
| Desvincular ativos da AEM Assets no Workfront | Um ativo vinculado existente do AEM pode ser desvinculado do documento do Workfront associado. Isso não exclui o ativo original dentro do AEM. | Instantâneo | Instantâneo | Instantâneo |
| Adicionar ativo com versão recente ao AEM Assets a partir do Workfront | Quando uma versão recém adicionada é adicionada em um documento no Workfront, um usuário pode enviar a nova versão para AEM para substituir a versão existente. | Instantâneo | Instantâneo | Instantâneo |
| Ativos vinculados no Workfront quando clicados em Usuário direto para AEM | Os usuários são direcionados ao AEM para visualizar um ativo vinculado no Workfront. | Instantâneo | Instantâneo | Personalizado |
| Criar automaticamente pastas de AEM vinculadas no Workfront | Criar automaticamente pastas de AEM vinculadas no Workfront usando status de objeto. Organize automaticamente AEM pastas com base em Portfolio, programas e projetos da Workfront. | Não | Não | Instantâneo |
| Sincronização de comentários | Sincronizar automaticamente comentários de ativos do [!DNL Workfront] para [!DNL Assets] | Não | Instantâneo | Instantâneo |
| Mapear metadados de ativos do Workfront para o AEM Assets | As propriedades de objeto e formulário personalizado do Workfront podem ser mapeadas para AEM propriedades de metadados de ativos. Os valores serão enviados no upload/link inicial. | Instantâneo | Instantâneo | Instantâneo |
| Criar automaticamente Forms personalizada de documentos no Workfront | Anexe formulários personalizados a documentos, tarefas e problemas do Workfront usando fluxos de trabalho AEM. | Não | Adicionar manualmente o formulário personalizado e, em seguida, a sincronização automatizada funciona | Instantâneo |
| Atualização automática bidirecional de metadados entre o AEM Assets e a Workfront | Atualizar automaticamente metadados entre o AEM Assets e o Workfront. | Não | Instantâneo | Instantâneo |
| Mapear metadados do Workfront para pastas do AEM Assets | Sincronize os metadados do projeto Workfront com as pastas de AEM vinculadas. | Não | Não | Instantâneo |
| AEM atualizações de metadados com novas versões | Uma configuração no AEM pode ser feita para determinar se um ativo recém-versionado no Workfront também envia alterações para seus metadados. | Não | Não | Instantâneo |
| Atualizar automaticamente metadados AEM em alterações no Forms personalizado no Workfront | O Workfront é configurado de forma que as propriedades especificadas AEM metadados do ativo sejam mapeadas para um formulário personalizado do documento. Quando um ativo é vinculado inicialmente ou quando um ativo é atualizado, os valores dessas propriedades de metadados são copiados para o campo de formulário personalizado do documento Workfront correspondente. É necessário tomar cuidado para impedir que a alteração AEM seja enviada de volta para AEM como se fosse uma alteração originada no Workfront. | Não | Instantâneo | Instantâneo |
| Criar nova versão de prova em ativos vinculados | Ao vincular um ativo no Workfront, uma prova pode ser gerada automaticamente. | Não | Instantâneo | Personalizado |
| Definir status em objetos Workfront | Definir status de objeto do Workfront com base em condições configuráveis usando workflows AEM | Não | Não | Instantâneo |
| Publicar ativos no ambiente de publicação do AEM ou no Brand Portal | Dê aos usuários do Workfront a opção de publicar automaticamente ativos vinculados em um ambiente de publicação do AEM ou no Brand Portal. | Não | Não | Instantâneo |
