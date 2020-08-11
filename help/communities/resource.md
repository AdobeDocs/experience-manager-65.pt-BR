---
title: Criar e atribuir recursos de habilitação
seo-title: Criar e atribuir recursos de habilitação
description: Adicionar recursos de ativação
seo-description: Adicionar recursos de ativação
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
translation-type: tm+mt
source-git-commit: e84c9a99ce9ec0447a5fb3e0ca5ba76b41c888cd
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 7%

---


# Criar e atribuir recursos de habilitação {#create-and-assign-enablement-resources}

## Adicionar um recurso de ativação {#add-an-enablement-resource}

Para adicionar um recurso de ativação ao novo site da comunidade:

* Faça logon como administrador do sistema na instância do autor:
   * Por exemplo, [http://localhost:4502/](http://localhost:4503/)
* Na navegação global, selecione **[!UICONTROL Comunidades]** > **[!UICONTROL Recursos]**

   ![recursos](assets/resources.png)

   ![ativlement-resource](assets/enablement-resource.png)
* Selecione o site da comunidade ao qual os recursos de ativação estão sendo adicionados:
   * Selecione Tutorial **[!UICONTROL de ativação]**.
* No menu, selecione **[!UICONTROL Criar]**.
* Selecione **[!UICONTROL Recurso]**.

![create-resource](assets/create-enablement-resource.png)

### Informações básicas {#basic-info}

Preencha as informações básicas do Recurso:

* **[!UICONTROL Nome do site]**

   Defina para o nome do site da comunidade selecionado: Tutorial de ativação

* **[!UICONTROL Nome do recurso &amp;ast;]**

   Lição de Esqui 1

* **[!UICONTROL Tags]**

   Tutorial: Esportes / Esqui

* **[!UICONTROL Mostrar no catálogo]**

   Defina para **Ligado**.

* **[!UICONTROL Descrição]**

   Deslizando sobre a neve para principiantes.

* **[!UICONTROL Adicionar]**

   Adicione uma imagem para representar o Recurso ao membro em sua visualização Atribuições.

   ![basic-info](assets/basic-info.png)

* Selecione **[!UICONTROL Próximo]**

### Adicionar conteúdo {#add-content}

Embora pareça que vários Recursos podem ser selecionados, somente um é permitido.

Selecione o `'+' icon`, no canto superior direito, para iniciar o processo de escolha do Recurso identificando a fonte.

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

Carregar um recurso. Se um recurso de vídeo fizer upload de uma imagem personalizada para ser exibida antes da reprodução dos start de vídeo, ou permitir que uma miniatura seja gerada a partir do vídeo (pode levar alguns minutos - não é necessário aguardar).

![upload-video](assets/upload-video.png)

* Selecione **[!UICONTROL Próximo]**.

### Configurações {#settings}

* **[!UICONTROL Configurações sociais]**

   Deixe as configurações padrão para experimentar comentários e classificações dos recursos de ativação pelos alunos.

* **[!UICONTROL Data de vencimento]**

   *(Opcional)* Uma data na qual a atribuição deve ser concluída pode ser selecionada.

* **[!UICONTROL Autor do recurso]**

   *(Opcional)* Deixe em branco.

* **[!UICONTROL &amp;Painel de Recurso;ast;]**

   *(Obrigatório)* Use o menu suspenso para selecionar o membro `Quinn Harper`.

* **[!UICONTROL Especialista de recurso]**

   *(Opcional)* Deixe em branco.

   **Observação**: Se os usuários ou grupos não estiverem visíveis, verifique se foram adicionados ao `Community Enable Members` grupo e *salvos* na instância de publicação.

   ![ativlement-settings](assets/enablement-settings.png)

* Selecione **[!UICONTROL Próximo]**

### Atribuições {#assignments}

* **[!UICONTROL Adicionar responsáveis]**

   Deixe indefinido, pois esse recurso de ativação será adicionado a um caminho de aprendizado. Se um aluno for atribuído ao recurso de ativação individual, bem como a um alunoPath que contém o recurso de ativação, o aluno será atribuído ao recurso de ativação duas vezes.

   ![atribuições adicionais](assets/add-assignments.png)

* Selecione **[!UICONTROL Criar]**

   ![create-resource](assets/create-resource.png)

Criação bem-sucedida do Recurso retorna ao console Recursos com o Recurso recém-criado selecionado. Desse console, é possível publicar, adicionar alunos e alterar outras configurações.

Para carregar uma nova versão do recurso de ativação, é recomendável criar um novo Recurso e, em seguida, cancelar a inscrição dos membros da versão antiga e inscrevê-los na nova versão.

### Publicar o recurso {#publish-the-resource}

Antes de os inscritos poderem ver o recurso atribuído, ele deve ser publicado:

* Selecionar o `Publish` ícone do mundo

A ativação é confirmada com uma mensagem de sucesso:

![publish-resource](assets/publish-resource.png)

## Adicionar um segundo recurso de ativação {#add-a-second-enablement-resource}

Repita as etapas acima para criar e publicar um segundo recurso de ativação relacionado a partir do qual um caminho de aprendizado será criado.

![add-resource](assets/add-resource.png)

**Publique** o segundo recurso.

Retorne à lista Tutorial de ativação de Recursos.

*Dica: Se ambos os Recursos não estiverem visíveis, atualize a página.*

![refresh-resource](assets/refresh-resource.png)

## Adicionar um caminho de aprendizado {#add-a-learning-path}

Um caminho de aprendizado é um agrupamento lógico de recursos de ativação que formam um curso.

* No console Recursos, selecione `+ Create`
* Select **[!UICONTROL Learning Path]**

![add-learning-path](assets/add-learning-path.png)

Adicione as Informações **** básicas:

* **[!UICONTROL Nome do Caminho de aprendizagem]**

   Lições de esqui

* **[!UICONTROL Tags]**

   Tutorial: Esqui

* **[!UICONTROL Mostrar no catálogo]**

   Deixar desmarcado

* **[!UICONTROL Carregar uma imagem]**

   Para representar o caminho de aprendizado no console Recursos.

   ![learningpath-basic](assets/learningpath-basic.png)

* Selecione **[!UICONTROL Próximo]**.

Ignore o próximo painel, pois não há caminhos de aprendizado de pré-requisito para adicionar.

* Selecione **[!UICONTROL Próximo]**

No painel Adicionar recursos:

* Selecione `+ Add Resources` para selecionar os 2 recursos de lesões de esqui a serem adicionados ao caminho de aprendizado.

   Observação: Somente Recursos **publicados** poderão ser selecionados.

>[!NOTE]
>
>Você só pode selecionar os recursos disponíveis no mesmo nível do caminho de aprendizado. Por exemplo, para um caminho de aprendizado criado em um grupo, somente os recursos de nível de grupo estão disponíveis; para um caminho de aprendizado criado em um site da comunidade, os recursos desse site estão disponíveis para adição ao caminho de aprendizado.


* Selecione **[!UICONTROL Enviar]**.

   ![learningpath](assets/learningpath-add.png)

   ![create-learningpath](assets/create-learningpath.png)

* Selecione **[!UICONTROL Próximo]**

   ![learningpath-settings](assets/learningpath-settings.png)

* **[!UICONTROL Adicionar responsáveis]**

   Use o menu suspenso para selecionar o `Community Ski Class` grupo, que deve incluir os membros `Riley Taylor` e `Sidney Croft.`

* **[!UICONTROL &amp;Painel de Contato do Caminho de Aprendizagem;ast;]**

   *(Obrigatório)* Use o menu suspenso para selecionar o membro `Quinn Harper`.

* Selecione **[!UICONTROL Criar]**.

   ![learningpath-info](assets/learningpath-info.png)

A criação bem-sucedida do caminho de aprendizado retorna ao console Recursos com o caminho de aprendizado recém-criado selecionado. Desse console, é possível publicar, adicionar alunos e alterar outras configurações.

**Publique** o caminho de aprendizado.

