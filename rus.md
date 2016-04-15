# Новая возможность языка в ES2016: Array.prototype.includes

`Array.prototype.includes` — это новая возможность ECMAScript, предложенная 
Домиником Дениколой (Domenic Denicola) и Риком Валдроном (Rick Waldron). 
Она находится на четвертой стадии [процесса формирования релизов][6], то есть готова и является частью 
стандарта [ECMAScript 2016][1].


## includes — новый метод Array
 
`includes` — новый метод `Array`. Его сигнатура:

    Array.prototype.includes(value : any) : boolean

Метод возвращает `true`, если массив содержит `value`, в противном случае —  `false`:

    > ['a', 'b', 'c'].includes('a')
    true
    
    > ['a', 'b', 'c'].includes('d')
    false
    
`includes` подобен `indexOf`, следующие два выражения практически 
эквивалентны друг другу:

    arr.includes(x)
    arr.indexOf(x) >= 0

Основное отличие заключается в том, что `includes()` находит `NaN`, 
в то время как `indexOf()` — нет:

    > [NaN].includes(NaN)
    true
    
    > [NaN].indexOf(NaN)
    -1

`includes` не отличает `+0` от `-0` ([что абсолютно нормально для JavaScript][2]):

    > [-0].includes(+0)
    true

У типизированных массивов тоже есть метод `includes()`:

    let tarr = Uint8Array.of(12, 5, 3);
    console.log(tarr.includes(5)); // true
    

## Часто задаваемые вопросы

* **Почему метод называется `includes`, а не `contains`?**   
  Изначально так и планировалось, но обнаружили, что в результате ломается код,
  который уже есть в сети ([MooTools добавляет метод `contains` в `Array.prototype`][3]).

* **Почему метод называется `includes`, а не `has`?**   
  `has` используется для ключей (`Map.prototype.has`), `includes` используется
  для элементов (`String.prototype.includes`). Элементы `Set` можно рассматривать
  как и то, и другое, поэтому есть `Set.prototype.has` (и нет `includes`).

* **[Метод `String.prototype.includes` из ES6][4] работает с целыми строками,
  а не с отдельными буквами. Разве логично, что Array.prototype.includes ищет
  отдельные элементы?**   
  Если бы `includes` массивов работал точно так же, как и `includes` строк, он
  принимал бы массивы, а не отдельные элементы. Но логика работы обоих `includes`
  такая же, как у соответствующих методов `indexOf`: буквы рассматриваются
  как частный случай строк с произвольной длиной.


## Материалы для дальнейшего изучения

*   [`Array.prototype.includes`][5] (разработано Домиником Дениколой и Риком Валдроном)


[1]: http://www.2ality.com/2016/01/ecmascript-2016.html
[2]: http://speakingjs.com/es5/ch11.html#two_zeros
[3]: https://esdiscuss.org/topic/having-a-non-enumerable-array-prototype-contains-may-not-be-web-compatible
[4]: http://exploringjs.com/es6/ch_strings.html#_checking-for-containment-and-repeating-strings
[5]: https://github.com/tc39/Array.prototype.includes/
[6]: http://www.2ality.com/2015/11/tc39-process.html
