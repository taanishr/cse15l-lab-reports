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

reverseInPlace initially accessed the original array instead of making a copy. This meant that the array would become a mirror image of the elements in the second half of the array. By making a temporary array with `int temp[] = new int[arr.length];`, making a deep copy of `arr`'s elements with `System.arraycopy(arr, 0, temp, 0, arr.length);`, and accessing the `temp[]` array's elements instead of `arr[]`'s, the method then properly swapped the beginning and end elements.

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

This command line option captures the lines before and after the matched content along with the matched line. In this case, `2` was provided as the number of lines to capture. This may be useful while looking through a long code base and you want to key in on the context surrounding a certain function call or variable mention.

Source: Found in `man grep`.

Example 2:
```
treja@taanishs-air technical % grep -C5 salad biomed/*.txt
biomed/1471-2458-3-11.txt-          including types of swimming locations and entering hot
biomed/1471-2458-3-11.txt-          tubs; person-to-person fecal exposures, specifically,
biomed/1471-2458-3-11.txt-          contact with child-care centers, diapered, and ill
biomed/1471-2458-3-11.txt-          individuals; consumption of "risky" food items (risky
biomed/1471-2458-3-11.txt-          foods refers to a list of standard food items asked in
biomed/1471-2458-3-11.txt:          the CDC foodborne questionnaires, e.g. salads, cold
biomed/1471-2458-3-11.txt-          cuts/meats, raw vegetables/fruits, raw oysters/shellfish,
biomed/1471-2458-3-11.txt-          cider/juice), consumption of unpasteurized foods and
biomed/1471-2458-3-11.txt-          handling of raw foods; zoonotic contact including farm
biomed/1471-2458-3-11.txt-          animals and pets; and, for adults over 18 years of age,
biomed/1471-2458-3-11.txt-          details on specific sexual practices. Sexual contact was
--
biomed/1472-6882-1-7.txt-          Hallelujah Acres, Inc. ( 
biomed/1472-6882-1-7.txt-          God's Way to Ultimate Health, Recipes
biomed/1472-6882-1-7.txt-          for Life...from God's Garden, 21 Days to health the
biomed/1472-6882-1-7.txt-          Hallelujah diet way ) and informational pamphlets.
biomed/1472-6882-1-7.txt-          Instructions were given on what foods to eat (fresh
biomed/1472-6882-1-7.txt:          fruits, salads, raw vegetables, carrot juice, nuts,
biomed/1472-6882-1-7.txt-          seeds, whole grain products, tubers, flax seed oil, extra
biomed/1472-6882-1-7.txt-          virgin olive oil) what foods to avoid (alcohol, caffeine,
biomed/1472-6882-1-7.txt-          foods containing refined sugar, corn syrup, refined
biomed/1472-6882-1-7.txt-          and/or hydrogenated oil, refined flour, dairy, eggs, and
biomed/1472-6882-1-7.txt-          all meat) and how to prepare freshly extracted carrot
--
biomed/1472-6882-1-7.txt-          than at 2 months. The dehydrated barley grass juice was
biomed/1472-6882-1-7.txt-          consumed by all but 2 subjects who reported immediate
biomed/1472-6882-1-7.txt-          nausea upon consumption of the powder. Flax seed oil was
biomed/1472-6882-1-7.txt-          consumed by 23 of 26 participants so that the mean intake
biomed/1472-6882-1-7.txt-          of n-3 fatty acids was about 6 g/day. Fresh fruit and
biomed/1472-6882-1-7.txt:          salads, based mostly on leaf lettuce and dark leafy
biomed/1472-6882-1-7.txt-          greens rather than head lettuce, were consumed daily. The
biomed/1472-6882-1-7.txt-          high intakes of fruits and vegetables resulted in high
biomed/1472-6882-1-7.txt-          intakes of fiber, vitamin C, folate, potassium, and
biomed/1472-6882-1-7.txt-          magnesium. Animal product consumption was very low,
biomed/1472-6882-1-7.txt-          especially intakes of meat, poultry, and fish. Intakes
```

This command line option captures the lines before and after the matched content along with the matched line. In this case, `5` was provided as the number of lines to capture. This specific example highlights how the `-C` flag may be useful to capture longer sections of text (such as paragraphs) which contain a specific string.

Source: Found in `man grep`

### Command-line option 2: Only listing file names with `-l`

Example 1:
```
treja@taanishs-air technical % grep -l salad biomed/*.txt
biomed/1471-2458-3-11.txt
biomed/1472-6882-1-7.txt
```

This command line option only lists the filenames where a search was found. This is useful when the data from a list of pattern matched files needs to processed later. For example, while making an automated grading system, we may need to search for all files with a certain function header and then use those file names to run tests later. This command line option is also useful when processing a large amount of files, as the smaller output saves on processing time compared to the regular grep command.

Source: Found in `man grep`

Example 2:

```
treja@Taanishs-MacBook-Air technical % echo "DNA is a complex molecule." | grep -l DNA
(standard input)
```

The `-l` flag can also search through standard input. If the output of a command is piped to `grep -l` with a string provided, the command will output `(standard input)` if the string was found. This may be useful when trying to determine if the output of some command contained a specific exit code, but the contents of its output aren't needed.

Source: Found in `man grep`

### Command-line option 3: Matching the exact word provided with `-w`
Example 1:

```
treja@Taanishs-MacBook-Air technical % grep -w "apple" biomed/*.txt
biomed/1471-2202-2-5.txt:            computer http://www.apple.com. If the criteria for
biomed/1471-2458-3-11.txt:        fresh-pressed apple cider [ 28 ] . Other foodborne
```

This command line option only lists matches if the exact string is found (i.e., it is not a substring). For example, when searching for accept, a word like acceptance would be excluded from the search. This is useful for filtering text. For instance, when examining how a variable's data is transformed over time in a file, using grep -w with the variable name to find exact instances of that variable name in the file could be helpful.

Source: Found in `man grep`

Example 2:

```
treja@taanishs-air technical % grep -w I government/Alcohol_Problems/*.txt
government/Alcohol_Problems/DraftRecom-PDF.txt:She cited differences between Level I trauma centers and community
government/Alcohol_Problems/DraftRecom-PDF.txt:relate to Level I trauma care research. Therefore, he supported
government/Alcohol_Problems/Session2-PDF.txt:With Harmful Alcohol Consumption, I. Addiction 1993;88:349-62.
government/Alcohol_Problems/Session3-PDF.txt:Level I trauma center. Patients who screened positive on a
government/Alcohol_Problems/Session3-PDF.txt:31. Dinh-Zarr T, Diguiseppi C, Heitman E, Roberts I. Preventing
government/Alcohol_Problems/Session3-PDF.txt:I am honored to be a discussant following Dr. DiClemete's
government/Alcohol_Problems/Session3-PDF.txt:I am going to show you a clip from a video entitled The
government/Alcohol_Problems/Session3-PDF.txt:16. Dinh-Zarr T, Diguiseppi C, Heitman E, Roberts I. Preventing
government/Alcohol_Problems/Session4-PDF.txt:I am honored to have the opportunity to participate in this
government/Alcohol_Problems/Session4-PDF.txt:providers represented here today. I think this effort reflects the
government/Alcohol_Problems/Session4-PDF.txt:I feel strongly that the ED-based research agenda should address
government/Alcohol_Problems/Session4-PDF.txt:users, alcohol abusers, and alcoholics. When I first began
government/Alcohol_Problems/Session4-PDF.txt:model. I look forward to the day when the next Joint Commission
government/Alcohol_Problems/Session4-PDF.txt:I think Dr. Gentilello's presentation nicely outlined the
government/Alcohol_Problems/Session4-PDF.txt:environment because of concerns about non-payment for services. I
government/Alcohol_Problems/Session4-PDF.txt:emergency departments, and I agree with Dr. Gentilello's assessment
government/Alcohol_Problems/Session4-PDF.txt:At this point, I want to depart from the biomedical research
government/Alcohol_Problems/Session4-PDF.txt:population health. I feel that the research agenda should also
government/Alcohol_Problems/Session4-PDF.txt:not have simple solutions. I think that some clarifications are
government/Alcohol_Problems/Session4-PDF.txt:Finally, I would like to address the issue of funding. Much of
```

This command line option only lists matches if the exact string is found (i.e., it is not a substring). For example, when searching accept, a word like acceptance would be excluded from the search. In this case, using I as the regex search helps single out personal annecdotes, quotes and acknowledgments rather than including words that begin with a capital I, making it powerful for text processing.

Source: Found in `man grep`

### Command-line option 4: Limiting number of matches per file with `-m`

Example 1:
```
treja@taanishs-air technical % grep -m 1 DNA government/Media/*.txt
government/Media/Making_a_case.txt:DNA-People's Legal Services' monthly seminar on how to represent
government/Media/New_funding_sources.txt:DNA-People's Legal Services in Flagstaff. The Arizona Equal Justice
government/Media/The_State_of_Pro_Bono.txt:of her own money on an appeal based on DNA evidence.
```

This command line option only limits matches to the number provided per file (in this case 1). This is useful for when we care to determine which files contain a string but only care about matching it a certain amount of times. If the number is 1, `-m` provides similar functionality to `-l`, but also gives the matched line, which may be useful for data processing.

Source: Found in `man grep`

Example 2:
```
treja@taanishs-air technical % grep -m 2 ball government/*/*.txt
government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt:campaign, or for use in "advocating or opposing any ballot
government/Env_Prot_Agen/final.txt:the Western Hemisphere, and with our allies globally, to
government/Env_Prot_Agen/multi102902.txt:these globally traded commodity chemicals, it is projected that
government/Env_Prot_Agen/multi102902.txt:ball mills) equipment
government/Gen_Account_Office/Testimony_cg00010t.txt:United States against an intercontinental ballistic missile attack
government/Media/A_helping_hand.txt:Linda Samels Ceballos entered Loyola Law School in Los Angeles
government/Media/A_helping_hand.txt:Mintie, a Claremont resident, made it possible for Ceballos to
government/Media/Entities_Merge.txt:Verde County elections by absentee ballot after a former Ku Klux
government/Media/Legal-aid_chief.txt:Cornhusker football player, he shooed a young Tom Osborne off a
government/Media/Legal-aid_chief.txt:160-pound quarterback joined the freshman football team. It was
government/Media/Terrorist_Attack.txt:Judge Kaye's hopes for keeping the pro bono ball rolling:
government/Media/Unusual_Woodburn.txt:in the late 1990s. He sees Mixtecs playing basketball, shopping in
government/Media/predatory_loans.txt:penalties and balloon payments on high-cost home loans.
government/Post_Rate_Comm/Gleiman_EMASpeech.txt:crystal ball, I thought you might be interested in a brief outline
government/Post_Rate_Comm/Gleiman_EMASpeech.txt:This fellow is flying a hot air balloon and suddenly realizes he
government/Post_Rate_Comm/Gleiman_gca2000.txt:rabid baseball fan. So much so that he tries to see at least one
government/Post_Rate_Comm/Gleiman_gca2000.txt:story, Denton was leaning into the plate in fantasy baseball camp
```


This command line option only limits matches to the number provided per file (in this case 2). Limiting the number of matches to a number other than 1 may be useful when we need to cap the size of the output, or only need to process a certain amount of occurences of the string.

Source: Found in `man grep`

