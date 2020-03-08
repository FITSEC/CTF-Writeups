Spooky Store
=====
#### Solver: ap3xsh0t

## Category: Web

> "It's a simple webpage with 3 buttons, you got this :)"

## Methodology






```php
window.contentType = 'application/xml';

function payload(data) {
    var xml = '<?xml version="1.0" encoding="UTF-8"?>';
    xml += '<locationCheck>';

    for(var pair of data.entries()) {
        var key = pair[0];
        var value = pair[1];

        xml += '<' + key + '>' + value + '</' + key + '>';
    }

    xml += '</locationCheck>';
    return xml;
}
```
