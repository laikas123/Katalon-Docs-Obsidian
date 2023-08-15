## Katalon: Call Another Test Case and Pass Arguments to The Called Test Case

In Katalon it's possible to call another test case from the current test case. This is helpful for doing repeated things like logging in, updating video descriptions, or uploading files.

As a sample of how this works consider the following test case, all it does is open the browser.

![[start-point.png]]

Let's say we want it to login and update a video description. These are both things we will want to automate so rather than manually recording a test I also have two test cases that can be called from the main test case:

![[callable-cases.png]]

To call these test cases go back to the main test case and click the **drop down arrow** next to add "Add" then choose "Call Test Case":

![[add-call-test-case.png]]

A new window will appear. We first want to login, so we choose the "Login" test then click "Ok":

![[add-login-call.png]]

We can see the test call was successfully added:

![[login-added.png]]

The third column titled Input is where you can pass optional variables to the test you are calling. Since we mainly login with "testing@screencast-o-matic" we don't need to pass arguments to the login test case.

The next thing we wanted to do was update the video description, so let's also add a test case call to the "Update Video Description" test:

![[add-update-descript-test-case.png]]

Now, for this test case we may want to provide some variables as input. 

Perhaps we want to specify which video should be updated, as well as what the contents of the description should be. To do so we can double click on the third column with the '[:]' sybmol:

![[3dot.png]]

This will bring up a window like the following:

![[Pasted image 20230815135341.png]]

If we again click the "[:]" symbol in the "Value" column we can add variables in the new window that pops up by clicking the insert button:

![[insert.png]]

It will insert a new entry like the following:

![[newentry.png]]

The "Key" column is the name of the variable, and the "Value" column is the actual value you want to pass. For this scenario, let's pass the URL to the video we want to modify as well as the content we want the description to be. We can insert another entry, and then after double clicking the key and value columns to modify their values, we get something like the following:

![[added-fields.png]]

As shown above be sure to click "Ok" after it looks good.

Ok great, so now the test looks something like the following:

![[updated-test.png]]

But how does the "Update Video Description" test case know how to access/use these values?

Well it doesn't... 

We need to change that.

Here are the contents of the "Update Video Description" test case:

![[contents-vid-descript-test.png]]

You can see it navigates to a hardcoded video URL then updates its description with a hardcoded string.

Let's change that so that it uses our variables "videoURL" and "description" from the test case call.

To do so first double click the "Input" column for the "Navigate to URL" command and it will bring up a window like the following:

![[hardcodeurl.png]]

This is the hardcoded URL. 

Notice the value is of type string. Clicking this once, and then clicking the right hand side of it will open a drop down menu:

(Getting the drop down menu to open is a bit finnicky...)

![[dropdown.png]]

We will want to choose "Variable" and then enter the name of the variable which is "videoURL":

![[videoURL.png]]

**Note** as seen above you do not want to put the variable name in quotes. That is only for Strings that need to have quotes.

Click "Ok" to make sure the variable gets update and then we can see the test has been updated:

![[ok2.png]]

![[testupdated2.png]]


We can do the exact same thing for the variable for the "Set Text" command and the "Update Video Description" test now looks good:

![[alldone.png]]

Great! Now the main test that calls both of the other test cases is good to go. Clicking run we can verify that it calls both test cases and does what it should:

![[run.png]]

We can see in the console that it indeed calls both test cases and uses the variables we passed:

![[callbsoth.png]]

![[varsused.png]]


Cool! So that's how to call test cases from the main test.

**PRO TIP:** Any test cases you plan to be callable such as the "Login" and "Update Video Description" tests from this example **SHOULD NOT** implement the "Open Browser" command.

Notice only my test case that called the functions had this command:

![[open-browser.png]]

Whereas the test cases being called did not:

![[call1.png]]
![[call2.png]]

The reason is that otherwise the test would spawn a whole new browser and likely mess things up. 









