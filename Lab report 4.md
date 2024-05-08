# Part 1

* A failure-inducing input
```
@Test
public void testReverseInPlace2() {
  int [] input1 = {1, 2, 3, 5, 6};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{6, 5, 3, 2, 1}, input1);
}
```
* An input that doesn't induce a failture
```
@Test 
public void testReverseInPlace() {
  int[] input1 = {1, 2, 3, 2, 1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1, 2, 3, 2, 1}, input1);
}
```
* The bug (before)
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
* After
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
* Explanation
The original buggy version fails to convert the second half of the values to the first half, because the first half already changed. This revision swaps both ends at the same time, and stops midpoint, so that no one would be missed out.

# Part 2

