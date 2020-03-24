---
title: Imagens inteligentes
description: A geração de imagens inteligentes aproveita as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: d690bcc80052f356425cd85c498aa48b1caf44bc

---


# Imagem inteligente {#smart-imaging}

## O que é &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

A tecnologia Smart Imaging aproveita os recursos do Adobe Sensei AI e trabalha com &quot;predefinições de imagens&quot; existentes para melhorar o desempenho do delivery de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem, com base nos recursos do navegador do cliente.

O Smart Imaging também se beneficia do aumento de desempenho ao ser totalmente integrado ao melhor serviço premium CDN da Adobe. Este serviço encontra a melhor rota da Internet entre servidores, redes e pontos de peering que tem a menor latência e/ou a menor taxa de perda de pacotes do que a rota padrão da Internet.

Os exemplos de ativos de imagem a seguir mostram a otimização adicionada de Imagens inteligentes:

| Image<br>(URL) | Miniatura   | Tamanho<br> (JPEG) | Tamanho (WebP)<br> (com ***Smart Imaging***) | % redução |
|---|:---:|:---:|:---:|:---:|:---:|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Média = 51% |

Semelhante ao acima, a Adobe também executou um teste com 7009 URLs de sites de clientes ao vivo, e conseguiu uma média de 38% de otimização de tamanho de arquivo adicional para JPEG e 31% de otimização de tamanho de arquivo adicional para PNG com formato WebP, devido à capacidade de criação de imagens inteligentes.

## Quais são os principais benefícios do Smart Imaging mais recente? {#what-are-the-key-benefits-of-smart-imaging}

Como as imagens constituem a maioria do tempo de carregamento de uma página, o aprimoramento do desempenho pode ter um impacto profundo nos KPIs comerciais, como conversão mais alta, tempo gasto no site e menor taxa de rejeição do site.

Aprimoramentos na versão mais recente do Smart Imaging:

* Serve conteúdo otimizado imediatamente (em tempo de execução).
* Usa a tecnologia Adobe Sensei para converter de acordo com a qualidade (qlt) especificada na solicitação de imagem.
* A Imagem inteligente pode ser desativada usando o parâmetro de URL &quot;bfc&quot;.
* TTL (Tempo de vida) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que a Imagem inteligente funcionasse.
* Anteriormente, as imagens original e derivada eram armazenadas em cache e era um processo de 2 etapas para invalidar o cache. Na última geração de imagens inteligentes, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de etapa única.
* Os clientes que usam cabeçalhos personalizados em seus conjuntos de regras (por exemplo, &quot;Origem de permissão de tempo&quot;, &quot;X-Robot&quot;, conforme sugerido em [Adicionar um valor de cabeçalho personalizado a respostas de imagem|O Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) se beneficiarão da imagem inteligente mais recente, já que esses cabeçalhos não estão bloqueados, ao contrário da versão anterior do Smart Imaging.

## Há algum custo de licenciamento associado à geração de imagens inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. O Smart Imaging está incluído na licença existente do Dynamic Media Classic (Scene7) ou do AEM Dynamic Media (no Prem, AMS e AEM como um serviço em nuvem).

>[!NOTE]
>
>O Smart Imaging não está disponível para clientes do Dynamic Media - Hybrid.


## Como funciona a geração de imagens inteligentes? {#how-does-smart-imaging-work}

O Smart Imaging usa o Adobe Sensei para converter imagens automaticamente no formato, tamanho e qualidade mais ideais, com base na capacidade do navegador:

* Converta automaticamente para WebP para navegadores como Chrome, Firefox, Microsoft Edge, Android e Opera.
* Converter automaticamente para JPEG2000 para navegadores como Safari.
* Converter automaticamente em JPEG para navegadores como Internet Explorer 9+.
* Para navegadores que não suportam esses formatos, o formato de imagem solicitado originalmente é atendido.

Se o tamanho original da imagem for menor do que o que o Smart Imaging produz, então a imagem original será disponibilizada.

## Quais formatos de imagem são suportados? {#what-image-formats-are-supported}

Os seguintes formatos de imagem são suportados para Imagens inteligentes:
* JPEG
* PNG

Para qualquer outro formato mencionado em um URL, você deve desativar explicitamente a Imagem inteligente.  Anexar modificador `bfc=off` ao URL para formatos de arquivo diferentes de JPEG e PNG. Você pode fazer isso usando um dos seguintes métodos:

* Use um conjunto de regras se o `fmt` modificador for mencionado no URL.
* Anexar no campo modificadores de URL das predefinições em questão.

A Adobe está trabalhando em uma correção permanente que não exige que você acrescente `bfc=off` para `fmt !=JPEG` ou `fmt !=PNG`. Este tópico será atualizado após a correção ser entregue.


## Como o Smart Imaging funciona com as predefinições de imagens existentes que já estão em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

O Smart Imaging funciona com as &quot;predefinições de imagens&quot; existentes e observa todas as suas configurações de imagem, com exceção da qualidade (qlt) e do formato (fmt), se o formato de arquivo solicitado for JPEG ou PNG. Para conversão de formato, mantemos a fidelidade visual completa, conforme definido pelas configurações predefinidas da imagem, mas em um tamanho de arquivo menor. Se o tamanho original da imagem for menor do que o que o Smart Imaging produz, então a imagem original será disponibilizada.

Além disso, se as predefinições de imagem forem usadas para retornar `fmt !=JPEG` ou `fmt !=PNG`, anexe `bfc=off` o campo modificador predefinido para retornar o formato de arquivo solicitado.

## Será necessário alterar quaisquer URLs, predefinições de imagens ou implantar qualquer novo código no meu site para o Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

A Imagem inteligente funciona perfeitamente com os URLs de imagem e as predefinições de imagem existentes. Além disso, o Smart Imaging não exige que você adicione qualquer código ao seu site para detectar o navegador de um usuário. Tudo isso é feito automaticamente.

Como mencionado anteriormente, o Smart Imaging suporta apenas formatos de imagem JPEG e PNG. Para outros formatos, é necessário anexar o `bfc=off` modificador ao URL, conforme descrito anteriormente.

Além disso, consulte [Estou qualificado para usar a Imagem inteligente?](#am-i-eligible-to-use-smart-imaging) para entender os pré-requisitos para o Smart Imaging.

## O Smart Maging está funcionando com HTTPS? Que tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

O Smart Imaging funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Estou qualificado para usar imagens inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para usar a Imagem inteligente, seu empresa Dynamic Media Classic ou Dynamic Media na conta AEM deve atender aos seguintes requisitos:

* Use o CDN (Content Delivery Network) fornecido pela Adobe como parte de sua licença.
* Use um domínio dedicado (por exemplo, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (por exemplo, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

Tap **[!UICONTROL Setup > Application Setup > General Settings]**. Procure o campo Nome **[!UICONTROL do servidor]** publicado. Se você estiver usando um domínio genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição ao enviar um ticket de suporte técnico.

Seu primeiro domínio personalizado não tem custo adicional com uma licença do Dynamic Media.

## Qual é o processo para ativar a criação de imagens inteligentes em minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Você deve iniciar a solicitação para usar a geração inteligente de imagens; ela não é ativada automaticamente.

1. Iniciar uma solicitação de suporte técnico (email: s7support@adobe.com).
1. Forneça as seguintes informações em sua solicitação de suporte:

   1. Nome do contato principal, email, telefone.
   1. Todos os domínios a serem ativados para geração de imagens inteligente (ou seja, images.empresa.com ou mycompany.sceno7.com).

      Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.

      Procure o campo Nome **[!UICONTROL do servidor]** publicado.
   1. Verifique se você está usando o CDN pela Adobe e não é gerenciado com um relacionamento direto.
   1. Verifique se você está usando um domínio dedicado, como `images.company.com` ou `mycompany.scene7.com`, e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.

      Procure o campo Nome **[!UICONTROL do servidor]** publicado. Se você estiver usando um domínio genérico do Dynamic Media Classic, é possível solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.
   1. Indique se você também precisa que isso funcione em HTTP/2.

1. O suporte técnico adicionará você à Lista de espera do cliente de Smart Imaging com base na ordem em que as solicitações foram enviadas.
1. Quando a Adobe estiver pronta para lidar com sua solicitação, o suporte entrará em contato com você para coordenar e definir uma data de público alvo.
1. **Opcional**: Você tem a opção de testar a geração inteligente de imagens no armazenamento temporário antes de a Adobe colocar o novo recurso em produção.
1. Você é notificado após a conclusão pelo suporte.
1. Para maximizar os aprimoramentos de desempenho do Smart Imaging, a Adobe recomenda definir o Tempo de vida (TTL) como 24 horas ou mais. O TTL define quanto tempo os ativos são armazenados em cache pelo CDN. Para alterar essa configuração:

   1. Se você usar o Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor]** de imagem. Defina o valor Tempo de vida **** padrão do Cache do cliente como 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](config-dynamic.md). Defina o valor de **[!UICONTROL Expiração]** 24 horas ou mais.

## Quando posso esperar que minha conta seja ativada com a Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Suporte Técnico, de acordo com a Lista de Espera.

>[!NOTE]
Pode ser que haja um longo lead time, pois a habilitação da Imagem inteligente envolve a limpeza do cache pela Adobe. Portanto, apenas algumas transições de clientes podem ser tratadas a qualquer momento.

## Quais são os riscos com a alternância para usar o Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Não há risco para uma página da Web do cliente. No entanto, você deve estar ciente de que a transição para o Smart Imaging limpa seu cache no CDN, pois isso envolve mudar para uma nova configuração do Dynamic Media Classic ou do Dynamic Media no AEM.

Durante a transição inicial, as imagens não armazenadas em cache acessam diretamente os servidores de origem da Adobe até que o cache seja reconstruído novamente. Por esse motivo, a Adobe planeja lidar com algumas transições de clientes de cada vez para que o desempenho aceitável seja mantido ao retirar solicitações de nossa origem. Para a maioria dos clientes, o cache é totalmente construído novamente no CDN dentro de aproximadamente 1 a 2 dias.

## Como posso verificar se a geração de imagens inteligentes está funcionando como esperado?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que a sua conta for configurada com imagens inteligentes, carregue um URL de imagem do Dynamic Media Classic (Scene7)/Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome clicando em **[!UICONTROL Visualização > Desenvolvedor > Ferramentas]** do desenvolvedor no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows - navegue até as configurações no painel de ferramentas do desenvolvedor e marque a caixa de seleção **[!UICONTROL Desativar cache (enquanto os devtools estiverem abertos)]** .
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A seguinte captura de tela mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome.
1. Repita esse teste em navegadores e condições de usuário diferentes.

>[!NOTE]
Nem todas as imagens são convertidas. O Smart Imaging decide se a conversão é necessária para melhorar o desempenho. Em alguns casos, quando não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## A Imagem inteligente pode ser desativada para qualquer solicitação? {#turning-off-smart-imaging}

Sim. Você pode desativar a Imagem inteligente adicionando o modificador `bfc=off` ao URL.

## Que &quot;ajuste&quot; está disponível? Há alguma configuração ou comportamento que possa ser definido? (#tuning-settings)

Atualmente, você pode ativar ou desativar a Imagem inteligente. Nenhum outro ajuste está disponível.

## Se o Smart Imaging gerenciar as configurações de qualidade, há mínimos e máximos que podemos definir? Por exemplo, é possível definir &quot;não inferior a 60&quot; e &quot;qualidade não superior a 80&quot;? (#Minimum-maximum)

Não há essa capacidade de provisionamento na Imagem inteligente atual.

## Em alguns casos, uma imagem JPEG é retornada ao Chrome em vez de uma imagem WebP. Por que isso acontece? (#jpeg-webp)

O Smart Imaging determina se a conversão é benéfica ou não. Ele retorna a nova imagem somente se a conversão resultar em um tamanho de arquivo menor com qualidade comparável.
