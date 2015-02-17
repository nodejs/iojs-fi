# ES6 ja io.js

io.js nojaa tuoreisiin [V8](https://code.google.com/p/v8/):n versioihin. Pysymällä ajan tasalla viimeisimpien versioiden kanssa varmistetaan sekä uusimpien [JavaScript ECMA-262 specification](http://www.ecma-international.org/publications/standards/Ecma-262.htm) ominaisuuksien, että suorituskykyyn ja vakauteen liittyvät parannukset nopea saapuminen kehittäjien ulottuville.

io.js:n versio 1.2.0 sisältää V8 version 4.1.0.14, mikä ES6:n osalta ylittää tuntuvasti version 3.28.72 mikä sisältyy Node.js™ 0.12.x-versioihin.

## Ei enää --harmony lippua

Node.js™@0.12.x (V8 3.28+) ajonaikainen `--harmony`-lippu aktivoi kaikki **valmiit**, **koekäytössä olevat** ja **vasta kehityksessä olevat** ES6-ominaisuudet (poikkeuksena `proxies`, joille on oma `--harmony-proxies`-lippunsa). Toisin sanoen jotkin bugiset tai jopa rikkinäiset ominaisuudet kuten [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) on yhtä lailla käytettävissä kuin [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*), millä on vähän tai ei yhtään tunnettuja ongelmia. Usein kehittäjät ottavat käyttöön vain tiettyjä ominaisuuksia käyttämällä täsmällisiä ajonaikaisia ominaisuuslippuja (esim. `--harmony-generators`), tai yksinkertaisesti ottavat kaiken käyttöön ja pitäytyvät käytössään rajatussa osassa.

io.js@1.8 (V8 4.1+) myötä nuo hankaluudet poistuvat. Kaikki harmonyn ominaisuudet on nyt loogisesti jaoteltu kolmeen ryhmään **valmiisiin**, **koekäytössä oleviin** ja **vasta kehityksessä oleviin**:

* Kaikki **valmiit** ominaisuudet, eli ne jotka V8 määrittelee vakaiksi (_stable_), kuten [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*, [templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings, [new string methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla#Additions_to_the_String_object) ja moni muu on **oletuksena käytössä io.js:ssä**, eikä siis vaadi minkäänlaisia ajonaikaisia lippuja
* **Koekäytössä olevat** ominaisuudet ovat lähes valmiita ominaisuuksia mitä ei vielä olev täysin testattuja tai päivitetty vastaamaan uusinta määrittelyä, eikä siksi määritellä V8-tiimin osalta vakaiksi (_stable_) (esim. voi olla olemassa joitain vielä tuntemattomia rajatapauksia). Tähän tilaan kuuluu luultavasti [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*) versiossa 3.26. Nämä ovat "käytä omalla vastuullasi" tyyppisiä ominaisuuksia, mitkä nyt vaativat käyttöönottoa varten ajonaikaisen lipun: `--es_staging` (tai sen synonyymin `--harmony`).
* **Kehityksessä olevat** ominaisuudet on otettavissa käyttöön yksitellen kunkin omalla lipullaan (esim. `--harmony_arrow_functions`), joskin tämä ei ole suositeltavaa muuhun kuin koemielessä.

## Mitkä ES6 ominaisuudet ovat io.js:ssä oletuksena käytössä (ilman ajonaikaisia lippuja)?

*   Block scoping

    *   [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

    *   [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

    *   `function`-in-blocks

    >As of v8 3.31.74.1, block-scoped declarations are [intentionally implemented with a non-compliant limitation to strict mode code](https://groups.google.com/forum/#!topic/v8-users/3UXNCkAU8Es). Developers should be aware that this will change as v8 continues towards ES6 specification compliance.

*   Collections

    *   [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

    *   [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

    *   [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

    *   [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)

*   [Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)

*   [Binary and Octal literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Numeric_literals)

*   [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

*   [New String methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla#Additions_to_the_String_object)

*   [Symbols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

*   [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)

Yksityiskohtaisempi lista, mihin sisältyy myös vertailu muihin ajoympäristöihin, löytyy [compat-table](https://kangax.github.io/compat-table/es6/)-projektin sivulta.

## Mitä ES6 ominaisuudet ovat --es_staging lipun takana?

*   [Classes](https://github.com/lukehoban/es6features#classes) (strict mode only, behind flag `--harmony_classes` which implies block scoping & object literal extensions)

*   [Object literal extensions](https://github.com/lukehoban/es6features#enhanced-object-literals) (behind flag `--harmony_object_literals`)

*   [`Symbol.toStringTag`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (user-definable results for `Object.prototype.toString`, behind flag `--harmony_tostring`)