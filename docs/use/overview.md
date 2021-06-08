# CodeSee overview

Here's an overview to the primary features of CodeSee, including recordings, Data Flows, Stories, and sharing.

## Making recordings with the CodeSee button
<p class="block">
  <img alt="CodeSee button in browser" src="../../img/codesee_in_browser@2x.png" width="244" height="162" align="right">
</p>

If you see the CodeSee button when you run your app locally, you're ready to start using CodeSee.

- If the button is purple, it means you are logged in and ready to record. Click once to start recording, interact with your app, then click it again to stop recording.
- If it's red, click the button to log into CodeSee.
- You can click and drag the button to move it to another part of the screen.

Next, choose how much data you want to see in your recording.

- Verbose mode: Gets all of the runtime data, but it will take your recording a little longer to process. 
- Terse mode: Shows you a little less runtime data, but your recordings will be more performant.

Verbose mode is the default, and we recommend starting out in verbose mode as it provides you with the most insight into your application. If you have a large application, a data heavy application, or experience any performance issues, try terse mode. If you prefer to use verbose mode with a large or data heavy application, it helps to keep recordings as short as possible – focus on the one interaction you want to understand better. 

When you finish recording, CodeSee transmits the data to your CodeSee account (either hosted on our platform, or locally if you're using CodeSee Local). CodeSee then opens a new tab where you can view your recording. Larger recordings or slower networks can cause some buffering, so please wait for it to finish sending the recording to our servers.

!!! note
    If the delay is long enough, your browser's pop-up blocker may decide to block the page from displaying. You may want to change your settings to always allow pop-ups from the `app.codesee.io` domain. If the page is blocked, you can always go to [app.codesee.io/library](https://app.codesee.io/library) to see all your latest recordings.

## Understanding Data Flows

A Data Flow is a detailed timeline view of the code that ran during a CodeSee recording. The Data Flow is laid out in code execution order, meaning that it shows what order each function was called in regardless of what file the function is located in.

![CodeSee Data Flow](../../img/data_flow.png)

### Source code

- Source code that executed is displayed in the left-most column.
- The function name is located at the top left and the file path is located to the right.
- Any code that was skipped during execution is shown grayed out.

### Runtime data

* The Data Flow shows expressions in the center column and the value of each of the expressions at the time the recording was made in the right most column.
* When you hover over the expression in the center column it highlights the expression in the code in the left most column.
* When a function calls another function, you can explore it in more depth by clicking on the expand button `>` in the middle column to view the nested function.

### Loops

* If there is a loop, whether it's an explicit loop like a `for` loop or an implicit loop like `reduce`, you can visualize each iteration of the loop and the values of the data on each loop's iteration.

### Call stack

* When you are exploring a Data Flow, the current function that you are exploring sticks to the top so you're always aware which line of code is part of which function. If more than three functions are in the stack, a message appears to say how many functions are hidden.

### Side effects

* When you select **View** in the center column for a side effect, such as a network request, an inspector panel appears in the Data Flow. Here you can inspect details about any side effects that occurred.

### Filtering

* You can hover over any function name and click on the **•••** button to filter out and hide all occurrences of that same function by selecting **Exclude All - Filter out all instances**.


## Using Stories to capture your understanding

Stories allow you to annotate a Data Flow recording and add notes that are anchored to specific points in the code execution.

To create or view a story, open the story bar on the far right of the Data Flow screen.


## Sharing recordings and Stories

You can share your Data Flows and Stories publicly or with team members on the same domain. To bring up sharing options, select **Share** from the top of your recording, or the three-dot overflow menu on the library page.

From the **Get Link** pop-up, you can choose to change who can access your recording page, along with any Stories you've attached to the Data Flow. If you choos **Public**, anyone with the link can view the page. If you choose **Organization**, only CodeSee users registered with the same email domain as you can see the page.


## Editing recording titles

Select the ✏️ (pencil) icon to edit the title of your recording so you can refer to it later.

## Deleting a recording

Select the **•••** button, then select **Delete** to remove your recording permanently from your library. This deletes any Stories you've written associated with the Data Flow.

