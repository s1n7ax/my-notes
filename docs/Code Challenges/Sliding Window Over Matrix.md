# Sliding Window Over Matrix

```java
public class Main {
    public static void main(String[] args) {
        int windowSize = 3;

        int[][] matrix = {
            { 1, 1, 0, 1, 0 },
            { 1, 1, 1, 1, 1 },
            { 0, 0, 1, 1, 1 },
            { 0, 0, 1, 1, 1 },
            { 1, 1, 0, 0, 0 }
        };

        // NOTE: the windowSize - 1 is needed to go to full length
        // otherwise the loop will stop one element before the end
        for (int i = 0; i < matrix.length - (windowSize - 1); i++) {
            for (int j = 0; j < matrix[i].length - (windowSize - 1); j++) {

                // we can make this a vector instead of matrix
                int[][] window = new int[windowSize][windowSize];
                int windowX = 0;
                int windowY = 0;

                for (int x = i; x < i + windowSize; x++) {
                    for (int y = j; y < j + windowSize; y++) {
                        window[windowX][windowY] = matrix[x][y];
                        windowY++;
                    }

                    windowY = 0;
                    windowX++;
                }

                // printing the window
                for (int x = 0; x < window.length; x++) {
                    for (int y = 0; y < window[x].length; y++) {
                        System.out.print(window[x][y] + " ");
                    }
                    System.out.println("");
                }
                System.out.println("");
            }
        }
    }
}
```
