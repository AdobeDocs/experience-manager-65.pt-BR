---
title: Trabalhar com publicação seletiva no Dynamic Media
description: Informações sobre como trabalhar com Publicação seletiva no Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 29f91713f5760ab0b5a557b5c811ef2efee1cc61
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 4%

---


# Configuração da publicação seletiva no nível da pasta no Dynamic Media {#selective-publish-configure-folder}

Você pode optar por publicar ou cancelar a publicação de ativos de ou para o AEM ou o Dynamic Media no nível de pasta, usando **[!UICONTROL Gerenciar publicação]** ou Publicação **** rápida, em vez de depender exclusivamente da Configuração **** do Dynamic Media cujas configurações são globais para todas as pastas na sua instância do Dynamic Media.

Por exemplo, com a publicação seletiva, você pode trabalhar em ativos para produtos que ainda não estão ativos. Nesse caso, uma equipe de marketing pode acessar imagens de recorte inteligente e representações dinâmicas que são sincronizadas com o Dynamic Media para que possam criar materiais promocionais, tudo isso sem a necessidade de publicar esses ativos no Dynamic Media para delivery global.

>[!IMPORTANT]
>
>A Publicação seletiva está disponível somente no modo Mídia dinâmica - Scene7.

>[!NOTE]
>
>*Copiar* ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como Publicação **** seletiva, o estado de publicação desses ativos é mantido.

Se posteriormente você decidir alterar as configurações de Publicação **** seletiva em uma pasta, essas alterações afetarão somente os novos ativos que você carrega para essa pasta a partir desse ponto em diante. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente da caixa de diálogo Publicação **** rápida ou **[!UICONTROL Gerenciar publicação]** .

A opção do modo **[!UICONTROL Publicação de mídia]** dinâmica no nível de pasta sempre assume o valor padrão na configuração **[!UICONTROL Publicar ativos]** na Configuração de mídia **[!UICONTROL dinâmica.]** As etapas a seguir neste tópico, no entanto, mostram como alterar manualmente esse valor padrão no nível da pasta (conforme descrito nas etapas a seguir) para substituir o valor de Configuração **[!UICONTROL de mídia]** dinâmica.

Independentemente de você depender do valor **[!UICONTROL Publicar ativos]** definido na Configuração **[!UICONTROL de Mídia]** Dinâmica ou do valor do modo **[!UICONTROL Publicação de Mídia]** Dinâmica definido nas propriedades no nível da pasta, você ainda poderá escolher **[!UICONTROL Imediatamente]**, **[!UICONTROL Na Ativação]****[!UICONTROL ou na Publicação Seletiva.]** Por exemplo, você pode definir o valor **[!UICONTROL Publicar ativos]** em sua Configuração **[!UICONTROL de mídia]** dinâmica como **[!UICONTROL Na Ativação]**, mas definir o valor do modo de Publicação **[!UICONTROL de mídia]** dinâmica no nível da pasta como Publicação **** seletiva, vice-versa e assim por diante.

Depois de configurar a publicação seletiva em uma pasta, você pode fazer o seguinte:

* [Publicar ativos no Dynamic Media ou AEM de forma seletiva usando Gerenciar publicação.](#selective-publish-manage-publication)
* [Cancele a publicação seletiva de ativos do Dynamic Media ou AEM usando Gerenciar publicação.](#selective-unpublish-manage-publication)
* [Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida.](#quick-publish-aem-dm)
* [Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa.](#selective-publish-unpublish-search-results)

**Para configurar a publicação seletiva no nível de pasta no Dynamic Media**

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e, em seguida, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Faça uma das seguintes opções:
   * Edite as propriedades de uma pasta existente - Na Visualização **[!UICONTROL do]** cartão, na Visualização **[!UICONTROL da]** coluna ou na Visualização **[!UICONTROL da]** Lista, navegue até uma pasta cujas propriedades você deseja editar. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Propriedades.]**
   * Edite as propriedades de uma nova pasta - Na Visualização **[!UICONTROL do]** cartão, na Visualização **[!UICONTROL da]** coluna ou na Visualização **[!UICONTROL da]** Lista, próximo ao canto superior direito da página, toque em **[!UICONTROL Criar > Pasta.]** Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite um título (obrigatório) para a pasta e, em seguida, toque em **[!UICONTROL Criar.]** Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Propriedades.]**

1. Na lista suspensa Modo **[!UICONTROL de]** sincronização, selecione uma das seguintes opções:

   | Modo de sincronização | Descrição |
   | --- | --- |
   | **[!UICONTROL Herdado]** | Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão definido na Configuração do **[!UICONTROL Dynamic Media.]** O status detalhado para **[!UICONTROL Herdado]** é exibido por meio de uma dica de ferramenta. |
   | **[!UICONTROL Sincronizar tudo nesta subárvore da pasta à mídia dinâmica]** | Para que a publicação no Dynamic Media tenha êxito, os ativos devem ser sincronizados com o Dynamic Media. A seleção dessa opção incluirá todos os ativos nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem a configuração padrão na Configuração do **[!UICONTROL Dynamic Media.]** |
   | **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização de mídia dinâmica]** | Exclua todos os ativos desta subárvore da sincronização para o Dynamic Media. |

   ![Publicação seletiva de nível de pasta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Na lista suspensa do modo **[!UICONTROL de publicação do]** Dynamic Media, selecione uma opção. Observe que a opção de modo **[!UICONTROL Publicação de mídia]** dinâmica sempre assume o valor padrão definido na Configuração de mídia **[!UICONTROL dinâmica.]** No entanto, é possível substituir manualmente esse valor padrão de Configuração **[!UICONTROL do]** Dynamic Media usando uma das seguintes opções.

   >[!IMPORTANT]
   >
   >Esteja ciente de que, independentemente da opção do modo de Publicação de Mídia Dinâmica selecionada, quaisquer atualizações feitas posteriormente em um ativo que *já* esteja publicado, essas atualizações serão publicadas imediatamente sem nenhuma outra ação do usuário.

   | Opção de modo de publicação do Dynamic Media | Descrição |
   | --- | --- |
   | **[!UICONTROL Imediatamente]** | Quando os ativos são carregados para essa pasta, o sistema ingere os ativos no AEM e fornece o URL/Incorporado instantaneamente. Essa opção está vinculada apenas AEM publicação e não há necessidade de intervenção do usuário para publicar ativos.<br>Essa opção *não* estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização]** de mídia dinâmica no modo **[!UICONTROL de]** sincronização na etapa anterior. |
   | **[!UICONTROL Por ativação]** | Quando os ativos são carregados para essa pasta, é necessário publicar explicitamente o ativo primeiro antes de fornecer um URL/link Incorporado. Essa opção está vinculada apenas AEM publicação.<br>Essa opção *não* estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização]** de mídia dinâmica no modo **[!UICONTROL de]** sincronização na etapa anterior. |
   | **[!UICONTROL Publicação seletiva]** | Os ativos são publicados à sua escolha de AEM ou para o Dynamic Media para delivery no domínio público. Ambos os métodos de publicação são mutuamente exclusivos entre si.  Ou seja, você pode publicar ativos no DMS7 para poder usar recursos como Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente para AEM para visualização segura; esses mesmos ativos *não* são publicados no DMS7 para delivery no domínio público. Essa opção não estará disponível se você tiver selecionado **[!UICONTROL Excluir tudo nesta subárvore de pasta da sincronização]** de mídia dinâmica no modo **** Sincronizar na etapa anterior. |

1. No canto superior direito da página, toque em **[!UICONTROL Salvar e fechar]** e, em seguida, toque em **[!UICONTROL OK]** para retornar ao AEM Assets.

## Publicar ativos seletivamente no Dynamic Media ou AEM usando Gerenciar publicação{#selective-publish-manage-publication}

Antes de usar **[!UICONTROL Gerenciar publicação]** para publicar ativos seletivamente no Dynamic Media ou para AEM, certifique-se de ter definido a opção **[!UICONTROL Publicar ativos]** na Configuração **[!UICONTROL do]** Dynamic Media como Publicação **** seletiva ou configurado a publicação seletiva no nível da pasta.

Consulte [Criação de uma configuração](#configuring-dynamic-media-cloud-services) de mídia dinâmica ou [Configuração de publicação seletiva no nível de pasta no Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>A Publicação seletiva está disponível somente no modo Mídia dinâmica - Scene7.

>[!NOTE]
>
>*Copiar* ativos de e para pastas limpa o estado de publicação desses ativos. No entanto, quando você *move* ativos de e para pastas cuja propriedade de pasta está definida como Publicação **** seletiva, o estado de publicação desses ativos é mantido.

**Para publicar ativos seletivamente no Dynamic Media ou AEM usando Gerenciar publicação**

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e, em seguida, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em Visualização **[!UICONTROL de]** cartão, Visualização **[!UICONTROL de]** coluna ou Visualização **[!UICONTROL de]** Lista, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]**  Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gerenciar publicação]** não for exibido na barra de ferramentas, toque no botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu lista.

1. Na página **[!UICONTROL Gerenciar publicação - Opções]** , em **[!UICONTROL Ação]**, selecione o tipo de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Publicar]** (para AEM) | Selecione essa opção para publicar ativos para AEM para pré-visualização segura. |
   | **[!UICONTROL Publicar no Dynamic Media]** | Selecione essa opção para publicar ativos no Dynamic Media para delivery no domínio público ou para que você possa usar recursos como Recorte inteligente ou representações dinâmicas.<br>Essa opção estará disponível somente se o modo **[!UICONTROL Publicação de mídia]** dinâmica estiver definido como Publicação **** seletiva nas propriedades da pasta. |

1. Em **[!UICONTROL Agendamento]**, defina o horário da publicação.

   | Agendamento | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para publicar os ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para publicar os ativos em uma data e hora específicas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]** , toque em **[!UICONTROL Avançar.]**
1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , execute um dos procedimentos a seguir:

   * Se necessário, selecione um ou mais ativos que deseja remover da publicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]** , toque em **[!UICONTROL Publicar]** ou **[!UICONTROL Publicar no Dynamic Media.]**
1. Toque em **[!UICONTROL OK.]**

### Cancele a publicação seletiva de ativos do Dynamic Media ou AEM usando Gerenciar publicação {#selective-unpublish-manage-publication}

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo, toque no ícone Navegação (logo acima do ícone Ferramentas) e, em seguida, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em Visualização **[!UICONTROL de]** cartão, Visualização **[!UICONTROL de]** coluna ou Visualização **[!UICONTROL de]** Lista, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Selecione a pasta e, na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]**  Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja cancelar a publicação. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gerenciar publicação]** não for exibido na barra de ferramentas, toque no botão de reticências e selecione **[!UICONTROL Gerenciar publicação]** no menu lista.

1. Na página **[!UICONTROL Gerenciar publicação - Opções]** , em **[!UICONTROL Ação]**, selecione o tipo de cancelamento de ativação desejado.

   | Ação | Descrição |
   | --- | --- |
   | **[!UICONTROL Cancelar publicação]** (de AEM) | Selecione essa opção para cancelar a publicação de ativos do AEM. |
   | **[!UICONTROL Desfazer publicação no Dynamic Media]** | Selecione essa opção para cancelar a publicação de ativos do Dynamic Media.<br>Essa opção estará disponível somente se o modo **[!UICONTROL Publicação de mídia]** dinâmica estiver definido como Publicação **** seletiva nas propriedades da pasta. |

1. Em **[!UICONTROL Agendamento]**, defina o tempo da desativação.

   | Agendamento | Descrição |
   | --- | --- |
   | **[!UICONTROL Agora]** | Selecione para cancelar a publicação dos ativos imediatamente. |
   | **[!UICONTROL Posteriomente]** | Selecione para cancelar a publicação dos ativos em uma data e hora específicas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação]** , toque em **[!UICONTROL Avançar.]**
1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , execute um dos procedimentos a seguir:
   * Selecione um ou mais ativos que deseja remover da despublicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]** , toque em **[!UICONTROL Cancelar publicação]** ou **[!UICONTROL Cancelar publicação do Dynamic Media.]**
1. Toque em **[!UICONTROL OK.]**

## Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida {#quick-publish-aem-dm}

Você pode usar a Publicação **** rápida para casos simples de ativação de ativos. **[!UICONTROL A Publicação]** rápida publica os ativos selecionados imediatamente sem nenhuma outra interação do usuário. Por isso, todas as referências não publicadas também são publicadas automaticamente.

>[!NOTE]
>
>Para usar a Publicação **** rápida para publicar ativos no Dynamic Media ou AEM, verifique se a Publicação **** seletiva está ativada na Configuração **[!UICONTROL do]** Dynamic Media ou nas propriedades da pasta selecionada.

**Publicar ativos no Dynamic Media ou AEM usando a Publicação rápida**

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e, no lado direito da página, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em Visualização **[!UICONTROL de]** cartão, Visualização **[!UICONTROL de]** coluna ou Visualização **[!UICONTROL de]** Lista, execute um dos seguintes procedimentos:
   * Navegue até uma pasta cujos ativos você deseja publicar. Selecione a pasta e, na barra de ferramentas, toque em Publicação **[!UICONTROL rápida.]**  Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de uma pasta específica.
   * Navegue até uma pasta cujos ativos você deseja publicar. Abra a pasta e selecione um ou mais ativos. Na barra de ferramentas, toque em Publicação **[!UICONTROL rápida.]** Você pode achar útil usar a Visualização **[!UICONTROL de]** Lista para verificar mais facilmente o status de publicação de um ativo específico.

      >[!NOTE]
      >
      >Se a Publicação **** rápida não for vista na barra de ferramentas, toque no botão de reticências e selecione Publicação **** rápida no menu lista.

      ![Publicação rápida em nível de pasta no Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selecione uma das seguintes opções na lista do menu Publicação **** rápida.

   | Opção Publicação rápida | O que ele faz |
   | --- | --- | 
   | Publicar no AEM | Publica os ativos selecionados imediatamente em AEM. |
   | Publicar no Brand Portal | Publica os ativos selecionados imediatamente no **[!UICONTROL Brand Portal.]**<br>Essa opção só estará disponível se sua instância do AEM Assets já tiver o Portal**[!UICONTROL  da ]**Marca configurado. |
   | Publicar no Dynamic Media | Publica os ativos selecionados imediatamente no Dynamic Media.<br>Um ativo já deve ser sincronizado com o Dynamic Media. Se necessário, certifique-se de que o modo **[!UICONTROL de]** sincronização nas propriedades de uma pasta já esteja definido para **[!UICONTROL Sincronizar tudo nesta subárvore de pasta para o dynamicmedia.]** |

1. Toque em **[!UICONTROL OK]** e em **[!UICONTROL Fechar.]**

## Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa {#selective-publish-unpublish-search-results}

Os resultados da pesquisa podem mostrar ativos de todas as pastas de ativos que têm diferentes configurações de publicação do Dynamic Media. Quando você selecionou um ou mais ativos dos resultados da pesquisa e os ativos têm configurações diferentes do modo de publicação do Dynamic Media, é possível acionar **[!UICONTROL Gerenciar publicação]** na barra de ferramentas para publicar ou cancelar a publicação.

Consulte também [Pesquisar ativos em AEM.](/help/assets/search-assets.md)

**Publicar ou cancelar a publicação seletiva de ativos por meio de resultados de pesquisa**

1. Em AEM, no canto superior esquerdo da página, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e, em seguida, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Na barra de ferramentas, perto do canto superior direito da página, toque no ícone Pesquisar (lupa).
1. No campo **[!UICONTROL Tipo para pesquisar]** texto, digite uma palavra-chave e pressione **[!UICONTROL Enter.]**
1. Perto do canto superior direito da página, toque no ícone de Visualização **[!UICONTROL da]** Lista.
1. Perto do canto superior esquerdo da página, toque no ícone **[!UICONTROL Filtros]** .

   ![Visualização de listas e Filtros nos resultados da pesquisa](/help/assets/assets-dm/select-publish-search-result.png)

1. No painel esquerdo, expanda **[!UICONTROL Status]** e expanda o predicado de pesquisa **[!UICONTROL Dynamic Media]** .
1. Use as caixas de seleção **[!UICONTROL Publicado]** e **[!UICONTROL Não publicado]** para refinar ainda mais os resultados da pesquisa com base no estado publicado dos ativos de Mídia dinâmica.
Como opção, você pode usar essas caixas de seleção juntamente com o predicado de pesquisa **[!UICONTROL Publicar]** para refinar os resultados de pesquisa dos ativos de AEM **[!UICONTROL Publicados]** e **[!UICONTROL Não publicados]** .
1. Faça uma das seguintes opções:
   * Selecione um ou mais ativos que deseja publicar ou cancelar a publicação.
   * Perto do canto superior direito da página Resultados **[!UICONTROL da]** pesquisa, toque em **[!UICONTROL Selecionar tudo.]**
1. Na barra de ferramentas, toque em **[!UICONTROL Gerenciar publicação.]** Talvez seja necessário tocar no ícone de reticências na barra de ferramentas para consultar **[!UICONTROL Gerenciar publicação.]**
1. Na página **[!UICONTROL Gerenciar publicação - Opções]** , selecione a ação desejada.

   | Ação selecionada | Configuração Publicar ativos na configuração do Dynamic Media | Os ativos são |
   | --- | --- | --- |
   | Publicação | Imediatamente ou na Ativação | Publicado no AEM e no Dynamic Media. |
   | Publicação | Publicação seletiva | Publicado somente em AEM. |
   | Cancelar publicação | Imediatamente ou na Ativação | Não publicado do AEM e do Dynamic Media. |
   | Cancelar publicação | Publicação seletiva | Não publicado somente no AEM. |
   | Publicar no Dynamic Media | Imediatamente ou na Ativação | Não publicado no AEM, no Dynamic Media ou em ambos. |
   | Publicar no Dynamic Media | Publicação seletiva | Publicado somente no Dynamic Media. |
   | Desfazer publicação no Dynamic Media | Imediatamente ou na Ativação | Não publicado do AEM, do Dynamic Media ou de ambos. |
   | Desfazer publicação no Dynamic Media | Publicação seletiva | Não publicado somente no Dynamic Media. |

1. Em **[!UICONTROL Agendamento]**, defina o tempo da desativação.

   | Agendamento selecionado | O que acontece |
   | --- | --- |
   | Agora | A ação selecionada é executada imediatamente. |
   | Posteriomente | A ação selecionada é executada na data e hora específicas selecionadas. |

1. No canto superior direito da página **[!UICONTROL Gerenciar publicação - Opções]** , toque em **[!UICONTROL Avançar.]**
1. (Opcional) Na página **[!UICONTROL Gerenciar publicação - Escopo]** , reveja a coluna **[!UICONTROL Publicar Público alvo]** na tabela para os ativos selecionados.

   | Configuração Publicar ativos na configuração do Dynamic Media | Ação selecionada | Direcionamento da publicação |
   | --- | --- | --- |
   | Imediatamente ou <br>na Ativação | Publicação | AEM e Dynamic Media |
   | Imediatamente ou <br>na Ativação | Publicar no Dynamic Media | Nenhum |
   | Publicação seletiva | Publicação | AEM |
   | Publicação seletiva | Publicar no Dynamic Media | Dynamic Media |
   | Imediatamente ou <br>na Ativação | Cancelar publicação | AEM e Dynamic Media |
   | Imediatamente ou <br>na Ativação | Desfazer publicação no Dynamic Media | Nenhum |
   | Publicação seletiva | Cancelar publicação | AEM |
   | Publicação seletiva | Desfazer publicação no Dynamic Media | Dynamic Media |

1. Na página **[!UICONTROL Gerenciar publicação - Escopo]** , execute um dos procedimentos a seguir:
   * Selecione um ou mais ativos que você deseja remover da publicação ou da despublicação.
   * No canto superior direito da página **[!UICONTROL Gerenciar publicação - Escopo]** , toque em **[!UICONTROL Publicar]** ou **[!UICONTROL Cancelar publicação]** para iniciar a ação.
1. Toque em **[!UICONTROL OK.]**

## Como verificar o status de publicação de um ativo {#check-publish-status-of-asset}

Você pode usar **[!UICONTROL Linha]** do tempo com visualização **[!UICONTROL de]** cartão, Visualização **[!UICONTROL de]** coluna ou Visualização **[!UICONTROL de]** Lista em AEM para verificar rapidamente o estado de publicação de um ativo.

**Para verificar o status de publicação de um ativo**

1. Em AEM, no canto superior esquerdo da página, toque no logotipo AEM para acessar o console de navegação global. No lado esquerdo da página, toque no ícone Navegação (logo acima do ícone Ferramentas) e, em seguida, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Em Visualização **[!UICONTROL de]** cartão, Visualização **[!UICONTROL de]** coluna ou Visualização **[!UICONTROL de]** Lista (a captura de tela abaixo mostra a Visualização **[!UICONTROL de]** Lista), abra uma pasta que contenha ativos que você tenha publicado ou não publicado.
1. Selecione um ativo para que ele apareça com uma marca de seleção. Consulte a captura de tela abaixo, por exemplo.
1. Near the upper-left corner of the page, from the drop-down menu, select **[!UICONTROL Timeline.]** A região **[!UICONTROL Status]** no painel esquerdo mostra o estado de publicação do ativo selecionado.
Quando você usa a Visualização **[!UICONTROL de]** Lista, uma coluna adicional para o estado de publicação do **[!UICONTROL Dynamic Media]** é exibida.
   * Uma pasta configurada para sincronizar com o Dynamic Media exibirá a coluna **[!UICONTROL Dynamic Media]** por padrão.
   * Uma pasta *não* configurada para sincronizar com o Dynamic Media não exibirá a coluna Mídia dinâmica.
      ![Visualização e linha do tempo da lista](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solução de problemas de publicação seletiva {#selective-publish-troubleshoot}

Um ativo que não é sincronizado com o Dynamic Media, mas que tem uma ação de publicação do Dynamic Media ativada, resulta na seguinte mensagem de erro e solução:

![Erro de publicação seletiva](/help/assets/assets-dm/selective-publish-error.png)

