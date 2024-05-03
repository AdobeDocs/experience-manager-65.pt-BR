---
title: Adicionar domínios
description: Saiba como adicionar um domínio corporativo, local ou híbrido usando configurações do Gerenciamento de domínio e considerações gerais para nomes de domínio e IDs.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# Adicionar domínios {#adding-domains}

## Adicionar um domínio enterprise {#add-an-enterprise-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Novo Domínio Enterprise.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique se deseja ativar o bloqueio de conta. (Consulte [Definir configurações de bloqueio de conta](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Por padrão, Ativar bloqueio de conta está selecionado.
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação, selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa. Os valores possíveis são LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.

   Se você selecionar LDAP, poderá usar o servidor LDAP especificado na configuração do diretório ou escolher outro servidor LDAP para usar na autenticação. Se você escolher um servidor diferente, seus usuários deverão existir em ambos os servidores LDAP.

1. Forneça todas as informações adicionais necessárias na página. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Adicione um diretório ou uma SPI (Interface de Provedor de Serviço) personalizada. (Consulte [Adição de diretórios ou SPIs personalizadas](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Clique em Concluir e em OK.

Após criar um domínio enterprise, sincronize manualmente o diretório ou crie um trigger para executar uma sincronização antes que o Gerenciamento de Usuários possa usá-lo. Em seguida, você pode configurar uma programação de sincronização de diretório e executar a sincronização manual, conforme necessário. (Consulte [Sincronização de diretórios](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Adicionar um domínio local {#add-a-local-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Novo domínio local.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique se deseja ativar o bloqueio de conta e clique em OK. (Consulte [Definir configurações de bloqueio de conta](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Por padrão, Ativar bloqueio de conta está selecionado.

## Adicionar um domínio híbrido {#add-a-hybrid-domain}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Novo domínio híbrido.
1. Na caixa ID, digite um identificador exclusivo para o domínio e, na caixa Nome, digite um nome descritivo para o domínio. (Consulte [Considerações importantes para nomes de domínio e IDs](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação, selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa. Os valores possíveis são LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.
1. Forneça todas as informações adicionais necessárias na página. (Consulte [Configurações de autenticação](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Clique em OK e em OK novamente.

## Considerações importantes para nomes de domínio e IDs {#important-considerations-for-domain-names-and-ids}

Lembre-se das seguintes considerações ao escolher um nome de domínio e uma ID:

### Considerações gerais {#general-considerations}

* Quando você está usando um provedor de banco de dados diferente do DB2, a ID do domínio pode conter até 50 bytes. Se você estiver usando caracteres ASCII de byte único, o limite será de 50 caracteres. Se o identificador de domínio contiver caracteres multibyte, esse limite será reduzido. Por exemplo, se você criar um domínio cujo identificador contém caracteres de 3 bytes, o limite será de 16 caracteres. Além disso, não é possível criar domínios que contenham caracteres de 4 bytes. Se você criar uma ID de domínio que exceda esse limite, os formulários AEM estarão em um estado instável. Para se recuperar desse estado instável, consulte o &quot; [Remova um domínio que contenha caracteres estendidos ou multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; nesta página.
* O número de domínios corporativos e domínios locais que podem ser criados em formulários AEM depende do comprimento de cada uma das IDs de domínio. Quando você adiciona um domínio corporativo ou híbrido, o User Management atualiza a string configInstance no nó AuthProviders do arquivo de configuração dos formulários AEM (config.xml). A cadeia de caracteres configInstance contém uma lista separada por vírgulas dos caminhos absolutos de todos os domínios associados ao provedor de autorização. Esta cadeia de caracteres tem um limite de tamanho de 8.192 caracteres. Quando esse limite é atingido, não é possível criar domínios adicionais.

### Considerações ao usar DB2 {#considerations-when-using-db2}

Ao usar DB2 para o banco de dados de formulários AEM, o comprimento máximo permitido da ID do domínio depende do tipo de caracteres usados:

* 100 bytes únicos (ASCII) (por exemplo, caracteres usados em inglês, francês ou alemão)
* 50 bytes duplos (por exemplo, caracteres usados nos idiomas chinês, japonês ou coreano)
* 25 quatro bytes (por exemplo, caracteres usados no idioma chinês tradicional)

### Considerações ao usar o MySQL {#considerations-when-using-mysql}

Ao usar o MySQL como banco de dados do AEM Forms, as seguintes limitações se aplicam:

* Use somente caracteres de byte único (ASCII) para a ID do domínio e o nome do domínio. Se você usar caracteres ASCII estendidos, os formulários AEM estarão em um estado instável e poderão gerar uma exceção se você tentar excluir o domínio. Para se recuperar desse estado instável, consulte o &quot; [Remova um domínio que contenha caracteres estendidos ou multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; nesta página.
* Você não pode criar dois domínios que tenham o mesmo nome, mas que sejam diferentes em maiúsculas e minúsculas. Por exemplo, tentar criar um domínio chamado *Adobe* quando um domínio chamado *adobe* já existe resulta em um erro.
* O Gerenciamento de usuários não pode diferenciar entre dois nomes de domínio que diferem somente no uso de caracteres estendidos. Por exemplo, se você criar um domínio chamado *abcde* e um domínio chamado *âbcdè*, eles são considerados iguais.

### Remova um domínio que contenha caracteres estendidos ou multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exporte o arquivo de configuração, conforme descrito em [Importação e exportação do arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Abra o arquivo de configuração e, no nó Domínios, localize o nó cujo atributo de nome corresponde ao nome do domínio criado com caracteres estendidos ou de vários bytes. Exclua o nó inteiro relacionado a esse domínio.
1. Em seu banco de dados, pesquise pelo domínio na tabela edcprincipaldomainentity:

   * Selecionar `*` de edcprincipaldomainentity.
   * Localize o nome de domínio que contém caracteres estendidos ou multibyte e defina seu status como OBSOLETE.

1. Importe o arquivo de configuração atualizado, conforme descrito em [Importação e exportação do arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
