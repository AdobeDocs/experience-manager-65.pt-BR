---
title: Teasers e estratégias
seo-title: Teasers e estratégias
description: Campanhas costumam usar teasers como um mecanismo para atrair um segmento específico da população visitante até o conteúdo focado em seus interesses. Um ou mais teasers são definidos para uma campanha específica.
seo-description: Campanhas costumam usar teasers como um mecanismo para atrair um segmento específico da população visitante até o conteúdo focado em seus interesses. Um ou mais teasers são definidos para uma campanha específica.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
translation-type: tm+mt
source-git-commit: dc1985c25c797f7b994f30195d0586f867f9b3ee
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 82%

---


# Teasers e estratégias{#teasers-and-strategies}

Campanhas costumam usar teasers como um mecanismo para atrair um segmento específico da população visitante até o conteúdo focado em seus interesses. Um ou mais teasers são definidos para uma campanha específica.

>[!NOTE]
>
>O componente Teaser foi descontinuado no AEM 6.2. Use o [componente Target](/help/sites-authoring/content-targeting-touch.md) em vez disso.

* **As** páginas de marca são armazenadas na seção Campanhas do site. Uma marca contém as campanhas individuais.
* **As** páginas de campanha são armazenadas na seção Campanhas do site. Cada campanha tem uma página individual, na qual as definições de teaser são mantidas. A página de contêiner, ou visão geral, também inclui algumas informações e estatísticas sobre as páginas de teaser individuais.

Os teasers no AEM são compostos por várias partes:

* **As** páginas do teaser são armazenadas na página de campanha apropriada e mantêm as definições dos parágrafos do teaser disponíveis para cada campanha específica. Essas definições são usadas ao exibir os parágrafos de teaser, incluindo variações de conteúdo, o segmento a ser usado para selecionar uma variação e um fator de reforço.
* O **componente Teaser** está disponível para uso imediato e permite que você crie uma instância do seu parágrafo de teaser específico em uma página de conteúdo. É possível arrastar o componente de teaser do sidekick e especificar sua definição para criar seu próprio parágrafo de teaser. **Observação:** o componente Teaser foi substituído no AEM 6.2. Em vez disso, use o  [componente ](/help/sites-authoring/content-targeting-touch.md) Público alvo.
* Os **parágrafos de Teaser** são instâncias reais do seu teaser dentro de uma página de conteúdo. Eles atraem um segmento de visitantes para um conteúdo focado em seus interesses.
* As páginas que contêm o conteúdo da campanha focado em um segmento específico de visitantes. Geralmente, os parágrafos de teaser direcionarão o visitante a essas páginas.

## Estratégias {#strategies}

Ao adicionar um parágrafo teaser a uma página, é necessário definir a **Estratégia**.

Isso é para o caso de vários teasers estarem disponíveis para seleção, pois todos os segmentos atribuídos resolvem com sucesso. A **Estratégia** especifica os critérios adicionais usados para selecionar o teaser mostrado:

* A **Pontuação de sequência de cliques** baseia-se nas tags e nas ocorrências de tag relacionadas mantidas no contexto de cliente do visitante (mostram com que frequência um visitante clicou em páginas que contêm a respectiva tag). As taxas de ocorrência de tags definidas na página de teaser são comparadas.
* **Aleatório**, para seleção &quot;aleatória&quot;; usa o fator aleatório gerado para uma página, isso pode ser visto com o contexto [ do ](/help/sites-administering/client-context.md)cliente.
* **** Determine a lista dos segmentos resolvidos. A ordem é a dos teasers na página do contêiner da campanha.

O [Fator de aumento](/help/sites-administering/campaign-segmentation.md#boost-factor) do segmento também tem um impacto na seleção. Este é um fator de ponderação adicionado a uma definição de segmento para aumentar/diminuir a probabilidade relativa de ser selecionado.

O processo e as relações entre os diferentes critérios de seleção podem ser ilustrados melhor com um exemplo (um método que também pode ser usado para garantir que seus teasers atingirão o público exigido).

Se os segmentos a seguir já tiverem sido criados e atribuídos com seu respectivo Fator de reforço:

| Segmento | Fator de aumento |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

E usamos as seguintes definições de teaser:

<table>
 <tbody>
  <tr>
   <td>Campanha</td>
   <td>Teaser</td>
   <td>Segmentos atribuídos</td>
   <td>Tags atribuídas </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Negócios, Marketing</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Negócios<br /> </td>
  </tr>
 </tbody>
</table>

Em seguida, se aplicarmos isso a um visitante, em que:

* **S1**,  **S2** e  **S6** resolvem com êxito

* a tag **marketing** tem 3 ocorrências
* a tag **comercial** tem 6 ocorrências

Teremos o seguinte resultado:

* sucesso de correspondência - qualquer um dos segmentos atribuídos ao teaser é resolvido com sucesso para o visitante atual?
* fator de reforço - o maior fator de reforço de todos os segmentos aplicáveis
* pontuação de sequência de cliques - o total acumulado de todas as ocorrências de tags aplicáveis

que são calculados antes da aplicação da estratégia apropriada:

<table>
 <tbody>
  <tr>
   <td>Campanha</td>
   <td>Teaser</td>
   <td>Segmentos atribuídos</td>
   <td>Tags </td>
   <td>Correspondência bem-sucedida?</td>
   <td>Fator de aumento resultante</td>
   <td>Pontuação de sequência de cliques resultante </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Negócios, Marketing</td>
   <td>Sim</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>Sim</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>Não</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>Sim<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
   <td>Sim</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Negócios</td>
   <td>Sim</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Esses valores são usados para determinar os teasers que o visitante verá, dependendo da **Estratégia** aplicada ao parágrafo de teaser:

<table>
 <tbody>
  <tr>
   <td>Estratégia</td>
   <td>Teaser resultante</td>
   <td>Comentários</td>
  </tr>
  <tr>
   <td>Primeiro</td>
   <td>T5</td>
   <td>Somente T5 e T6 são considerados como seus segmentos todos resolvem <i>e</i> eles têm o fator de aumento mais alto. A lista retornada está na ordem de T5, T6; assim, T5 será selecionado e exibido.</td>
  </tr>
  <tr>
   <td>Aleatório</td>
   <td>T5 ou T6</td>
   <td>Ambos os teasers têm segmentos que todos resolvem e o mesmo fator de aumento. Portanto, os dois teasers serão mostrados em proporções iguais.</td>
  </tr>
  <tr>
   <td>Pontuação da sequência de cliques</td>
   <td>T6</td>
   <td><p>Os segmentos para T1, T4, T5 e T6 são resolvidos para o visitante. Os maiores fatores de reforço de T5 e T6 e, portanto, T1 e T4 são excluídos. Por fim, a pontuação de sequência de cliques mais alta de T6 resulta na sua seleção.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se, após realizadas as técnicas de resolução descritas acima, vários teasers estiverem disponíveis para seleção, uma seleção interna (aleatória) selecionará um único teaser para exibição.
>
>Por exemplo, se a estratégia fosse Pontuação de sequência de cliques e T5 tivesse a mesma Pontuação de sequência de cliques que T6 (ou seja, 6 em vez de 3), a seleção interna (aleatória) seria usada para selecionar um desses dois.

Páginas/parágrafos de teaser são usados para direcionar segmentos de visitantes específicos ao conteúdo focado em seus interesses. Eles podem apresentar uma gama de opções para o visitante escolher ou podem mostrar apenas um parágrafo de teaser que se baseia no segmento específico do visitante. Por exemplo, o parágrafo de teaser mostrado pode depender da idade do visitante.

Geralmente, uma página de teaser é uma ação temporária que durará por um período específico, até ser substituída pela próxima página de teaser.

Após criar a marca e a campanha, é possível criar e configurar a experiência de teaser.

### Criação de um ponto de contato para o teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>O componente Teaser foi descontinuado no AEM 6.2. Use o [componente Target](/help/sites-authoring/content-targeting-touch.md) em vez disso.

1. Navegue até a página de conteúdo à qual deseja adicionar o parágrafo do teaser que direcionará para a página da sua campanha.
1. Adicione um componente **Teaser** (disponível na seção **Personalização** do sidekick) na posição desejada. Quando criado pela primeira vez, mostrará que o caminho da campanha ainda não foi configurado:

   ![chlimage_1](assets/chlimage_1.png)

1. Edite o componente de teaser para adicionar o seguinte:

   * **Caminho da campanha** O caminho para a página da campanha que contém a página de teaser individual. Segmentos determinam exatamente qual teaser é mostrado.

   * **[Estratégia](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)** Método usado para seleção quando vários segmentos são resolvidos com sucesso.
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Clique em **OK** para salvar. Dependendo dos segmentos que você definiu no teaser e do perfil do usuário com o qual você está conectado no momento, o conteúdo apropriado será exibido:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Posicione o cursor do mouse sobre o parágrafo do teaser para revelar o ícone de ponto de interrogação (canto inferior direito do componente). Clique para ver os segmentos aplicados e se eles resolvem atualmente.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Visão geral de teasers {#teaser-overview}

Além da visualização da campanha no MCM, a página da campanha também fornece informações sobre os teasers conectados a ela:

1. No console **Sites**, abra a página da campanha; por exemplo:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Isso mostra uma visão geral das definições de teaser e das estatísticas de exibição:

   ![chlimage_1-4](assets/chlimage_1-4.png)
