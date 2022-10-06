---
title: Obter documentos XDP e PDF no AEM Forms
seo-title: Getting XDP and PDF documents in AEM Forms
description: O AEM Forms permite carregar formulários e ativos suportados para usar com formulários adaptáveis. Também é possível fazer o upload em massa de formulários e recursos relacionados como um ZIP.
seo-description: AEM Forms allows you to upload forms and supported assets to use with adaptive forms. You can also bulk upload forms and related resources as a ZIP.
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# Obter documentos XDP e PDF no AEM Forms{#getting-xdp-and-pdf-documents-in-aem-forms}

## Visão geral {#overview}

É possível importar seus formulários do sistema de arquivos local para o repositório CRX, fazendo upload no AEM Forms. A operação de upload é compatível com os seguintes tipos de ativos:

* Modelos de formulário (formulários XFA)
* PDF forms
* Documento (documentos de PDF simples)

Você pode fazer upload dos tipos de ativos suportados individualmente ou como um arquivo ZIP. Você pode fazer upload de um ativo do tipo `Resource`, somente com um formulário XFA em um arquivo ZIP.

>[!NOTE]
>
>Certifique-se de que você é um membro do `form-power-users` para poder carregar arquivos XDP. Entre em contato com o administrador para se tornar membro do grupo.

## Upload de formulários {#uploading-forms}

1. Faça logon na interface do usuário do AEM Forms acessando `https://'[server]:[port]'/aem/forms.html`.
1. Navegue até a pasta onde deseja fazer upload do formulário ou da pasta que contém os formulários.
1. Na barra de ferramentas das ações, toque em **Criar > Upload de arquivo**.

   ![Arquivos da opção de armazenamento local em Criar](assets/step.png)

1. A caixa de diálogo Upload form(s) ou package permite procurar e escolher o arquivo que deseja carregar. O navegador de arquivos exibe apenas os formatos de arquivo compatíveis (ZIP, XDP e PDF).

   >[!NOTE]
   >
   >Um nome de arquivo só pode conter caracteres alfanuméricos, hífen ou sublinhado.

1. Clique em Fazer upload após a seleção do arquivo para fazer upload dos arquivos ou clique em &quot;Cancelar&quot; para cancelar o upload. Um pop-up lista os ativos adicionados e os ativos que são atualizados no local atual.

   >[!NOTE]
   >
   >Para um arquivo ZIP, os caminhos relativos de todos os ativos compatíveis são exibidos. Os ativos não suportados dentro do ZIP são ignorados e não listados. No entanto, se o arquivo ZIP contiver apenas os ativos não suportados, uma mensagem de erro será exibida em vez da caixa de diálogo pop-up.

   ![Fazer upload da caixa de diálogo ao fazer upload de um formulário XFA](assets/upload-scr.png)

1. Se um ou mais ativos tiverem um nome de arquivo inválido, um erro será exibido. Corrija os nomes de arquivo realçados em vermelho e faça o upload novamente.

   ![Mensagem de erro ao carregar um formulário XFA](assets/upload-scr-err.png)

Quando o upload é concluído, um workflow em segundo plano gera miniaturas para cada ativo, com base na visualização do ativo. As versões mais recentes dos ativos, se carregadas, substituem os ativos existentes.

### Modo protegido {#protected-mode}

O servidor AEM Forms permite que você execute o código JavaScript. Um código JavaScript mal-intencionado pode prejudicar um ambiente AEM Forms. O modo protegido restringe o AEM Forms a executar arquivos XDP somente de ativos e locais confiáveis. Todos os XDP disponíveis na interface do usuário do AEM Forms são considerados ativos confiáveis.

Por padrão, o modo protegido está ativado. Se necessário, você pode desativar o modo protegido:

1. Faça logon no Console da Web AEM como administrador. O URL é https://&#39;[server]:[porta]&#39;/system/console/configMgr
1. Abra Configurações do Mobile Forms para edição.
1. Desmarque a opção Modo protegido e clique em **Salvar**. O modo protegido está desativado.

## Atualização de formulários XFA referenciados {#updating-referenced-xfa-forms}

No AEM Forms, um template de formulário XFA pode ser referenciado por um formulário adaptável ou outro template de formulário XFA. Além disso, um template pode se referir a um recurso ou outro template XFA.

Um formulário adaptável que se refere a um XFA tem seus campos vinculados aos campos disponíveis no XFA. Ao atualizar um modelo de formulário, o formulário adaptável associado tenta sincronizar com o XFA. Para obter mais detalhes, consulte [Sincronização de formulários adaptáveis com o XFA associado](../../forms/using/synchronizing-adaptive-forms-xfa.md).

Remover um modelo de formulário corrompe o formulário adaptável dependente ou o modelo de formulário. Esse formulário adaptável às vezes é chamado informalmente de formulário sujo. Na interface do usuário do AEM Forms, você pode encontrar os formulários sujos das duas maneiras a seguir.

* Um ícone de aviso é exibido na miniatura do formulário adaptável na lista de ativos e a seguinte mensagem é exibida quando você passa o ponteiro do mouse sobre o ícone de aviso.\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![Aviso para um formulário adaptável fora de sincronia após atualizar o XFA associado](assets/dirtyaf.png)

Um sinalizador é mantido para indicar se um formulário adaptável está sujo. Essas informações estão disponíveis na página de propriedades do formulário, juntamente com os metadados do formulário. Apenas para formulários adaptáveis sujos, uma propriedade de metadados `Model Refresh` exibições `Recommended` valor.

![Indicação de um formulário adaptável que está fora de sincronia com o modelo XFA](assets/model-refresh.png)
