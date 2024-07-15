---
title: Classificações de Adobe
description: Saiba como usar as Classificações de Adobe para exportar dados de classificações para o Adobe Analytics.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Classificações de Adobe{#adobe-classifications}

As Classificações de Adobe exportam os dados de classificações para [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma agendada. O exportador é uma implementação de um **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar isso:

1. Usando a **Navegação**, selecione **Ferramentas**, **Cloud Service** e **Cloud Service herdados**.
1. Role até **Adobe Analytics** e selecione **Mostrar configurações**.
1. Clique no link **[+]** ao lado da sua configuração do Adobe Analytics.

1. Na caixa de diálogo **Criar Estrutura**:

   * Especifica um **Título**.
   * Opcionalmente, você pode especificar o **Nome** para o nó que armazena os detalhes da estrutura no repositório.
   * Selecionar **Classificações do Adobe Analytics**

   E clique em **Criar**.

   ![Caixa de diálogo Criar Estrutura](assets/aa-25.png)

1. A caixa de diálogo **Configurações de classificação** é aberta para edição.

   ![Caixa de diálogo Configurações de Classificações](assets/aa-classifications-settings.png)

   As propriedades incluem o seguinte:

   | **Campo** | **Descrição** |
   |---|---|
   | Habilitado | Selecione **Sim** para habilitar as configurações de Classificações de Adobe. |
   | Substituir quando houver conflito | Selecione **Sim** para substituir qualquer colisão de dados. Por padrão, isso é configurado como **Não**. |
   | Exclusão processada | Se definido como **Sim**, exclui os nós processados após serem exportados. O padrão é **Falso**. |
   | Exportar descrição da tarefa | Informe uma descrição para o job de Classificações de Adobe. |
   | E-mail de notificação | Insira um endereço de email para notificação de Classificações de Adobe. |
   | Conjunto de relatórios | Informe o Conjunto de relatórios para o qual executar o job de importação. |
   | Conjunto de Dados | Insira a ID de relação do conjunto de dados para a qual executar o trabalho de importação. |
   | Transformador | No menu suspenso, selecione uma implementação de transformador. |
   | Fonte de Dados | Navegue até o caminho do container de dados. |
   | Exportar programação | Selecione o cronograma da exportação. O padrão é a cada 30 minutos. |

1. Clique em **OK** para salvar suas configurações.

## Modificação do tamanho da página {#modifying-page-size}

Os registros são processados em páginas. Por padrão, as Classificações de Adobe criam páginas com tamanho de página de 1000.

Uma página pode ter no máximo 25000 páginas, por definição em Classificações de Adobe e pode ser modificada a partir do console Felix. Durante a exportação, as Classificações de Adobe bloqueiam o nó de origem para impedir modificações simultâneas. O nó é desbloqueado após a exportação, por erro ou quando a sessão é encerrada.

Para alterar o tamanho da página:

1. Navegue até o console OSGI em **https://&lt;host>:&lt;port>/system/console/configMgr** e selecione **Exportador de Classificações de AEM Adobe**.

   ![aa-26](assets/aa-26.png)

1. Atualize o **Tamanho da Página de Exportação** conforme necessário e clique em **Salvar**.

## TransformadorpadraoSAINT {#saintdefaulttransformer}

>[!NOTE]
>
>As Classificações Adobe eram anteriormente conhecidas como Exportador de SAINT.

Um Exportador pode usar um Transformador para transformar os dados exportados em um formato específico. Para Classificações de Adobe, foi fornecida uma subinterface `SAINTTransformer<String[]>` que implementa a interface do Transformador. Esta interface é usada para restringir o tipo de dados a `String[]`, que é usado pela API SAINT, e para ter uma interface de marcador para encontrar esses serviços para seleção.

Na implementação padrão SAINTDefaultTransformer, os recursos secundários da origem do exportador são tratados como registros com nomes de propriedade como chaves e valores de propriedade como valores. A coluna **Chave** é adicionada automaticamente como primeira coluna; seu valor será o nome do nó. As propriedades de namespace (contendo `:`) são desconsideradas.

*Estrutura do nó:*

* classificação de id `nt:unstructured`

   * 1 `nt:unstructured`

      * Produto = Meu nome de produto (String)
      * Preço = 120,90 (String)
      * Tamanho = M (String)
      * Cor = preto (String)
      * Cor^Código = 101 (Cadeia de caracteres)

Cabeçalho e Registro **SAINT:**

| **Chave** | **Produto** | **Preço** | **Tamanho** | **Cor** | **Cor^Código** |
|---|---|---|---|---|---|
| 1 | Nome do meu produto | 120,90 | S | black | 101 |

As propriedades incluem o seguinte:

<table>
 <tbody>
  <tr>
   <td><strong>Caminho da propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>transformador</td>
   <td>Um nome de classe de uma implementação SAINTransformer</td>
  </tr>
  <tr>
   <td>email</td>
   <td>Endereço de email de notificação.</td>
  </tr>
  <tr>
   <td>conjuntos de relatórios</td>
   <td>IDs de conjunto de relatórios para os quais executar o trabalho de importação. </td>
  </tr>
  <tr>
   <td>conjunto de dados</td>
   <td>ID da relação do conjunto de dados para a qual executar o trabalho de importação. </td>
  </tr>
  <tr>
   <td>descrição</td>
   <td>Descrição do trabalho. <br /> </td>
  </tr>
  <tr>
   <td>substituir</td>
   <td>Sinalizador para substituir colisões de dados. O padrão é <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>checkdivisions</td>
   <td>Sinalizador para verificar a compatibilidade dos conjuntos de relatórios. O padrão é <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Sinalizador para excluir os nós processados após a exportação. O padrão é <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatização da exportação de classificações do Adobe {#automating-adobe-classifications-export}

Você pode criar seu próprio fluxo de trabalho, para que qualquer nova importação inicie o fluxo de trabalho para criar os dados apropriados e corretamente estruturados em **/var/export/** para que ele possa ser exportado para Classificações de Adobe.
