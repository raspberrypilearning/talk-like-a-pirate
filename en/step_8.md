## Change text on key press

- It is always a good idea to include this check for whether the page has loaded in your jQuery programs, so that the page doesn't try to interact with elements which haven't loaded yet. However, we don't really want to pop up a box saying the page has loaded every time someone visits our page, so delete the line `alert("Page has loaded");` and instead paste in this code:

  ```JavaScript
  $("#normal").keyup(function(){
    var words = $("#normal").val();

    $("#pirate").val(words);
  });
  ```

  This code says:
  
  - `$("#normal")` - Referring to the textarea with the id `normal` (# means id)... (**identifier**)
  - `.keyup(` - When a key is pressed and let go... (**event**)
  - `function(){` - ...Execute the code inside this function... (**action**)

  What do you think the code `var words = $("#normal").val();` means? Can you break it down into parts?
  
  - `var words =` - We are making a variable called `words` to store some data.
  - `$('#normal')` - What is this identifier referring to?
  - `.val();` - This function means "the value of".

  Can you break down the line `$("#pirate").val(words);` and have a guess what it does?

  Predict what will happen when you save the code and type something into the Landlubbers box, then try it and see if you were right.

- If your code worked correctly, the same words you type in the Landlubbers box should appear in the Pirates box as you type. Although this is not the finished product, it is a good step forward because we now know how to make the contents of the `pirate` textarea change when something is typed in the `normal` textarea.

