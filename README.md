# Combux
Comparador y buscador de texto - case insensitive

### Ejemplos de uso:

```js
const Resultado = combux.contiene('drU', 'Esdrújula');
// Resultado: TRUE
```

```js
const Resultado = combux.esIgual('esdrUjula', 'Esdrújula');
// Resultado: TRUE
```


Ejemplo sin eliminar Diacríticos:
```js
/**
 * Compara dos textos, si se encuentra la Aguja en el Pajar retorna true, de lo contrario retorna false.
 * Si pEsIgual es 1: (esIgual) compara si Pajar es igual a Aguja.
 * Si pEsIgual es 0: (contiene) busca si Pajar contiene Aguja.
 * Si pSensible es 1: (case-sensitive) Si distingue entre mayúsculas y minúsculas.
 * Si pSensible es 0: (case-insensitive) No distingue entre mayúsculas y minúsculas.
 * @param {String} pAguja
 * @param {String} pPajar
 * @param {Number} pEsIgual Default 1
 * @param {Number} pSensible Default 0
 * @return {Boolean}
 */
let compararStrings = (pAguja, pPajar, pEsIgual, pSensible) => {
  if ("string" !== typeof pAguja || "string" !== typeof pPajar) {
    throw "Parámetros inválidos. La aguja y el pajar deben ser de tipo String.";
    return false;
  } else {
    let escapar = w => w.replace(/[-[\]{}()*+?.,\\^$|#\s]/g, "\\$&");

    let t = escapar(pAguja)
      .trim()
      .replace("  ", " ");
    let p = escapar(pPajar)
      .trim()
      .replace("  ", " ");
    let esSensible =
      "undefined" !== typeof pSensible && 1 === pSensible ? 1 : 0;
    let esIgual = "undefined" !== typeof pEsIgual && 0 === pEsIgual ? 0 : 1;

    if (0 === esSensible) {
      t = t.toLowerCase();
      p = p.toLowerCase();
    }

    return 1 === esIgual ? p === t : p.includes(t);
  }
};

console.log("Ejemplo de contiene: ", compararStrings(" we/\ *-+-- oP", " we/\ *-+-- opd ", 0));
console.log("Ejemplo de esIgual: ", compararStrings(" we/\ *-+-- oP", " we/\ *-+-- oP"));


```
