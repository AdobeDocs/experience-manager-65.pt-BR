---
title: Personalização
seo-title: Personalization
description: Saiba mais sobre a personalização no AEM.
seo-description: Learn about personalization in AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
source-git-commit: d6b595b6b5477b5cad662e219f1abd483491897f
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 16%

---

# Personalização {#personalization}

## O que é personalização? {#what-is-personalization}

Há um volume cada vez maior de conteúdo disponível hoje, seja na internet, na extranet ou em sites da intranet.

A personalização centra-se em fornecer ao usuário um ambiente personalizado que exibe conteúdo dinâmico selecionado de acordo com suas necessidades específicas; seja com base em perfis predefinidos, na seleção de usuários ou no comportamento interativo do usuário.

Há três elementos principais envolvidos na personalização:

### Usuários {#users}

* Ter perfis, individuais e de grupo. Esses perfis contêm características (como descrição de trabalho, localização, interesses) que podem ser usadas para personalizar o conteúdo que podem ver.
* Execute ações. Elas podem então ser analisadas e comparadas com as regras de comportamento para adaptar o conteúdo que veem.

### Conteúdo {#content}

* É o que o usuário deseja ver. Conteúdo preferível de interesse, e uso para que possam cumprir as suas tarefas.
* Pode ser categorizado e, portanto, disponibilizado para usuários de acordo com regras predefinidas.
* Deve ser dinâmico.

Em outras palavras, o conteúdo deve, de alguma forma, depender do usuário. Se todos os usuários visualizarem o mesmo conteúdo, a personalização será redundante.

### Regras {#rules}

* Defina como a personalização realmente acontece - qual conteúdo o usuário pode ver e quando.

A personalização pode ser:

#### Explícita {#explicit}

* Personalização: em que o usuário faz seleções a partir de uma escolha de fontes de conteúdo.

#### Implicado {#implicit}

* Baseado em regras: os gerentes de negócios definem regras específicas para ações com base em perfis e/ou comportamentos específicos.
* Filtragem simples: as seleções são feitas com base em perfis predefinidos no nível do usuário e/ou grupo.
* Filtragem colaborativa/de recomendação: o comportamento do usuário é registrado de acordo com regras predefinidas. Essas regras se baseiam no comportamento observado com indivíduos com ideias semelhantes. As informações coletadas são usadas para adaptar as informações exibidas ao usuário, principalmente na forma de recomendações.

## Como e quando a personalização pode ser usada? {#how-and-when-can-personalization-be-used}

A personalização pode ser usada em muitos casos, por exemplo:

### Páginas da Intranet {#intranet-pages}

* O conteúdo pode ser oferecido com base na localização, no departamento e/ou na função de um usuário - já definido em uma rede interna.
* Dependendo da escolha disponível, o usuário pode fazer mais seleções.

### Grupos de usuários do Target específicos, limitados - Extranets {#extranets}

* Os usuários exigem um logon para autorização; isso será vinculado a um perfil que fornece as informações necessárias para a personalização; possivelmente detalhes como a localização, relação com o produto, histórico de uso, responsabilidades orçamentárias etc.
* Essas instâncias podem se espalhar por sites, como:
* Empresas que fornecem sítios Web a uma parte altamente especializada do seu mercado, por exemplo, uma empresa farmacêutica que disponibiliza um sítio Web especializado para médicos.
* Empresas que fornecem sítios Web que permitem ao seu cliente visualizar informações sobre a conta corrente e sobre a faturação; por exemplo, provedores de telefone.

### Site de vendas e distribuição {#sales-site}

* Sites de vendas e distribuição, como o Amazon, podem combinar um perfil de usuário, o histórico de vendas do usuário e seu histórico de navegação para fazer sugestões sobre o que pode interessar ao usuário em seguida.

### Sites de pesquisa {#search-site}

* Muitos dos principais sites de mecanismos de pesquisa têm ferramentas analíticas muito poderosas que registram o comportamento do usuário, os termos de pesquisa que usam e os sites que realmente visitam. Isso é usado para personalizar o conteúdo fornecido, principalmente em relação à exibição de anúncios.

### Pontos a considerar e pontos de personalização {#strengths-of-personalization-and-points-to-consider}

A seguir estão os motivos pelos quais a personalização deve ser usada:

* Um usuário pode experimentar um site confortável e focado.
* A personalização pode ser usada para propagar automaticamente o acesso à versão mais recente do conteúdo.
* Os recursos de colaboração social estão disponíveis para os usuários se comunicarem entre si, pois podem ser identificados por seus perfis.
* Um usuário pode receber o conteúdo necessário para realizar uma tarefa específica. Na intranet de uma empresa, isso pode fornecer uma ferramenta valiosa para disseminar informações.
* Um usuário pode receber o conteúdo necessário/desejado, reduzindo o tempo necessário para executar operações de pesquisa.
* O provedor de conteúdo pode orientar o conteúdo a ser visualizado por categorias específicas de usuários.
* As regras podem ser definidas para fornecer conteúdo com base em combinações de características e comportamento do usuário. Isso fornece um mecanismo sofisticado para personalizar sua experiência na Web.

Ao usar a personalização, considere o seguinte:

#### Show {#performance}

* Naturalmente, a análise e a avaliação suplementares têm um impacto no desempenho. No entanto, os métodos usados são altamente sofisticados e podem ser otimizados para minimizar o impacto.

#### Autorização {#authorization}

* A personalização requer um mecanismo de logon, pois o site deve ser capaz de identificar o usuário.

#### Armazenamento em cache {#caching}

* O armazenamento em cache é um aspecto que o usuário verá em termos de desempenho e precisão: a rapidez com que o site entrega conteúdo personalizado e é sempre atual.
* O armazenamento em cache é uma consideração importante ao configurar a personalização e o tempo deve ser considerado para garantir que a implementação correta seja usada.

>[!TIP]
>
>O efeito da personalização no desempenho e os tópicos relacionados de armazenamento em cache são mais discutidos no documento [Otimização de desempenho.](/help/sites-deploying/configuring-performance.md)

#### Precisão das regras {#accuracy}

* A personalização realizada por meio do rastreamento do comportamento do usuário ou da definição de regras com base no perfil do usuário deve ser precisa e lógica.
* Não há nada mais frustrante para o usuário do que ter conteúdo forçado, ou negado a ele, por causa da lógica imprecisa de uma regra.
* Portanto, as regras devem ser bem pensadas - com os requisitos do usuário em primeiro plano. Isto pode levar muito a cabo e não deve ser subestimado; definir as regras de negócios geralmente supera o esforço técnico ao implementar a personalização.

#### Quando usar {#when-to-use}

* Como muitos recursos na Web, a personalização deve ser usada com cuidado. A sua utilização beneficiará realmente o utilizador? deve ser sempre a primeira consideração - ou se o objetivo desejado pode ser alcançado com menos esforço por outro método. A personalização pode correr o risco de ser um recurso que os usuários configuram uma vez (para ver como funciona) e apenas uma vez, pois não traz vantagens reais para eles.
* A personalização só tem significado quando o conteúdo é dinâmico, dependendo do usuário de alguma forma. Se todos os usuários visualizarem o mesmo conteúdo, a personalização será redundante.

#### Confidencialidade {#confidentiality}

* Muitos usuários estão preocupados com a proteção e a segurança de dados. Em especial no que respeita aos dados recuperados ao acompanhar o seu comportamento ao navegar na Web.

## Personalização e acesso {#personalization-and-access}

A personalização deve ser considerada separadamente do controle de acesso, mas elas se relacionam.

A personalização em si não cria nenhuma forma de controle de acesso. Trata-se simplesmente de um método de orientação do que o utilizador vê; não restringe o usuário de acessar outro conteúdo e, como em qualquer conteúdo, ele precisa ter os controles de acesso corretos já atribuídos.

No entanto, o controle de acesso pode ser usado para criar uma forma de personalização. Se você permitir ou negar a um usuário o acesso ao conteúdo, isso afetará inevitavelmente a escolha do conteúdo que ele tem disponível, personalizando assim sua experiência da Web.

## Componentes disponíveis para personalização {#components-available-for-personalization}

Vários componentes são fornecidos com AEM para personalização. Alguns permitem que os usuários façam logon e editem seus perfis, outros (como Meus gadgets) permitem que os usuários configurem uma página específica:

| Título no Sidekick | Propósito |
|---|---|
| Campo de senha marcado | Solicita a senha e a confirmação da senha. |
| Inscrição no logon combinado | Permite que o usuário faça logon em uma conta existente ou se inscreva em uma nova conta. |
| Campo de endereço Forms | Um campo complexo que permite a entrada de um endereço internacional. |
| Forms Begin | Inicia uma definição de formulário |
| Forms Captcha | Um campo que consiste em uma palavra alfanumérica que é atualizada automaticamente. O componente de captcha protege websites contra bots. |
| Grupo de caixas de seleção do Forms | Vários itens organizados em uma lista e precedidos por caixas de seleção. Os usuários podem selecionar várias caixas de seleção. |
| Lista suspensa do Forms | Vários itens organizados em uma lista suspensa. A opção Multisselecionáveis especifica se vários elementos podem ser selecionados na lista. |
| Forms End | Encerra a definição do formulário. |
| Upload de arquivo Forms | Um elemento de carregamento que permite ao usuário carregar um arquivo no servidor. |
| Campo oculto do Forms | Este campo não é exibido para o usuário. Ele pode ser usado para transportar um valor para o cliente e de volta para o servidor. Esse campo não deve ter nenhuma restrição. |
| Botão Imagem do Forms | Um botão de envio adicional para o formulário que é renderizado como uma imagem. |
| Campo de senha do Forms | Igual ao campo de texto, mas somente uma única linha é permitida e a entrada de texto do usuário não fica visível no campo. |
| Grupo de opções do Forms | Vários itens organizados em uma lista precedida por um botão de rádio. Os usuários devem selecionar somente um botão de rádio. |
| Botão Enviar da Forms | Um botão de envio adicional para o formulário, onde o título é exibido como texto no botão. |
| Campo de texto Forms | Campo de texto que permite que os usuários insiram informações. |
| Meus gadgets | Permite incluir uma de uma seleção de gadgets disponíveis. |
| Foto de avatar do perfil | Permite a entrada de uma foto de avatar. |
| Nome detalhado de perfil | Entrada de detalhes do nome, incluindo elementos como título, nome do meio e sufixo, se necessário. |
| Nome de exibição no perfil | O nome a ser exibido. |
| E-mail do perfil | Entrada de um endereço de e-mail. |
| Gênero do perfil | Permite a entrada de gênero. |
| Número de telefone principal do perfil | Permite a entrada de um número de telefone. |
| URL principal do perfil | Permite a entrada de um URL. |
| Propriedade de perfil de texto geral | Propriedades do perfil. |
| Fazer logon | Permite enviar um nome de usuário e senha ao fazer logon. |
| Sair | Indica o usuário conectado no momento e fornece um link para fazer logoff. |
| Nuvem de tags | Uma nuvem de tags para mostrar uma seleção de tags apresentada graficamente em seu site |
| Teaser | Um conteúdo (geralmente uma imagem) exibido em uma página principal para &quot;incentivar&quot; os usuários a acessarem o conteúdo subjacente. |

## Personalização e conteúdo da comunidade {#personalization-and-community-content}

Recursos da comunidade como blogs, fóruns e calendários resultam na criação de conteúdo da comunidade, comumente conhecido como conteúdo gerado pelo usuário (UGC). Quando o UGC é inserido em um ambiente de publicação que consiste em várias instâncias AEM (um [publicar farm](/help/communities/topologies.md)), um dos principais problemas foi como sincronizar o UGC em todas as instâncias.

Com [AEM Communities 6.1](/help/communities/overview.md) , esse problema é resolvido usando um [loja comum para UGC](/help/communities/working-with-srp.md). No que diz respeito à personalização, as Comunidades incluem [Logon do Social](/help/communities/social-login.md) - a capacidade de fornecer a opção para os visitantes do site fazerem logon com a Facebook e a Twitter.

Sem a extensão Communities, vários métodos para explorar o problema de consistência UGC são:

* Sincronize as várias instâncias de publicação quando necessário
* Envie o UGC da instância de publicação para o ambiente do autor, de onde ele pode ser publicado de uma maneira semelhante ao conteúdo da página de publicação

O método usado para obter a consistência do UGC em um ambiente de publicação que consiste em várias instâncias de publicação deve ser cuidadosamente projetado e testado para garantir o desempenho e a consistência.
