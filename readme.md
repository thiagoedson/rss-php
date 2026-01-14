# RSS & Atom Feeds para PHP

[![Downloads no mês](https://img.shields.io/packagist/dm/dg/rss-php.svg)](https://packagist.org/packages/dg/rss-php)
[![Última versão estável](https://poser.pugx.org/dg/rss-php/v/stable)](https://github.com/dg/rss-php/releases)
[![Licença](https://img.shields.io/badge/license-New%20BSD-blue.svg)](https://github.com/dg/rss-php/blob/master/license.md)

Biblioteca pequena e fácil de usar para consumir feeds RSS e Atom em PHP.

## Sumário

- [Requisitos](#requisitos)
- [Instalação](#instalação)
- [Uso básico](#uso-básico)
  - [RSS](#rss)
  - [Atom](#atom)
- [Cache](#cache)
- [Autenticação básica](#autenticação-básica)
- [Conversão para array](#conversão-para-array)
- [Tratamento de erros](#tratamento-de-erros)
- [Exemplos](#exemplos)
- [Licença](#licença)

## Requisitos

- PHP 5.2.2 ou superior.
- Extensão cURL habilitada **ou** `allow_url_fopen` ativo no PHP.

## Instalação

Com Composer:

```bash
composer require dg/rss-php
```

Ou com o binário local do Composer:

```bash
php composer.phar require dg/rss-php
```

## Uso básico

### RSS

```php
$rss = Feed::loadRss($url);

echo 'Título: ', $rss->title;
echo 'Descrição: ', $rss->description;
echo 'Link: ', $rss->link;

foreach ($rss->item as $item) {
	echo 'Título: ', $item->title;
	echo 'Link: ', $item->link;
	echo 'Timestamp: ', $item->timestamp;
	echo 'Descrição: ', $item->description;
	echo 'Conteúdo HTML: ', $item->{'content:encoded'};
}
```

### Atom

```php
$atom = Feed::loadAtom($url);

foreach ($atom->entry as $entry) {
	echo 'Título: ', $entry->title;
	echo 'Link: ', $entry->link['href'];
	echo 'Atualizado em: ', $entry->updated;
	echo 'Timestamp: ', $entry->timestamp;
}
```

## Cache

O cache é opcional e pode ser habilitado definindo o diretório e o tempo de expiração.

```php
Feed::$cacheDir = __DIR__ . '/tmp';
Feed::$cacheExpire = '5 hours';
```

## Autenticação básica

Caso o feed exija autenticação, informe usuário e senha:

```php
$rss = Feed::loadRss($url, $usuario, $senha);
$atom = Feed::loadAtom($url, $usuario, $senha);
```

## Conversão para array

Se preferir trabalhar com arrays, utilize `toArray()`:

```php
$rss = Feed::loadRss($url);
$dados = $rss->toArray();
```

## Tratamento de erros

As falhas de carregamento ou validação disparam `FeedException`:

```php
try {
	$rss = Feed::load($url);
} catch (FeedException $erro) {
	echo 'Falha ao carregar o feed: ', $erro->getMessage();
}
```

## Exemplos

Veja os exemplos prontos na raiz do projeto:

- `example-rss.php`
- `example-atom.php`

## Licença

New BSD License. Consulte o arquivo [`license.md`](license.md).

---
(c) David Grudl, 2008 (http://davidgrudl.com)
