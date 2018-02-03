# Speech Synthesis

A page built to experiment with working with Chrome's speech synthesis API. Built for Wes Bos' [JavaScript 30](https://javascript30.com/) course.

[![Screenshot of the speech synthesis site](https://res.cloudinary.com/gerhynes/image/upload/v1517674755/Screenshot-2018-2-3_Speech_Synthesis_vpeom9.png)](https://gk-hynes.github.io/speech-synthesis/)

## Notes

### Speech Synthesis

First make sure that the voice, rate and text have name attributes that match them. This is so that the name of them lines up with the property on the utterance.

Create a new `SpeechSynthesisUtterance`, an empty array for the voices, and select everything else: the voice, the range, the textarea, and the speak and stop buttons.

Set `msg.text` to the value of the textarea.

Take the global variable speechSynthesis, add an event listener, and listen for the `voiceschanged` event.

Make a function, `populateVoices`, and override the `voices` array with `this.getVoices()`.

`Map` over all of the voices and set them as options in the dropdown.

```js
.map(
      voice =>
        `<option value="${voice.name}">${voice.name} (${voice.lang})</option>`
    )
    .join("");
```

Make another function, `setVoice`, to be called when a voice is selected from the dropdown.

You need to find not just the name of each voice but the corresponding `speechSynthesisVoice` object.

Use `find` to find where `voice.name` quals `this.value`.

Now make a function, `toggle`, so that every time you change an input the speech is restarted.

Inside toggle, cancel anything that is currently speaking and restart `speechSynthesis.speak(msg)`.

Make sure `toggle` is called at the end of `setVoice`.

Pass toggle a flag `startOver = true`, and use an if statement to check this within the function. This is so that you can later choose to not restart by calling `toggle(false)`.

Finally, listen for a click on the `speak` and `stop` buttons, and run `toggle`.

You can't just call `toggle(false)` because it'll just run on pageload. You can use `bind` or an inline function to get around this.

To filter for just Anglophone voices, inside `populateVoices` use `filter` and check if `voice.lang.includes("en")`.

### Manipulating the Speech

Add an event listener to each of the options, listen for the `change` event, and run a function called `setOption`.

Inside `setOption` set the property to be changed, `this.name`, to the value it is changed to, `this.value`.

```js
function setOption() {
  console.log(this.name, this.value);
  msg[this.name] = this.value;
  toggle();
}
```
