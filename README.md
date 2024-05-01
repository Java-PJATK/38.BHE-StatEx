# BHE-StatEx
38 BHE-StatEx/StatExample.java 69  

Cont. from [36.37.BGR-BasicClass](https://github.com/Java-PJATK/36.37.BGR-BasicClass)

## 8.5 Static members  

Any class can also declare static members — both fields (data) and methods (but not static constructors!) We can imagine a static members as belonging the class as a whole, not to objects. As such, they can be used even if we haven’t created any object of our class — they are brought into existence and initialized when the class is loaded by the JVM (if the class happens to be an enum, after all the enum values have been created).

Inside a static function there is no this, which normally exists and is the reference to the object the function was invoked on — static functions are not invoked on any object and consequently cannot use this. From the outside of a class, we refer to its static members using just the name of the class. We can, although it’s very confusing, use reference to any object of this class for the same purpose. For example, in the last line of

```java
public class AnyClass {
public static int stat;
// ...
}
// somewhere else
AnyClass.stat = 7;
AnyClass a = new AnyClass();
// ...
a.stat = 28;
```

we refer to static member stat just by putting a before the dot, but the compiler will use only the information about the type of a — which particular object of class AnyClass is used in this context is completely irrelevant. Looking at this line alone, one is not able to tell whether stat is a static or non-static member of the class; for this reason it is recommended to always use the first syntax, with the name of a class, as here, it is obvious that stat must be static.  

In the following example:  

## Listing 38 BHE-StatEx/StatExample.java

```java
public class StatExample {
    private static double rate =  1;
    private static char     ID = 'A';

    private double amount;
    private char       id;

    public static   void setRate(double r) { rate = r; }
    public static double getRate() { return rate; }

    StatExample(double a) {
        id = ID++;
        amount = a;
    }

    @Override
    public String toString() {
        return "I'm " + id + ", I have $" + amount +
            " = " + rate*amount + " PLN";
    }

    public static void main (String[] args) {
       StatExample.setRate(4.1);
       StatExample sa = new StatExample(10);
       StatExample sb = new StatExample(16);
       StatExample sc = new StatExample(20);
       System.out.println(sc + "\n" + sb + "\n" + sa);
    }
}
```
`ID` is a static member whose value is assigned in the constructor to non-static field `id` and then incremented by one; in this way each object will get its unique `id`.

Also rate is static, as it represents a rate which is common for all objects and used by them to convert one currency into another.  

Consequently, function `setRate` is static, because it only affects rate and does not even need any object of the class to exist; as we can see, it is invoked before creating any objects. 

The program prints  

```
I'm C, I have $20.0 = 82.0 PLN
I'm B, I have $16.0 = 65.6 PLN
I'm A, I have $10.0 = 41.0 PLN
```

Next: [39.AFL-FunRecur](https://github.com/Java-PJATK/39.AFL-FunRecur)


