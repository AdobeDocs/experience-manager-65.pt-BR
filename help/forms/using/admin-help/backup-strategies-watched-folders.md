---
title: Estratégias de backup para pastas monitoradas
description: Este documento descreve como as pastas monitoradas são afetadas por diferentes cenários de backup e recuperação, as limitações e os resultados desses cenários e como minimizar a perda de dados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Estratégias de backup para pastas monitoradas {#backup-strategies-for-watched-folders}

Esse conteúdo descreve como as pastas monitoradas são afetadas por diferentes cenários de backup e recuperação, as limitações e os resultados desses cenários e como minimizar a perda de dados.

*Pasta monitorada* é um aplicativo baseado em sistema de arquivos que invoca operações de serviço configuradas que manipulam o arquivo em uma das seguintes pastas na hierarquia de pastas monitoradas:

* Entrada
* Fase
* Saída
* Falha
* Preservar

Um usuário ou aplicativo cliente primeiro solta o arquivo ou pasta na pasta de entrada. A operação de serviço move o arquivo para a pasta de preparo para processamento. Depois que o serviço executa a operação especificada, ele salva o arquivo modificado na pasta de saída. Os arquivos de origem processados com sucesso são movidos para a pasta de preservação e os arquivos de processamento com falha são movidos para a pasta de falha. Quando a variável `Preserve On Failure` o atributo da pasta monitorada estiver ativado, os arquivos de origem processados com falha serão movidos para a pasta de preservação. (Consulte [Configurando pontos de extremidade de pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

Você pode fazer backup de pastas monitoradas fazendo backup do sistema de arquivos.

>[!NOTE]
>
>Esse backup é independente do processo de backup e recuperação do banco de dados ou do armazenamento de documentos.

## Como as pastas monitoradas funcionam {#how-watched-folders-work}

Este conteúdo descreve o processo de manipulação de arquivos de pastas monitoradas. É importante entender esse processo antes de desenvolver um plano de recuperação. Neste exemplo, a variável `Preserve On Failure` o atributo da pasta monitorada está habilitado. Os arquivos são processados na ordem em que chegam.

A tabela a seguir descreve a manipulação de cinco arquivos de amostra (file1, file2, file3, file4, file5) durante todo o processo. Na tabela, o eixo x representa o tempo, como Tempo 1 ou T1, e o eixo y representa as pastas dentro da hierarquia de pastas monitoradas, como Entrada.

<table>
 <thead>
  <tr>
   <th><p>Pasta</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Entrada</p></td>
   <td><p>arquivo1, arquivo2, arquivo3, arquivo4</p></td>
   <td><p>arquivo2, arquivo3, arquivo4</p></td>
   <td><p>arquivo3, arquivo4</p></td>
   <td><p>arquivo4</p></td>
   <td><p>vazio</p></td>
   <td><p>arquivo5</p></td>
   <td><p>vazio</p></td>
  </tr>
  <tr>
   <td><p>Fase</p></td>
   <td><p>vazio</p></td>
   <td><p>arquivo1</p></td>
   <td><p>arquivo2</p></td>
   <td><p>arquivo3</p></td>
   <td><p>arquivo4</p></td>
   <td><p>vazio</p></td>
   <td><p>arquivo5</p></td>
  </tr>
  <tr>
   <td><p>Saída</p></td>
   <td><p>vazio</p></td>
   <td><p>vazio</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Falha</p></td>
   <td><p>vazio</p></td>
   <td><p>vazio</p></td>
   <td><p>vazio</p></td>
   <td><p>vazio</p></td>
   <td><p>file3_fail, arquivo3 </p></td>
   <td><p>file3_fail, arquivo3 </p></td>
   <td><p>file3_fail, arquivo3 </p></td>
  </tr>
  <tr>
   <td><p>Preservar</p></td>
   <td><p>vazio</p></td>
   <td><p>vazio</p></td>
   <td><p>arquivo1 </p></td>
   <td><p>arquivo1, arquivo2 </p></td>
   <td><p>arquivo1, arquivo2 </p></td>
   <td><p>arquivo1, arquivo2, arquivo4 </p></td>
   <td><p>arquivo1, arquivo2, arquivo4 </p></td>
  </tr>
 </tbody>
</table>

O texto a seguir descreve a manipulação de arquivo para cada vez:

**T1:** Os quatro arquivos de amostra são colocados na pasta de entrada.

**T2:** A operação de serviço move o arquivo 1 para a pasta de preparo para manipulação.

**T3:** A operação de serviço move o arquivo 2 para a pasta de preparo para manipulação. Ele coloca os resultados de file1 na pasta de saída e move file1 para a pasta de preservação.

**T4:** A operação de serviço coloca o arquivo 3 na pasta de preparo para manipulação. Ele coloca os resultados do arquivo 2 na pasta de saída e coloca o arquivo 2 na pasta de preservação.

**T5:** A operação de serviço coloca o arquivo 4 na pasta de preparo para manipulação. A manipulação do arquivo 3 falha e a operação de serviço o coloca na pasta de falha.

**T6:** A operação de serviço coloca o arquivo 5 na pasta de entrada. Ele coloca os resultados do arquivo4 na pasta de saída, coloca o arquivo4 na pasta de preservação.

**T7:** A operação de serviço coloca o arquivo 5 na pasta de preparo para manipulação.

## Fazendo backup de pastas monitoradas {#backing-up-watched-folders}

É recomendável fazer backup de todo o sistema de arquivos da pasta monitorada para outro sistema de arquivos.

## Restaurando pastas monitoradas {#restoring-watched-folders}

Esta seção descreve como restaurar pastas monitoradas. As pastas monitoradas geralmente invocam processos de vida curta que são concluídos em um minuto. Nesses casos, a restauração da pasta monitorada com um backup feito por hora não evitará a perda de dados.

Por exemplo, se um backup for feito no momento T1 e o servidor falhar em T7, então file1, file2, file3 e file4 já estarão manipulados. Restaurar a pasta monitorada com um backup feito em T1 não evita a perda de dados.

Se um backup mais recente tiver sido feito, você poderá restaurar os arquivos. Ao restaurar os arquivos, considere em qual pasta de hierarquia de pastas o arquivo atual reside:

**Estágio:** Os arquivos nesta pasta serão processados novamente depois que a pasta monitorada for restaurada.

**Entrada:** Os arquivos nesta pasta serão processados novamente depois que a pasta monitorada for restaurada.

**Resultado:** Os arquivos nesta pasta não são processados.

**Saída:** Os arquivos nesta pasta não são processados.

**Preservar:** Os arquivos nesta pasta não são processados.

## Estratégias para minimizar a perda de dados {#strategies-to-minimize-data-loss}

As estratégias a seguir podem minimizar a perda de dados da pasta de saída e de entrada ao restaurar uma pasta monitorada:

* Faça backup das pastas de saída e de falha com frequência, por exemplo, a cada hora, para evitar a perda de arquivos de resultado e de falha.
* Fazer backup dos arquivos de entrada em uma pasta diferente da pasta monitorada. Isso garante a disponibilidade do arquivo após a recuperação, caso não seja possível encontrar os arquivos na pasta de saída ou de falha. Verifique se o esquema de nomenclatura de arquivo é consistente.

  Por exemplo, se você estiver salvando a saída com `%F.`*extensão*, o arquivo de saída terá o mesmo nome que o arquivo de entrada. Isso ajuda a determinar quais arquivos de entrada são manipulados e quais devem ser reenviados. Se você vir somente o arquivo file1_out na pasta de resultados e não file2_out, file3_out e file4_out, deverá reenviar o arquivo2, file3 e file4.

* Se o backup de pasta monitorada disponível for mais antigo do que o tempo necessário para processar o trabalho, você deverá permitir que o sistema crie uma pasta monitorada e coloque automaticamente os arquivos na pasta de entrada.
* Se o último backup disponível não for suficientemente recente, o tempo de backup for menor que o tempo necessário para processar os arquivos e a pasta monitorada for restaurada, o arquivo será manipulado em um dos seguintes estágios diferentes:

   * **Fase 1:** Na pasta de entrada
   * **Fase 2:** Copiado para a pasta de preparo, mas o processo ainda não foi chamado
   * **Fase 3:** Copiado para a pasta de preparo e o processo é chamado
   * **Fase 4:** Manipulação em andamento
   * **Fase 5:** Resultados retornados

  Se os arquivos estiverem no Estágio 1, eles serão manipulados. Se os arquivos estiverem no Estágio 2 ou 3, coloque-os na pasta de entrada para que a manipulação ocorra novamente.

  >[!NOTE]
  >
  >Se a manipulação de um arquivo ocorrer mais de uma vez, a perda de dados será evitada, mas os resultados poderão ser duplicados.

## Conclusão {#conclusion}

Devido à natureza dinâmica e em constante mudança de uma pasta monitorada, a restauração de pastas monitoradas deve ser feita com arquivos cujo backup seja feito em um dia. Uma prática recomendada seria fazer backup dos resultados, armazenar a pasta de entrada em um servidor e rastrear arquivos de entrada para que você possa reenviar o trabalho se houver uma falha.
