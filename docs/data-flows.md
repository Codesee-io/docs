# Getting Started With CodeSee: Anatomy of a Data Flow

When you record an interaction with CodeSee you create a Data Flow. A data flow is a detailed view of every line of the code that ran in that interaction.   
### Code that ran
The function name is located at the top left and the file path is located to the right of the function name (screenshot)
  * Loops! If there is a loop, whether it’s an explicit loop like a for  loop or an implicit loop like reduce,  you can visualize each iteration of the loop and the values of the data on each loop’s iteration. (02-gif)
* Execution order
  * The CodeSee Data Flow is laid out in code execution order meaning that it shows what order each function was called in regardless of what file the function is located in (screenshot)
* Runtime data
  * The column on the right shows all of the values of the variables, functions, objects etc when you made a recording. (03-gif)
* Expanders
  * Most dev tools are organized in files and folders. Normally to understand what’s going on we have to mentally map how functions call each other. With CodeSee when a function calls another function don’t need to do this mental gymnastics, to see a function that calls another function, you can dive in that function by clicking on the expand button to see more about the called function. (04-gif)
* Call stack
  * When you are diving in to a Data Flow, the current function that you are exploring sticks to the top so you always are aware of what line of code is part of which function. When that function is about to scroll off screen, we show you where the function ends. If you have nested functions, we show you the end of each function. (05-gif)
* Side Effects
  * Sometimes your function does something that is beyond what that function was intended to do. For example, we write a function that takes X and doubles it, and it returns that doubling. Every time we call it with three, we’re going to get six, every time. But let’s imagine that whenever you call this function, something else happens like the number six getting written to a file or getting sent over the network, stored in a database, logged to disk or printed onto the screen. Those other events are called side effects. We think those side effects are really important in understanding how a program works so we highlight them in a special way. If a function has a side effect, it will be indicated as this function and to view that side effect, you can use the inspector simply by clicking view. 
  * Inspector
    * The inspector is like having x-ray vision into side effects. You can view details about the following side effects
      * Network Requests
      * others coming soon. 
* Expressions 
  * JavaScript distinguishes expressions and statements. An expression produces a value and can be written wherever a value is expected, for example as an argument in a function call. Each of the following lines contains an expression:
    myvar
    3 + x
    myfunc("a", "b")
  * Roughly, a statement performs an action. Loops and if statements are examples of statements. A program is basically a sequence of statements (we’re ignoring declarations here). Wherever JavaScript expects a statement, you can also write an expression. Such a statement is called an expression statement. The reverse does not hold: you cannot write a statement where JavaScript expects an expression. For example, an if statement cannot become the argument of a function. 
  * CodeSee shows you the statements in the left most column of the data flow, it shows you the expressions in the center column and the value of each of the expressions at the time the recording was made in the right most column.
* Code Highlights
  * when you hover over the expression in the center column it highlights the expression in the code in the left most column. 
* Filtering
  * If you are overwhelmed by the information presented in the data flow or you want to remove some of the cruft in order to narrow down your focus, you can filter out functions by hovering over the ellipses and clicking Exclude All - Filter out all instances