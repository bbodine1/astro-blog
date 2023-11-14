---
title: Function Overloads in Typescript
description: This is an example of Function Overloading in Typescript
pubDate: '2023-11-13T18:44:29-06:00'
heroImage: /assets/blog-placeholder-2.jpg
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
