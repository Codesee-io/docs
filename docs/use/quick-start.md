# Getting started with CodeSee

Here's an overview to the primary features of CodeSee, including recordings, data flows, stories, and sharing.

## Making recordings with the CodeSee button
<p class="block">
  <img alt="CodeSee button in browser" src="../../img/codesee_in_browser@2x.png" width="244" height="162" align="right">
</p>

If you see the CodeSee button when you run your app locally, you're ready to start using CodeSee.

- If the button is **purple**, it means you are logged in and ready to record. Click once to start recording, interact with your app, then click it again to stop recording.
- If it's **red**, click the button to log into CodeSee.
- You can click and drag the button to move it to another part of the screen.

It helps to keep recordings as short as possible – focus on the one interaction you want to understand better.

When you finish recording, CodeSee will open a new tab for your recording once all the data has been transmitted. Larger recordings or slower networks can cause some buffering, so please wait for it to finish sending the recording to our servers.

- Note: If the delay is long enough, your browser's pop-up blocker may decide to block the page from displaying. You may want to change your settings to always allow pop-ups from the app.codesee.io domain. If the page is blocked, you can always go to [app.codesee.io/library](https://app.codesee.io/library) to see all your latest recordings.

## Understanding data flows

A data flow is a detailed timeline view of the code that ran during a CodeSee recording. The data flow is laid out in code execution order, meaning that it shows what order each function was called in regardless of what file the function is located in.

![CodeSee data flow](../../img/data_flow.png)

**Source code**

- Source code that executed is displayed in the left-most column.
- The function name is located at the top left and the file path is located to the right.
- Any code that was skipped during execution is shown grayed out.

**Runtime data**

* The data flow shows expressions in the center column and the value of each of the expressions at the time the recording was made in the right most column.
* When you hover over the expression in the center column it highlights the expression in the code in the left most column.
* When a function calls another function, you can dive in by clicking on the expand button `>` in the middle column to view the nested function.

**Loops**

* If there is a loop, whether it’s an explicit loop like a `for` loop or an implicit loop like `reduce` you can visualize each iteration of the loop and the values of the data on each loop’s iteration.

**Call stack**

* When you are diving into a data flow the current function that you are exploring sticks to the top so you always are aware of what line of code is part of which function. If more than 3 functions are in the stack, a message appears to say how many functions are hidden.

**Side Effects**

* When you click on the "View" button in the center column for a side effect, such as a network request, an inspector panel appears in the data flow. Here you can inspect details about any side effects that occurred.

**Filtering**

* You can hover over any function name and click on the `•••` button to filter out and hide all occurrences of that same function by selecting "Exclude All - Filter out all instances."


## Using stories to capture your understanding

Stories allow you to annotate a data flow recording and add notes that are anchored to specific points in the code execution.

To create or view a story, open the story bar on the far right of the data flow screen.


## Sharing recordings and stories

You can share your data flows and stories publicly or with team members on the same domain. To bring up sharing options, click on the **Share** button from the top of your recording, or the three-dot overflow menu on the library page.

From the **Get Link** pop-up, you can choose to change who can access your recording page, along with any stories you've attached to the data flow. If you make it Public, anyone with the link will be able to view the page. If you make it Organization, only CodeSee users registered with the same email domain as you will be able to see the page.


## Editing recording titles

Click the ✏️ (pencil) icon to edit the title of your recording so you can refer to it later.

## Deleting a recording

Click the **•••** button, then **Delete** to remove your recording permanently from your library. This will delete any stories you've written associated with the data flow.

