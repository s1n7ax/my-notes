# Remove First & Last Digit From an Integer

## Remove the First Digit

```java
public class Main {
    public static void main(String[] args) {
        int x = 2351;

        int div;
        for (div = 1; x >= div * 10; div *= 10)
            ;

        System.out.println(x % div);
        // 351
    }
}
```

## Remove the Last Digit

```java
public class Main {
    public static void main(String[] args) {
        int x = 2351;

        System.out.println(x / 10);
        // 235
    }
}
```
