# Flappy bird in Unity

A simple 2d game.
Source: https://www.youtube.com/watch?v=XtQMytORBmM

0. Install Unity Editor and WebGL. Visual Studio only if desired.

1. Create a new project of type `2D Core`.

2. Import assets (_Assets_ -> _Import New Asset_).

3. Create the bird object.
   a) _Hierarchy_ -> _Create Empty_, name `Bird`.
   b) Add graphics: _Inspector_ -> _Add component_ -> _Rendering_ -> _Sprite renderer_.
   c) Drag the bird _asset_ to `Sprite` property.
   d) In _Game_ tab adjust resolution to _HD_.
   e) Zoom out the _Main camera_ by changing `Size` property.
   f) Adjust the `Background` property.
   g) Add physics: _Inspector_ -> _Add component_ -> _Physics 2D_ -> _Rigidbody 2D_.
   h) Add collision: _Inspector_ -> _Add component_ -> _..._ -> _Circle collider 2D_. Adjust `Offset` and `Radius`.
   i) Add script: _Inspector_ -> _Add component_ -> _..._ -> _Script machine_. Purpose: jump up on _spacebar_.
   j) Create `Rigidbody` variable of type _Rigidbody 2D_.
   j) Drag the _Rigidbody 2D_ component onto the script's `Rigidbody` slot.
   k) Add handling of pressed _spacebar_. Set vertical speed of `Rigidbody` upon _key down_.
   l) Change speed nudge to a new variable.

4. Create pipes object.
   a) _Hierarchy_ -> _Create Empty_, name `Pipe`.
   b) _Pipe_ -> _Create Empty_, name `Top`.
   c) Add graphics: _Inspector_ -> _Add component_ -> _Rendering_ -> _Sprite renderer_.
   d) Drag the pipe _asset_ to `Sprite` property of _Top_.
   e) Add collision: _Inspector_ -> _Add component_ -> _..._ -> _Box collider 2D_.
   f) Drag up, keep `X` at 0.
   g) Duplicate (right-click), call it `Bottom`.
   h) Change `Y scale` to `-1`, move it down.
   i) Add script: _Inspector_ -> _Add component_ -> _..._ -> _Script machine_. Purpose: continuously move the pipe to the left.
   j) Create `Speed` variable of type _float_. Change `transform.position`.
   k) Remember `Time.deltaTime`.

5. Create spawner.
   a) Drag `Pipe` from _Hierarchy_ to _Assets_. Delete `Pipe` in _Hierarchy_.
   b) _Hierarchy_ -> _Create Empty_, name `Pipe spawner`.
   c) Move to the right of the visible area.
   d) Add script: _Inspector_ -> _Add component_ -> _..._ -> _Script machine_. Purpose: spawn pipes at certain intervals.
   e) Create `Pipe` variable of type _Game Object_.
   f) Drag the `Pipe` asset to the `Pipe` variable slot.
   g) Use `Instantiate`.
   h) Add the time-related functionality.
   i) Extract the spawning into a single place, spawn at start.

6. Distribute the pipes vertically.
   a) Create `Offset` variable of type _float_.
   b) Use `Random.Range` for `Y` coordinate of spawning.

7. Destroy the pipes.
   a) Destroy the pipe if `X` is less than something.

8. Score.
   a) Create UI -> Text. Set _Canvas Scaler_ -> _UI Scale Mode_ to _Scale with screen size_. Set _Reference Resolution_ to HD.
   b) Adjust the text. Do not use _Scale_ but size. Set default text to `0`.
   c) _Hierarchy_ -> _Create Empty_, name `Logic`.
   d) Add a _Script machine_ component. Variables: `int Score`, `UnityEngine.UI.Text Text`. Implement the event.
   e) Drag _Text_ from _Hierarchy_ to the variable.
   f) Add an empty object to the _Pipe_ prefab. Add _Box Collider 2D_, set _Is Trigger_.
   g) Add _Script machine_. Add a variable for the logic component.
   h) Add a tag (and set it) for the _Logic_ object.
   i) Implement the trigger.
   j) Set _Bird_'s layer (note the number). Add a layer check in the trigger script.

9. Game over.
   a) Add an empty object to _Canvas_, call `Game over`.
   b) In it, add a _Legacy_ -> _Text_ with `Game over` text. Adjust.
   c) Alongside, add a _Legacy_ -> _Button_. Resize. Change text of _Button_ -> _Text_ element to `Restart`.
   d) Set the click action to send an event.
   e) Add `RestartLevel` event handler in `Logic` object. Use `UnityEngine.SceneManagement.SceneManager.LoadScene()`.
   f) Disable `Game over`, add `GameOver` event handler to enable the object.
   g) In `Bird` script use a collision handler with a pipe 'whole'.
   h) Add a flag in `Bird` to disallow playback when dead.

10. Build and publish.

11. Additions.
   - Game over when the bird is off the screen.
   - Sound effects: add _Audio Source_ component to `Logic`.
   - Clouds: particle system.
   - Wing flap: _Window_ -> _Animation_.
   - Title screen: a new scene, remember to add to the build.
   - Save score: `PlayerPrefs`.
   