Нам нужно найти символ `#`, за которым следуют 6 шестнадцатеричных символов.

Шестнадцатеричный символ может быть описан с помощью регулярного выражения как `pattern:[0-9a-fA-F]`. Или же как `pattern:[0-9a-f]`, если мы используем модификатор `i`.

Затем мы можем добавить квантификатор `pattern:{6}`, так как нам нужно 6 таких символов.

В результате наше регулярное выражение получилось таким: `pattern:/#[a-f0-9]{6}/gi`.

```js run
let reg = /#[a-f0-9]{6}/gi;

let str = "color:#121212; background-color:#AA00ef bad-colors:f#fddee #fd2"

alert( str.match(reg) );  // #121212,#AA00ef
```

Проблема в том, что находятся также совпадения, принадлежащие более длинным последовательностям символов:

```js run
alert( "#12345678".match( /#[a-f0-9]{6}/gi ) ) // #12345678
```

Чтобы исправить это, мы можем добавить в конец нашего регулярного выражения `pattern:\b`:

```js run
// цвет
alert( "#123456".match( /#[a-f0-9]{6}\b/gi ) ); // #123456

// не цвет
alert( "#12345678".match( /#[a-f0-9]{6}\b/gi ) ); // null
```