> **Author's note, please read if incorporating TypedJSON into a serious application:**
>
> TypedJSON is currently an experimental release and is not guaranteed to satisfy all use-cases reliably. Minor version updates may introduce breaking changes before `v1.0.0` as the concept is fleshed out and the dozens of native issues are either worked around or accepted and documented as limitations (with the primary issue being the very primitive and limited reflection support in TypeScript).
> 
> The upcoming planned minor update to v0.2.0 is a complete rehaul of the TypedJSON API with significant improvements over the initial release, based on significant amounts of feedback and practical use. Since numerous unnecessary features and decisions will be abandoned, **this update will introduce breaking changes**, of which the most notable will be:
> - TypedJSON will require instantiation with a root type-constructor specified
> - JsonMember and JsonObject settings will be altered significantly (especially for `Array`)
> - Configurable type-hint key replaced with configurable type-resolver and type-emitter callbacks (although with an identical default behavior)
> 
> This update is live as soon as all unit and integration testing is done in the host project (TypedJSON is being developed as a part of an enterprise project), anticipated in January, 2017. The main principle of TypedJSON is not subject to change, the API is permanently locked to a decorator-based approach.
>
> Notable non-breaking changes in this update will be:
> - Native support for ES6 `Set` and ES6 `Map`
> - Native support for all typed arrays (such as `Float32Array`) and `ArrayBuffer`
> - Meaningful error messages and configurable error handler callback

# TypedJSON

Strong-typed JSON parsing and serializing for TypeScript with [decorators](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Decorators.md). Parse JSON into actual class instances. Recommended (but not required) to be used with [ReflectDecorators](https://github.com/rbuckton/ReflectDecorators), a prototype for an ES7 Reflection API for Decorator Metadata.

 - Parse regular JSON to typed class instances, safely
 - Seamlessly integrate into existing code with [decorators](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Decorators.md), ultra-lightweight syntax

## Install & Use

```none
npm install typedjson-npm
typings install npm:typedjson-npm
```

 1. Snap the [@JsonObject decorator](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference#jsonobject) on a class
 2. Snap the [@JsonMember decorator](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference#jsonmember) on properties which should be serialized and deserialized
 3. Parse and stringify with the [TypedJSON class](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference#typedjson)

```typescript
@JsonObject
class Person {
    @JsonMember
    firstName: string;

    @JsonMember
    lastName: string;

    public getFullname() {
        return this.firstName + " " + this.lastName;
    }
}
```

```typescript
var person = TypedJSON.parse('{ "firstName": "John", "lastName": "Doe" }', Person);

person instanceof Person; // true
person.getFullname(); // "John Doe"
```

If you choose to omit using [ReflectDecorators](https://github.com/rbuckton/ReflectDecorators), the class (constructor function) of each [@JsonMember](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference#jsonmember) decorated property must be specified manually through the [`type` setting](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference#jsonmember), for example:

```typescript
@JsonMember({ type: String })
firstName: string;
```

[Learn more about decorators in TypeScript](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Decorators.md)

## Documentation

 - [API reference](https://github.com/JohnWhiteTB/TypedJSON/wiki/API-reference)

## License

TypedJSON is licensed under the MIT License.
