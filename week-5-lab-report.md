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

# Part 2
## Command: `grep`
### Command-line option 1: Capturing surrounding content of match with `-C`
Example 1: 
```
treja@Taanishs-MacBook-Air technical % grep -C2 Coronary plos/*.txt
plos/pmed.0020098.txt-        Patients at risk for atherosclerotic cardiovascular disease are identifiable only up to
plos/pmed.0020098.txt-        a point using traditional methods, including the Framingham risk score [1], the European
plos/pmed.0020098.txt:        SCORE (Systemic Coronary Risk Evaluation) [2], and the C-reactive protein level [3]. These
plos/pmed.0020098.txt-        are particularly effective for people in the highest risk groups, but they have serious
plos/pmed.0020098.txt-        flaws. They do not take family history of premature coronary artery disease into account;
--
plos/pmed.0020123.txt-      
plos/pmed.0020123.txt-        Introduction
plos/pmed.0020123.txt:        Coronary heart disease (CHD) remains the leading cause of morbidity and mortality in the
plos/pmed.0020123.txt-        United States and is associated with substantial economic cost [1]. Hyperlipidemia
plos/pmed.0020123.txt-        represents an important modifiable risk factor in the development and progression of CHD.
--
plos/pmed.0020149.txt-      
plos/pmed.0020149.txt-        
plos/pmed.0020149.txt:        Coronary heart disease (CHD) is the leading cause of morbidity and mortality in
plos/pmed.0020149.txt-        developed countries, and identifying and treating patients with high cholesterol has an
plos/pmed.0020149.txt-        essential role in the prevention of CHD. Therapeutic lifestyle changes are important for
```

This command line option captures the lines before and after the matched content along with the matched line. In this case, 2 was provided as the number of lines to capture. This may be useful while looking through a long code base and you want to key in on the context surrounding a certain function call or variable mention.

Example 2:
