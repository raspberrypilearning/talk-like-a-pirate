## Using regular expressions to alter words

So how does the computer know which word we want to replace and what to replace it with? Remember the line of code we wrote to replace "hello" with "ahoy":

```JavaScript
words = words.replace(/hello/gi, "ahoy");
```

You might have wondered why we had to write `/hello/gi` for the word to find, and only `"ahoy"` for the word to replace it with. Why is that? The answer is that to specify the sequence of characters we are looking for, we are actually using something called a **regular expression** (sometimes called a **regex** for short).

A regular expression is a way of specifying a particular sequence of characters to look for in a piece of text.

- The characters we are searching for are put between the slashes `/`, so in this case we are just searching for the word `/hello/`.
- The `g` after the second slash means **global**: we are telling the code to replace the word `hello` with `ahoy` **every time it is found**. If we did not put a `g` here, only the first `hello` found would be replaced.
- The `i` means **case insensitive**: we are telling the code that we don't mind if it finds `Hello` or `HELLO` or even `hELlo'`. All of these will match and will be replaced with `ahoy`.

Regular expressions are extremely powerful: not only can they match exact sequences of characters like `hello`, they can also be used to match patterns of characters. There is a good [guide on how to create a regex](https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Regular_Expressions), but we will explain some examples that you could use in your pirate text generator to get you started:

- You could use the regex character `^` (Shift + 6 on many keyboards) which means "the start of the text". This code will insert the line `"Arr, me hearties. "` at the start of anything you type!
  
  ```JavaScript
  words = words.replace(/^/, "Arr, me hearties. ");
  ```

- You could use the regex `/(\w+)ev(\w+)\s/g, "$1e'$2 "`. This one is a bit trickier, so we'll break it down:

  - `\w` - Matches any single alphanumeric character (so any letter, number, or underscore)
  - `+` - Matches the previous pattern one or more times
  - `\w+` - ...So together they mean **any** one or more alphanumeric characters

  - `()` - Brackets around any part of a regex mean "save what was matched so we can use it later"

  - `ev` - This is just the normal letters e and v. (Notice that the `\w` had a backslash character to show that it means something different to a normal letter w.)
  - `\s` - This means a single space character
  - `/g` - We already know that the `g` means to match all the instances where this pattern is found

  So, to explain this regex in plain English: "Find ALL matches containing any one or more letters/numbers (and remember them), then the letters ev, then any one or more letters/numbers (and remember them), then a space".

  So this would match any words containing the letters ev such as n**ev**er or what**ev**er, as long as they are followed by a space. Of course, pirates say "ne'er" instead of "never", so we tell the program to reconstruct the word, but with an apostrophe instead of the v.

  - `$1` Means what was matched by the first brackets, `$2` means the second brackets, and so on...

  In the case of the word "never":
  
  - `$1` would equal `n` (all letters/numbers up to but not including "ev")
  - `$2` would equal `er` (all letters/numbers after "ev")
  - So `"$1e'$2 "` means "the first saved string (n), then e', then the second saved string (er)", which equals `ne'er`.

  You might be wondering why we didn't just look up and replace all instances of letter `v` with an apostrophe? Firstly, we wouldn't want to replace the letter `v` at the start of words, as we would end up saying things like `'oyage` instead of `voyage` which doesn't make much sense. We also don't want to replace the letter `v` in the middle of words if it doesn't have an `e` before it, otherwise we would end up with `shi'er me timbers` which just isn't what a pirate would say.

  Here is the finished code:

  ```JavaScript
  words = words.replace(/(\w+)ev(\w+)\s/g, "$1e'$2 ");
  ```
  
  Here is our finished pirate text generator with both of these regular expressions demonstrated, as well as some other pirate word replacements.

  ![Finished pirate](images/finished-pirate.png)


