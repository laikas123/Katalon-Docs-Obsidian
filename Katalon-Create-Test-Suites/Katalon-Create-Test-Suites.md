# Katalon: Creating Test Suites

As the number of tests grow it's nice to be able to organize them into test suites. To create a new test suite, right click on the "Test Suites" folder and then select "New -> Test Suite":

![[test-suite-folder.png]]
![[test-suite-create.png]]

After giving the test suite a name, a new test suite will open and should look something like this:

![[blank-test-suite.png]]

To add a new test to the test suite, click "Add" and then select the tests you want to add:

![[add-test.png]]
![[select-tests-to-add.png]]

The test will now successfully be in the test suite:

![[test-added.png]]

Tests can later be added or removed using the "Add" and "Delete" buttons respectively.


As a side note, notice how in the last image there is this small "\*" icon next to the name of the test suite:

![[asterisk.png]]

In Katalon studio be sure to press CTRL+S (or Mac equivalent for save) often to make sure to save progress. This is helpful for of course not losing data, but also to make sure Github Desktop sees changes made. This is important because otherwise changes won't get pushed to the repo.

After pressing CTRL+S (or Mac equivalent) the "\*" icon will go away and GIthub Desktop should notice any changes you make:

![[test-saved.png]]