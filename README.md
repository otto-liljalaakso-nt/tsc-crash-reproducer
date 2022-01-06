## TypeScript crash reproducer

Reproducer repository for [TypeScript/issues/47299][issue].

[issue]: https://github.com/microsoft/TypeScript/issues/47299

### Usage

#### Preparation

1. Clone the repository
2. Install dependencies: `$ yarn`

#### Visual Studio Code problem
1. Open the repository in Visual Studio Code
2. Open file `ui/src/index.tsx`

##### Expected result
No errors, IntelliSense and so on work.

##### Actual result
First high cpu and memory usage,
then the following error pops up in Visual Studio Code:

```
The TypeScript language service died 5 times right after it got started.
The service will not be restarted.
```

#### Compilation problem

1. Compile the repository: `$ yarn tsc --build`

##### Expected result
No errors

##### Actual result
The following error appears:

```
/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:47148
            if (type.flags & 524288) {
                     ^

TypeError: Cannot read property 'flags' of undefined
    at getPropertyOfObjectType (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:47148:22)
    at getPropertyOfType (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:47710:24)
    at resolveESModuleSymbol (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:40904:54)
    at getTargetOfNamespaceImport (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:40191:28)
    at getTargetOfAliasDeclaration (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:40405:28)
    at resolveAlias (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:40446:30)
    at getSymbol (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:39225:38)
    at resolveNameHelper (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:39464:34)
    at resolveName (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:39448:20)
    at resolveEntityName (/home/otto/src/external/otto-urpelainen-nt/tsc-crash-reproducer/node_modules/typescript/lib/tsc.js:40573:42)
```

### Workaround

Both errors disappear if, in `ui/src/index.tsx`,
the imports are replaced with commented-off alternative.
