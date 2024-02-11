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
### Command-line option 2: Highlight matches with `--color`
```
treja@Taanishs-MacBook-Air technical % grep --color 911 government/About_LSC/*.txt
government/About_LSC/State_Planning_Special_Report.txt:19881989199019<p style="color:red">911</p>992199319941995199619971998199920002001
government/About_LSC/commission_report.txt:S16<p style="color:red">911</p> (Oct. 17, 1986) (statement of Sen. Kennedy); March Comments
```
