# Assignment Submission

## Project Selected: <Enter Todo MVC>

## I. Introduction
- Provide a detailed description of two test cases in the selected open-source project.

## II. Test Case 1: [Add Two Todo Items]
### A. Description
- This test case is a test in the suite which verifies the correct functionality of the Add New Todo Item. It adds two ites while checking twice to see if the first was added and then if the second overwrote the first or wether they both were correctly displayed on the todo list. This is checking the memory and no the display however so the code could be storing correctly but not displaying and this test would pass.
### B. Gherkin Syntax (if applicable)
- Scenario: Adding Todo Items
    - Given the user is on the Todo application page
    - When the user adds a new todo item with text "Anything at all 1"
    - Then the todo list should display "Anything at all 1"
    
    - When the user adds another todo item with text "Anything at all 2"
    - Then the todo list should display "Anything at all 1" and "Anything at all 2"
### C. Test Steps
- 1. Simulate adding an itme
- 2. Test to see if item was added correctly
- 3. Simulate adding a second item in the same instance
- 4. Test to see if both items were added and stored correctly
### D. Code Segments Under Test
- This code is testing the addition of a singular todo list item being added and all the different options that can happen. This is from the App View of Node.js.

```Java
// Test case itself
test.it('should allow me to add todo items', function (done) {
				page.enterItem(TODO_ITEM_ONE);
				testOps.assertItems([TODO_ITEM_ONE]);
				page.enterItem(TODO_ITEM_TWO);
				testOps.assertItems([TODO_ITEM_ONE, TODO_ITEM_TWO])
					.then(function () { done(); });
			});

this.enterItem = function (itemText) {
		var self = this;
		var nItems;
		return self.getListItems()
			.then(function (items) {
				nItems = items.length;
			})
			.then(this.waitForNewItemInputField.bind(this))
			.then(function (newItemInput) {
				return newItemInput.sendKeys(itemText).then(function () { return newItemInput; });
			})
			.then(function (newItemInput) {
				return browser.wait(function () {
					// Hit Enter repeatedly until the text goes away
					return newItemInput.sendKeys(webdriver.Key.ENTER)
						.then(newItemInput.getAttribute.bind(newItemInput, 'value'))
						.then(function (newItemInputValue) {
							return newItemInputValue.length === 0;
						});
				}, DEFAULT_TIMEOUT);
			})
			.then(function () {
				return self.waitForElement(self.getLastListItemLabelCss(nItems));
			})
			.then(this.waitForTextContent.bind(this, itemText.trim(),
				'Expected new item label to read ' + itemText.trim()));
	};

    // Add a single todo item to the list by creating a view for it, and
    // appending its element to the `<ul>`.
    AppView.prototype.addOne = function (todo) {
        var view = new TodoView({ model: todo });
        this.$('.todo-list').append(view.render().el);
    };

    // Generate the attributes for a new Todo item.
    AppView.prototype.newAttributes = function () {
        return {
            title: this.input.val().trim(),
            order: Todos.nextOrder(),
            completed: false
        };
    };

    // If you hit return in the main input field, create new **Todo** model,
    // persisting it to *localStorage*.
    AppView.prototype.createOnEnter = function (e) {
        if (e.which === TodoView.ENTER_KEY && this.input.val().trim()) {
            Todos.create(this.newAttributes());
            this.input.val('');
        }
    };

    function AppView() {
        _super.call(this);
        // Delegated events for creating new items, and clearing completed ones.
        this.events = {
            'keypress .new-todo': 'createOnEnter',
            'click .todo-clear button': 'clearCompleted',
            'click .toggle-all': 'toggleAllComplete'
        };
        // Instead of generating a new element, bind to the existing skeleton of
        // the App already present in the HTML.
        this.setElement($('.todoapp'), true);
        // At initialization we bind to the relevant events on the `Todos`
        // collection, when items are added or changed. Kick things off by
        // loading any preexisting todos that might be saved in *localStorage*.
        _.bindAll(this, 'addOne', 'addAll', 'render', 'toggleAllComplete', 'filter');
        this.input = this.$('.new-todo');
        this.allCheckbox = this.$('.toggle-all')[0];
        this.mainElement = this.$('.main')[0];
        this.footerElement = this.$('.footer')[0];
        this.statsTemplate = _.template($('#stats-template').html());
        Todos.bind('add', this.addOne);
        Todos.bind('reset', this.addAll);
        Todos.bind('all', this.render);
        Todos.bind('change:completed', this.filterOne);
        Todos.bind('filter', this.filter);
        Todos.fetch();
        // Initialize the router, showing the selected view
        var todoRouter = new TodoRouter();
        Backbone.history.start();
    }

```
### E. Initial State
- The program only needs to be running at the start, the list ill be checked for the items added and not the total length of the items or any other portion of the program.
### F. Transition
- An item is added and then after confirmation that it exists another item is added both being simulated into the enviornment but enter key presses of the test framework.
### G. Expected State
- The list will be expected to conatin both of the two added items. Nothing else is checked for.

## III. Test Case 2: [Clear Input Box after Item Addition]
### A. Description
- The purpose of this test case is to ensure the text box is cleared after submitting an item to the todo list.
### B. Gherkin Syntax (if applicable)
- Scenario: Clearing Text Input Field
    - Given the user has entered a todo item with text "Anything at all"
    - When the user adds the todo item
    - Then the todo input field should be cleared
### C. Test Steps
- 1. Add a new item to the todo list
- 2. Check if the input box is empty or not
### D. Code Segments Under Test
- When adding a new item, the code would follow through these code snippets. The snippets are ascocited with the input to dsplay of adding a new item to the todo list.

```Java
test.it('should clear text input field when an item is added', function (done) {
				page.enterItem(TODO_ITEM_ONE);
				testOps.assertNewItemInputFieldText('')
					.then(function () { done(); });
			});

this.enterItem = function (itemText) {
		var self = this;
		var nItems;
		return self.getListItems()
			.then(function (items) {
				nItems = items.length;
			})
			.then(this.waitForNewItemInputField.bind(this))
			.then(function (newItemInput) {
				return newItemInput.sendKeys(itemText).then(function () { return newItemInput; });
			})
			.then(function (newItemInput) {
				return browser.wait(function () {
					// Hit Enter repeatedly until the text goes away
					return newItemInput.sendKeys(webdriver.Key.ENTER)
						.then(newItemInput.getAttribute.bind(newItemInput, 'value'))
						.then(function (newItemInputValue) {
							return newItemInputValue.length === 0;
						});
				}, DEFAULT_TIMEOUT);
			})
			.then(function () {
				return self.waitForElement(self.getLastListItemLabelCss(nItems));
			})
			.then(this.waitForTextContent.bind(this, itemText.trim(),
				'Expected new item label to read ' + itemText.trim()));
	};

    // Add a single todo item to the list by creating a view for it, and
    // appending its element to the `<ul>`.
    AppView.prototype.addOne = function (todo) {
        var view = new TodoView({ model: todo });
        this.$('.todo-list').append(view.render().el);
    };

    // Generate the attributes for a new Todo item.
    AppView.prototype.newAttributes = function () {
        return {
            title: this.input.val().trim(),
            order: Todos.nextOrder(),
            completed: false
        };
    };

    // If you hit return in the main input field, create new **Todo** model,
    // persisting it to *localStorage*.
    AppView.prototype.createOnEnter = function (e) {
        if (e.which === TodoView.ENTER_KEY && this.input.val().trim()) {
            Todos.create(this.newAttributes());
            this.input.val('');
        }
    };

    function AppView() {
        _super.call(this);
        // Delegated events for creating new items, and clearing completed ones.
        this.events = {
            'keypress .new-todo': 'createOnEnter',
            'click .todo-clear button': 'clearCompleted',
            'click .toggle-all': 'toggleAllComplete'
        };
        // Instead of generating a new element, bind to the existing skeleton of
        // the App already present in the HTML.
        this.setElement($('.todoapp'), true);
        // At initialization we bind to the relevant events on the `Todos`
        // collection, when items are added or changed. Kick things off by
        // loading any preexisting todos that might be saved in *localStorage*.
        _.bindAll(this, 'addOne', 'addAll', 'render', 'toggleAllComplete', 'filter');
        this.input = this.$('.new-todo');
        this.allCheckbox = this.$('.toggle-all')[0];
        this.mainElement = this.$('.main')[0];
        this.footerElement = this.$('.footer')[0];
        this.statsTemplate = _.template($('#stats-template').html());
        Todos.bind('add', this.addOne);
        Todos.bind('reset', this.addAll);
        Todos.bind('all', this.render);
        Todos.bind('change:completed', this.filterOne);
        Todos.bind('filter', this.filter);
        Todos.fetch();
        // Initialize the router, showing the selected view
        var todoRouter = new TodoRouter();
        Backbone.history.start();
    }
```
### E. Initial State
- The initial condition is only that the app is runnning. When the test runs, it adds text to the input field which mean that even if it had text, it ould still add an item to the todo list though it may be giberish to a human. It then checks based on the result of after the item is submitted and what state the prgram is in.
### F. Transition
- The program test simulates adding an item which is like hitting the enter key (there is no submit button) to add the item. 
### G. Expected State
- The expected state of this test is only that the input text box is cleared at the end of the test after the item has been submitted.

