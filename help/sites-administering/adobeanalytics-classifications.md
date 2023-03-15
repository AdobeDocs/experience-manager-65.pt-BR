---
title: Classificações do Adobe
seo-title: Adobe Classifications
description: Saiba mais sobre Classificações Adobe.
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 7%

---

# Classificações do Adobe{#adobe-classifications}

Classificações Adobe exportam dados de classificações para [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma programada. O exportador é uma implementação de um **com.adobe.cq.scheduled.exportador.Exporter**.

Para configurar isso:

1. Usando **Navegação**, selecione **Ferramentas**, **Cloud Services**, em seguida **Cloud Services herdados**.
1. Rolar para **Adobe Analytics** e selecione **Mostrar configurações**.
1. Clique no botão **[+]** link ao lado da configuração do Adobe Analytics.

1. No **Criar estrutura** caixa de diálogo:

   * Especifica um **Título**.
   * Opcionalmente, é possível especificar a variável **Nome**, para o nó que armazena os detalhes da estrutura no repositório.
   * Selecionar **Classificações Adobe Analytics**

   E clique em **Criar**.

   ![Caixa de diálogo Criar estrutura](assets/aa-25.png)

1. O **Configurações de classificações** será aberta para edição.

   ![Caixa de diálogo Configurações das classificações](assets/aa-classifications-settings.png)

   As propriedades incluem:

   | **Texto** | **Descrição** |
   |---|---|
   | Ativado | Selecionar **Sim** para ativar as configurações de Classificações de Adobe. |
   | Substituir quando houver conflito | Selecionar **Sim** para substituir qualquer conflito de dados. Por padrão, isso é definido como **Não**. |
   | Exclusão processada | Se estiver definido como **Sim**, exclui os nós processados após serem exportados. O padrão é **Falso**. |
   | Exportar descrição da tarefa | Insira uma descrição para o job Adobe Classifications. |
   | E-mail de notificação | Insira um endereço de email para a notificação de Classificações de Adobe. |
   | Conjunto de relatórios | Insira o Conjunto de relatórios para executar o trabalho de importação. |
   | Conjunto de Dados | Insira a ID de relação do conjunto de dados para executar o trabalho de importação. |
   | Transformador | No menu suspenso , selecione uma implementação de transformador. |
   | Fonte de Dados | Navegue até o caminho para o contêiner de dados. |
   | Exportar programação | Selecione o agendamento para a exportação. O padrão é a cada 30 minutos. |

1. Clique em **OK** para salvar suas configurações.

## Modificando o tamanho da página {#modifying-page-size}

Os registros são processados em páginas. Por padrão, as Classificações de Adobe criam páginas com um tamanho de página de 1000.

Uma página pode ter no máximo 25000 páginas, por definição em Classificações de Adobe e pode ser modificada no console Felix. Durante a exportação, as Classificações Adobe bloqueiam o nó de origem para evitar modificações simultâneas. O nó é desbloqueado após a exportação, com erro ou quando a sessão é fechada.

Para alterar o tamanho da página:

1. Navegue até o console OSGI em **https://&lt;host>:&lt;port>/system/console/configMgr** e selecione **Exportador de classificações de Adobe AEM**.

   ![aa-26](assets/aa-26.png)

1. Atualize o **Exportar tamanho da página** conforme necessário, em seguida, clique em **Salvar**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Classificações Adobe eram conhecidas anteriormente como Exportador SAINT.

Um exportador pode utilizar um Transformador para transformar os dados de exportação em um formato específico. Para Classificações Adobe, uma subinterface `SAINTTransformer<String[]>` foi fornecida a implementação da interface Transformer. Essa interface é usada para restringir o tipo de dados a `String[]` que é usada pela API do SAINT e para ter uma interface de marcador para localizar esses serviços para seleção.

Na implementação padrão SAINTDefaultTransformer, os recursos secundários da origem do exportador são tratados como registros com nomes de propriedade como chaves e valores de propriedade como valores. O **Chave** é adicionada automaticamente como primeira coluna - seu valor será o nome do nó. Propriedades namespaces (contendo `:`) não são tomadas em consideração.

*Estrutura do nó:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Produto = Meu nome do produto (cadeia de caracteres)
      * Preço = 120,90 (String)
      * Size = M (String)
      * Cor = preto (cadeia de caracteres)
      * Cor^Código = 101 (Cadeia de Caracteres)

**Cabeçalho e registro de SAINT:**

| **Chave** | **Produto** | **Preço** | **Tamanho** | **Cor** | **Cor^Código** |
|---|---|---|---|---|---|
| 1 | Meu nome de produto | 120.90 | M | black | 101 |

As propriedades incluem:

<table>
 <tbody>
  <tr>
   <td><strong>Caminho da propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>transformador</td>
   <td>Um nome de classe de uma implementação SAINTTransformer</td>
  </tr>
  <tr>
   <td>email</td>
   <td>Endereço de email de notificação.</td>
  </tr>
  <tr>
   <td>conjuntos de relatórios</td>
   <td>IDs de conjunto de relatórios para executar o trabalho de importação. </td>
  </tr>
  <tr>
   <td>conjunto de dados</td>
   <td>ID da relação do conjunto de dados para executar o trabalho de importação. </td>
  </tr>
  <tr>
   <td>descrição</td>
   <td>Descrição da tarefa. <br /> </td>
  </tr>
  <tr>
   <td>substituir</td>
   <td>Sinalizador para substituir colisões de dados. O padrão é <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisões de verificação</td>
   <td>Sinalizador para verificar a compatibilidade dos conjuntos de relatórios. O padrão é <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Sinalizador para excluir os nós processados após a exportação. O padrão é <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatizando a exportação de classificações de Adobe {#automating-adobe-classifications-export}

Você pode criar seu próprio fluxo de trabalho, de modo que qualquer nova importação inicie o fluxo de trabalho para criar os dados apropriados e estruturados corretamente no **/var/export/** para que possa ser exportado para Classificações Adobe.
