## Factory Method Design Pattern

**Intent:**

Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

**Also Known As:** Virtual Constructor

![Factory Method Structure](/Creational%20Patterns/Factory%20Method/Factory_Method.png)

**Applicability:**

*   Use the Factory Method when you don’t know beforehand the exact types and dependencies of the objects your code should work with.
*   Use the Factory Method when you want to provide users of your library or framework with a way to extend its internal components.
*   Use the Factory Method when you want to save system resources by reusing existing objects instead of rebuilding them each time.

**How to Implement:**

1.  Make all products follow the same interface. This interface should declare methods that make sense in every product.
2.  Add an empty factory method inside the creator class. The return type of the method should match the common product interface.
3.  In the creator’s code find all references to product constructors. One by one, replace them with calls to the factory method, while extracting the product creation code into the factory method.
4.  You might need to add a temporary parameter to the factory method to control the type of returned product.
5.  Now, create a set of creator subclasses for each type of product listed in the factory method. Override the factory method in the subclasses and extract the appropriate bits of construction code from the base method.

**Pros:**

*   You avoid tight coupling between the creator and the concrete products.
*   Single Responsibility Principle. You can move the product creation code into one place in the program, making the code easier to support.
*   Open/Closed Principle. You can introduce new types of products into the program without breaking existing client code.

**Cons:**

*   The code may become more complicated since you need to introduce a lot of new subclasses to implement the pattern. The best case scenario is when you’re introducing the pattern into an existing hierarchy of creator classes.

**Relations with Other Patterns:**

*   Many designs start by using Factory Method (less complicated and more customizable via subclasses) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, but more complicated).
*   Abstract Factory classes are often based on a set of Factory Methods, but you can also use Prototype to compose the methods on these classes.
*   You can use Factory Method along with Iterator to let collection subclasses return different types of iterators that are compatible with the collections.
*   Prototype isn’t based on inheritance, so it doesn’t have its drawbacks. On the other hand, Prototype requires a complicated initialization of the cloned object. Factory Method is based on inheritance but doesn’t require an initialization step.
*   Factory Method is a specialization of Template Method. At the same time, a Factory Method may serve as a step in a large Template Method.
*It also uses single responsibility principle and Open closed principle.

**Reference:** [Factory Method Design Pattern](https://refactoring.guru/design-patterns/factory-method)
