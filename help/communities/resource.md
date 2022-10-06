---
title: Criar e atribuir recursos de habilitação
seo-title: Create and Assign Enablement Resources
description: Adicionar recursos de ativação
seo-description: Add enablement resources
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
exl-id: 78908a9c-a260-44ff-ad1e-baa6d78ae399
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 7%

---

# Criar e atribuir recursos de habilitação {#create-and-assign-enablement-resources}

## Adicionar um recurso de ativação {#add-an-enablement-resource}

Para adicionar um recurso de ativação ao novo site da comunidade:

* Faça logon como administrador do sistema na instância do autor:
   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)
* Na navegação global, selecione **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

   ![recursos](assets/resources.png)

   ![ativation-resource](assets/enablement-resource.png)
* Selecione o site da comunidade ao qual os recursos de ativação estão sendo adicionados:
   * Selecionar **[!UICONTROL Tutorial de ativação]**.
* No menu, selecione **[!UICONTROL Criar]**.
* Selecionar **[!UICONTROL Recurso]**.

![create-resource](assets/create-enablement-resource.png)

### Informações básicas {#basic-info}

Preencha as informações básicas do Recurso:

* **[!UICONTROL Nome do site]**

   Defina para o nome do site de comunidade selecionado: Tutorial de ativação

* **[!UICONTROL Nome do Recurso &amp;;]**

   Lição de Esqui 1

* **[!UICONTROL Tags]**

   Tutorial: Esportes / Esqui

* **[!UICONTROL Mostrar no catálogo]**

   Defina como **Ligado**.

* **[!UICONTROL Descrição]**

   Deslizando sobre a neve para os iniciantes.

* **[!UICONTROL Adicionar]**

   Adicione uma imagem para representar o Recurso ao membro na exibição Atribuições.

   ![informações básicas](assets/basic-info.png)

* Selecione **[!UICONTROL Próximo]**

### Adicionar conteúdo {#add-content}

Embora pareça que vários Recursos podem ser selecionados, somente um é permitido.

Selecione o `'+' icon`, no canto superior direito, para iniciar o processo de escolha do Recurso identificando a fonte.

![adicionar conteúdo](assets/add-content.png)

![recurso de upload](assets/upload-resource.png)

Faça upload de um recurso. Se um recurso de vídeo, faça o upload de uma imagem personalizada para exibição antes que o vídeo comece a ser reproduzido ou permita que uma miniatura seja gerada a partir do vídeo (pode levar alguns minutos - não é necessário aguardar).

![upload-video](assets/upload-video.png)

* Selecione **[!UICONTROL Próximo]**.

### Configurações {#settings}

* **[!UICONTROL Configurações sociais]**

   Deixe as configurações padrão para experimentar comentários e avaliações dos recursos de ativação pelos alunos.

* **[!UICONTROL Data de vencimento]**

   *(Opcional)* Pode ser selecionada uma data até à qual a atribuição deve ser concluída.

* **[!UICONTROL Autor do recurso]**

   *(Opcional)* Deixe em branco.

* **[!UICONTROL Contato do Recurso &amp;;]**

   *(Obrigatório)* Use o menu suspenso para selecionar o membro `Quinn Harper`.

* **[!UICONTROL Especialista de recurso]**

   *(Opcional)* Deixe em branco.

   **Observação**: Se os usuários ou grupos não estiverem visíveis, verifique se eles foram adicionados à variável `Community Enable Members` grupo e *Salvo* na instância de publicação.

   ![configurações de ativação](assets/enablement-settings.png)

* Selecione **[!UICONTROL Próximo]**

### Atribuições {#assignments}

* **[!UICONTROL Adicionar responsáveis]**

   Deixe indefinido, pois esse recurso de ativação será adicionado a um caminho de aprendizado. Se um aluno for atribuído ao recurso de ativação individual, bem como a um LearningPath contendo o recurso de ativação, o aluno será atribuído ao recurso de ativação duas vezes.

   ![atribuições adicionais](assets/add-assignments.png)

* Selecione **[!UICONTROL Criar]**

   ![create-resource](assets/create-resource.png)

A criação bem-sucedida do Recurso retorna ao console Recursos com o Recurso recém-criado selecionado. Nesse console, é possível publicar, adicionar alunos e alterar outras configurações.

Para fazer upload de uma nova versão do recurso de ativação, é recomendável criar um novo recurso e, em seguida, cancelar a inscrição dos membros da versão antiga e inscrevê-los na nova versão.

### Publicar o recurso {#publish-the-resource}

Antes de os Inscritos poderem ver o Recurso atribuído, eles devem ser publicados:

* Selecione o mundo `Publish` ícone

A ativação é confirmada com uma mensagem de sucesso:

![publish-resource](assets/publish-resource.png)

## Adicionar um segundo recurso de ativação {#add-a-second-enablement-resource}

Repita as etapas acima para criar e publicar um segundo recurso de ativação relacionado do qual um caminho de aprendizado será criado.

![recurso adicional](assets/add-resource.png)

**Publicar** o segundo recurso.

Retorne à lista Tutorial de ativação de Recursos.

*Dica: Se ambos os Recursos não estiverem visíveis, atualize a página.*

![refresh-resource](assets/refresh-resource.png)

## Adicionar um caminho de aprendizado {#add-a-learning-path}

Um caminho de aprendizagem é um agrupamento lógico de recursos de ativação que formam um curso.

* No console Recursos, selecione `+ Create`
* Selecionar **[!UICONTROL Caminho de aprendizado]**

![add-learning-path](assets/add-learning-path.png)

Adicione o **[!UICONTROL Informações básicas]**:

* **[!UICONTROL Nome do Caminho de aprendizagem]**

   Lições de Esqui

* **[!UICONTROL Tags]**

   Tutorial: Esqui

* **[!UICONTROL Mostrar no catálogo]**

   Deixar desmarcado

* **[!UICONTROL Fazer upload de uma imagem]**

   Para representar o caminho de aprendizagem no console Recursos.

   ![learningpath-basic](assets/learningpath-basic.png)

* Selecione **[!UICONTROL Próximo]**.

Pule o próximo painel, pois não há caminhos de aprendizado de pré-requisito para adicionar.

* Selecione **[!UICONTROL Próximo]**

No painel Adicionar recursos :

* Selecionar `+ Add Resources` para selecionar os 2 recursos de lesões de esqui a serem adicionados ao caminho de aprendizado.

   Observação: Somente **publicado** Os recursos serão selecionáveis.

>[!NOTE]
>
>Você só pode selecionar os recursos disponíveis no mesmo nível que o caminho de aprendizagem. Por exemplo, para um caminho de aprendizado criado em um grupo, somente os recursos de nível de grupo estão disponíveis; para um caminho de aprendizado criado em um site da comunidade, os recursos nesse site estão disponíveis para adição ao caminho de aprendizado.

* Selecione **[!UICONTROL Enviar]**.

   ![learningpath](assets/learningpath-add.png)

   ![create-learningpath](assets/create-learningpath.png)

* Selecione **[!UICONTROL Próximo]**

   ![learningpath-settings](assets/learningpath-settings.png)

* **[!UICONTROL Adicionar responsáveis]**

   Use o menu suspenso para selecionar a variável `Community Ski Class` grupo, que deve incluir membros `Riley Taylor` e `Sidney Croft.`

* **[!UICONTROL Contato do Caminho de Aprendizagem &amp;;]**

   *(Obrigatório)* Use o menu suspenso para selecionar o membro `Quinn Harper`.

* Selecione **[!UICONTROL Criar]**.

   ![learningpath-info](assets/learningpath-info.png)

A criação bem-sucedida do caminho de aprendizado retorna ao console Recursos com o caminho de aprendizado recém-criado selecionado. Nesse console, é possível publicar, adicionar alunos e alterar outras configurações.

**Publicar** o caminho de aprendizado.
