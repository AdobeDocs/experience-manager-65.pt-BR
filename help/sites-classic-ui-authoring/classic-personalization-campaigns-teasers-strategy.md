---
title: Teasers e estratégias
description: As campanhas geralmente usam teasers como um mecanismo para atrair um segmento específico da população de visitantes até o conteúdo focado em seus interesses. Um ou mais teasers são definidos para uma campanha específica.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 2%

---

# Teasers e estratégias{#teasers-and-strategies}

As campanhas geralmente usam teasers como um mecanismo para atrair um segmento específico da população de visitantes até o conteúdo focado em seus interesses. Um ou mais teasers são definidos para uma campanha específica.

>[!NOTE]
>
>O componente de Teaser agora está obsoleto no AEM 6.2. Em vez disso, use o [Componente de destino](/help/sites-authoring/content-targeting-touch.md).

* **Páginas da marca** são armazenadas na seção Campanhas do site. Uma marca contém as campanhas individuais.
* **Páginas de campanha** são armazenadas na seção Campanhas do site. Cada campanha tem uma página individual, sob a qual as definições do teaser são mantidas. O container, ou a página de visão geral, também contém determinadas informações e estatísticas sobre as páginas de teaser individuais.

Os teasers dentro do AEM são compostos de várias partes:

* **As páginas de teaser** são armazenadas na página de campanha apropriada e mantêm as definições dos parágrafos de teaser disponíveis para cada campanha específica. Essas definições são usadas ao exibir os parágrafos do teaser; incluindo variações de conteúdo, o segmento a ser usado para selecionar uma variação e um fator de reforço.
* O **Componente de teaser** está disponível imediatamente e permite criar uma instância do seu parágrafo de teaser específico em uma página de conteúdo. Você pode arrastar o componente de teaser do sidekick e, em seguida, especificar sua definição de teaser para criar seu próprio parágrafo de teaser. **Observação:** o componente de Teaser agora está obsoleto no AEM 6.2. Em vez disso, use o [Componente de destino](/help/sites-authoring/content-targeting-touch.md).
* **Os parágrafos do teaser** são instâncias reais do teaser em uma página de conteúdo. Eles atraem um segmento de visitantes para um conteúdo focado em seus interesses.
* Páginas que contêm o conteúdo da campanha focado em um segmento de visitante específico. Normalmente, os parágrafos do teaser levam o visitante a essas páginas.

## Estratégias {#strategies}

Ao adicionar um parágrafo de teaser a uma página, defina a **Estratégia**.

Isso ocorre porque vários teasers estão disponíveis para seleção à medida que seus segmentos atribuídos são resolvidos com êxito. A **Estratégia** especifica um critério extra usado para selecionar o teaser mostrado:

* A **Pontuação da sequência de cliques**, é baseada nas marcas e ocorrências de marcas relacionadas mantidas no contexto de cliente do visitante (mostra a frequência com que um visitante clicou em páginas que contêm a respectiva marca). As taxas de hit das tags definidas na página do teaser são comparadas.
* **Aleatório**, para seleção &quot;aleatória&quot;; usa o fator aleatório gerado para uma página; isso pode ser visto com o [contexto do cliente](/help/sites-administering/client-context.md).
* **Primeiro** na lista de segmentos resolvidos. A ordem é a dos teasers na página do container da campanha.

O [Fator de reforço](/help/sites-administering/campaign-segmentation.md#boost-factor) do segmento também afeta a seleção. É um fator de ponderação adicionado a uma definição de segmento para aumentar/diminuir a probabilidade relativa de sua seleção.

O processo e as inter-relações dos vários critérios de seleção são melhor ilustrados com um exemplo (um método que também pode ser usado para garantir que seus teasers atinjam o público necessário).

Se os segmentos a seguir já tiverem sido criados e atribuídos a seus respectivos Fatores de reforço:

| Segmento | Fator de reforço |
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
   <td>Campaign</td>
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
   <td>Empresa<br /> </td>
  </tr>
 </tbody>
</table>

Em seguida, se aplicarmos isso a um visitante em que:

* **S1**, **S2 e **S6** resolvidos com êxito

* a marca **marketing** tem três ocorrências
* a tag **business** tem seis ocorrências

Podemos ver o resultado:

* correspondência bem-sucedida - algum dos segmentos atribuídos ao teaser é resolvido com êxito para o visitante atual?
* fator de reforço - o fator de reforço mais alto de todos os segmentos aplicáveis
* pontuação de sequência de cliques - o total acumulativo de todas as ocorrências de tag aplicáveis

que são calculados antes da aplicação da estratégia adequada:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmentos atribuídos</td>
   <td>Tags </td>
   <td>Correspondência bem-sucedida?</td>
   <td>Fator de reforço resultante</td>
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
   <td>Somente T5 e T6 são considerados como segmentos, todos resolvem <i>e</i> porque têm o fator de reforço mais alto. A lista retornada está na ordem T5, T6; portanto, T5 é selecionado e exibido.</td>
  </tr>
  <tr>
   <td>Aleatório</td>
   <td>T5 ou T6</td>
   <td>Ambos os teasers têm segmentos que resolvem e o mesmo fator de reforço. Portanto, os dois teasers são mostrados em proporção igual.</td>
  </tr>
  <tr>
   <td>Pontuação de sequência de cliques</td>
   <td>T6</td>
   <td><p>Todos os segmentos para T1, T4, T5 e T6 resolvem para o visitante. Os fatores de reforço mais elevados de T5 e T6, em seguida, excluem T1 e T4. Por fim, a Pontuação de sequência de cliques mais alta de T6 resulta na seleção disso.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se, após as técnicas de resolução acima, vários teasers estiverem disponíveis para seleção, uma seleção interna (aleatória) selecionará um único teaser para exibição.
>
>Por exemplo, se a estratégia fosse Pontuação de sequência de cliques e T5 tivesse a mesma Pontuação de sequência de cliques que T6 (ou seja, seis em vez de três), a seleção interna (aleatória) seria usada para selecionar um desses dois.

As Páginas/parágrafos do teaser são usados para direcionar segmentos específicos de visitantes para um conteúdo que foca em seus interesses. Eles podem apresentar uma variedade de opções para o visitante escolher ou mostrar apenas um parágrafo de teaser que seja baseado no segmento de visitante específico. Por exemplo, o parágrafo de teaser mostrado pode depender da idade do visitante.

Normalmente, uma página de teaser é uma ação temporária que durará um período específico, até ser substituída pela próxima página de teaser.

Depois de criar sua marca e campanha, você pode criar e configurar sua experiência de teaser.

### Criar um ponto de contato para o teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>O componente de Teaser agora está obsoleto no AEM 6.2. Em vez disso, use o [Componente de destino](/help/sites-authoring/content-targeting-touch.md).

1. Navegue até a página de conteúdo na qual deseja colocar o parágrafo de teaser que levará à página da campanha.
1. Adicione um componente de **Teaser** (disponível na seção **Personalization** do sidekick) na posição desejada. Quando criado pela primeira vez, ele mostrará que o caminho da campanha ainda não está configurado:

   ![chlimage_1](assets/chlimage_1.png)

1. Edite o componente de teaser para adicionar o:

   * **Caminho da campanha**
Caminho para a página da campanha que contém a página de teaser individual; os segmentos determinam exatamente qual teaser será mostrado.

   * **[Estratégia](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
Método usado para seleção quando vários segmentos são resolvidos com sucesso.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Clique em **OK** para salvar. Dependendo dos segmentos definidos no teaser e no perfil do usuário com o qual você está conectado no momento, o conteúdo apropriado será exibido:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Passe o mouse sobre o parágrafo de teaser para revelar o ícone de ponto de interrogação (canto inferior direito do componente). Clique aqui para exibir os segmentos aplicados e se eles estão resolvidos no momento.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Visão geral do Teaser {#teaser-overview}

Além da visualização da campanha no MCM, a página da campanha também fornece informações sobre os teasers conectados a ela:

1. No console **Sites**, abra a página da campanha; por exemplo:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Isso mostra uma visão geral das definições do teaser e da exibição de estatísticas:

   ![chlimage_1-4](assets/chlimage_1-4.png)
