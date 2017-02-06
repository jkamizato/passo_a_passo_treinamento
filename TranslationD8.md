# Translation Drupal 8

Cenários do blog da Kaplan e como resolvemos.
URL: http://www.kaplaninternational.com/blog
Blog multi-idioma
100% Traduzível


## Cenário 1. Criar conteúdo traduzível.

Para o exemplo, vamos criar 2 idiomas:
Ingles (padrão) e Português

- Visão geral (Simples e rápida)
	- Content Translation
	- User Interface Translation
	- Configuration Translation



## Cenário 2. 
Criar um bloco com configurações traduzíveis. Por exemplo, o site da Kaplan tem diferentes páginas de facebook para cada idioma.Criar um widget que carrega uma página para cada idioma:
Ver:
* http://www.kaplaninternational.com/blog
* http://www.kaplaninternational.com/ar/blog
Mesmo bloco, mas com carregamento de widgets diferente

___


- Bloco com configurações traduzíveis
	- Adicionando schema
	
No módulo deve adicionar o arquivo module/config/schema/module.schema.yml

file: module.schema.yml

```yml
block.settings.custom_block_id:
	type: block_settings
	mapping: 
		custom_block_field:
	     type: label			 
	     label: Custom Block Field
```

https://developers.facebook.com/docs/plugins/page-plugin

- Patch facebook
	https://www.drupal.org/node/2758615
- Patch disqus
	https://www.drupal.org/node/2707313


## Cenário 3.
Perfil moderador traduzir configuração de apenas 1 bloco espefícico.

Ver: http://www.kaplaninternational.com/blog

Ad block
___

- Criar Role Moderator
- Criar module.permissions.yml
	[file module.permissions.yml]
		nome da permissao:
			title: Título da Permissao
			description: Descrição da permissão.
	[file]
- Busca por 'translate configuration'
	- Override o config_translation.access.overview :access
	- Copia a classe
	
Classe: ConfigTranslationOverviewAcess: function doCheckAccess
	
```php
if ($account->hasPermission('custom permission') &&
  in_array('block.block.adbottomblock', $mapper->getConfigNames())) {
  return AccessResult::allowed()->cachePerPermissions();
}
```



# Cola
//Se sobrar tempo
- Mudança do NID
Scheduler translation
Patch
https://www.drupal.org/node/2776665


Patch importantes
https://www.drupal.org/node/2189267
