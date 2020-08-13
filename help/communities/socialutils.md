---
title: Refatoração de SocialUtils
seo-title: Refatoração de SocialUtils
description: O pacote com.adobe.cq.social.ugcbase.SocialUtils foi substituído no AEM 6.1
seo-description: O pacote com.adobe.cq.social.ugcbase.SocialUtils foi substituído no AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Refatoração de SocialUtils {#socialutils-refactoring}

## Pacote SocialUtils obsoleto {#socialutils-package-deprecated}

O pacote `com.adobe.cq.social.ugcbase.SocialUtils` foi substituído no AEM 6.1.

As tabelas a seguir listas os métodos a serem usados no lugar dos `SocialUtils` métodos.

## Pacote SocialResourceUtilities  {#socialresourceutilities-package}

| Métodos em com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| CheckPermission booleano(Resolver de Recursos, caminho de String, ação String) |  |
| SocialResourceProvider getSocialResourceProvider(recurso) |  |
| SocialResourceConfiguration getStorageConfig(recurso de recurso) |  |
| Recurso getUGCResource(Resource userResource) |  |
| Recurso getUGCResource(Resource userResource, ResourceResolverFactory rf) | novo |
| Recurso getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | novo |
| Recurso getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(recurso de recurso) |  |
| String resourceToACLPath(Resource) |  |
| String resourceToUGCStoragePath (recurso) | substitui String resourceToUGCPath(recurso de recurso) |
| String UGCToResourcePath(Resource) |  |
| String UGCToResourcePath(String ugcPath) | assinatura de método alterada |
| String UGCToResourcePath(String ugcPath, ResourceResolver resolvedor) | novo |

| Métodos em `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(recurso) | substitui SocialResourceProvider getConftifiedProvider(recurso) |

## Pacote SCFUtilities {#scfutilities-package}

| Métodos em `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, tamanho int) |
| String getAvatar(UserProperties userProperties, String fixedDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String fixedDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Página getContainPage(Recurso) |
| String getSocialProfileURL(String username, ResourceResolver resolver, página) |
| UserProperties getUserProperties(Resolver de Recursos, UserId de Cadeia de Caracteres) |

## For Internal Use Only {#for-internal-use-only}

| booleano canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(mensagem String) |
| String createUniqueNameHint(mensagem String, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(caminho de string, resolvedor do ResourceResolver) |
| String getPagePath(Recurso) |
| String getPagePath(Caminho da string) |
| String getResourceTypeForIncludedResource(Componente de recurso, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Recurso, String styleProperty, String defaultValue) |
| boolean isResourceOwner(Recurso) |
| String mapUGCPath(Recurso) |
| String mapUGCPath(String ugcPath, ResourceResolver resolvedor) |
| boolean mayPost(ResourceResolver resolver, recurso de recurso) |
| String prepareUserGeneratedContent(Resolver resolvedor de Recursos, caminho de String) |

## Métodos não disponíveis {#methods-no-longer-available}

| Nó createNode(Resolver Resolver resolvedor de Recursos, caminho de String, nodeType de String) |
|---|
| Recurso getResourceAtPath(Resolver resolvedor de Recursos, caminho de String) |
| Recurso getResourceAtPath(ResourceResolver resolvedor, caminho da string, String resourceType) |
| Configuração getStorageCloudServiceConfig (recurso de recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booleano mayAccessUGC(ResourceResolver resolver) |

