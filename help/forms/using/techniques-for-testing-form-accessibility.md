---
title: Técnicas para testar a acessibilidade do formulário
description: Saiba mais sobre as técnicas para testar a acessibilidade de formulários no designer de formulários
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
exl-id: 77fd3bc5-9a05-4442-af2b-238169d8061a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%
---
# Técnicas para testar a acessibilidade do formulário

Para garantir que seus formulários sejam acessíveis a uma grande variedade de usuários, você deve testá-los com uma variedade de tecnologias assistivas. Você pode testar seus formulários de maneira simples e econômica usando as técnicas descritas nesta seção.
Verifique se o formulário pode ser preenchido somente com o teclado. Certifique-se de preencher o formulário inteiro e testar todos os campos e botões. Ao preencher o formulário, determine se são necessárias melhorias com base nas respostas às seguintes perguntas:

* Há operações que não podem ser executadas?
* Há alguma operação complicada ou difícil de executar?
* Os mecanismos de teclado estão bem documentados?
* Todos os controles e itens de menu têm teclas de acesso sublinhadas?

As versões demo do software de leitor de tela podem ser baixadas gratuitamente pela Internet. Para testar os resultados do leitor de tela, desligue o monitor e use somente o leitor de tela para navegar e preencher o formulário. Se você for o autor do formulário, sua familiaridade com o formulário pode dificultar a determinação de se as informações lidas pelo leitor de tela são suficientes e fazem sentido. Se possível, peça para outra pessoa testar seu formulário dessa maneira.

Versões demo do software de ampliação de tela também estão disponíveis para testes na Internet.

Software de fala para texto, disponível a um custo nominal, pode ser usado para testar o formulário usando apenas entrada de voz.
Muitos usuários com deficiências visuais dependem de alto contraste entre o texto e o plano de fundo para ler o formulário. O Microsoft Windows tem um esquema de cores de alto contraste que fornece uma exibição semelhante à que muitos usuários com deficiências visuais usarão para preencher o formulário. Para definir seu vídeo para o modo de alto contraste, habilite o recurso por meio das Opções de Acessibilidade no Painel de Controle do Windows. Ao preencher o formulário neste modo, determine se são necessárias melhorias com base nas respostas às seguintes perguntas:

* Partes do formulário se tornam invisíveis, irreconhecíveis ou difíceis de usar?
* Alguma área continua a aparecer em preto sobre um fundo branco?
* Algum elemento está dimensionado ou truncado incorretamente?
