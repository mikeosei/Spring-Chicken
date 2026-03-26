## Why is tightly coupled code bad?

```
public class FruitCatapult() {
Apple apple = new Apple();

public String throw() {
return "throw" + apple.getName();
}

```
1. Rippling Affect: When a class imports another class, that imported class becomes a dependency. Apple is a dependency. A change to the Apple class would require a change to the FruitCatapult's instantiation of Apple(Example: Spelling change).Or maybe the signiture of getName() changes. Not only does this break FruitCatapult but any other classes calling it, rippiling the effect. Or maybe the product team suddenly springs on you that they want the catapult to work with different fruit.  The current implentation's logic is tightly coupled to Apple. The dependency's coupling does not allow for easy/potential redesigns/tailoring of our usage of that dependency.
```
public class FruitCatapult() {
Orange orange = new Orange();

public String throw() {
return "throw" + orange.getName();
}
```

2. Testing difficulty, tight coupling of Apple to FruitCatapult makes it hard to test FruitCatapult in isolation. What if Apple method creation creates the multiple threads or unnecessary db calls. Directly intantiating the Apple outside of the construct makes testing only FruitCatapult difficult.


Does  using a constructor fix rippling effect and testing difficulty

Yes and No
Using a constructor makes testing easier because now a stub can be passed into the FruitCatapult during unit testing
```
public class FruitCatapult() {
  private Apple apple;
  public FruitCatapult(Apple apple) {
    this.apple = apple;

}

public String throw() {
return "throw" + apple.getName();
}
```
```
class FakeApple implements APple {
    public String getName() {
        return "apple";
    }
}

@Test
void testFruitCatapult() {
    FakeApple fake = new FakeApple();
    FruitCatapult fruitCatapult = new FruitCatapult(fake);

    assertEquals("apple", fruitCatapult.getName());
}
```

So what’s the problem?

This approach doesn’t scale well:

You have to manually create fake classes for everything
If your controller has 4 dependencies → you stub all 4
If dependencies have dependencies → it snowballs fast

Apple is still tightly coupled to FruitCatapult even though we are using constructor

3. 


4. 
5.  
This is an example of tightly coupled code


## Why do we use interfaces
