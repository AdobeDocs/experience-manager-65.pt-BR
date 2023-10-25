---
title: Classificações do Adobe
seo-title: Adobe Classifications
description: Saiba como usar as Classificações de Adobe para exportar dados de classificações para o Adobe Analytics.
seo-description: Learn how to use Adobe Classifications to export classifications data to Adobe Analytics.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 6%

---

# Classificações do Adobe{#adobe-classifications}

Classificações de Adobe exportam dados de classificações para [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma programada. O exportador é uma implementação de um **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar isso:

1. Usar **Navegação**, selecione **Ferramentas**, **Cloud Service**, depois **Cloud Service herdados**.
1. Navegue até **Adobe Analytics** e selecione **Exibir configurações**.
1. Clique em **[+]** ao lado da configuração do Adobe Analytics.

1. No **Criar estrutura** diálogo:

   * Especifica um **Título**.
   * Opcionalmente, é possível especificar a variável **Nome**, para o nó que armazena os detalhes da estrutura no repositório.
   * Selecionar **Classificações do Adobe Analytics**

   E clique em **Criar**.

   ![Caixa de diálogo Criar estrutura](assets/aa-25.png)

1. A variável **Configurações de classificações** será aberta para edição.

   ![Caixa de diálogo Configurações de classificações](assets/aa-classifications-settings.png)

   As propriedades incluem o seguinte:

   | **Texto** | **Descrição** |
   |---|---|
   | Habilitado | Selecionar **Sim** para ativar as configurações de Classificações de Adobe. |
   | Substituir quando houver conflito | Selecionar **Sim** para substituir qualquer colisão de dados. Por padrão, é definido como **Não**. |
   | Exclusão processada | Se definida como **Sim**, exclui os nós processados após serem exportados. O padrão é **Falso**. |
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

1. Navegue até o console OSGI em **https://&lt;host>:&lt;port>/system/console/configMgr** e selecione **Exportador de classificações do Adobe AEM**.

   ![aa-26](assets/aa-26.png)

1. Atualize o **Exportar tamanho da página** conforme necessário, em seguida clique em **Salvar**.

## TransformadorpadraoSAINT {#saintdefaulttransformer}

>[!NOTE]
>
>As Classificações Adobe eram anteriormente conhecidas como Exportador de SAINT.

Um Exportador pode usar um Transformador para transformar os dados exportados em um formato específico. Para Classificações de Adobe, uma subinterface `SAINTTransformer<String[]>` A implementação da interface do transformador foi fornecida. Essa interface é usada para restringir o tipo de dados a `String[]` que é usado pela API SAINT e para ter uma interface de marcador para encontrar esses serviços para seleção.

Na implementação padrão SAINTDefaultTransformer, os recursos secundários da origem do exportador são tratados como registros com nomes de propriedade como chaves e valores de propriedade como valores. A variável **Chave** A coluna é adicionada automaticamente como primeira coluna; seu valor será o nome do nó. Propriedades Namespace (contendo `:`) são ignorados.

*Estrutura do nó:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Produto = Meu nome de produto (String)
      * Preço = 120,90 (String)
      * Tamanho = M (String)
      * Cor = preto (String)
      * Cor^Código = 101 (Cadeia de caracteres)

**Cabeçalho e registro de SAINT:**

| **Chave** | **Produto** | **Preço** | **Tamanho** | **Cor** | **Cor^Código** |
|---|---|---|---|---|---|
| 1 | Nome do meu produto | 120.90 | M | black | 101 |

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

Você pode criar seu próprio workflow, para que qualquer nova importação inicie o workflow para criar os dados apropriados e corretamente estruturados no **/var/export/** para que possa ser exportado para Classificações de Adobe.
