<img width="373" alt="image" src="https://github.com/taanishr/cse15l-lab-reports/assets/49845822/0fd72fd0-1906-406e-8020-011298fc3ef7"># Step 1: Logging into ieng6
![Login step](/loginstep.png)
Keys pressed: `<s><s><h><SPACE><t><r><e><j><a><@><i><e><n><g><6><.><u><c><s><d><.><e><d><u>`

Here, I logged into the remote server by typing in each character of `ssh treja@ieng6.ucsd.edu`

# Step 2: Cloning my fork of the repository
![Clone step](/clonestep.png)
Keys pressed `<g><i><t><SPACE><c><l><o><n><e><CTRL><V>`

Here, I cloned my fork of the repository by typing the command `git clone` then copying and pasting the ssh key from my fork on github, resulting in the full command being `git clone git@github.com:taanishr/lab7.git`.

# Step 3: Running the failing tests
![Running failing tests](/failedtests.png)
Keys pressed: `<c><d><SPACE><l><a><b><7><ENTER><b><a><s><h><SPACE><t><TAB>`

Here, I entered the directory where the repository was cloned by typing `cd lab7`, and then ran the test script with `bash test.sh`. I used tab while calling bash so I wouldn't need to fill out the entire file name.

# Step 4: Editing the code
![Replacing character](/step4replace.png)

Keys pressed: `<v><i><m><SPACE><L><TAB><.><TAB><ENTER><4><3><j><e><x><i><2>`

Here, I typed the command `vim ListExamples.java`, using tab after `L` and `.` in order to autofill the file name, and then navigated down to the end of the first word of the 43rd line with `<4><3><j><e>`, and finally deleted the character at the end of the wod with `<x>` before replacing it with 2 by typing `<i><2>`.

![Replacing character](/step4saveandexit.png)

Keys pressed: <ESCAPE><:><x><ENTER>

To get back to the terminal, I exited out of insert mode by hitting `<ESCAPE>`, then typed `<:><x><ENTER>` to save and exit the file.

# Step 5: Running the tests again
![Running tests successfully](/passedtests.png)

Keys pressed: `<UP><UP>`

Here, I pressed the up arrow twice to get back to the bash command I called earlier (`bash test.sh`)

# Step 6: Pushing to repository
![Adding file changes](/step6add.png)
Keys pressed: `<g><i><t><SPACE><a><d><d><SPACE><L><TAB><ENTER>`

Here, I typed `git add L` then pressed tab to get `git add ListExamples.java`, which staged those change.

![Commiting file changes](/step6commit.png)
Keys pressed: `<g><i><t><SPACE><c><o><m><TAB><-><m><f><i><x><e><d>`
Here, I typed `git commit -m fixed` to commit the changes with the message `fixed`.

![Pushing changes](/step6push.png)
Keys pressed: `<g><i><t><SPACE><p><u><s><h><SPACE><o><TAB><main>`
Here, I typed `git push origin main` to push the commited changes to the main branch of my repository on github.

