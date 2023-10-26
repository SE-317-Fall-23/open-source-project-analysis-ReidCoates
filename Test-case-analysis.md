# Assignment Submission

## Project Selected: <Enter project name>

## I. Introduction
- Briefly introduce the purpose of this section, which is to provide a detailed description of two test cases in the selected open-source project.

## II. Test Case 1: [Name of Test Case]
### A. Description
- Provide a concise overview of what this test case is designed to verify or validate within the project.
### B. Gherkin Syntax (if applicable)
- If you choose to use Gherkin syntax, write the Gherkin scenario for this test case.
### C. Test Steps
- Enumerate the sequence of steps or actions involved in the test case.
### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.

```Java
test.describe('New Todo', function () {

			test.it('should allow me to add todo items', function (done) {
				page.enterItem(TODO_ITEM_ONE);
				testOps.assertItems([TODO_ITEM_ONE]);
				page.enterItem(TODO_ITEM_TWO);
				testOps.assertItems([TODO_ITEM_ONE, TODO_ITEM_TWO])
					.then(function () { done(); });
			});

			test.it('should clear text input field when an item is added', function (done) {
				page.enterItem(TODO_ITEM_ONE);
				testOps.assertNewItemInputFieldText('')
					.then(function () { done(); });
			});

			test.it('should append new items to the bottom of the list', function (done) {
				createStandardItems();
				testOps.assertItemCount(3);
				testOps.assertItemText(0, TODO_ITEM_ONE);
				testOps.assertItemText(1, TODO_ITEM_TWO);
				testOps.assertItemText(2, TODO_ITEM_THREE)
					.then(function () { done(); });
			});

			test.it('should trim text input', function (done) {
				page.enterItem('   ' + TODO_ITEM_ONE + '  ');
				testOps.assertItemText(0, TODO_ITEM_ONE)
					.then(function () { done(); });
			});

			test.it('should show #main and #footer when items added', function (done) {
				page.enterItem(TODO_ITEM_ONE);
				testOps.assertMainSectionVisibility(true);
				testOps.assertFooterVisibility(true)
					.then(function () { done(); });
			});

		});
```
### E. Initial State
- Describe the initial state or conditions of the system or component before executing the test.
### F. Transition
- Explain the actions or events that trigger a change in the system's state.
### G. Expected State
- Clearly outline the expected state or outcome after the test steps have been completed.

## III. Test Case 2: [Name of Test Case]
### A. Description
- Provide a concise overview of the purpose of the second test case.
### B. Gherkin Syntax (if applicable)
- If you choose to use Gherkin syntax, write the Gherkin scenario for this test case.
### C. Test Steps
- Enumerate the sequence of steps or actions involved in this test case.
### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.
```Java
// Enter code
```
### E. Initial State
- Describe the initial state or conditions of the system or component before executing the test.
### F. Transition
- Explain the actions or events that trigger a change in the system's state.
### G. Expected State
- Clearly outline the expected state or outcome after the test steps have been completed.

