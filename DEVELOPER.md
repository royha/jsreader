# JavaScript Speed Reader 0.30 Developer Documentation

The JavaScript Speed Reader is a well-documented, self-contained, single-file, easy-to-use, speed reading program for use in HTML5 capable desktop browsers.

To try the JavaScript Speed Reader, click here: **[http://bit.ly/jsreader](http://bit.ly/jsreader)**.

## Design philosophy

The design of the JavaScript Speed Reader is to make it as easy to use as possible. To that end, all of the HTML, CSS, and JavaScript resides in a single, self-contained file. The file, which is the complete application, can just as easily be copied to or from a flash drive or hard drive, emailed, or hosted on a website by copying that one, single file. This simplicity is one key to the JavaScript Speed Reader's ease of use.

The other design philosophy of the JavaScript Speed Reader is to make the code easy to read and understand. Functions and variables are all extensively documented, and this document is designed to give a thorough overview of the code -- not just what is there, but how it works -- to make it easy for web designers and developers to understand and easily modify the JavaScript Speed Reader for whatever custom purpose they might desire.

## How to incorporate it on your website

The easiest way to add this to your website is to just add the `jsreader.html` file to your site.

The JavaScript Speed Reader uses the MIT license, so you can freely add it to your website, modify it as you see fit, and even make money on it if you wish.

## How does the JavaScript Speed Reader work?

How does this program choose the letter to highlight within each word?

Put simply, it multiplies the letter value of a word by a display position value to get a score, and then highlights the letter with the highest score.

The display position values are a pre-calculated curve. For every valid word length there is a value for each position in the word. As an example, for four-letter words, the values are 4 for the first position, 9 for the second, 7 for the third, and 3 for the fourth. For ten-letter words, the values are 1258984300. These values are stored in the `highlightCurveValue` array.

Each letter of the alphabet has a score from three to five, with higher values given to vowels and specific consonants. Numbers and punctuation have scores from 1 to 3. Letters are stored in the `highlightLetters` string, and the letter scores are stored as numerals in the corresponding locations in the `highlightLetterValue` string.

For a word, each letter value is multiplied by the corresponding display position value. As stated before, the `highlightCurveValue` is "4973" for four-letter words. Using the word "from", the letter "f" has a value of 3, and the first position has a value of 4, which gives a score of 12. The letter "r" is 3\*9 which equals 27, "o" is 5\*7 or 35, and "m" is 3\*3 which is 9. In this scenario, the letter "o" has the highest score of 35 and becomes the highlighted letter.

## Overview of the code

For the broader view, here is how the program works.

When the user clicks the play button (`startStopButton`), the `startStopReader()` function is called, which in turn calls the `startReader()` function.

The `startReader()` function prepares the JavaScript Speed Reader to start the reading process, including such tasks as preparing the timer to update the displayed word at the proper intervals using a `setTimeout()` timer that invokes `updateWord()` at the end of the timeout.

The `updateWord()` function gets the next word from the `nextWord()` function, then displays the word using the `displayWord()` function. The `updateWord()` function then sets `wordUpdateTimer` to the proper time span to keep the current word displayed. Note that the code is designed to display long words for a longer time than short words.

The `nextWord()` function parses the next word from the text in the `inputTextArea` text area and returns that word. If the word is longer than the `max_word_length` value (which is 13), then the `hyphenateWord()` function is called to separate out the long word with an appropriately placed hyphen, and returns the hyphenated portion that is less than `max_word_length`.

After `nextWord()` returns to `updateWord()`, `updateWord()` calls `displayWord()` with the new word.

The `displayWord()` function calls four functions: `padAndHighlightWord()`, `selectWordInTextArea()`, `updateProgressBar()`, and `displayWordsPerMinute()`.

The `padAndHighlightWord()` function takes the word to display, chooses which letter to highlight (as described above), then returns the appropriate HTML markup to display the word with the highlighted letter in a consistent location using a fixed width font. For example, if the word "reading" were passed to the `padAndHighlightWord()` function, `padAndHighlightWord()`would return the string "`&nbsp;&nbsp;&nbsp;&nbsp;re<span class="highlight">a</span>ding`".

The `displayWord()` function sets the return value from `padAndHighlightWord()` to `outputTextElement.innerHTML` to display the word.

The `selectWordInTextArea()` function scrolls the text area so that the current display word can be seen in context, then highlights that word by selecting it.

The `updateProgressBar()` function updates the progress bar beneath the display word to represent the current reading location.

The `displayWordsPerMinute()` function updates the `Words per minute:` display.

If there are no further words to display, the `updateWord()` function calls the `setStopState()` function to return the JavaScript Speed Reader to a stopped state.

## Contributions

I do not have plans to continue development on this project, except for fixing major bugs.

Will I accept contributions? Possibly, though I would prefer that you fork this project and make it your own.

If you want to contribute to this project, here are some features I want to add:

* Play/Pause/Resume combination button and a standalone Stop button. The current Start/Stop and Play/Pause buttons don't match any known player and is less intuitive than I would like.
* Expand to more written languages. Left to right languages are not supported, but I would welcome changes that include them.

What I want maintained in submitted changes:

* Keep the structure of the file so that it's easy to read and understand.
* Keep this speed reader to a single file which would include all HTML, JavaScript, and CSS.
* Clear and concise comments above each function to describe the summary of the function, the parameters, and return values.
* Comments within each function to describe the actions of the function.
* A comment on each variable to describe the use and purpose of that variable.

Contributions that do not maintain these standards are not likely to be accepted.