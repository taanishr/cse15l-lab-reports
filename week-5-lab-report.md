# Part 1

## Failure-inducing input
```
public void testReverseInPlace() {
  int[] input2 =  { 1, 2, 3};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{ 3, 2, 1 }, input2);
}
```

## Input which does not induce a failure
```
public void testReverseInPlace() {
  int[] input1 =  { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```

## Symptom
![Symptom when both tests are ran](/w5-s.png)

## Bug
### Before
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}
```

### After
```
static void reverseInPlace(int[] arr) {
    int temp[] = new int[arr.length];
    System.arraycopy(arr, 0, temp, 0, arr.length);
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = temp[arr.length - i - 1];
    }
}
```

reverseInPlace initially accessed the original array instead of making a copy. This meant that the array would become a mirror image of the elements in the second half of the array. By making a copy and accessing that copy instead, the method theny properly swapped the beginning and end elements.


