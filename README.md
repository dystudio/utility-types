# React / Redux / TypeScript Utils
> Utility belt for React + Redux + TypeScript Projects
- Semantic Versioning
- No external dependencies
- Output separate bundles for your specific workflow needs:
  - ES5 + CommonJS - `main`
  - ES5 + ES-Modules - `module` 
  - ES2015 + CommonJS - `jsnext:main`

# Table of Contents (v3.0)

## TS Redux Actions
> For advanced docs check here: https://github.com/piotrwitek/ts-redux-actions
- [createAction](#createaction)

## Mapped Types
- [Diff](#diff)
- [Omit](#omit)
- [Overwrite](#overwrite)

## Type Utils
- [getReturnOfExpression](#getreturnofexpression)

---

Archived docs:
- [Docs v2.X](#READMEv2.0.md)

---

## TS Redux Actions

### createAction

```ts
createAction(typeString, creatorFunction?)
typeString: TS extends string,
creatorFunction: (...args: any[]) => { type: TS, payload?: P, meta?: M, error?: boolean }
return: (
  (...args: any[]) => { type: TS, payload?: P, meta?: M, error?: boolean }
) & { readonly type: TS }
```

---

## Mapped Types


### Diff
```ts
// TestDiff expects: ('a' | 'b')
type TestDiff =
  Diff<'a' | 'b' | 'c', 'c' | 'd'>;
```

### Omit
```ts
// TestOmit expects: { b: number, c: boolean }
type TestOmit =
  Omit<{ a: string, b: number, c: boolean }, 'a'>;
```

### Overwrite
```ts
// TestOverwrite expects: { b: number, c: boolean } & { a: number }
type TestOverwrite =
  Overwrite<{ a: string, b: number, c: boolean }, { a: number }>;
```

---

## Type Utils

### getReturnOfExpression
> Get return value of an "expression" with inferred return type  
> alias: returntypeof  
https://github.com/Microsoft/TypeScript/issues/6606

```ts
// this polyfill exist because TypeScript does not support getting type of expression 
// (tracking issue: https://github.com/Microsoft/TypeScript/issues/6606)
function getReturnOfExpression<T>(
  expression: (...params: any[]) => T,
): T;

// Example:
import { getReturnOfExpression } from 'react-redux-typescript';

const increment = () => ({ type: 'INCREMENT' as 'INCREMENT' });

const returnOfIncrement = getReturnOfExpression(increment);
type INCREMENT = typeof returnOfIncrement; // { type: "INCREMENT"; }
```

---
MIT License

Copyright (c) 2016 Piotr Witek <piotrek.witek@gmail.com> (http://piotrwitek.github.io)
