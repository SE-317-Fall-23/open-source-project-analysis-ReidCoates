## Project Selected: <"Todo MVC">

## I. Introduction
- The goal of this analysis was to see a real world application of the types of testing frameworks we have been learning in 317. Being able to see tests and look directly at the code from an outside view allows you to build your own strategy for testing and see how that applies and what was actually chosen.

## II. Types of Testing in the Project
### A. Unit Testing
- N/A

### B. Integration Testing
- N/A

### C. UI (User Interface) Testing
- Javascript is run through Selenium Webdriver as the only tool. The tests don't use parametization but rely on small individual tests 
- Css file are used for the confirmation of UI elements and the button presses are simulated by function calls on the backend (or js end which technically is still front end but this app only has that and the display).
- Selenium Webdriver is the only tool used for these test cases even with display and operation testing. The main way that testing is done (instead of pupeteering) it to make calls to functions and then check the css files returned to ensure things are displayed or hidden throughout.
- Regression and acceptance testing seem to be the biggest reason for this testing suite. There aren't large lists of parameterized tests to test all the edge cases, it simple confirms basic operaions.

### D. Other Types of Testing (if applicable)
- N/A

## III. Reasons for Choosing These Testing Types
- Because this project is so simple and the input so small, widespread edge case testing is not needed ad relatively impossible
- When all of your items are simply unformatted strings, you only need test to see if one string works for it and this makes parameteriztion testing very inefficient.
- This is not a high tech application so as long as the display featres operate as they should and the add and remove work, then this app has reached an acceptable level of confimraed correctness. This is accomplished through the basic unit testing and simple scenarios to show each feature works independatnly and together


## 2. Test Data Generation
### A. Static Test Data
- Static lists of items (strings) to be added are created for the tests
- This is enough because all the test needs to confirm is that a single string works in the app for specific functions which then cofirms that all strings will work
### B. Dynamic Test Data
- No dynamic test data. All of the data is staticaly created. Only three strings are needed.

## 3. Test Doubles
- The test use a fake server to run all of the tests but otherwise there were not fakes, stubs, or doubles that I could find
- Stubs would be important to use if this project used a lot of external tools and libraries. Then you could test your individual functions while not having to blindly trust that the other processes are working as they should be. An example of this would be in you had a function which would use the current date to display an item as highlighted red (the project doesn't hve this). This program doesn't use any of those and for what it does use, it gets around it by using the css file confirmations to keep even UI testing simple. 

## 4. Discussion on Testing Practices
<!-- 
To find discussions on testing strategy in a GitHub repository, you can follow these steps:

Visit the GitHub repository for the project you're interested in.
Look for the "Issues" tab on the repository's page.
Use the search bar within the Issues tab to search for terms related to testing, such as "testing strategy," "test cases," or "test automation."
-->
- Investigate any discussions related to testing practices within the project.
- https://github.com/tastejs/todomvc/issues/1880
- There is very little discussion of testing in any of the project's issues, but this discussion focused on where testing would be maintained and supported. The conclusion was to only maintain suporting tests for the production ready version of TodoMVC. The ain reason was because of how time consuming creating vast test suites for every verson would be so the contributors decided to focus there efforts on the place where the most good could come from as this is an open source project and not funded by people. I think this aligns with the view that testing is very important but it costs a lot of time and money and so if you have little of both you should then use it to make sure your code operates as acceptable as possible. This would mean supporting production read code (not production but the step before) so that you are confirming anything you put out has been tested as thouroughly as possible. This aligns with the industry standards of outputting code with acceptance testing. Now I think if the project were to be funded then a larger effort should be focused on testing. There are files in this project which outline which parts of the code is not tested at all for various reasons. This is unacceptable and if you have untested modules it can compromise the integrity of well tested modules. Therefore I believe this project is doing the best that it can but that if it were to be a paid service or anything other than a project for developers to learn frameworks and get their feet wet then it should have a much higher standard  fo testing.
