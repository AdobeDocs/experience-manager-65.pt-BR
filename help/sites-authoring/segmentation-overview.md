---
title: Noções sobre segmentação ao criar uma campanha
description: A segmentação é uma consideração importante ao criar uma campanha.
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 31%

---

# Noções sobre segmentação{#understanding-segmentation}

A segmentação é uma consideração importante ao criar uma campanha. Na maioria dos casos, é necessário ter segmentos já definidos antes de iniciar a campanha.

Os visitantes têm interesses e objetivos diferentes quando chegam a um site. Entender essas metas e atender às expectativas é um fator importante de sucesso para o marketing online.

A segmentação ajuda a conseguir isso ao analisar e caracterizar o de um visitante:

* atividade no site
* perfil
* atividade em outros sites

O conteúdo pode então ser direcionado especificamente para as necessidades e os interesses do visitante, dependendo dos segmentos aos quais ele corresponde.

## Uso da segmentação {#using-segmentation}

Os segmentos são definidos em [Configuração da segmentação](/help/sites-administering/campaign-segmentation.md). Eles são usados para orientar o conteúdo real visto por um público-alvo específico.

## Terminologia de segmentação {#segmentation-terminology}

Ao discutir segmentação, a seguinte terminologia é usada:

**Visitante** Um visitante é uma pessoa que visita um site. Normalmente, a visita dessa pessoa começa em uma página de referência, em seguida, avança para uma ou mais exibições de página em seu próprio site. Um perfil comportamental pode ser criado a partir dos detalhes da visita dessa pessoa.

**Usuário** Um usuário é um visitante que se registra no site para receber um perfil de conta. Para gerar seu perfil, eles fornecem identificação adicional, como um endereço de email e gênero, entre outros. Informações adicionais também podem ser coletadas, incluindo a atividade da comunidade e os padrões de compra, entre outros. Com base nas informações fornecidas no perfil, um perfil demográfico pode ser criado.

**Característica** Uma característica é uma característica ou propriedade de um visitante que pode ser usada para determinar a associação a um segmento específico.

**Segmento** Um segmento é uma coleção de visitantes que compartilham certas características. Segmentos devem ser distintos, com um mínimo de sobreposição com outros segmentos.

**Características comportamentais** Características comportamentais são aquelas que se relacionam ao comportamento de um visitante no site. Dentre elas:

* Interesse no seu site; incluindo páginas visitadas e produtos comprados.
* Interesse no site de referência; incluindo termos de pesquisa usados ou anúncios clicados.
* Interesse em outros sites, determinado com o uso de ferramentas como o Spyjax.
* Fidelidade do visitante; duração da visita, frequência das visitas.

**Características demográficas** São características selecionadas da população, incluindo:

* Idade
* Renda
* Tamanho da família
* Estado civil
* Sexo
* Local

**Características derivadas** Algumas características demográficas são difíceis de determinar sem registro, mas podem ser derivadas pela combinação de características comportamentais e demográficas.

Por exemplo, a combinação do URL de referência (como uma característica comportamental) com os dados demográficos (adquiridos de ferramentas como o [Google Ad Planner](https://www.google.com/adplanner/)) permite aos proprietários do site obterem características demográficas de seus visitantes.

**Subsegmento** Um segmento pode ser subdividido em vários subsegmentos. Isso é feito com a definição de características adicionais.

**Página de Teaser** Uma página de teaser é direcionada a um público-alvo específico. Ela tem conteúdo reutilizável que pode ser usado no parágrafo de teaser.

**Campanha** Uma campanha é uma coleção de páginas de teaser e páginas de marketing por email, como boletins informativos ou convites. Normalmente, uma campanha é executada por um período limitado e é substituída por outra campanha.

**Parágrafo do Teaser** Este é um parágrafo que extrai conteúdo de outra página dependendo de uma estratégia de seleção. Essa estratégia de seleção pode considerar segmentos e campanhas.

**Lista** Uma lista é extraída de um segmento de usuários registrados. Por exemplo, a localização usada para orientar o conteúdo do parágrafo de teaser.

>[!NOTE]
>
>Consulte [Segmentação](/help/sites-administering/campaign-segmentation.md) para obter mais informações sobre segmentos em AEM.
