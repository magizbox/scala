# Basic Syntax

## Print print

```
> println("Hello, Scala!");

Hello, Scala!
```

## Conditional 

`if` Statement

`if` statement consists of a Boolean expression followed by one or more statements.

```scala
var x = 10;
if( x < 20 ){
 println("This is if statement");
}
```

`if-else` Statement

```scala
var x = 30
if( x < 20 ){
  println("This is if statement");
} else {
  println("This is else statement");
}
```

`if-else if-else` Statement

```scala
 var x = 30;
if( x == 10 ){
 println("Value of X is 10");
} else if( x == 20 ){
 println("Value of X is 20");
} else if( x == 30 ){
 println("Value of X is 30");
} else{
 println("This is else statement");
}
```



## Coding Convention [^1]

### Keep It Simple

### Don't pack two much in one expression

```scala
/*
 * It's amazing what you can get done in a single statement
 * But that does not mean you have to do it.
 */
jp.getRawClasspath.filter(
  _.getEntryKind == IClasspathEntry.CPE_SOURCE).
  iterator.flatMap(entry =>
    flatten(ResourcesPlugin.getWorkspace.
      getRoot.findMember(entry.getPath)))
```

#### Refactor

* There's a lot of value in meaningfull names.
* Easy to add them using inline vals and defs

```scala
val sources = jp.getRawClasspath.filter(
  _.getEntryKind == IClasspathEntry.CPE_SOURCE)
def workspaceRoot =
  ResourcesPlugin.getWorkspace.getRoot
def filesOfEntry(entry: Set[File]) =
  flatten(worspaceRoot.findMember(entry.getPath)
sources.iterator flatMap filesOfEntry
```

### Prefer Functional

By default

- use vals, not vars
- use recursions or combinators, not loops
- use immutable collections
- concentrate on transformations, not CRUD

When to deviate from the default
- sometimes, mutable gives better performance.
- sometimes (but not that often!) it adds convenience

### But don't diablolize local state

Why does mutable state lead to complexity?

It interacts with different program parts in ways that are hard to track.

=> Local state is less harmful than global state.

### "Var" Shortcuts

```scala
var interfaces = parseClassHeader()...
if (isAnnotation) interfaces += ClassFileAnnotation
```

**Refactor**

```scala
val parsedIfaces = parseClassHeader()
val interfaces =
  if (isAnnotation) parsedIfaces + ClassFileAnnotation
  else parsedIfaces
```

[^1]: [Martin Odersky - Scala with Style](https://www.youtube.com/watch?v=kkTFx3-duc8)
