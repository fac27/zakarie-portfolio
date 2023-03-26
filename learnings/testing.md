## 1. Check that passing a given input into our tests returns the expected output

```javascript
test("Submitting a new task adds it to the list", () => {
  const oldLength = tasks.length;
  addTask({ task: "Wash dishes", taskstatus: false });
  const newLength = tasks.length;
  notEqual(newLength, oldLength);
});
```

Our first unit test for our **'add'** functionality. The test checks whether submitting a new task adds it to the list, <br />
and it expects that the new list length will be different from the old list length. If the test passes, <br />
it means that the expected output is returned when the given input is passed to the function being tested.

## 2. Write tests to mimic the behaviour of a user performing different actions

```javascript
// delete a task
test('E2E test: Deleting an entry removes it from the list', () => {
  const addNewTask = document.querySelector('.task-input');
  addNewTask.value = 'Go to the gym';

  const submitButton = document.querySelector('.add-task');
  submitButton.click();

  // select the last added element on the dom
  const resultElements = todoContainer.querySelectorAll('.todo-list');
  const resultElement = resultElements[resultElements.length - 1];

  const deleteButton = resultElement.querySelector('.delete-btn');
  deleteButton.click();

  // select the updated elements on the DOM and
  // check if the todo element no longer exists in the DOM
  const todos = todoContainer.querySelectorAll('.todo-list');
  const todo = todos[todos.length - 1];
  const todoText = todo.querySelector('.task');

  const expected = true;
  const actual = !(todoText.textContent === 'Go to the gym');

  equal(expected, actual);
});
```

The function above is one of our ***end-to-end (E2E) tests*** that simulates a user's interaction with the application. <br />
It is adding a new task on to the page, deleting it by using the <code>delete</code> button, <br />
and checking if it has been removed from the DOM. <br />

The test uses DOM manipulation to select and interact with different elements on the page, <br />
and the expected and actual outcomes are compared to see if our pieces of code work together as expected.

## 3. Write testable, modular functions

```javascript
// delete tasks from list and array
const deleteTask = (taskText) => {
  const task = tasks.filter((task) => task.task === taskText)[0];
  tasks.splice(tasks.indexOf(task), 1);

  todoContainer.innerHTML = '';
  tasks.forEach(updateTasks);
};

// edit tasks
const editTask = (taskText) => {
  const inputElement = document.querySelector('.task-input');
  inputElement.value = taskText;
  inputElement.focus();
};

// mark completed tasks
const toggleCheckbox = (taskText, status) => {
  const task = tasks.filter((task) => task.task === taskText)[0];
  task.done = status;

  const taskElement = Array.from(document.querySelectorAll('.task')).filter(
    (task) => task.textContent === taskText
  )[0];

  status
    ? taskElement.classList.add('done')
    : taskElement.classList.remove('done');
};
```

The functions <code>deleteTask</code>, <code>editTask</code>, and <code>toggleCheckbox</code> are all modular in that they perform <br />
specific actions and are self-contained. We can test them independently and are reusable in different parts of the codebase. <br />
By writing functions that perform a single, well-defined action, they are easier to read, maintain, and test. <br /><br />

These functions also do not rely on external *state* or mutable *variables*. <br />
Each function takes in *arguments* and returns a result based on that input, without mutating any external state. <br />
This makes it easier to write automated tests for these functions and ensures that they behave consistently regardless of external factors.

## 4. Write functions that add, remove or modify DOM nodes

```javascript
// add tasks
const addTask = (e) => {
  e.preventDefault();

  const taskValue = document.querySelector('.task-input').value;

  if (taskIsUnique(taskValue)) {
    const done = false;
    const task = { task: taskValue, done };

    tasks.push(task);
    e.target.reset();

    // clear the previous tasks first before updating
    todoContainer.innerHTML = '';
    tasks.forEach(updateTasks);
  } else {
    const erroDiv = document.querySelector('.error-div');
    erroDiv.innerHTML = '';

    const errorMessageElement = document.createElement('p');
    errorMessageElement.className = 'error';
    errorMessageElement.textContent = 'tasks must be unique';

    erroDiv.append(errorMessageElement);

    setTimeout(
      () => (document.querySelector('.error').style.display = 'none'),
      2000
    );
  }
};

const taskIsUnique = (taskText) => {
  return tasks.filter((task) => task.task === taskText).length < 1;
};

document.querySelector('.task-form').addEventListener('submit', addTask);

// delete tasks from list and array
const deleteTask = (taskText) => {
  const task = tasks.filter((task) => task.task === taskText)[0];
  tasks.splice(tasks.indexOf(task), 1);

  todoContainer.innerHTML = '';
  tasks.forEach(updateTasks);
};

// edit tasks
const editTask = (taskText) => {
  const inputElement = document.querySelector('.task-input');
  inputElement.value = taskText;
  inputElement.focus();
};
```

The <code>addTask()</code>, <code>deleteTask()</code>, and <code>editTask()</code> functions are all manipulate on the DOM in some way. <br /><br />

<code>addTask()</code> adds a new task to the DOM by creating a new DOM element, populating it with the task data, and appending <br />
it to the existing list of tasks.
<code>deleteTask()</code> removes a task from the DOM by finding the corresponding task element and removing it from the parent element.
<code>editTask()</code> modifies an existing task by setting the value of the input field to the task text and giving it focus,<br />  
allowing the user to modify the text.

## 5. Apply event listeners to HTML form elements

```javascript
const checkbox = domFragment.querySelector('#checkbox');
checkbox.addEventListener('click', () => {
  const [taskText, status] = getTaskText(checkbox, 'input');
  toggleCheckbox(taskText, status);
});
```

The code above attaches an event listener to an ***checkbox*** element and listens for the click event. When the checkbox is clicked, <br />
the <code>toggleCheckbox</code> function is called with the task text and status as arguments. The effect is that the text is visually shown as <br />
striken-through and funcionally the element is marked as **'done'** for filtering purposes.

## 6. Use scope to control what variables are accessible inside functions and blocks

```javascript
const getPendingTasks = () => {
  const newTasks = tasks.filter((task) => !task.done);
  todoContainer.innerHTML = '';
  newTasks.forEach(updateTasks);
};

const getCompletedTasks = () => {
  const newTasks = tasks.filter((task) => task.done);
  todoContainer.innerHTML = '';
  newTasks.forEach(updateTasks);
};
```

We have the same variable <code>newTasks</code> in both of the above functions but they are two distinct variables due to scope. <br />
Their scope is limited to those functions only. This means that they are not accessible outside of those functions, <br />
making our code more modular and less prone to errors caused by accidental modification of those variables outside their intended use.



<!-- ## 7. Use CSS grid to create complex layouts
## 8. Use CSS grid to make layouts that adapt to the viewport size -->
