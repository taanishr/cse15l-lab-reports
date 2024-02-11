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

This command line option captures the lines before and after the matched content along with the matched line. In this case, `2` was provided as the number of lines to capture. This may be useful while looking through a long code base and you want to key in on the context surrounding a certain function call or variable mention.

Source: Found in `man grep`.

Example 2:
```
grep -C5 M.A. government/Post_Rate_Comm/*.txt
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Economics, Liberalization of Postal Markets.
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Cohen, Robert, Carla Pace, Matthew Robinson, Gennaro
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Scarfiglieri, Vincenzo Visco Comandini, John Waller and Spyros
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Xenakis. 2002. "A Comparison of the Burden of Universal Service in
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Italy and the United States." In Postal and Delivery Services:
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt:Pricing, Productivity, Regulation and Strategy, edited by M.A. Crew
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-and P.R. Kleindorfer. Boston, MA: Kluwer Academic Publishers.
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-PRC Docket No. R2000-1 USPS LR-I-481, FY 1999 and TY Mail
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Processing Unit Costs by Shape with Piggyback Factors (Update to
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-LR-I-81 & 464 Provided in Response to POR No. 116) Using FY 99
government/Post_Rate_Comm/Cohenetal_Cost_Function.txt-Base Year and Alternative IOCS Methodology
--
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-Xenakis
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-Office of Rates, Analysis and Planning
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-U.S. Postal Rate Commission
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-October 1998
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-Published in Emerging Competition in Postal and Delivery
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:Systems, edited by M.A. Crew and
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-P.R. Kleindorfer. Boston: Kluwer Academic Publishers, 1999.
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-An Analysis of the Potential for Cream Skimming in the U.S.
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-Residential Delivery Market
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-A. Introduction
--
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-for capture by cream skimmers. The maximum impact on overall postal
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-rates is, however, likely to be limited. The negative impact on
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-Postal Service's finances would likely be offset to a great extent
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-by the effect of limited competition on the Postal Service's
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-efficiency, service performance and product innovation.
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:Table 4 IMPACT OF CREAM SKIMMING ON
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-I. Comparison Of Business And Residential Routes
government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt-We do not analyze cream skimming on business routes because only
--
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-unit delivery costs for France and the U.S., respectively, over
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-reasonable ranges of the delivery cost drivers. The data used for
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-the analysis are described in the Appendix.
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt:2. SOME BASIC COMPARISONS
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-It would seem that the variation of delivery costs within the
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-U.S. would be greater than in France. Population density in the
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-former ranges from very high (New York City) to very low (Wyoming
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-and Montana). France, on the other hand, has densely populated
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-cities but no areas as sparsely settled as in the United States.2
--
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Kleindorfer. Boston, MA: Kluwer Academic Publishers
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Cohen, Robert, Carla Pace, Matthew Robinson, Gennaro
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Scarfiglieri, Vincenzo Visco Comandini, John Waller and Spyros
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Xenakis. 2002. "A Comparison of the Burden of Universal Service in
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Italy and the United States." In Postal and Delivery Services:
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt:Pricing, Productivity, Regulation and Strategy, edited by M.A. Crew
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-and P.R. Kleindorfer. Boston, MA: Kluwer Academic Publishers.
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Cremer, Helmuth, André Grimaud, and Jean-Jacques Laffont. 2000.
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-"The Cost of Universal Service in the Postal Sector." In Current
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Directions in Postal Reform, edited by Michael A. Crew and Paul R.
government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt-Kleindorfer. Boston, MA: Kluwer Academic Publishers.
--
government/Post_Rate_Comm/Cohenetal_Scale.txt-
government/Post_Rate_Comm/Cohenetal_Scale.txt-
government/Post_Rate_Comm/Cohenetal_Scale.txt-
government/Post_Rate_Comm/Cohenetal_Scale.txt-
government/Post_Rate_Comm/Cohenetal_Scale.txt:A MEASURE OF SCALE ECONOMIES FOR POSTAL SYSTEMS
government/Post_Rate_Comm/Cohenetal_Scale.txt-ROBERT H. COHEN
government/Post_Rate_Comm/Cohenetal_Scale.txt-
government/Post_Rate_Comm/Cohenetal_Scale.txt-U. S. POSTAL RATE COMMISSION
government/Post_Rate_Comm/Cohenetal_Scale.txt-EDWARD H. CHU
government/Post_Rate_Comm/Cohenetal_Scale.txt-U.S. ENVIRONMENTAL PROTECTION AGENCY
--
government/Post_Rate_Comm/Cohenetal_comparison.txt-net avoided cost measures for the cost of the USO.
government/Post_Rate_Comm/Cohenetal_comparison.txt-The portion of mail not requiring delivery is a very important
government/Post_Rate_Comm/Cohenetal_comparison.txt-contributor to the finances of a post.
government/Post_Rate_Comm/Cohenetal_comparison.txt-
government/Post_Rate_Comm/Cohenetal_comparison.txt-
government/Post_Rate_Comm/Cohenetal_comparison.txt:2. COMPARATIVE STATISTICS
government/Post_Rate_Comm/Cohenetal_comparison.txt-Table 1 contains some statistics for Italy and the U.S. and for
government/Post_Rate_Comm/Cohenetal_comparison.txt-their postal administrations.6 Italy has 21 percent of the U.S.
government/Post_Rate_Comm/Cohenetal_comparison.txt-population and 16 percent (approximately one seventh) of the U.S.
government/Post_Rate_Comm/Cohenetal_comparison.txt-per capita volume. Most of the delivery statistics in the table's
government/Post_Rate_Comm/Cohenetal_comparison.txt-second section are reasonably close to this 16 percent figure. The
--
government/Post_Rate_Comm/Cohenetal_comparison.txt-8
government/Post_Rate_Comm/Cohenetal_comparison.txt-It is also the result of the quantity of non-delivered mail (See
government/Post_Rate_Comm/Cohenetal_comparison.txt-Section 4).
government/Post_Rate_Comm/Cohenetal_comparison.txt-
government/Post_Rate_Comm/Cohenetal_comparison.txt-
government/Post_Rate_Comm/Cohenetal_comparison.txt:3. RELATIVE IMPACT OF VOLUME LOSS ON POSTAL SYSTEMS
government/Post_Rate_Comm/Cohenetal_comparison.txt-The burden of the USO on a postal system lies within its fixed
government/Post_Rate_Comm/Cohenetal_comparison.txt-costs. Ceteris paribus, unit (per piece) fixed costs are higher in
government/Post_Rate_Comm/Cohenetal_comparison.txt-a low volume per capita system than in a high volume per capita
government/Post_Rate_Comm/Cohenetal_comparison.txt-system. We examine the effect of volume on unit total costs.
government/Post_Rate_Comm/Cohenetal_comparison.txt-The sensitivity of cost to volume for a postal system can be
--
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-APPENDIX
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-Postal Service Product Innovations and Special-Purpose Mail
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-Classification Changes Reviewed by the Postal Rate Commission Since
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-January 1, 2000
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-
government/Post_Rate_Comm/ReportToCongress2002WEB.txt:I. SUMMARY
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-This report provides an analysis of the United States Postal
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-Service's current legal authority to: (1) introduce and provide new
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-products and services; and (2) enter into negotiated service
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-agreements with individual customers. This report also includes
government/Post_Rate_Comm/ReportToCongress2002WEB.txt-background on the use of such authority within the past two
--
government/Post_Rate_Comm/WolakSpeech_usps.txt-attributes
government/Post_Rate_Comm/WolakSpeech_usps.txt-12 N
government/Post_Rate_Comm/WolakSpeech_usps.txt-(observable and unobservable characteristics) of the
government/Post_Rate_Comm/WolakSpeech_usps.txt-household.
government/Post_Rate_Comm/WolakSpeech_usps.txt-Define the household's demand function for the ith (i=1,...,K)
government/Post_Rate_Comm/WolakSpeech_usps.txt:good x * = D (p ,p ,...,p ,M,A ,A ,...,A )
government/Post_Rate_Comm/WolakSpeech_usps.txt-i i12K 12 N
government/Post_Rate_Comm/WolakSpeech_usps.txt-the amount each good, x , the household consumes. There are K
government/Post_Rate_Comm/WolakSpeech_usps.txt-goods and
government/Post_Rate_Comm/WolakSpeech_usps.txt-i
government/Post_Rate_Comm/WolakSpeech_usps.txt-N characteristics.
--
government/Post_Rate_Comm/WolakSpeech_usps.txt-2) Increasing penetration of personal computing technology
government/Post_Rate_Comm/WolakSpeech_usps.txt-
government/Post_Rate_Comm/WolakSpeech_usps.txt-Using econometric modeling techniques applied to our sample of
government/Post_Rate_Comm/WolakSpeech_usps.txt-households, we are able recover an estimate of the demand
government/Post_Rate_Comm/WolakSpeech_usps.txt-function
government/Post_Rate_Comm/WolakSpeech_usps.txt:x * = D (p ,p ,...,p ,M,A ,A ,...,A )
government/Post_Rate_Comm/WolakSpeech_usps.txt-i i12K 12 N
government/Post_Rate_Comm/WolakSpeech_usps.txt-for each household in the sample.
government/Post_Rate_Comm/WolakSpeech_usps.txt-Demand functions differ across household depending on observable
government/Post_Rate_Comm/WolakSpeech_usps.txt-and unobservable characteristics of the household
government/Post_Rate_Comm/WolakSpeech_usps.txt-Using our econometric model, we can compute an estimate of any
```
This command line option captures the lines before and after the matched content along with the matched line. In this case, `5` was provided as the number of lines to capture. This specific example highlights how the `-C` flag may be useful to capture longer sections of text (such as paragraphs) which contain a specific string.

Source: Found in `man grep`

## Command: `grep`
### Command-line option 2: Only listing file names with `-l`
Example 1:
```
reja@Taanishs-MacBook-Air technical % grep -l DNA biomed/*.txt
biomed/1471-2091-2-10.txt
biomed/1471-2091-2-11.txt
biomed/1471-2091-2-12.txt
biomed/1471-2091-2-13.txt
biomed/1471-2091-2-5.txt
biomed/1471-2091-2-7.txt
biomed/1471-2091-3-13.txt
biomed/1471-2091-3-14.txt
biomed/1471-2091-3-15.txt
biomed/1471-2091-3-16.txt
biomed/1471-2091-3-18.txt
biomed/1471-2091-3-22.txt
biomed/1471-2091-3-23.txt
biomed/1471-2091-3-30.txt
biomed/1471-2091-3-4.txt
biomed/1471-2091-4-1.txt
biomed/1471-2091-4-5.txt
biomed/1471-2105-1-1.txt
biomed/1471-2105-2-8.txt
biomed/1471-2105-2-9.txt
biomed/1471-2105-3-12.txt
biomed/1471-2105-3-14.txt
biomed/1471-2105-3-17.txt
biomed/1471-2105-3-22.txt
biomed/1471-2105-3-24.txt
biomed/1471-2105-3-26.txt
biomed/1471-2105-3-28.txt
biomed/1471-2105-3-3.txt
biomed/1471-2105-3-30.txt
biomed/1471-2105-3-34.txt
biomed/1471-2105-3-37.txt
biomed/1471-2105-3-4.txt
biomed/1471-2105-3-6.txt
biomed/1471-2105-4-25.txt
biomed/1471-2105-4-26.txt
biomed/1471-2105-4-27.txt
biomed/1471-2121-1-2.txt
biomed/1471-2121-2-11.txt
biomed/1471-2121-2-12.txt
biomed/1471-2121-2-15.txt
biomed/1471-2121-2-21.txt
biomed/1471-2121-2-22.txt
biomed/1471-2121-2-6.txt
biomed/1471-2121-3-10.txt
biomed/1471-2121-3-11.txt
biomed/1471-2121-3-12.txt
biomed/1471-2121-3-13.txt
biomed/1471-2121-3-15.txt
biomed/1471-2121-3-16.txt
biomed/1471-2121-3-19.txt
biomed/1471-2121-3-2.txt
biomed/1471-2121-3-22.txt
biomed/1471-2121-3-25.txt
biomed/1471-2121-3-30.txt
biomed/1471-2121-3-4.txt
biomed/1471-2121-3-6.txt
biomed/1471-2121-3-8.txt
biomed/1471-2121-4-1.txt
biomed/1471-2121-4-3.txt
biomed/1471-2121-4-4.txt
biomed/1471-2121-4-6.txt
biomed/1471-213X-1-1.txt
biomed/1471-213X-1-10.txt
biomed/1471-213X-1-11.txt
biomed/1471-213X-1-12.txt
biomed/1471-213X-1-15.txt
biomed/1471-213X-1-2.txt
biomed/1471-213X-1-3.txt
biomed/1471-213X-1-4.txt
biomed/1471-213X-1-9.txt
biomed/1471-213X-2-8.txt
biomed/1471-213X-3-2.txt
biomed/1471-213X-3-3.txt
biomed/1471-213X-3-4.txt
biomed/1471-2148-1-1.txt
biomed/1471-2148-1-6.txt
biomed/1471-2148-2-12.txt
biomed/1471-2148-2-14.txt
biomed/1471-2148-2-17.txt
biomed/1471-2148-2-2.txt
biomed/1471-2148-2-5.txt
biomed/1471-2148-2-7.txt
biomed/1471-2148-2-8.txt
biomed/1471-2148-3-18.txt
biomed/1471-2148-3-3.txt
biomed/1471-2148-3-4.txt
biomed/1471-2148-3-7.txt
biomed/1471-2156-2-12.txt
biomed/1471-2156-2-17.txt
biomed/1471-2156-2-3.txt
biomed/1471-2156-2-5.txt
biomed/1471-2156-2-7.txt
biomed/1471-2156-2-8.txt
biomed/1471-2156-3-11.txt
biomed/1471-2156-3-16.txt
biomed/1471-2156-3-17.txt
biomed/1471-2156-3-3.txt
biomed/1471-2156-3-4.txt
biomed/1471-2156-4-10.txt
biomed/1471-2156-4-5.txt
biomed/1471-2156-4-6.txt
biomed/1471-2156-4-9.txt
biomed/1471-2164-2-1.txt
biomed/1471-2164-2-2.txt
biomed/1471-2164-2-4.txt
biomed/1471-2164-2-6.txt
biomed/1471-2164-2-7.txt
biomed/1471-2164-2-8.txt
biomed/1471-2164-2-9.txt
biomed/1471-2164-3-1.txt
biomed/1471-2164-3-10.txt
biomed/1471-2164-3-13.txt
biomed/1471-2164-3-15.txt
biomed/1471-2164-3-16.txt
biomed/1471-2164-3-18.txt
biomed/1471-2164-3-19.txt
biomed/1471-2164-3-24.txt
biomed/1471-2164-3-26.txt
biomed/1471-2164-3-27.txt
biomed/1471-2164-3-28.txt
biomed/1471-2164-3-29.txt
biomed/1471-2164-3-30.txt
biomed/1471-2164-3-31.txt
biomed/1471-2164-3-32.txt
biomed/1471-2164-3-33.txt
biomed/1471-2164-3-34.txt
biomed/1471-2164-3-35.txt
biomed/1471-2164-3-4.txt
biomed/1471-2164-3-6.txt
biomed/1471-2164-3-7.txt
biomed/1471-2164-3-8.txt
biomed/1471-2164-3-9.txt
biomed/1471-2164-4-13.txt
biomed/1471-2164-4-14.txt
biomed/1471-2164-4-15.txt
biomed/1471-2164-4-16.txt
biomed/1471-2164-4-19.txt
biomed/1471-2164-4-2.txt
biomed/1471-2164-4-21.txt
biomed/1471-2164-4-22.txt
biomed/1471-2164-4-23.txt
biomed/1471-2164-4-24.txt
biomed/1471-2164-4-25.txt
biomed/1471-2164-4-26.txt
biomed/1471-2164-4-28.txt
biomed/1471-2164-4-4.txt
biomed/1471-2164-4-5.txt
biomed/1471-2164-4-6.txt
biomed/1471-2172-1-1.txt
biomed/1471-2172-2-10.txt
biomed/1471-2172-2-3.txt
biomed/1471-2172-2-4.txt
biomed/1471-2172-3-1.txt
biomed/1471-2172-3-10.txt
biomed/1471-2172-3-12.txt
biomed/1471-2172-3-16.txt
biomed/1471-2172-3-2.txt
biomed/1471-2172-3-4.txt
biomed/1471-2180-1-12.txt
biomed/1471-2180-1-16.txt
biomed/1471-2180-1-26.txt
biomed/1471-2180-1-28.txt
biomed/1471-2180-1-29.txt
biomed/1471-2180-1-31.txt
biomed/1471-2180-1-33.txt
biomed/1471-2180-1-34.txt
biomed/1471-2180-1-7.txt
biomed/1471-2180-1-8.txt
biomed/1471-2180-2-13.txt
biomed/1471-2180-2-16.txt
biomed/1471-2180-2-20.txt
biomed/1471-2180-2-22.txt
biomed/1471-2180-2-26.txt
biomed/1471-2180-2-29.txt
biomed/1471-2180-2-38.txt
biomed/1471-2180-2-7.txt
biomed/1471-2180-3-10.txt
biomed/1471-2180-3-13.txt
biomed/1471-2180-3-15.txt
biomed/1471-2180-3-4.txt
biomed/1471-2180-3-9.txt
biomed/1471-2199-2-1.txt
biomed/1471-2199-2-10.txt
biomed/1471-2199-2-12.txt
biomed/1471-2199-2-2.txt
biomed/1471-2199-2-3.txt
biomed/1471-2199-2-4.txt
biomed/1471-2199-2-5.txt
biomed/1471-2199-2-6.txt
biomed/1471-2199-3-10.txt
biomed/1471-2199-3-11.txt
biomed/1471-2199-3-12.txt
biomed/1471-2199-3-17.txt
biomed/1471-2199-3-3.txt
biomed/1471-2199-3-7.txt
biomed/1471-2199-4-4.txt
biomed/1471-2199-4-5.txt
biomed/1471-2202-2-12.txt
biomed/1471-2202-2-14.txt
biomed/1471-2202-2-15.txt
biomed/1471-2202-2-16.txt
biomed/1471-2202-2-2.txt
biomed/1471-2202-2-3.txt
biomed/1471-2202-2-5.txt
biomed/1471-2202-3-1.txt
biomed/1471-2202-3-11.txt
biomed/1471-2202-3-14.txt
biomed/1471-2202-3-16.txt
biomed/1471-2202-3-19.txt
biomed/1471-2202-3-20.txt
biomed/1471-2202-3-3.txt
biomed/1471-2202-3-4.txt
biomed/1471-2202-3-7.txt
biomed/1471-2202-4-10.txt
biomed/1471-2202-4-11.txt
biomed/1471-2202-4-12.txt
biomed/1471-2202-4-6.txt
biomed/1471-2210-1-10.txt
biomed/1471-2210-1-7.txt
biomed/1471-2210-2-14.txt
biomed/1471-2210-2-5.txt
biomed/1471-2210-2-9.txt
biomed/1471-2210-3-1.txt
biomed/1471-2229-1-3.txt
biomed/1471-2229-2-11.txt
biomed/1471-2229-2-3.txt
biomed/1471-2229-2-9.txt
biomed/1471-2229-3-3.txt
biomed/1471-2261-2-11.txt
biomed/1471-2261-3-4.txt
biomed/1471-230X-1-10.txt
biomed/1471-230X-1-5.txt
biomed/1471-230X-2-23.txt
biomed/1471-230X-3-3.txt
biomed/1471-2334-1-24.txt
biomed/1471-2334-1-9.txt
biomed/1471-2334-2-5.txt
biomed/1471-2334-2-7.txt
biomed/1471-2334-3-12.txt
biomed/1471-2334-3-15.txt
biomed/1471-2334-3-9.txt
biomed/1471-2350-2-11.txt
biomed/1471-2350-2-12.txt
biomed/1471-2350-2-2.txt
biomed/1471-2350-2-8.txt
biomed/1471-2350-3-1.txt
biomed/1471-2350-3-12.txt
biomed/1471-2350-3-7.txt
biomed/1471-2350-3-9.txt
biomed/1471-2350-4-3.txt
biomed/1471-2350-4-4.txt
biomed/1471-2350-4-6.txt
biomed/1471-2369-3-1.txt
biomed/1471-2377-3-4.txt
biomed/1471-2407-1-15.txt
biomed/1471-2407-1-6.txt
biomed/1471-2407-2-15.txt
biomed/1471-2407-2-16.txt
biomed/1471-2407-2-17.txt
biomed/1471-2407-2-18.txt
biomed/1471-2407-2-33.txt
biomed/1471-2407-2-9.txt
biomed/1471-2407-3-3.txt
biomed/1471-2407-3-4.txt
biomed/1471-2415-3-3.txt
biomed/1471-2415-3-5.txt
biomed/1471-2431-2-1.txt
biomed/1471-2431-2-12.txt
biomed/1471-2458-3-5.txt
biomed/1471-2474-2-1.txt
biomed/1471-2474-2-2.txt
biomed/1472-6750-1-11.txt
biomed/1472-6750-1-12.txt
biomed/1472-6750-1-13.txt
biomed/1472-6750-1-6.txt
biomed/1472-6750-1-8.txt
biomed/1472-6750-2-10.txt
biomed/1472-6750-2-13.txt
biomed/1472-6750-2-14.txt
biomed/1472-6750-2-21.txt
biomed/1472-6750-3-11.txt
biomed/1472-6750-3-6.txt
biomed/1472-6769-1-1.txt
biomed/1472-6769-1-4.txt
biomed/1472-6793-1-11.txt
biomed/1472-6793-1-15.txt
biomed/1472-6793-1-8.txt
biomed/1472-6793-2-4.txt
biomed/1472-6793-2-8.txt
biomed/1472-6793-3-4.txt
biomed/1472-6793-3-5.txt
biomed/1472-6793-3-6.txt
biomed/1472-6807-1-1.txt
biomed/1472-6807-2-3.txt
biomed/1472-6807-2-5.txt
biomed/1472-6807-3-1.txt
biomed/1472-6823-2-2.txt
biomed/1472-6874-2-8.txt
biomed/1472-6882-1-11.txt
biomed/1472-6890-3-2.txt
biomed/1475-2867-2-15.txt
biomed/1475-2867-2-7.txt
biomed/1475-2867-3-12.txt
biomed/1475-2867-3-2.txt
biomed/1475-2867-3-3.txt
biomed/1475-2867-3-4.txt
biomed/1475-2875-1-5.txt
biomed/1475-2875-2-14.txt
biomed/1475-2875-2-4.txt
biomed/1475-2883-2-11.txt
biomed/1475-2891-1-2.txt
biomed/1475-4924-1-10.txt
biomed/1475-4924-1-5.txt
biomed/1475-9268-1-1.txt
biomed/1476-4598-1-3.txt
biomed/1476-4598-1-6.txt
biomed/1476-4598-1-8.txt
biomed/1476-4598-2-1.txt
biomed/1476-4598-2-2.txt
biomed/1476-4598-2-20.txt
biomed/1476-4598-2-24.txt
biomed/1476-4598-2-25.txt
biomed/1476-4598-2-3.txt
biomed/1476-511X-1-2.txt
biomed/1476-9433-1-2.txt
biomed/1476-9433-1-3.txt
biomed/1477-7827-1-17.txt
biomed/1477-7827-1-23.txt
biomed/1477-7827-1-27.txt
biomed/1477-7827-1-31.txt
biomed/1477-7827-1-36.txt
biomed/1477-7827-1-48.txt
biomed/1477-7827-1-54.txt
biomed/1477-7827-1-6.txt
biomed/1477-7827-1-9.txt
biomed/1478-1336-1-2.txt
biomed/1478-1336-1-3.txt
biomed/1478-1336-1-4.txt
biomed/ar104.txt
biomed/ar118.txt
biomed/ar120.txt
biomed/ar130.txt
biomed/ar149.txt
biomed/ar297.txt
biomed/ar319.txt
biomed/ar321.txt
biomed/ar328.txt
biomed/ar331.txt
biomed/ar407.txt
biomed/ar409.txt
biomed/ar422.txt
biomed/ar612.txt
biomed/ar68.txt
biomed/ar745.txt
biomed/ar774.txt
biomed/ar778.txt
biomed/ar792.txt
biomed/ar795.txt
biomed/ar93.txt
biomed/bcr284.txt
biomed/bcr294.txt
biomed/bcr303.txt
biomed/bcr317.txt
biomed/bcr45.txt
biomed/bcr568.txt
biomed/bcr570.txt
biomed/bcr571.txt
biomed/bcr583.txt
biomed/bcr588.txt
biomed/bcr602.txt
biomed/bcr620.txt
biomed/bcr631.txt
biomed/cc1547.txt
biomed/cvm-2-6-278.txt
biomed/gb-2000-1-1-research002.txt
biomed/gb-2000-1-2-research0003.txt
biomed/gb-2001-2-10-research0041.txt
biomed/gb-2001-2-10-research0042.txt
biomed/gb-2001-2-11-research0045.txt
biomed/gb-2001-2-11-research0046.txt
biomed/gb-2001-2-12-research0051.txt
biomed/gb-2001-2-12-research0054.txt
biomed/gb-2001-2-12-research0055.txt
biomed/gb-2001-2-2-research0004.txt
biomed/gb-2001-2-3-research0007.txt
biomed/gb-2001-2-3-research0008.txt
biomed/gb-2001-2-4-research0010.txt
biomed/gb-2001-2-4-research0011.txt
biomed/gb-2001-2-4-research0012.txt
biomed/gb-2001-2-4-research0014.txt
biomed/gb-2001-2-6-research0018.txt
biomed/gb-2001-2-6-research0021.txt
biomed/gb-2001-2-7-research0024.txt
biomed/gb-2001-2-7-research0025.txt
biomed/gb-2001-2-8-research0027.txt
biomed/gb-2001-2-8-research0030.txt
biomed/gb-2001-2-8-research0031.txt
biomed/gb-2001-2-8-research0032.txt
biomed/gb-2001-2-9-research0037.txt
biomed/gb-2001-3-1-research0001.txt
biomed/gb-2001-3-1-research0005.txt
biomed/gb-2002-3-10-research0052.txt
biomed/gb-2002-3-10-research0053.txt
biomed/gb-2002-3-10-research0055.txt
biomed/gb-2002-3-10-research0056.txt
biomed/gb-2002-3-11-research0059.txt
biomed/gb-2002-3-11-research0062.txt
biomed/gb-2002-3-11-research0065.txt
biomed/gb-2002-3-12-research0071.txt
biomed/gb-2002-3-12-research0072.txt
biomed/gb-2002-3-12-research0078.txt
biomed/gb-2002-3-12-research0079.txt
biomed/gb-2002-3-12-research0080.txt
biomed/gb-2002-3-12-research0081.txt
biomed/gb-2002-3-12-research0082.txt
biomed/gb-2002-3-12-research0083.txt
biomed/gb-2002-3-12-research0085.txt
biomed/gb-2002-3-12-research0086.txt
biomed/gb-2002-3-12-research0087.txt
biomed/gb-2002-3-12-research0088.txt
biomed/gb-2002-3-2-research0008.txt
biomed/gb-2002-3-2-research0009.txt
biomed/gb-2002-3-3-research0011.txt
biomed/gb-2002-3-3-research0012.txt
biomed/gb-2002-3-4-research0018.txt
biomed/gb-2002-3-4-research0019.txt
biomed/gb-2002-3-5-research0020.txt
biomed/gb-2002-3-5-research0021.txt
biomed/gb-2002-3-5-research0022.txt
biomed/gb-2002-3-5-research0024.txt
biomed/gb-2002-3-5-research0025.txt
biomed/gb-2002-3-6-research0029.txt
biomed/gb-2002-3-6-software0001.txt
biomed/gb-2002-3-7-research0032.txt
biomed/gb-2002-3-7-research0035.txt
biomed/gb-2002-3-7-research0036.txt
biomed/gb-2002-3-7-research0037.txt
biomed/gb-2002-3-8-research0038.txt
biomed/gb-2002-3-8-research0039.txt
biomed/gb-2002-3-8-research0040.txt
biomed/gb-2002-3-9-research0043.txt
biomed/gb-2002-3-9-research0045.txt
biomed/gb-2002-3-9-research0046.txt
biomed/gb-2002-3-9-research0048.txt
biomed/gb-2002-3-9-research0049.txt
biomed/gb-2002-3-9-research0051.txt
biomed/gb-2002-4-1-r1.txt
biomed/gb-2002-4-1-r2.txt
biomed/gb-2003-4-1-r5.txt
biomed/gb-2003-4-1-r7.txt
biomed/gb-2003-4-2-r11.txt
biomed/gb-2003-4-2-r16.txt
biomed/gb-2003-4-2-r8.txt
biomed/gb-2003-4-2-r9.txt
biomed/gb-2003-4-3-r17.txt
biomed/gb-2003-4-3-r20.txt
biomed/gb-2003-4-4-r24.txt
biomed/gb-2003-4-4-r26.txt
biomed/gb-2003-4-4-r28.txt
biomed/gb-2003-4-5-r30.txt
biomed/gb-2003-4-5-r32.txt
biomed/gb-2003-4-5-r34.txt
biomed/gb-2003-4-6-r37.txt
biomed/gb-2003-4-6-r39.txt
biomed/gb-2003-4-6-r41.txt
biomed/gb-2003-4-7-r42.txt
biomed/gb-2003-4-7-r43.txt
biomed/gb-2003-4-7-r46.txt
biomed/gb-2003-4-8-r50.txt
biomed/gb-2003-4-8-r51.txt
biomed/gb-2003-4-9-r57.txt
biomed/gb-2003-4-9-r58.txt
biomed/gb-2003-4-9-r60.txt
biomed/rr166.txt
biomed/rr171.txt
biomed/rr172.txt
biomed/rr191.txt
biomed/rr196.txt
```

This command line option only lists the filenames where a search was found. This is useful when data needs to processed later, or when a large volume of files need to be searched through, as `-l` saves on processing time.

Source: found in `man grep`
