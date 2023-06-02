# docs-for-taglets

This is a document that explains the meaning of the taglets used by the fsc4j plugin, built by Bart Jacobs.
The plugin can be found [here](
https://github.com/btj/ogptaglets).

Some information in the document can be incomplete or incorrect, as it is based on the interpretation of the students.
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
#### method is deprecated
- This tag should be used when a method cannot be documented using any other `@basic` methods. It is used to indicate that a method is not complex and does not require additional documentation.

### `@creates`
- This tag should be used when a method creates a new object that is not a representation object or peer object of an existing object. It is used to indicate that the new object is completely independent of any existing objects and can be safely modified or inspected by the client.

### `@immutable`
- This tag should be used when a class or method is immutable and cannot be modified after construction. It is used to indicate that the state of the object will not change over time.

### `@invar`
- This tag should be used to indicate an invariant condition that must always be true for a class or method. It can be used both within the definition of a class or method and outside of it to provide public documentation.

### `@mutates`
- This tag should be used when a method modifies an existing object or a representation object of an existing object. It is used to indicate that the state of the object will change as a result of calling the method.

### `@inspects`
- This tag should be used when a method only reads the state of an object and does not modify it. It is used to indicate that the state of the object will not change as a result of calling the method.

### `@pre`
- This tag should be used to indicate a precondition that must be true before a method is called. It is used to indicate that the method may not behave correctly if the precondition is not met.

### `@post`
- This tag should be used to indicate a postcondition that must be true after a method is called. It is used to indicate what the method guarantees to do.

### `@representationObject`
- This tag should be used to indicate that a field is a representation object of an object. It is used to indicate that the field represents a part of the state of the object.

### `@representationObjects`
- This tag should be used to indicate that a field is a collection of representation objects of an object. It is used to indicate that the field represents a collection of parts of the state of the object.

### `@throws`
- This tag should be used to indicate an exception that may be thrown by a method. It is used to indicate what exceptions the method may throw.

### `@peerObject`
- This tag should be used to indicate that a field is a peer object of an object. It is used to indicate that the field represents an object that is not part of the state of the object, but is related to it in some way.

### `@peerObjects`
- This tag should be used to indicate that a field is a collection of peer objects of an object. It is used to indicate that the field represents a collection of objects that are not part of the state of the object, but are related to it in some way.

### `@mutates-properties`
- This tag should be used to indicate that a method modifies the properties of an object. It is used to indicate that the state of the object will change as a result of calling the method.

### `@may-throw`
- This tag should be used to indicate that a method may throw an exception. It is used to indicate that the method may not behave correctly in some cases.


# Authors
- [Wannes Tas](https://github.com/wannestas)

# Contributors
- [Tibo Stans](https://github.com/TIboStans
