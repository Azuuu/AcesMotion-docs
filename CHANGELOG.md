# Changelog

What changed in each release of AcesMotion, newest first.

## 0.14.2 (2026-10-23)

### New

- Hide while playing (on by default, in the View menu and Settings > Gizmos): while the scene plays, the gizmo, joint dots, bones, highlights, the trail, guides and camera frustums step aside so you watch the animation alone.
- Stack rows (a button on the rows header, View, the rows filter menu, Settings > Timeline; each row also has its own stack button beside Mute, to hide one row while it's on or show one row while it's off): turn it off to hide the generator, constraint and driver lanes under their rows, so you animate keys alone and a box select takes keys only. The blocks keep playing.
- Select several rows and right-click one: Add constraint and Add driver put the pick on every selected row in one undo step, as Add generator already did, with its target picked once for all of them.

### Fixed

- Duplicating a block on a stack row (a generator, constraint or driver) puts the copy in the sub-lane below at the same time, instead of after the scene's end where it couldn't be seen.
- A stack row is as tall as the sub-lanes its blocks use: a lone block moved to a lower lane no longer leaves empty lanes above it.
- IK posing on a custom R6 rig bends the arm or leg you drag instead of swinging the whole body: limbs named without the space (LeftArm, RightLeg) were taken for held props, and moved their holder, the torso. An IK chain set longer than the limb never takes the rig's root joint either.
- A Lock holds an R6 foot or hand: a limb that is one joint turns at the hip or shoulder to keep its end on the spot, instead of keeping its angle and sliding with the body.
- Posing a rig at its locks' first frame keeps every locked foot planted: a lock with no Spot yet gets the spot it holds before the pose moves anything, so posing the hips no longer drags it along.

## 0.14.1 (2026-10-23)

### New

- Scenes play on rigs in a ViewportFrame, such as an inventory card or a reveal. A card is judged by how it shows on screen instead of by the world camera: it rests while hidden, disabled or scrolled out of its list, MaxDistance leaves it alone, and copies the scene spawns stay inside the card.

### Improved

- Custom generators, constraints and drivers keep their id under their own attribute: AcesMotion_GeneratorId, AcesMotion_ConstraintId and AcesMotion_DriverId. Modules made earlier keep working; their AcesMotion_ActionId is still read and copied over the next time the plugin touches them.
- A custom action whose Scrub errors in a game now warns once in Output, as it does in Studio.
- A custom constraint whose Solve errors or returns no CFrame warns once in Output, like generators and drivers.
- AcesMotion.Cast accepts a typed list such as { Model } for a list role under --!strict.

### Fixed

- After a PlayForAll, the server puts an NPC where players saw it end, Motion Warp and attach keys included, and a prop the scene carries and drops lands where it was dropped instead of staying behind on the server.
- With MaxDistance set, a scene that drives the camera keeps playing however far its anchor is, instead of freezing the view.
- Dragging a handle in the Ease window updates the curve, the fields and the scene as you drag, not only when you let go.
- Curves no longer draw flat on their zero line when the curve editor is zoomed out to a wide range of values (0 to 100 degrees in a short graph).
- Destroying a Track also disconnects LengthChanged, CameraAttached, CameraDetached and ShotChanged.
- A custom driver with a required target left unset changes nothing, like the built-in drivers, so the value under it plays.
- A custom generator can have its own Low, High, Speed or StepRate setting: the Between Low and High, Scroll and Pattern modes keep their values apart from it.

## 0.14.0 (2026-10-23)

### New

- Screen effects: add them from the + menu, the Cast tab or the Camera row, then key letterbox bars (top and bottom), a vignette, blur, a fade to any colour, colour correction and bloom. Studio shows them while you look through a camera, and games draw them on the player's screen while a scene has the camera, easing in and out with it.
- Depth of field per camera: a Lens section with focus distance, Focus on (an actor or part the focus follows), in-focus radius and near and far blur.
- Hold / Fade, a new generator, and Screen effects presets in the Library: Fade to black, Fade from black, Flash white, Letterbox and Vignette pulse. The Screen row's menu adds fades, a flash and letterbox bars at the playhead.
- A fighter's point of view: attach a camera to a head from its Camera section and press Eyes. In games it follows the head as it really moves, the game's own animation included.
- Scriptable cameras for games: Camera = "Manual" works the scene's camera out without touching the player's, read with GetCamera (its screen effects and lens too), with AttachCamera, DetachCamera and the CameraAttached, CameraDetached and ShotChanged signals.
- Camera in game: press the Camera row to set how a game's camera glides into the scene and back out, with its own ease, and what happens when the scene is stopped early.
- Reorder actors by dragging them in the Cast tab or on the Timeline. A scene can keep its own Timeline order.
- OKLab and OKLCH colour blends for colour tracks and the gradient editor: colours fade from one to the next in even, natural steps.

### Improved

- Cameras turn like a camera head: the rotate gizmo pans and tilts without rolling, and pans and orbits blend smoothly between keys.
- Menu items that don't explain themselves have tooltips.
- Settings > Audio > Peak sensitivity sets how quiet a waveform hit can be and still snap.
- The Sequence editor opens taller.

### Fixed

- A camera in a scene that measures root motion from each actor's root part no longer tilts up or rolls between keys, and plays in Studio as it does in games.
- Posing a Lock's target moves the locked part with it, also at the lock's first frame.
- Reset to default works on screen effect and lens values.

## 0.13.0 (2026-10-22)

### New

- Scene versions: Alt+Shift+S or the Hub's new History tab saves a version of the scene, and automatic ones are kept as you work, on open and close, before exports and before heavy edits. Preview one read-only, Compare it as a ghost with faint keys while you work, Restore the whole scene or only the selected actors, or Branch it into a new scene.
- A dot after the scene name marks changes no version you saved holds, in the Timeline, the Hub and the scene lists.
- Toasts show what happened in the window you work in, with Undo and other actions where they help. Click the status bar's message for the recent ones; Settings > Look sets how long they stay and where.
- Save as asks for the copy's name and opens the copy.
- Pose library: save poses for any rig, apply them with a click or a slot key (Alt+1 to Alt+9), blend toward one with an Alt drag, and find one fast with the quick pose picker (Ctrl+Alt+P). Poses are yours and travel with Export presets.
- Locks: plant a foot or hold a hand where it is, in the world or on another actor, while the rest of the body moves. Lock between selected keys, Shift+L on a picked part, or turn pins into locks; posing a locked part keys where the lock holds it, so one lock can run the whole timeline. Chain length, Spot only and a viewport marker that turns red when the limb can't reach. Locks play in games and export natively.
- Let the prop lead: key a held sword's swing and the arm follows it.

### Improved

- Bars (constraints, generators, drivers and action blocks) no longer add main keys, so a main key moves only keys.
- Copy and paste is context aware: a copied block pastes onto the selected block or row.
- Export presets puts a folder in ServerStorage and selects it, and Import presets reads the export selected in the Explorer.
- Settings > Versions sets automatic versions and how many this place keeps.

### Fixed

- Keying on a layer, or on Base under layers, keeps the pose you see instead of adding the layers above on top of it.
- Keys sit centred on the playhead line at every zoom and UI scale.
- A Floor on a rig measures its pose at that frame, keeps a locked foot on the floor instead of lifting the rig early, and Bounding box now counts each part's box.
- A block dragged past the scene's end can be dragged back.

## 0.12.0 (2026-10-21)

### New

- Scene layers: animate on top of Base with Override or Additive layers, each with a keyable Weight, a mask, Mute and Solo. Manage them in the Hub's Layers tab and switch with the toolbar's layer picker; the Timeline shows one layer at a time.
- Posing on a layer saves what you see: an Additive key holds the difference from the layers below, an Override key the blend that lands on your pose.
- Show other layers draws the other layers' keys as faint dots for timing. Merge down and Bake to Base fold layers without changing the pose.
- Layers play in games as in Studio, and options.Layers or Track:SetLayerWeight fades a layer by name. Native export bakes the layers in.
- A Gizmos page in Settings gathers every gizmo, bone and joint dot setting, with bone colour, thickness and transparency and joint dot colour, size and transparency.
- Every colour setting has a colour picker: click its swatch.

### Fixed

- A joint turned past 90 degrees about one axis keeps that turn instead of flipping to a half turn on the other two, so rigs no longer roll between keys. Turns past 180 degrees and whole turns keep going the way they were turned, in keys, bakes, merges, imports and exports.

## 0.11.0 (2026-10-21)

### New

- Held props ride a joint in games: a part or model attached to a hand costs nothing per frame. Unanchor, Massless and Non-colliding switches in the Attached group say what it is while held, and attaching an anchored prop offers to unanchor it.
- Command palette: press F3 to find and run any command, with your recent ones first.
- Every shortcut can be rebound in Settings, and Settings has a search across all of its pages.
- Right click in the viewport for a menu of posing, keying and attach commands.
- Tween slider: blend the picked joints between their keys into Breakdowns.
- Solo rows and actors in the editor, and set what a curve does before and after its keys: Hold, Cycle, or Cycle with offset.
- Copy and paste blocks, Camera switch keys and attach keys. Presets drag from the Library onto Timeline rows.
- Select keys before, after or at the playhead, by key type, or inverted. Selected keys show a Key panel in the Inspector.
- Gizmo drags take typed amounts, X, Y and Z axis locks and a Shift fine drag. An Arrow length setting, with shorter arrows by default.

### Improved

- The gizmo's hit areas grow with its size, the nearest handle wins, and handles fade out edge-on. Joint dots inside the trackball take the click.
- Viewport dots, trails and guides are drawn like the gizmo, with a faint copy on top, and can show for selected actors only or hide with Hide overlays.
- Alt flips snapping for one drag, and frame snapping holds with Snap off. Auto-key on shows in record red.
- Esc or a right click cancels any Timeline drag or viewport pick. Undo and redo bring the selection back, and every undo step is named AcesMotion with what it did.
- Shorter menus, every shortcut named in its menu or tooltip, and Inspector panels remember their folded sections.
- The trail can show a range around the playhead with a frame tick step, and the property list can show animated properties only.
- Renaming an actor renames everything that names it, and crash recovery keeps a copy per scene.

### Fixed

- Delete, Backspace and Esc reach markers, rows and the Inspector, locked keys stay selected with the reason, and removing an actor says what it leaves.
- Tangent modes keep Broken shapes, normalised curves hold their fit while dragging, and the graph picks the nearer of a key and a tangent knob.
- A sound's Stop at follows the ruler's units, and what rides an actor follows its root generators in games.

## 0.10.0 (2026-10-18)

### New

- A scene played on a moving part or attachment rides it: the Anchor is followed every frame, for every player. FollowAnchor = false reads it once, as before.
- Camera blends: a switch key's Blend glides into its shot from the camera before it (in Studio's look through too), and CameraBlendIn and CameraBlendOut glide from the player's camera into the scene and back.

### Improved

- Motion Warps, spawned actors and attached props cost much less to play in games: far ones pose less often, an attached prop poses with what it rides, and a looped scene reuses its spawned copies.
- A target the scene doesn't move, like a walking NPC or a player, is read where it stands now, so warps follow it and props stuck to it go with it.
- Far crowds look smoother: on computers and consoles everything within 80 studs poses every frame, then 30, 20 and 12 times a second out to 320 studs and beyond, and level of detail starts at 64 actors on screen. Phones keep the lighter settings.
- The camera's glide back after a scene follows the player's camera wherever the character went, even while it walks.

### Fixed

- A Per target volley lands each copy on its own target in games and in Studio (they all flew to the first one).
- In games a dropped object stays where it was when it dropped, even when the target or the anchor isn't where the stand-in was.
- A Motion Warp that ends on a target hands the actor over to an Attach or Detach key after it, so a sticky shot can drop later.

## 0.9.2 (2026-10-18)

### New

- Motion Warp path shapes have their own settings: Turns for a Spiral, and Zig-zags and Corner smoothing for a Zig-zag. Bake shape to keys follows them.

### Fixed

- A spawned actor's preview copy no longer blinks off at some playheads (in games, a spawn no longer copies an earlier copy).
- Redo brings back a camera added at view, with its preview camera.

## 0.9.1 (2026-10-18)

### New

- Cameras you add at view are virtual: they live in the scene's data, show as a temporary Camera while the scene is open, and leave nothing in your place when it closes. In games they drive the player's camera.

### Improved

- A selected Motion Warp that bends joints no longer slows Studio down; its path follows a key drag with fewer points and draws exactly again when you stop.
- Dragging many keys in the curve editor is much smoother. Past 500 keys the curves follow the drag and the rest catches up when you let go.
- Scrubbing, playback, posing and the idle viewport do less work every frame, most of all in big scenes and with a motion trail, onion skins or drivers on.
- Motion Warps and attached props cost less to play in games.

## 0.9.0 (2026-10-17)

### New

- Motion Warp: animate a trip once against the stand-ins and it lands on the real target in games, wherever that is. Add it from an actor, root or joint row.
- Path shapes (Lob, High arc, Spiral, Zig-zag, Straight) fly live, and Bake shape to keys writes one into keys. Click the curve's diamond for its arrow (Arc) and drag the diamond along its circle (Arc turn).
- Ease a trip: select a Motion Warp bar and press E. Timed By speed, a far target takes longer and what comes after waits.
- Bends: a warp can bend a rig's joints so a hand, a claw or a head reaches the target, or bend the path and the joints together.
- Repeat a spawned actor: one copy per target in a game list, or a count spread round an axis or at random, with a stagger.
- Hit-stop: a marker's Hold freezes the scene (or one actor) for a few frames, with an optional camera kick.
- New generators: Overshoot / Settle and Stepped. The Library has a Warps tab of presets.
- Spread works on whole actors: spread a column of main keys to offset each actor's keys, blocks and markers.

### Improved

- Viewport guides, motion trails, camera frustums and bones draw like the posing gizmo, solid and easy to see.
- Selecting a joint row shows that part's properties; the root row shows the root part. Instance attributes show in the Inspector.
- Adding a camera at view puts its shot on the Camera row, and right clicking the Camera row can remove it.
- The Timeline toolbar keeps to two rows when it fits.

### Fixed

- Box select picks up keys on a block's setting rows, and clicking one shows its block in the Inspector at that setting.

## 0.8.0 (2026-10-17)

### New

- Drivers: set a property, a joint or one of its axes from something else. Copy a property, or map a distance, an axis, a speed or a property onto it, with a shape, a clamp and Smooth.
- A driver's Inspector panel has Capture buttons for its ranges and a mapping graph you can drag. Add a driver from a row, a lane or a property, or copy a property and Paste as driver.
- Copy drivers on joints copy a pose or a placement, all of it or the axes you tick.
- Colour ramps, viewport guides, custom driver modules tagged AcesMotionDriver, presets and the Library's Drivers tab.
- Keys too close to tell apart draw as one group key bar, and stacked main keys draw as an amber bar. Zoom in and they split.

### Improved

- Big scenes stay smooth: thousands of keys, key groups and blocks pan, zoom, scroll, select and drag at full speed. Moving more than 500 keys or blocks slides them on the Timeline and applies the move when you let go.
- Posing in FK and IK with the motion trail on is much lighter.
- Time fields in the Inspector and the Hub follow the ruler: seconds when it shows seconds, frames when it shows frames.
- The amber triangle on an actor's row is now called a main key. A group key is the bar of keys that act as one.
- The Hub opens taller.

### Fixed

- Selecting a constraint on the Timeline shows its viewport guide.

## 0.7.1 (2026-10-16)

### New

- Settings > About shows the full changelog, every release, under its buttons.
- A Settings button on the Open a scene card, so Settings is one click away with no scene open.

### Improved

- Studio checks for updates every 30 minutes while it stays open, and notes a new version in Output too.
- Settings fits a larger UI size: the page list scrolls, and a setting's control moves under its name when the row is too narrow.

### Fixed

- A place whose runtime is synced from files no longer calls it out of date.

## 0.7.0 (2026-10-16)

### New

- The first team release, on the Creator Store. Studio tells you when an update is out.
- Settings > Export: the export options every scene starts from.
- Settings > Versions: turn the update check and What's new on or off.
- Settings > Timeline: the frame rate new scenes start at, row height, plain or typed key shapes, the playhead snapping to keys, and how fast the wheel scrolls rows.
- Settings > Audio: how tall waveforms draw.

### Improved

- A thousand animated props play at a fraction of the cost: the parts a frame moves go in one bulk move.

## 0.6.5 (2026-10-16)

### New

- Level of detail only for crowds: with up to 50 characters on screen, every one moves every frame. Past that, far ones step gently, more so the bigger the crowd.

### Improved

- Nearby characters always move every frame, even when the frame budget is tight, and far ones never drop below 10 poses a second.
- A zoomed-in camera counts characters as closer.
- Characters stay spread over frames after a hitch, so a crowd doesn't stutter all at once.

## 0.6.4 (2026-10-16)

### New

- Level of detail in games: characters off screen stop posing and far ones pose less often, while their markers and events stay on time. A frame budget keeps crowds within a few milliseconds, lower on phones.
- The Important play option keeps a hero, a boss or a close-up smooth at any distance.

### Improved

- Crowds playing the same scene share their work, and scenes with nothing to do skip whole frames.

## 0.6.3 (2026-10-16)

### New

- Emotes and moves played on a player's own character from their client show for every player, like Roblox's own animations. The server checks the player owns what they animate.

### Improved

- The runtime plays scenes about four times faster, with far less memory churn: crowds of NPCs, cutscenes and emotes all cost less each frame.

## 0.6.2 (2026-10-16)

### New

- The Ease window: the ease popover is now a floating window that follows your key selection, with a foldable curve, the presets you used last and every preset one click away.
- Floor on an actor's root row can hold up all its parts, its feet, hands, limbs or parts you pick, by lifting the actor or bending the limbs.
- Floor can measure from a part's pivot or its bounding box.

### Improved

- The Timeline stays smooth with thousands of keys: dragging, selecting, panning, scrolling and zooming, in the dope sheet and the curve editor.
- The curve editor's toolbar sits above the ruler, next to the search row.
- A joint's keyed properties and generators sit right under its row.
- Constraint guides show only for the constraints selected on the Timeline, and the move, rotate and scale gizmo steps aside while they do.
- Submenus stay open while you move to them.

### Fixed

- The Library sometimes wouldn't scroll until the pointer left the window.
- Curve editor keys drifted off their curves while panning up and down.

## 0.6.1 (2026-10-16)

### New

- The Hub: one window for Scenes, Cast, Layers, History, the Inspector and the Library.

### Improved

- The Inspector lists a pick's properties first and the actor sections after them; a pick about the rig scrolls to them.
- Editing a custom action, generator or constraint shows the change in Studio's preview at once.
- Every image the plugin shows is public, so icons draw for everyone.

## 0.6.0 (2026-10-16)

### New

- Constraints: Track To, Damped Track, Locked Track, Copy Location, Copy Rotation, Copy Transforms, Limit Location, Limit Rotation, Limit Distance, Floor, Delay, Face Motion and Horizon Lock drive an actor's root or a rig's joints from other things, on top of their keys.
- They sit on the same lanes as generators and stack with them in your order: a camera's shake rides on top of its tracking. Influence, fades and their settings are keyable.
- Adding one picks its target straight away (or uses what's selected), and spans your selected keys, or a camera's current shot.
- Pose under a constraint: you edit the keys underneath and see the result. What it takes over greys out on the gizmo, and a Track To adds a Roll ring.
- Targets the game fills in: the local player, the nearest player, the player's camera or a tagged object, with a badge on the actor. Point targets aim at a spot you place and key.
- Distance fade on every constraint: full strength close by, fading out further away.
- Viewport guides show what each constraint does, with handles to drag its limits, distances and fades.
- Space and Relative to: measure a constraint's limits and axes from what it hangs from, its rest pose or any object you pick.
- Bake to keys takes the constraints above it along, and asks first when it would freeze something live. The Inspector's Stack section lists a row's stack in order, drag to reorder.
- Presets: Look at player, Turret, Level horizon, Bank into turns, Echo and your own, in the Library's new Constraints tab and in preset files.
- Custom constraints: ModuleScripts tagged AcesMotionConstraint, made from a typed template, live in Studio and in games.
- The runtime plays constraints live in games, and export bakes them into Roblox animations.

### Improved

- Fades on bars draw as one curve.
- Menus can show an icon on each item.

## 0.5.0 (2026-10-15)

### New

- Generators: Shake, Wiggle, Oscillate, Flicker / Strobe / Pulse, Spin and Recoil drive any value live over a span, on top of its keys, as blocks on a Generators lane under the row they drive.
- They drive numbers, vectors, GUI sizes and positions, colours, ranges, sequences, a rig's root and joints, and on/off values. Cycle / Flipbook steps through any list of values and Typewriter types out text.
- Blend each one by Add, Multiply or Replace, with Influence and fades, and key its settings: they show as rows under the block.
- Add camera shake on a camera actor in one click. Bake to keys writes a generator's result as keys.
- The generator panel in the Inspector has a live preview: Shape or Result, drag it to change size and timing, Shift+drag for a second setting, and pin it while you scroll. Pop it out into the Generator window.
- Drive modes: a colour along a gradient or in HSV, a number between Low and High, a position on an orbit, an on/off pattern, ranges and sequences moved, morphed or scrolled.
- Snap to Loop: a generator's speed snaps to values that loop seamlessly over its block, and Fit to playback range puts the block on the loop.
- Hold a channel a generator leaves alone at a number you type, and key it (S value 1 shows a hue cycle at full colour).
- Presets: built-in ones, your own from any block, and the Library's Generators tab. Preset files share ease and generator presets and saved colours, gradients and sequences with your team.
- Custom generators: ModuleScripts tagged AcesMotionGenerator, made from a typed template, live in Studio and in games.
- The runtime plays generators live, seeded so every player sees the same, and export bakes them into Roblox animations.
- The curve editor draws a generator's result faded over the keys it moves.

### Improved

- Much smoother playing, scrubbing and key dragging, above all with the Inspector open.
- Closed windows no longer cost any time while you edit.

## 0.4.0 (2026-10-14)

### New

- Audio lanes: the scene's own sounds (music, voice-over, ambience) on named lanes at the bottom of the Timeline, each with its own Mute, Lock and volume.
- Clips work exactly like sound bars: move, copy, trim, fade with shapes, loop, stretch, stack, scrub and snap to peaks, and they move together with your keys.
- Add a sound from the Explorer as a template (it keeps its volume and effects) or by its id, or add an empty clip and paste an id.
- Play a clip flat in 2D or in 3D from any part in the cast.
- The clip panel in the Inspector: timing, sound, volume, speed, trims, loop, fades and position. Select a lane for its own panel.
- The runtime plays audio lanes wherever the scene plays, starting partway on SetTime and late joins.

### Improved

- A sound bar's label starts after its fade in, so the fade line never crosses it.

### Fixed

- A sound at the start of a looped region plays on every pass, not only the first.
- Jumping back into a sound that already finished plays it again.

## 0.3.4 (2026-10-14)

### New

- Attach to (Shift+G): a part, joint, bone or whole actor follows anything you click, from the playhead, keeping its place. The grip is saved, so re-posing the hand carries the sword.
- Detach (Shift+Alt+G) drops it where it is. A rig joint detaches straight off its rig too: the torso no longer moves the arm, and its Motor6D stays.
- Back to rig (Shift+Alt+A) snaps a joint back into place, eased over a Blend; Back to rig where it is rejoins it without a jump.
- Attached rows on the Timeline: Attach, Detach and Back to rig keys with bands in the target's colour, menus, dragging, copying, and group keys that move them with the actor's other keys.
- The Attach panel in the Inspector works at the playhead like a property row, and every attached part shows an Attached section with its state and buttons.
- Attach to picking highlights what you hover, draws a line to it and names it; the gizmo hides while you pick.
- Moves by: a Model actor can move by one of its parts, so other designs with a part of the same name line up in game.
- IK through held objects: with IK on, dragging something a hand holds moves the arm. FK adjusts the grip instead.
- Clicking a welded part (an accessory, a held tool) picks the joint it's welded to. Pick welded parts turns this off.
- Attached joints bake into Roblox animations, and the runtime plays every attachment.
- Rigs always show a root row to key where the whole rig stands. Unkeyed joints (off by default) lists every joint as a row, keyed or not.

### Improved

- Joint rows follow the rig: parents before children.
- Shift+K or a double click on a rig's row keys every joint, even ones not keyed yet.
- Copy is Shift+C everywhere (keys, poses, property values).

## 0.3.3 (2026-10-14)

### New

- Camera actors: a frustum you pose with the gizmo like any actor; drag its blue dot or scale it on Z to change FieldOfView.
- Several cameras per scene, switched by keys on the Camera track at the top of the Timeline. The same switches play in game.
- Look through the live camera with Q. Move the view while paused to look away; scrub or play to snap back.
- Pilot camera (Ctrl+Shift+Q): fly Studio's view to move the camera you look through, keyed with auto-key.
- F turns a picked camera to look at what is under the mouse; Ctrl+F also levels its roll.
- Spawned actors act like real actors: a live copy is their stand-in, with their own Spawn row, Appear and Disappear keys, Parent to, Linger and Save look to template.
- The Hub is one window with Inspector and Library tabs that pop out, reorder and keep their order.
- Actor markers on an actor's row, and markers on one frame sit side by side.
- Key groups: group a row's keys into one bar that moves, copies and retimes as one.
- Convert an actor to a spawned actor and back.
- Fit scene length to a sound, and set the loop or export region from selected keys.
- Search in Settings > Shortcuts.
- The empty Timeline lists the place's scenes.
- A one-time notice when a scene uses features that need the runtime, plus an amber Runtime chip in the status bar.
- Toolbar layout: Two rows or One row, wrapping by width, with a More menu for what doesn't fit.

### Improved

- A sound's or emitter's bars re-measure when its properties change.
- Select several rows and mute or lock them all at once.
- Shift+Left and Shift+Right nudge selected keys.
- Library ease presets apply to the open sequence editor.
- Copy and paste property values between Inspector rows.
- Region handles light up on hover.

### Fixed

- The Library's Easing tab scrolls to its last sections.
- The sequence editor opens tall enough to use.

## 0.3.2 (2026-10-10)

### New

- Select an action block to edit it in the Inspector: its timing, every parameter its module declares (with each param's description as a tooltip), and its module with Open script and Select in Explorer.
- New parameter pickers: Actor, ActorPart (anything inside an actor, from a searchable list or by clicking it in the viewport or the Explorer), Joint, Template and Marker.
- Select a marker to edit its name, frame, colour and payload in the Inspector. Markers also fire OnEvent.
- Event blocks and markers share one payload table: named values of any type.
- Settings > Look: the object list can start expanded.

### Improved

- The Inspector's object list and every picker share one searchable dropdown.
- Open script brings an already open script's tab to the front.
- Group keys redrawn: even spacing, and a clearer look when some of their keys are selected.
- Marker lines are dashed and always draw above the grid.

## 0.3.1 (2026-10-10)

### New

- Action tracks on the Timeline: Event blocks and your own custom actions, as bars and chips you drag, trim, duplicate and delete.
- Custom actions are ModuleScripts tagged AcesMotionAction, wherever you keep them. New custom action makes one from a commented template.
- Actions run in Studio's preview as you play and scrub, loaded fresh each run so your edits apply right away.
- Action code gets the scene's time, frame, frame rate and speed, and can handle a cast change with Recast.
- Group keys include action blocks, and are now amber triangles.
- Drag stacked sound, Emit and action bars up or down to choose their lane.
- Settings > Actions.

### Improved

- Renaming or moving an action module keeps its blocks; Resolve target repairs a block whose module is gone.

## 0.3.0 (2026-10-10)

### New

- Animate any property: the Inspector lists every property by category with editors, drag to scrub and key diamonds; values that can't blend show as bars on the Timeline.
- Edits in Studio's Properties window are keyed with auto-key on.
- Emit() and Play() keys: sound bars with waveforms, trims, fades, speed, loops, audio scrubbing and snapping to waveform peaks.
- Effect preview: particles show while you scrub, with burst and stream bars and lifetime grips.
- Resize tool for parts and models, keyed as Size or Scale.
- Edit several objects at once in the Inspector.
- Colour picker, sequence editor and gradient editor windows with presets, saved colours, gradients and sequences, and their own undo.
- Settings: Look (accent colour, UI scale, tooltips), Shortcuts (every key, rebinding) and Storage pages; three icon styles.
- Crash recovery: a recovered copy is offered when a scene opens.

### Improved

- Add or remove actors and remove several tracks at once from the Timeline.
- Drag the top or bottom of a sound or effect row to make it taller.
- Move and rotate follow Studio's stepping settings.

## 0.2.0 (2026-10-09)

### New

- Posing: AcesMotion's own gizmo, pins, context IK, joint limits, mirror rules, pose tools and flip.
- Onion skin and motion trails you can edit, with pen, timing and limbs only modes.
- Curve editor: Channels and Ease views, split with the dope sheet, Euler filter and rotation modes.
- Ease tools: the ease popover (E), spread, presets built on animation principles, saved presets and the Library Easing tab.
- Export several rigs at once, as Roblox animations or as runtime scenes, and pack scenes for other games.
- Runtime: load a track, tune it and play it again and again; change its cast and options while it plays.
- Scenes can live in any folder.

### Improved

- Errors in one part of the plugin no longer break the rest.

## 0.1.0 (2026-10-08)

### New

- Plugin shell: Timeline, Hub, Inspector and Settings windows.
- Studio themed look with tooltips on every button.
- Runtime: play scenes in games with Play and PlayForAll, markers in server code, one click install.
