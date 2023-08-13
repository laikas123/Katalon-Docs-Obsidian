# Katalon: Add Assertions When Creating Tests

## What Are Assertions?

While recording different steps in a test it's handy to perform various checks to make sure the website is in a certain state before proceeding with the test.

There are two kind of assertions in Katalon:

- "Wait Assertions"
- "Verify Assertions"

Overall these two types of assertions are very similar. Each of them will be covered below.

## Wait Assertions

A wait assertion will wait until a certain condition is true. If after some timeout period the condition is not met the test will try to keep executing. Note the test will **not** fail, it will try to keep executing after the timeout. Katalon offers 4 types of wait assertions:

- Wait Until Element is Visible 
- Wait Until Element is Not Visible 
- Wait Until Element is Present 
- Wait Until Element is Not Present

You may be thinking, what is the difference between visible and present?  Visible refers to actually being able to see the element, that is you can physically see it. Whereas present simply means the element is loaded onto the page and inside of the actual code. So you might now physically see it, but it is actually there.

To give a concrete example of when to use a Wait Assertion consider a page that takes a long time to load. Let's say our login page takes a super long time to load. Well in this case it would be good to add a "Wait Until Element Visible" assertion on the Email input field. That way I could make sure the Email input field is actually on the screen before the test starts typing into it.

To do this I would start recording my test. Then before I start typing into the email field, I would hover my mouse over the email field until it turns red and I can see the correct identifier in the upper left corner of the browser as seen below:

![[hover-email.png]]

(Note that you don't need to do anything special for this red highlighting and object identifiers to appear. This happens automatically when recording tests with Katalon)

After checking that I'm hovering over the Email field correctly I would right click it and then add a "Wait Until Element Visible" assertion as shown below:

![[email-add-wait.png]]

After I finish my test I can see this step in the final test commands:

![[wait-added-to-test.png]]

The timeout (how long the test will try to check the condition is true before moving on) can be configured by double clicking the third column of the wait command and then setting a new value:

![[timeout0.png]]
![[timeout1.png]]
![[timeout2.png]]

(I'm not sure why it was set to 0 by default...)

The idea is the same for using any of the other wait assertions. And I'm sure as we continue to make tests we will figure out the best times to make use of these.

Please note we definitely don't need to add a wait assertion after every test step. It will probably be trial and error for figuring out when the best times to use them are.


## Verify Assertions

Verify assertions are very similar to wait assertions except for they can fail the test if the condition is not met. This is great for when we need to make sure things are a certain way otherwise the test really should be a failure. The different verify assertions offered by Katalon are:

- Verify Element Text
- Verify Element Present
- Verify Element Not Present
- Verify Element Visible
- Verify Element Not Visible
- Verify Element Clickable
- Verify Element Not Clickable

The distinction between Present and Visible is the same as before. The "Verify Element Text" is to verify that an element for which you can input text has the expected text, for example make sure the description field of a video says "Awesome Video!". And then "Clickable" checks if the element could be clicked, but doesn't actually click it.

So continuing with the example from earlier, let's say that in addition to our login page being slow to load we also noticed that sometimes after the developers commit it breaks the ability for users to click on the email field and start typing into it.

We've already added a wait for visible assertion so we know the email field should be visible on the screen. But let's also add a "Verify Element Clickable" to make sure the test can actually click on the email field so that it can type into it.

So again while recording a test after adding my wait assertion I would again hover over the email field and then right click, but this time add a "Verify Element Clickable" assertion:

![[hover-email.png]]
![[verify-element-clickable.png]]


And this can now be seen in the test:

![[verify-element-clickable-in-test.png]]

So now if the email field loads, but the bug appears where it can't be clicked, this verify statement will catch this and fail the test. This is where Katalon tests will help us when the devs create new releases because these failures will be broadcast in Github before the code reaches production.


## The Key Difference Between Wait and Verify

Consider if I change the above test to the following:

![[password-version.png]]

The only change I made between this test and the one of the image before it is that now it's trying to wait and verify the "password" input even though it's on the email page.

The wait will try to wait, it will give up (because the password input won't ever appear on the email page) and then let the test continue.

The verify will stop the test and mark it as a failure.

This can be seen below:

![[difference-wait-assert.png]]

In the box on the image above you can see there is a warning at step 4 which is the wait step. It tried to find the password field but couldn't. It warned us but let the test proceed. It then let step 5 run which was the verify step. This test could not click the password page and so it failed the test.

So **the big takeaways are**:

- Wait asserts will **try to delay** the test until a condition is met, but will **allow the test to continue even if that condition isn't met after waiting**. 
- Verify asserts **will fail the test if the condition is not met**.

So all in all the two sort of compliment each other. If in general a page is slow and you just want to make sure things probably loaded up, then a wait is probably fine. But if you need to make sure something is truly in a specific state before proceeding then a verify is the way to go.

I think that honestly a verify can work on it's own. But a wait should probably be always followed by a verify. At least that's what makes sense to me, but this will probably also be trial and error.