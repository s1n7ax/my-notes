# Reverse a Number

```java
public class Main {
    public static void main(String[] args) {
        int x = 12345;

        int reversed = 0;

        while (x != 0) {
            var lastDigit = x % 10;
            reversed = reversed * 10 + lastDigit;
            // getting rid of last digit is possible because java keeps the data
            // type as integer  without converting to it double ignoring the
            // fractional part of the decimal
            x = x / 10;
        }

        System.out.println(reversed);
        // 54321
    }
}
```
