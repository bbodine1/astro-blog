---
title: Function Overloads in Typescript
description: This is an example of Function Overloading in Typescript
pubDate: '2023-11-13T18:44:29-06:00'
heroImage: /assets/typescript.png
---
## Typescript

```typescript
// Function Overloading w/ Typescript

/**
 * Represents a coordinate with x and y values.
 */
interface Coordinate {
  x: number;
  y: number;
}

/**
 * Parses the given arguments and returns a Coordinate object.
 * @param obj - An object with x and y properties.
 * @returns A Coordinate object.
 * @param x - The x value of the coordinate.
 * @param y - The y value of the coordinate.
 * @returns A Coordinate object.
 * @param str - A string in the format "x:<number>,y:<number>".
 * @returns A Coordinate object.
 */
function parseCoordinate(obj: Coordinate): Coordinate;
function parseCoordinate(x: number, y: number): Coordinate;
function parseCoordinate(str: string): Coordinate;
function parseCoordinate(arg1: unknown, arg2?: unknown): Coordinate {
  let coord: Coordinate = {
    x: 0,
    y: 0,
  };

  if (typeof arg1 === "string") {
    (arg1 as string).split(",").forEach((str) => {
      const [key, value] = str.split(":");
      coord[key as "x" | "y"] = parseInt(value, 10);
    });
  } else if (typeof arg1 === "object") {
    coord = {
      ...(arg1 as Coordinate),
    };
  } else {
    coord = {
      x: arg1 as number,
      y: arg2 as number,
    };
  }

  return coord;
}

console.log(parseCoordinate({ x: 52, y: 35 }));
console.log(parseCoordinate(10, 20));
console.log(parseCoordinate("x:12,y:22"));
```

---

## Compiled Javascript

```javascript
"use strict";
// Function Overloading w/ Typescript
function parseCoordinate(arg1, arg2) {
    let coord = {
        x: 0,
        y: 0,
    };
    if (typeof arg1 === "string") {
        arg1.split(",").forEach((str) => {
            const [key, value] = str.split(":");
            coord[key] = parseInt(value, 10);
        });
    }
    else if (typeof arg1 === "object") {
        coord = Object.assign({}, arg1);
    }
    else {
        coord = {
            x: arg1,
            y: arg2,
        };
    }
    return coord;
}
console.log(parseCoordinate({ x: 52, y: 35 }));
console.log(parseCoordinate(10, 20));
console.log(parseCoordinate("x:12,y:22"));
```

Explore this code in the [TS Playground](https://www.typescriptlang.org/play?pretty=true&ssl=51&ssc=43&pln=1&pc=1#code/PTAEDEFcDsGMBcCWB7aoDyA3ApgJwDbICGAJotAOagDuYAKgJ4AO2AzrLok-AFA-AAqAT1ADQAJWxNcbbNHitQRULGTJcZaEXjYaieAAtQADyXQSoBqExF8kNgDoRA4D3I7cAMyKxdAYTUNcm1dAG8REwAuUGhIAFsAIzwAbgiGaNjElJ4AXz5BYVFQAAUiXFY2UENdCkQcNDKKeLkFMwsZeEhcaEVlAPVNENBkBIArbAQnIoABJjKiOOGx0ABaUABBNBHxhD1DEzbLUGlkFlwkR2dQaY6uno3QfqCtHSWd+CmxWfnF0zW6Ay6Uw2Oy6ZCeKqAlSBQY6T7XOa4BZHf5Qqwg+zDCHVaEDYJwq43bCdbqKdaPGH4sFjCYfQmI5GseC4VYPJmcSigciQ3SedRxbSgABExkiAB5MklcAA+AA06Ql8Sl0qF8KJJPu5KesOp70+rk8MAQKDQiIq2qpAApttELS9sABKW2U+2pQ1wJCoY5lc0ukKW0UxJV4WWWDLB3BOil4108d3Gr1m7B2-3s6Ls8gUKMpnRuo2e00+5N+nSWxoARmiMAA1tBkNRoKHGgAmAD8Vegtfr0GzJbCEXwxNxGmdMaGAF5QOFQDOoqAAAyyiIz9ILpcznKpCKICGW+DMbDgpS4Cjl0Dji-CjOUIUOqfL0Blk9noiKa9ZhysJj4fSWoWy28HD5XAAFEfAMS1LXZO9x2le9Z1nVQengUAAG1q2wBhQwxbAAF1z1AdlP2-X8hUiW9UgQmdVAGdDMKURQRSFUAAB9hQYIV8MnJMAEl5EtHDQ3LecHUo2cclEiIclAbB8AqLld33Fgjwrc9LyFbZaVveDEJhAjpyohwjKfU8GOjZ4QgdddxLE6TZPkgzqL0ydHNnQNVNfIMslwayENXFszMlEMH03KS+BnW5umHEhUjyHgkNYZBBwcQgKEtJMc2wS1QjnABWZtQ1XABmXLQAkySEqS7AUuQNKMr7S1hNDZsRIq1BEuS1L0qLTK-1FcsCvSZtm1vSSgA) 
