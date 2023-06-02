# docs-for-taglets

This is a document that tries to act as a reference sheet for the taglets used by the fsc4j plugin, built by Bart Jacobs.
The plugin can be found [here](https://github.com/btj/ogptaglets).

Some information in the document can be incomplete or incorrect, as it is based on the interpretation of the students. The course notes, available [here](https://btj.github.io/ogp-notes/), are definitely worth a read as they're very clear and thorough most of the time. This page should be used *in addition*, as a sort of reference sheet, and is ***not*** a substitute for the actual course materials.
If you find any mistakes, please make a pull request, we would be very grateful.

## Table of Contents
- [docs-for-taglets](#docs-for-taglets)
  * [`@basic`](#basic)
  * [`@creates`](#creates)
  * [`@immutable`](#immutable)
  * [`@invar`](#invar)
  * [`@mutates`](#mutates)
  * [`@inspects`](#inspects)
  * [`@pre`](#pre)
  * [`@post`](#post)
  * [`@representationObject`](#representationobject)
  * [`@representationObject(s)`](#representationobjects)
  * [`@throws`](#throws)
  * [`@peerObject`](#peerobject)
  * [`@peerobjects`](#peerobjects)
  * [`@mutates_properties`](#mutates-properties)
  * [`@may_throw`](#may-throw)


## Taglets

### `@basic`
#### this tag is deprecated
- This tag should be used when a method cannot be documented using other `@basic` methods. It is used to indicate that a method is one of the basic building blocks of a class. Commonly this is used for getters, but this is by no means a requirement. 

### `@creates`
- This tag should be used when a method creates a new object that is not a representation object or peer object of an existing object. It is used to indicate that the new object is completely independent of any existing objects and can be safely modified or inspected by the client.

### `@immutable`
- This tag should be used when a class or method is immutable and cannot be modified after construction. It is used to indicate that the state of the object will not change over time. For a method specifically this means that the result of that method will always be exactly the same over the lifetime of the instance this method is called upon.

### `@invar`
- This tag should be used to indicate an invariant condition that must always be true for a class. It can be used both within the definition of a class and outside of it to provide, respectively, private and public documentation.

### `@mutates`
- This tag should be used when a method modifies an existing object or a representation object of an existing object. It is used to indicate that the state of the object will change as a result of calling the method.

### `@inspects`
- This tag should be used when a method only reads the state of an object and does not modify it. It is used to indicate that the state of the object will not change as a result of calling the method. This is always allowed, but only **necessary** if the object in question is mutable, to indicate that it will not be mutated.

### `@pre`
- This tag should be used to indicate a precondition that must be true before a method is called. It is used to indicate that, should the condition not be met, it can not guarantee the result. This is less specific than `@throws` since it only states that if the condition is not met, no guarantees about what will happen can be made. Meanwhile `@throws` states it *will* throw an error if the condition is not met.

### `@post`
- This tag should be used to indicate a postcondition that must be true after a method is called correctly. It is used to indicate what the method guarantees to do, given that its pre-conditions were met.

### `@representationObject`
- This tag should be used to indicate that a field is a representation object of an object. It is used to indicate that the field represents a part of the state of the object. Generally I like to think of representation objects as "if a malicious third party was given this object, it could create an illegal state of the object it is a representation object of". For example a `Fibonacci` class that stores an ArrayList of the Fibonacci numbers in sequence that it has calculated so far. If an external object ever got hold of this exact ArrayList, it could add and remove objects at will, meaning the `Fibonacci` class would no longer contain a list of Fibonacci numbers in sequence.

### `@representationObjects`
- This tag should be used to indicate that a field is a collection of representation objects of an object. It is used to indicate that the field represents a collection of parts of the state of the object. Keep in mind that this collection of RepresentationObjects may in turn be a representation object itsself.

### `@throws`
- This tag should be used to indicate an exception that may be thrown by a method. It is used to indicate what exceptions the method may throw, and under what condition it will be thrown.

### `@peerObject`
- This tag should be used to indicate that a field is a peer object of an object. It is used to indicate that the field represents an object that is not part of the state of the object, but is part of its peer group.

### `@peerObjects`
- This tag should be used to indicate that a field is a collection of peer objects of an object. It is used to indicate that the field represents a collection of objects that are not part of the state of the object, but are related to it in some way.

### `@mutates-properties`
- This tag should be used to indicate that a method modifies the properties of an object. It is used to indicate that the state of the object will change as a result of calling the method. A difference with plain `@mutates` is that you specify which methods of the mutated object will return a different result instead of just stating that "something" will be different.

### `@may-throw`
- This tag should be used to indicate that a method may throw an exception, but is not guaranteed to. I honestly couldn't find any information on this tag other than it being used in an example a couple of times.

# Authors
- [Wannes Tas](https://github.com/wannestas)

# Contributors
- [Tibo Stans](https://github.com/TIboStans)
