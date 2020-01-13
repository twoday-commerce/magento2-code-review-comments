# Magento 2 Code Review Comments

This page collects common comments made during reviews of Magento code, so that a single detailed explanation can be referred to by shorthands.

Changes and additions should be discussed and agreed on before being added to this list.

- [Code style](#code-style)
- [No Object Manager](#no-object-manager)
- [PSR-3 Logger Exceptions](#psr-3-logger-exceptions)

## Code style
Code should be formatted according to PSR-12. Using a common code style makes it easier to see actual mechanical code changes in diffs, instead of user-specific editor formatting issues (tabs vs spaces, positioning of braces, etc). Use [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) to format your code. 

## No Object Manager
Magento prohibits the direct use of the ObjectManager in your code because it hides the real dependencies of a class. Any required classes should be added as dependencies using [constructor dependency injection](https://en.wikipedia.org/wiki/Dependency_injection#Constructor_injection_comparison). There are some exceptions, you can find them[ on the dedicated site about using the Object Manager](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/object-manager.html). 

## PSR-3 Logger Exceptions
When logging an exception, the `\Throwable` should in almost all cases be passed as a member of the logger context, named `exception`. [The PSR-3 document recommends this](https://www.php-fig.org/psr/psr-3/#13-context), and it gives valuable context to your logs, in addition to giving your exception objects more utility.

For example, don't write:
```php
$logger->error($e->getMessage());
```

Instead, write:
```php
$logger->error("An error occurred when doing X: {message}", ['exception' => $e, 'message' => $e->getMessage()]);
```
