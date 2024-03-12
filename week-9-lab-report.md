# Edstem post:

**Title:** Autograder calculating wrong final percentage!

**Body:** 

My autograder script isn't producing the correct final percentage. Here, it says 1 test failed, implying that the percentage should be 66%, but instead its saying 0?
```
[treja@ieng6-201]:grader-review-taanishr:430$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
Finished cloning
Tests failed: 0
Tests ran: 3
Submission grade: 1%
```

Here is the structure of my directory:
```
grader-review-taanishr
|-GradeServer.java  
|-Server.java  
|-TestListExamples.java  
|-git-output.txt  
|-grade.sh  
|-grading-area  
|-lib  
|-student-submission
```

Here's the code for where I calculate the grade:
```
if ([	$? -ne 0	])
then
	last_line=$(grep . junit-output.txt | tail -n 1)

	tests_run=$(echo $last_line | grep -oE "[0-9]+" | head -n 1)

	failures=$(echo $last_line | grep -oE "[0-9]+" | tail -n 1)
else
	last_line=$(grep . junit-output.txt | tail -n 1)

	tests_run=$(echo $last_line | grep -oE "[0-9]+" | head -n 1)

	failures=0
fi

grade=$((((tests_run-failures)/tests_run)))

echo -e "Tests failed: $failures\nTests ran: $tests_run\nSubmission grade: $grade%" 2>&1 | tee grade.txt
```

# TA leading question:
Try looking into how bash calculates division.

# Student response:
Oh, got it. Thanks. It looks like bash doesn't do floating point divison. Therefore, 2/3 was just dividing into zero. I fixed this by changing my script to multiply the tests failed by 100. Here's how it looks now:

```
[treja@ieng6-201]:grader-review-taanishr:442$ bash grade.sh https://github.com/ucsd-cse15l-f22/list-examples-subtle
Finished cloning
Tests failed: 1
Tests ran: 3
Submission grade: 66%
```
