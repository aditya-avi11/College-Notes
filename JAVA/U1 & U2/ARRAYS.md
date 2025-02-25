
# 1-D Array : 

```java
import java.lang.reflect.Array;;
public class Arr {
    public static void main(String[] args) {
    // Single dimenion array :
    int[] intArray = (int[]) Array.newInstance(int.class,5);
    //Mult-dimensional array :
    int[][] multiArray = (int[][]) Array.newInstance(int.class, 3,5);
    }
}
```


# Jagged Arrays :

```Java
int arr[][] = new int[][] {
	new int[] {1,2,3,4},
	new int[] {4,5},
	new int[] {1},
};
```

```Java
int arr[][] = { {1,2,3,4,5}, {1,2}, {1}};
```



## Write the difference between Mult-Dimensional arrays and Jagged Arrays :

| Mult-Dimensional Array                                                | Jagged Array                                                                 |
| --------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| In Mult-Dimensional Arrays columns have to be same same for each row. | In this column numbers need not be same.                                     |
| There is wastage of space.                                            | It saves space by reserving memory for elements which actually occupy space. |
