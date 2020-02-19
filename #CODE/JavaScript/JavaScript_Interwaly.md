# JavaScript - Interwały

## setTimeout()

`setTimeout(fn, time)` - przyjmuje dwa parametry:

- funkcję, która ma zostać wywołana z opóźnieniem
- czas w milisekundach po jakim zostanie wywołana funkcja

```javascript
function myFunc() {
  console.log("Jakiś tekst");
}

setTimeout(myFunc, 1200); // Zostanie wywołana po 1.2 s
```

`clearTimeout()` - przerywa wcześniej zainicjowany `setTimeout`. Wymaga referencji do timeoutu, który chcemy przerwać.

## setInterval()

`setInterval(fn, time)` - przyjmuje dwa parametry:

- funkcję, która ma zostać wywołana
- czas w milisekundach co jaki ma zostać wywołana funkcja

```javascript
const time = setInterval(function() {
  console.log("Przykładowy napis");
}, 1000);
```

`clearInterval()` - przerywa wcześniej zainicjowany `setInterval`. Wymaga referencji do interwału, który chcemy przerwać.

## Technika throttle

```javascript
function throttled(delay, fn) {
  let lastCall = 0;
  return function(...args) {
    const now = new Date().getTime();
    if (now - lastCall < delay) {
      return;
    }
    lastCall = now;
    return fn(...args);
  };
}
```

```javascript
const tHandler = throttled(200, printKey);
const input = document.querySelector("input");
input.addEventListener("input", tHandler);
```

## Technika debounce

**debounce** - technika, która pozwala na "zgrupowanie" wielu występujących jeden po drugim wywołań tej samej funkcji w jedno wywołanie.

```javascript
function debounced(delay, fn) {
  let timerId;
  return function(...args) {
    if (timerId) {
      clearTimeout(timerId);
    }
    timerId = setTimeout(() => {
      fn(...args);
      timerId = null;
    }, delay);
  };
}
```

```javascript
const tHandler = debounced(200, printKey);
const input = document.querySelector("input");
input.addEventListener("input", tHandler);
```
