---
title: Propriedades de configuração de Comunicações interativas
description: Editar propriedades de configuração padrão para Comunicações interativas
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 6%

---

# Propriedades de configuração de Comunicações interativas{#interactive-communications-configuration-properties}

As Comunicações Interativas incluem propriedades que são configuradas automaticamente após a instalação do pacote do [complemento do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Os autores de Comunicações interativas podem editar essas propriedades de configuração padrão usando a página **Configuração do console da Web do Adobe Experience Manager**.

Abra a página **Configuração do Console da Web do Adobe Experience Manager** usando esta URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

As propriedades de configuração incluem:

* [Configuração de fragmentos do documento](#document-fragments-configuration)
* [Criar configuração de correspondência](#create-correspondence-configuration)
* [Configuração do canal da Web do formulário adaptável e da comunicação interativa](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuração do tema do canal da Web do formulário adaptável e da comunicação interativa](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuração de fragmentos do documento {#document-fragments-configuration}

Selecione a **configuração de fragmentos de documento** na página **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração de fragmentos de documento.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Formatos de Exibição de Dados</td> 
   <td>Formato de exibição específico da localidade para campos, variáveis e elementos do modelo de dados de formulário disponíveis ao criar uma Comunicação interativa para canais de impressão e da Web.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR e ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Recuo</td> 
   <td>A largura da unidade única de recuo aplicada ao texto nos fragmentos do documento da lista.</td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima de números romanos</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número ao usar números romanos em fragmentos de documentos de lista. </td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima do número</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número ao usar listas numeradas separadas de números romanos em fragmentos de documentos de lista.</td> 
   <td>8,0 mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Criar configuração de correspondência {#create-correspondence-configuration}

Selecione **Criar configuração de correspondência** na página **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração da interface do usuário do Agente.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Mostrar conteúdo resolvido para edição</td> 
   <td>Marque a caixa de seleção para mostrar o conteúdo resolvido (valores reais em vez de espaços reservados) ao editar o módulo de texto na interface do agente.</td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
  <tr> 
   <td>Aplicar marca d'água durante a visualização</td> 
   <td>Marque a caixa de seleção para aplicar uma marca d'água ao canal de impressão de comunicação interativa no modo de Visualização.</td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
  <tr> 
   <td>Ativar incorporação de fontes no PDF</td> 
   <td><p>Marque a caixa de seleção para ativar as fontes incorporadas nos documentos do PDF. Após selecionar essa opção, é possível incorporar novas fontes após gerar ou visualizar os documentos do PDF usando a interface do usuário do agente. Use o canal de impressão de comunicação interativa para gerar e visualizar documentos PDF.</p> <p>A incorporação de fontes em um documento PDF é útil se uma fonte estiver disponível em uma máquina usada para gerar o PDF e não estiver disponível na máquina cliente que acessa o PDF.</p> <p>Para obter mais informações sobre como incorporar fontes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
 </tbody> 
</table>

## Configuração do canal da Web do formulário adaptável e da comunicação interativa {#adaptive-form-and-interactive-communication-web-channel-configuration}

Selecione **Configuração do canal da Web do Formulário Adaptável e da Comunicação Interativa** na página **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração do canal da Web do Forms Adaptável e das Comunicações Interativas. A tabela a seguir descreve as propriedades relacionadas às Comunicações Interativas:

| Propriedade | Descrição | Padrão | Valores aceitáveis |
|---|---|---|---|
| Mostrar espaço reservado | Marque a caixa de seleção para ativar a exibição de espaços reservados para campos incluídos em formulários adaptáveis e Comunicações interativas. | Selecionado | Não aplicável |
| Máximo de entradas de cache | Defina o número máximo de formulários adaptáveis e Comunicações interativas que podem ser recuperadas usando a memória cache. | 100 | Número |
| Tornar o nome do arquivo exclusivo | Marque a caixa de seleção para ter nomes exclusivos para arquivos incluídos como anexos no Adaptive Forms e nas Comunicações interativas. | Não selecionado | Não aplicável |

## Configuração do tema do canal da Web do formulário adaptável e da comunicação interativa {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Selecione **Configuração do tema de canal da Web do formulário adaptável e da comunicação interativa** na página **Configuração do console da Web do Adobe Experience Manager** para exibir as propriedades de configuração dos temas de canal da Web do Forms adaptável e das comunicações interativas.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Nome da lista de fontes</td> 
   <td>Lista de fontes disponíveis para uso ao criar o Forms adaptável e as Comunicações interativas.</td> 
   <td><p>Geórgia</p> <p>Livro Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Linotipo de Palatino</p> </td> 
   <td>Todas as fontes válidas do servidor Adobe</td> 
  </tr> 
 </tbody> 
</table>
