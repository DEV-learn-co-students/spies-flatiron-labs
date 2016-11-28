# Spies!
Test spies are useful to us in many ways. In this lesson, we'll discuss test spies before we dive into using them in the following lesson.

<image alt="secret-agent-mascot" src="http://i.giphy.com/ID9UXdNsqsE5G.gif"/>

## Objectives

1. Understand what test spies are
2. Understand the usages of test spies

## What are test spies & what are they used for?
In short, test spies are stand-ins or doubles for objects and functions that are used in our real code. Stunt doubles stand in for the real actor/actress and similarly, test spies allow us to stand in for certain functionality in our code. For instance, these functionalities that we may not want to actually run during our tests include HTTP requests or calls to a data source. Instead we can use spies to mock behavior or prevent the actual function from running.

Additionally, spies can be used to get more information about the usage of the function during the test. It can answer questions like "Was this function called?", "How many times was it called?", and "What arguments was this function called with?".

## Usages of Spies
Depending on the test spy library you use such as [Sinon.js](http://sinon.js.org/) or [Jasmine Spies](https://jasmine.github.io/2.0/introduction.html#section-Spies), your API will be different, but the spies will accomplish the same thing.

Here are some examples using Jasmine Spies:

#### Spying on an object's function
```js
const mathStuff = {
  add(x, y) {
    return x + y;
  }
}

spyOn(mathStuff, 'add'); // Spy on the object behavior

mathStuff.add(1, 2); // Call object behavior

// Assertion check
expect(mathStuff.add).toHaveBeenCalled();
expect(mathStuff.add).toHaveBeenCalledWith(1, 2);
```

#### Spying on a generic function
You don't always have a defined function to spy on i.e. asserting that a callback function is called. In those cases, you can create a generic spy:
```js
const spy = jasmine.createSpy('mySpy');

spy('hello', 'world')
expect(spy).toHaveBeenCalled();
expect(spy).toHaveBeenCalledWith('hello', 'world');
```

#### Gotchas
An important note with _Jasmine Spies_ is that **any function that spied on will be stubbed out**, meaning that the actual function will not run. If you want the function to actually run, you will need to change your `spyOn` call to the following:
```js
spyOn(mathStuff, 'add').and.callThrough();
```

## Resources
* [Jasmine Spies Doc](https://jasmine.github.io/2.0/introduction.html#section-Spies)
* [Using Jasmine Spies Blog](http://www.htmlgoodies.com/html5/javascript/spy-on-javascript-methods-using-the-jasmine-testing-framework.html#fbid=wM28pmxuAAG)
* [Sinon.js](http://sinonjs.org/)
* [Best Practices of using Sinon](https://semaphoreci.com/community/tutorials/best-practices-for-spies-stubs-and-mocks-in-sinon-js)
