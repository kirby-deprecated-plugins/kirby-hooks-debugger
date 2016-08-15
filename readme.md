# Kirby Hooks Debugger

There are two main problems with hook errors in the panel.

1. The panel hangs.
1. No useful information about the error is displayed.

This plugin presents a useful error message.

![](docs/screenshot2.png)

![](docs/screenshot1.png)

In the future I hope there will be a built in solution, but until then this plugin might be useful. 

## 1. Install

### Kirby CLI

Run this command:

```
kirby plugin:install jenstornell/kirby-hooks-debugger
```

### Manually

```
Add the folder kirby-hooks-debugger into /site/plugins/.
```

## 2. Usage

### 1. Blueprint

It's recommended to add this field before any other field.

```yml
fields:
  hooksdebugger:
    type: hooksdebugger
```

### 2. Must be loaded first

Kirby Hooks Debugger needs to load before any other plugin that uses hooks in order to work. There are at least two ways to do that:

**Alternative 1 - Rename the plugin**

Rename the folder `kirby-hooks-debugger` to `aaa` and the file `kirby-hooks-debugger.php` to `aaa.php`.

**Alternative 2 - Load the Kirby Hooks Debugger plugin from your plugin**

If you are building a plugin you can add this line to force load the Kirby Hooks Debugger plugin.

```php
kirby()->plugin('kirby-hooks-debugger');
```

### 3. Debug needs to be `true`

You need to set this in `config.php`:

```
c::set('debug', true);
```

## Options

Add them to config.php.

### Logfile path

Where the log should be stored.

```php
c::get( 'plugin.hooks.debugger.logfile', kirby()->roots()->index() . DS . 'hooks-debugger.txt' );
```

### Error types

Add an array with error numbers or constants.
http://php.net/manual/en/errorfunc.constants.php

Default is to only show fatal run-time errors.

```php
c::get('plugin.hooks.debugger.error.types', array(1));
```

### Hooks

Hooks to debug. Default is every built in hook.

```php
c::get('plugin.hooks.debugger.hooks', array(
  'panel.page.create',
  'panel.page.update',
  'panel.page.delete',
  'panel.page.sort',
  'panel.page.hide',
  'panel.page.move',
  'panel.site.update',
  'panel.file.upload',
  'panel.file.replace',
  'panel.file.rename',
  'panel.file.update',
  'panel.file.sort',
  'panel.file.delete',
  'panel.user.create',
  'panel.user.update',
  'panel.user.delete',
  'panel.avatar.upload',
  'panel.avatar.delete'
));
```

## Changelog

0.1

Initial release

## Requirements

Kirby 2.3.2

## License

MIT