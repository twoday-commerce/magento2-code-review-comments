# Magento 2 Code Review Comments

This page collects common comments made during reviews of Magento code, so that a single detailed explanation can be referred to by shorthands.

Changes and additions should be discussed and agreed on before being added to this list.

- [Code style](#code-style)
- [No Object Manager](#no-object-manager)

## Code style
Code should be formatted according to PSR-12. Using a common code style makes it easier to see actual mechanical code changes in diffs, instead of user-specific editor formatting issues (tabs vs spaces, positioning of braces, etc). Use [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) to format your code. 

## No Object Manager
Magento prohibits the direct use of the ObjectManager in your code because it hides the real dependencies of a class. Any required classes should be added as dependencies using [constructor dependency injection](https://en.wikipedia.org/wiki/Dependency_injection#Constructor_injection_comparison). There are some exceptions, you can find them[ on the dedicated site about using the Object Manager](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/object-manager.html). 
