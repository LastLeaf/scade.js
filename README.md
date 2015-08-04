# scade.js
Sequenceable and Cancellable Animation for DOM Elements

# What it does

* Manage series of animations for different "subjects" - a subject can be a property, an attribute, or anything that can be associated with a number. Subject manages the changes to this number.
* Animation series can be cancelled before they end so that new animation can be injected.
* In fact, it does not touch any DOM element directly. It only helps to manage complex and dynamic animation series, do interpolation, and sync animations between multiple DOM elements.

# API

`scade.getTime()`
Get current time.

`scade.createSubject(initVal, applyValFunc)`
Create and return a new subject, with an initial value `initVal`, and a callback function `applyValFunc` when the value changed.

`subject.add(options)`
Add a new animation to the subject. Options:
* `startTime` The start time of animation, default to the end of all pending animations of this subject (or the current time if no animation pending). Any running or pending animation at that point will be cancelled.
* `duration` The time length of the animation, default to 0.
* `fromVal` Expects the animation start from a value. If not, try to adjust `duration` to make the animation speed as it expects to be. Do not set this value if you do not need this behavior.
* `toVal` The target value when animation ends, default to `initVal`.
* `timing` The interpolation method. `scade.timing.linear()` and `scade.timing.cubicBezier(x1, y1, x2, y2)` are supported natively. The cubic-bezier works like it in CSS.
* `cancel` A function to be called when the animation is aborted before it starts. It is called when `startTime` reaches.
* `start` A function to be called when it starts. It may be called after `startTime`.
* `abort` A function to be called when it is aborted, after started.
* `end` A function to be called when it is normally ended.
 
`subject.abort([time])`
Cancel running and pending animation at a specific time (cancel now if not specified).

`subject.skip(duration)`
Skip animations for specified duration. Animations would be normally started and ended as if they have been run.

`subject.destroy()`
Destroys it. Frees the binding to animation frame generator.

# LICENSE

MIT
