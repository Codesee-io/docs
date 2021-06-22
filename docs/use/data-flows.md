# Getting Started With CodeSee: Anatomy of a Data Flow

When you record an interaction with CodeSee you create a Data Flow. A data flow is a detailed view of every line of the code that ran in that interaction.

### Icon legend

- ![Function Name and Path](https://codesee-docs.s3.amazonaws.com/back+end+tag.png) - Backend: This function connects to a function on the backend.
- ![Function Name and Path](https://codesee-docs.s3.amazonaws.com/go+to+execution+tag.png) - Go To Execution: Allows you to go to where the function is executed.
- ![Function Name and Path](https://codesee-docs.s3.amazonaws.com/network.png) - Network Request: Indicates a network request
- ![Function Name and Path](https://codesee-docs.s3.amazonaws.com/state_change2.png) - State Change: Indicates a React state change

### Execution Order

The CodeSee Data Flow is laid out in code execution order meaning that it shows what order each function was called in regardless of what file the function is located in.

### Code That Ran
The function name is located at the top left and the file path is located to the right of the function name

![Function Name and Path](https://codesee-docs.s3.amazonaws.com/01+-+Function+name+and+path.png)

### User Events on the Timeline

‍Every time you interact with your app via the mouse or keyboard, you can see what operations were triggered. Use the arrows to jump quickly to the next user interaction in the recording.

![User events in the timeline](../img/codesee-user-events-timeline.gif)

### Filtering

If you are overwhelmed by the information presented in the data flow or you want to remove some of the cruft in order to narrow down your focus, you can filter out functions by hovering over the ellipses and clicking **Exclude All - Filter out all instances**.

<!-- <iframe src="https://codesee-docs.s3.amazonaws.com/08-+filtering.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe> -->
![filtering functions](../img/cs-filter.gif)

### ‍Callback Go to Execution 

Understanding your code requires you to be able to follow the flow of execution from one function to the next and one file to the next. With CodeSee, you can instantly continue the flow of execution from a callback to where it’s executed with the click of a button. Using the **Go to Execution** menu that appears next to callback functions, you can jump to the points in the execution map where it was executed.

![Callback go to execution](../img/codesee-go-to-execution.gif)

### Runtime Data

The column on the right shows all of the values of the variables, functions, objects etc when you made a recording.

<iframe src="https://codesee-docs.s3.amazonaws.com/03-+Data.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe>

### Loops

If there is a loop, whether it’s an explicit loop like a for  loop or an implicit loop like reduce,  you can visualize each iteration of the loop and the values of the data on each loop’s iteration.

<iframe src="https://codesee-docs.s3.amazonaws.com/02+-+Loops.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe>

### ‍CodeSee.log()

Add CodeSee.log() where you want more visibility, record your app, and your data flow will have links in the right side bar that jump you directly to where each CodeSee.log() occurred. It’s like having a print statement... everywhere!

![CodeSee.log()](../img/codesee-log.png)

### Expanders

Most dev tools are organized in files and folders. Normally to understand what’s going on we have to mentally map how functions call each other. With CodeSee when a function calls another function don’t need to do this mental gymnastics, to see a function that calls another function, you can dive in that function by clicking on the expand button to see more about the called function.

<iframe src="https://codesee-docs.s3.amazonaws.com/04+-+expanders.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe>

### Call Stack

When you are diving in to a Data Flow, the current function that you are exploring sticks to the top so you always are aware of what line of code is part of which function. When that function is about to scroll off screen, we show you where the function ends. If you have nested functions, we show you the end of each function.

<iframe src="https://codesee-docs.s3.amazonaws.com/05-Call+Stack.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe>

### Side Effects

Sometimes your function does something that is beyond what that function was intended to do. For example, we write a function that takes X and doubles it, and it returns that doubling. Every time we call it with three, we’re going to get six, every time. But let’s imagine that whenever you call this function, something else happens like the number six getting written to a file or getting sent over the network, stored in a database, logged to disk or printed onto the screen. Those other events are called side effects. We think those side effects are really important in understanding how a program works so we highlight them in a special way. If a function has a side effect, it will be indicated as this function and to view that side effect, you can use the inspector simply by clicking view.

#### Inspector

<!--- need to create video for this --->
The inspector is like having x-ray vision into side effects. Right now we show you the behavior of Network Requests, the request and the response and data state changes, but we plan to show other side effects like  database calls and dom changes soon.

<iframe src="https://codesee-docs.s3.amazonaws.com/09+-+side+effects.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe>

### Expressions
JavaScript distinguishes expressions and statements. An expression produces a value and can be written wherever a value is expected, for example as an argument in a function call. Each of the following lines contains an expression:

    myvar
    3 + x
    myfunc("a", "b")

Roughly, a statement performs an action. Loops and if statements are examples of statements. A program is basically a sequence of statements (we’re ignoring declarations here). Wherever JavaScript expects a statement, you can also write an expression. Such a statement is called an expression statement. The reverse does not hold: you cannot write a statement where JavaScript expects an expression. For example, an if statement cannot become the argument of a function.

CodeSee shows you the statements in the left most column of the data flow, it shows you the expressions in the center column and the value of each of the expressions at the time the recording was made in the right most column.

### Code Highlights

When you hover over the expression in the center column it highlights the expression in the code in the left most column.

<!-- <iframe src="https://codesee-docs.s3.amazonaws.com/07-highlights.mp4" style="width:100%; height:340px; allow="autoplay;"></iframe> -->
![code highlights](../img/cs-highlights.gif)

### Data Search

You can search not only your code, but also your runtime data: the value of every variable and expression. Use Search in the top bar of your data flow to easily find any data, whether it’s a buggy value, an error message, or a specific user’s ID. All results will show up, even if they’re deeply nested in the call stack.

![Data search](../img/codesee-data-search.png)

### React State Changes

You can see each React state change (the value both before and after the change) directly next to your code in a data flow. You can examine not just the change but all of the code that led up to it. When you see the state change icon, click on “View” to see React state change details in the side effects panel. 

![React State Changes](../img/codesee-react-state-changes.gif)