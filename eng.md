`Array.prototype.includes` is an ECMAScript proposal by Domenic Denicola and
Rick Waldron. It is at stage 4 (finished) and part of[ECMAScript 2016][1].

 
The Array method `includes` has the following signature:

    Array.prototype.includes(value : any) : boolean
    

It returns `true` if `value` is an element of its receiver (`this`) and `false`

    > ['a', 'b', 'c'].includes('a')
        true
        > ['a', 'b', 'c'].includes('d')
        false
    

`includes` is similar to `indexOf` – the following two expressions are mostly
equivalent:

    arr.includes(x)
        arr.indexOf(x) >= 0
    

The main difference is that `includes()` finds `NaN`, whereas `indexOf()` doesn
’t:

    > [NaN].includes(NaN)
        true
        > [NaN].indexOf(NaN)
        -1
    

`includes` does not distinguish between `+0` and `-0` (
[which is how almost all of JavaScript works][2]):

    > [-0].includes(+0)
        true
    

Typed Arrays will also have a method `includes()`:

    let tarr = Uint8Array.of(12, 5, 3);
        console.log(tarr.includes(5)); // true
    

### Frequently asked questions {#frequently-asked-questions}

*   **Why is the method called `includes` and not `contains`?**  
    The latter was the initial choice, but that broke code on the web (
    [MooTools adds this method to `Array.prototype`][3]).

*   **Why is the method called `includes` and not `has`?**  
    `has` is used for keys (`Map.prototype.has`), `includes` is used for
    elements
    (`String.prototype.includes`). The elements of a Set can be viewed as being
    both keys and values, which is why there is a
   `Set.prototype.has` (and no `includes`).
*   **[The ES6 method `String.prototype.includes`][4] works with strings, not
    characters. Isn’t that inconsistent w.r.t.
   `Array.prototype.includes`?**  
    If Array `includes` worked exactly like string `includes`, it would accept
    arrays, not single elements. But the two
   `includes` follow the example of `indexOf`; characters are seen as a special
    case and strings with arbitrary lengths as the general case.
   

### Further reading {#further-reading}

*   [`Array.prototype.includes`][5] (Domenic Denicola, Rick Waldron)

 [1]: http://www.2ality.com/2016/01/ecmascript-2016.html
 [2]: http://speakingjs.com/es5/ch11.html#two_zeros

 [3]: https://esdiscuss.org/topic/having-a-non-enumerable-array-prototype-contains-may-not-be-web-compatible

 [4]: http://exploringjs.com/es6/ch_strings.html#_checking-for-containment-and-repeating-strings
 [5]: https://github.com/tc39/Array.prototype.includes/