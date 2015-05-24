# Other Topics

## Catchall Routes

You can use optional placeholder tokens to create a generic catchall route:

```php
<?php
$map->get('catchall', '{/controller,action,id}')
    ->defaults([
        'controller' => 'index',
        'action' => 'browse',
        'id' => null,
    ]);
?>
```

That will match these paths, with these attribute values:

- `/           : ['controller' => 'index', 'action' => 'browse', 'id' => null]`
- `/foo        : ['controller' => 'foo',   'action' => 'browse', 'id' => null]`
- `/foo/bar    : ['controller' => 'foo',   'action' => 'bar',    'id' => null]`
- `/foo/bar/42 : ['controller' => 'foo',   'action' => 'bar',    'id' => '42']`

Because routes are matched in the order they are added, the catchall should be the last route in the _Map_ so that more specific routes may match first.

## Logging

You may wish to log the _Matcher_ activity using a PSR-3 compliant logger. You can tell the _RouterContainer_ how to create a logger instance by passing a factory callable to `setLoggerFactory()`.

```php
<?php
$routerContainer->setLoggerFactory(function () {
    return new Psr3Logger();
});
?>
```

The _RouterContainer_ will use that callable to create the logger and inject it into the _Matcher_. You can then review the debug-level logs for _Matcher_ activity.