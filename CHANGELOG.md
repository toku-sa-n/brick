
Brick changelog
---------------

0.64.1
------

Bug fixes:
 * Fixed a bug where mouse clicks could fail to be noticed if
   "continueWithoutRedraw" was called.

0.64
----

API changes:
 * Added `Brick.Main.continueWithoutRedraw`, an alternative to
   `Brick.Main.continue` that does not trigger a screen redraw. See the
   Haddock and User Guide for details.
 * Added `Brick.Widgets.Core.putCursor` to support Vty's new (as of
   5.33) API for placing cursors without visually representing
   them. This change also updated `Brick.Forms.renderCheckbox` and
   `Brick.Forms.renderRadio` to use `putCursor` (thanks to Mario Lang
   for this work).

Other improvements:
 * `Brick.Widgets.Edit` now supports a few more Emacs-style keybindings
   (thanks Mario Lang):
    * `M-b` and `M-f` to navigate by word
    * `C-b` and `C-f` for consistency
    * `M-d` to delete word under cursor
    * `C-t` to transpose previous character with current character
    * `M-<` and `M->` to goto-beginning-of-file and end of file,
      respectively

0.63
----

API changes:
 * The `Viewport` type got a new field, `_vpContentSize` (and a
   corresponding lens `vpContentSize`) to get the size of the viewport's
   contents.

0.62
----

API changes:
 * `Brick.Widgets.Core` got new functions
   `crop{Left,Right,Bottom,Top}To`. Unlike the `crop...By` functions,
   which crop on the specified side by a particular amount, these
   `crop...To` functions crop on the specified side and take a desired
   overall width of the final result and use that to determine how much
   to crop. A widget `x` of width `w` could thus be cropped equivalently
   with `cropLeftBy a x` and `cropLeftTo (w - a) x`.

Other changes:
 * Added `programs/CroppingDemo.hs` to demonstrate the new (and
   preexisting) cropping functions.

0.61
----

API changes:
 * Brick.Forms got `editShowableFieldWithValidate`, a generalization
   of `editShowableField` that allows the caller to specify an
   additional validation function (thanks Ben Selfridge)

0.60.2
------

Bug fixes:
 * Widgets reported as `clickable` are now reported as clickable even
   when their renderings are cached with `cached` (#307; thanks Hari
   Menon)

0.60.1
------

Bug fixes:
 * `table []` no longer raises `TEUnequalRowSizes`.

0.60
----

New features:
 * Added `Brick.Widgets.Table` to support drawing basic tables. See
   `programs/TableDemo.hs` for a demonstration (`cabal new-run -f demos
   brick-table-demo`).

0.59
----

API changes:
 * `Brick.Widgets.List` got `listMoveToBeginning` and `listMoveToEnd`
   functions
 * `Extent`: removed the unused `extentOffset` field

Bug fixes:
 * Fixed a crash in the border rewriting code that attempted to rewrite
   empty images (#305) (thanks @dmwit)

0.58.1
------

Bug fixes:
 * Removed a defunct failing test from the List test suite

0.58
----

Package changes:
 * Updated dependency constraints to build on GHC 9.0.1 (thanks Ondřej
   Súkup)

API changes:
 * The FileBrowser module now exports individual functions for
   each of the events that it handles. This allows end users to
   trigger the behaviors directly rather than relying on the built-in
   `handleFileBrowserEvent` function. The documentation has been updated
   to indicate which functions are triggered by each key event. (Thanks
   David B. Lamkins)

Other changes:
 * The `List` module's `listFindBy` function now attempts to find a
   match anywhere in the list rather than just somewhere between the
   cursor and the end of the list.
 * The `FileBrowser` now positions a cursor at the beginning of the
   selected entry when the file browser is focused. (thanks Mario Lang)
 * The user guide's viewport visibility example got an important
   syntactic fix. (thanks Mario Lang)

0.57.1
------

Bug fixes:
 * Fixed a small space leak in the main rendering loop (#260)
 * Get `TailDemo` building on more versions of GHC

0.57
----

Package changes:
 * Raised lower bound on `vty` to 5.31 to get the new `strikethrough`
   style.

New features:
 * Added support for the `strikethrough` style in Brick theme
   customization files.

0.56
----

Package changes:
 * Increased upper bound for `base` to support GHC 8.10.2 (thanks Ryan
   Scott)

API changes:
 * Added `Brick.Forms.updateFormState` to update the state contained
   within (and managed by) a Form. This function takes care of the
   details of updating the form fields themselves to be consistent with
   the change in underlying state.
 * Added the overall window width (`windowWidth`) and height
   (`windowHeight`) to `Context`, the rendering context type (thanks Tom
   McLaughlin)

Other changes:
 * Added `brick-tail-demo`, a demonstration program for writing a
   `tail`-style output-following interface.
 * Updated `Brick.Widgets.ProgressBar` so that it handles near-endpoint
   cases more naturally (fixes #281)

0.55
----

Package changes:
 * Increased lower bound on `vty` dependency to 5.29.

Bug fixes:
 * `customMain` now restores the initial terminal input state on
   shutdown. This means that changes to the input state flags in the last
   `suspendAndResume` before program exit are no longer propagated to the
   end user's terminal environment (which could lead to broken or garbled
   terminal I/O).

0.54
----

API changes:
 * Exported `Brick.Widgets.FileBrowser.maybeSelectCurrentEntry` (thanks
   Róman Joost)

Other changes:
 * Added handlers for the `Home` and `End` keys to
   `Brick.Widgets.Edit.handleEditorEvent` (thanks Róman Joost)

0.53
----

Package changes:
 * Relaxed base bounds to allow building with GHC 8.10 (thanks Joshua
   Chia)

Bug fixes:
 * `vLimitPercent`: use correct horizontal size policy from child
   (thanks Janek Spaderna)
 * `str`: be more aggressive in determining how many characters to
   display (attempt to display as many zero-width characters as
   possible)

0.52.1
------

Bug fixes:
 * Attribute map lookups now merge styles in addition to merging colors
   (see `eb857e6bb176e119ac76f5e2af475f1b49812088`).
 * `txtWrapWith` now pads in the single-line case (see also
   `926d317c46b19d4e576748891a1702080287aa03`, #234, and #263)

0.52
----

API changes:
 * EventM now provides a MonadFail instance
 * EventM now provides MonadMask, MonadCatch, and MonadThrow instances
   (thanks Fraser Tweedale)

Other changes:
 * The FileBrowser now has support for vi-style bindings in addition to
   its previous bindings. New bindings include:
   * `j`/`k`: next/previous element
   * `C-n`/`C-p`: page down/up
   * `C-d`/`C-u`: half page down/up
   * `g`: select first entry
   * `G`: select last entry

0.51
----

API changes:
 * Added Brick.Focus.focusRingToList, which returns all of the elements
   in a focus ring as a list, starting with the focused entry and
   wrapping around (#257; thanks @4eUeP)

Bug fixes:
 * Fix Brick.Widgets.FileBrowser.fileExtensionMatch to match directories
   and also match symlinks that link to directories (thanks @YVee1)

Other changes:
 * Added demonstration program screenshot gallery (thanks @drola)

0.50.1
------

Bug fixes:
 * Fixed a bug where a self-referential symlink would cause the file
   browser to get into a loop and ultimately crash. (Thanks Kevin Quick)

API changes:
 * Added `Brick.Focus.focusRingLength` to get the size of a focus ring.
   (Thanks Róman Joost)

Other changes:
 * Updated Travis configuration and base dependency to support GHC
   8.8.1. (thanks Brandon Hamilton)

0.50
----

API changes:
 * Added `writeBChanNonBlocking`, which does a non-blocking write to a
   `BChan` and returns whether the write succeeded. This required
   raising the STM lower bound to 2.4.3.

0.49
----

New features:
 * The `FileBrowser` now supports navigation of directories via
   symlinks, so `Enter` on a symlink will descend into the target path
   of the symlink if that path is a directory. Part of this change is
   that the `FileInfo` type got a new file, `fileInfoLinkTargetType`,
   that indicates the type of file that the link points to, if any.

0.48
----

New features:
 * The `Edit` widget now supports `EvPaste` Vty events by default,
   assuming UTF-8 encoding of pasted bytes. If pasted bytes are not
   UTF-8-decodable, the pastes will be ignored. In any case, users can
   still intercept `EvPaste` events as before and handle them as desired
   if the default behavior is not desirable.

Other changes:
 * `txtWrapWith` now always pads its output to the available width to
   obey its `Greedy` requirement.

0.47.1
------

Bug fixes:
 * userguide: update stale Result construction
 * Added test case for List initial selection (thanks Fraser Tweedale)
 * Fixed build on GHC 7.10 due to RULES pragma formatting issue (thanks
   Fraser Tweedale)
 * Various CI-related fixes (thanks Fraser Tweedale)

0.47
----

API changes:
 * Changed `Brick.Main.customMain` so that it now takes an additional
   (first) argument: the initial `Vty` handle to use. This lets the
   caller have more control over the terminal state when, for example,
   they have previously set up Vty to do other work before calling
   `customMain`.
 * Added `Brick.Main.customMainWithVty`. This function is the same as
   `customMain` except that it also returns the final `Vty` handle that
   it used internally *without* shutting that Vty handle down. This
   allows the caller to continue using the terminal without resetting it
   after `customMainWithVty` finishes executing.

0.46
----

Performance improvements:
 * The box combinators `<=>`, `<+>`, `vBox`, and `hBox` got GHC rewrite
   rules that will optimize away redundant boxes. This change improves
   performance for chains of `<+>` or `<=>` as well as nested boxes
   using `hBox` and `vBox`. Previously chains of e.g. `<+>` produced
   binary trees of boxes that incurred more rendering overhead. Those
   are now optimized away.

API changes:
 * Data.Text.Markup: renamed `empty` to `isEmpty`

0.45
----

API changes:
 * List got a new `listFindBy` function (thanks Fraser Tweedale). This
   function uses a predicate to find a matching element in the list and
   move the cursor to that item.
 * Data.Text.Markup got a new `empty` function (#213)

0.44.1
------

Bug fixes:
 * `Brick.Markup` now properly renders empty lines in markup (#209)

0.44
----

API changes:
 * The `List` type got its container type generalized thanks to a lot of
   work by Fraser Tweedale. Note that this change is
   backwards-compatible with older Brick programs that use the `List`.
   Thanks to this work, the `List` now supports both `Data.Vector`
   and `Data.Sequence` as its container types out of the box and can
   be extended to support other sequence types with some simple type
   class instances. In addition, property tests are provided for `List`
   and its asymptotics are noted in the documentation. Along the way,
   various bugs in some of the list movement functions got fixed to
   bring them in line with the advertised behavior in the documentation.
   Thanks, Fraser!

0.43
----

API changes:
 * The FileBrowser module got the ability to select multiple files
   (#204). This means that the `fileBrowserSelection` function now
   returns a list of `FileInfo` rather than at most one via `Maybe`.
   The module also now uses a new attribute, `fileBrowserSelectedAttr`,
   to indicate entries that are currently selected (in addition to
   displaying an asterisk after their filenames). Lastly, the file
   size and type fields of `FileInfo` have been replaced with a
   new type, `FileStatus`, and `FileInfo` now carries an `Either
   IOException FileStatus`. As part of that safety improvement,
   `setWorkingDirectory` now no longer clobbers the entire entry listing
   if any of the listings fail to stat. In addition, the FileBrowser now
   uses the correct file stat routines to deal with symbolic links.

Package changes:
 * Added lower bound on `directory` (thanks Fraser Tweedale)

Test suite changes:
 * Test suite now propagates success/failure to exit status (thanks
   Fraser Tweedale)

0.42.1
------

Behavior changes:
 * File browsers in search mode now terminate search mode when `Enter`
   is pressed, resulting in better behavior.

0.42
----

New features:
 * Added `Brick.Widgets.FileBrowser`, which provides a filesystem
   browser for selecting files and directories. Read the Haddock
   module documentation and see the included demo program,
   `programs/FileBrowserDemo.hs`, for information on using the new
   functionality.

0.41.5
------

Miscellaneous:
 * `suspendAndResume` now empties the rendering cache when returning to
   the rendering event loop. This ensures that the state returned by the
   `IO` action is rendered completely rather than relying on potentially
   stale cache entries.

0.41.4
------

API changes:
 * Forms: added `setFormFocus` function to set focus for a form
 * Added `NFData` instances for `AttrMap` and `Theme` types (thanks
   Fraser Tweedale)

0.41.3
------

Bug fixes:
 * Lists now draw correctly without crashing due to a vector slice
   bounds check failure if their rendering area is too small (#195;
   thanks @andrevdm)

Other changes:
 * Relaxed base bounds to support GHC 8.6 (thanks @maoe)
 * Added towerHanoi to the featured projects list

0.41.2
------

Bug fixes:
 * Support STM 2.5 by allowing for `Natural` argument to `newTBQueue`
   (thanks @osa1)

0.41.1
------

New features:
 * `Forms`: added `checkboxCustomField` and `radioCustomField` to permit
   customization of characters used to draw selection state for such
   fields.

0.41
----

New features:
 * `Brick.Forms` got a new field constructor, `listField`, that provides
   a form field using a `List`.
 * `List`: added the `listMoveToElement` function for changing the list
   selection to the specified element, if it exists.

Package changes:
 * Now depends on vty >= 5.24.

Other changes:
 * `viewport`: fixed failable patterns for forward compatibility with
   GHC 8.6 (#183)
 * Add `Generic`, `NFData`, and `Read` instances for some types

0.40
----

New features:
 * Brick.Widgets.Core: added new functions `hLimitPercent` and
   `vLimitPercent`. These behave similarly to `hLimit` and `vLimit`
   except that instead of taking absolute numbers of columns or rows,
   they take percentages. (Thanks Roman Joost)

0.39
----

New features:
 * The `italic` keyword is now supported in theme customization file
   style lists. This requires `vty >= 5.23.1`

0.38
----

New features:
 * Added support for parsing `#RRGGBB` color values in theme
   customization files in addition to the color names already supported
   (thanks Brent Carmer). These values are mapped to the nearest
   reasonable entry in the 240-color space.

0.37.2
------

Bug fixes:
 * Theme customization files can now use empty lists for style
   customization.

0.37.1
------

API changes:
 * Exposed `Brick.Forms.renderFormFieldState`.

0.37
----

Behavior changes:
 * `listMoveBy` now automatically moves to the first or last position
   in the list if called when the list is non-empty but has no selected
   element (thanks Philip Kamenarsky)

API changes:
 * Added `Brick.Widgets.List.renderListWithIndex` that passes
   the index of each element to the item rendering function (thanks
   liam@magicseaweed.com)

0.36.3
------

Bug fixes:
 * Fixed a bug where mouse-up events in viewports were not translated
   into the global coordinate space, unlike mouse-down events (#173)

0.36.2
------

API changes:
 * The Forms API got two new functions, `setFormConcat` and
   `setFieldConcat`, used for controlling the previously hard-coded
   concatenation behavior of form fields. These are optional and both
   concatenation settings default to their former hard-coded values,
   `vBox` (#172).

0.36.1
------

Package changes:
 * Raised upper bound to support GHC 8.4.2 (#171)

Other changes:
 * Improved List accessor documentation (thanks liam <liam@magicseaweed.com>)
 * Brick.Main now uses a Set instead a list to track invalidation
   requests to avoid duplicates.

0.36
----

New features:
 * Dynamic border support: adjacent widgets that use borders can make
   those borders seamlessly connect to each other! Thanks
   so much to Daniel Wagner for this feature! Please see
   `programs/DynamicBorderDemo.hs` for a demonstration. Also see the
   "Joinable Borders" section of the User Guide.

0.35.1
------

 * Conditionally depend on semigroups for GHC before 8

0.35
----

 * Added support for GHC 8.4.
 * Updated travis build to test on all 8.x releases (thanks Peter
   Simons)

0.34.1
------

Bug fixes:
 * Fixed a bug where the "reverseVideo" style could not be parsed in a
   theme customization when it was all lowercase (thanks Yuriy Lazarev)

Documentation changes:
 * Guide: added more complete example of creating a default theme
   (thanks Mark Wales)
 * Guide: added offset to Extent pattern matching (thanks Mark Wales)

0.34
----

API changes:
 * Core: vLimit and hLimit now *bound* sizes rather than setting them.
   This was the original intention of these combinators. The change in
   behavior means that now `vLimit N` means that *at most* `N` rows will
   be available; if the context has less, then the smaller constraint in
   the context is used instead. Programs affected by this behavior will
   be those that assume that `vLimit` doesn't do this, but that should
   be very few or zero.

Other changes:
 * Dialog: now arrow keys no longer wrap around available buttons but
   stop at rightmost or leftmost button to avoid confusion when
   attempting to tell which button is selected in two-button dialogs
   (thanks to Karl Ostmo for this change)

Documentation changes:
 * Updated Haddocks for str/txt in Core to mention tab character
   considerations

0.33
----

API changes:
 * Forms: added support for external validation of form fields using
   `setFieldValid`. See the Haddock, User Guide, and FormDemo.hs for
   details.
 * Borders: removed all attribute names except `borderAttr` to simplify
   border attribute assignment.

0.32.1
------

Bug fixes:
 * Core: make all text wrap widgets Greedy horizontally

Miscellaneous:
 * Dialog: clarify purpose in documentation (w.r.t. #149)

0.32
----

API changes:
 * This release adds the new `Brick.Forms` module, which provides an API
   for type-safe input forms with automatic rendering, event handling,
   and state management! See the Haddock and the "Input Forms" section
   of the Brick User Guide for information on this killer feature! Many
   thanks to Kevin Quick for feedback on this new functionality.

0.31
----

Behavior changes:
 * `viewport` now implicitly causes generation of mouse events for the
   viewport when mouse mode is enabled. The mouse events are expressed
   in the coordinate system of the contents of the viewport. The
   consequence and intention of this change is to enable mouse event
   reporting for editors when clicks occur outside the known text area.

0.30
----

API changes:
 * `Brick.Focus`: added `focusSetCurrent` to make it easy to set the
    focus of a focus ring
 * `Brick.Main`: added a simple polymorphic `App` value, `simpleApp`

0.29.1
------

Bug fixes:
 * Mixed-case color names like "brightBlue" can now be parsed in theme
   customization files.

0.29
----

API changes:
 * Added Ord instances for `Location` and `BrickEvent` (thanks Tom
   Sydney Kerckhove)
 * `Brick.AttrMap`: attribute name components are now exposed via the
   `attrNameComponents` function. Also added a Read instance for
   AttrName.

New features:
 * This release adds user-customizable theme support. Please see the
   "Attribute Themes" section of the User Guide for an introduction; see
   the Haddock documentation for `Brick.Themes` for full details. Also,
   see the new `programs/ThemeDemo.hs` for a working demonstration.

0.28
----

API changes:
 * Brick.AttrMap.setDefault was renamed to setDefaultAttr.
 * Added Brick.AttrMap.getDefaultAttr: get the default attribute from an
   attribute map.
 * Added Brick.Widgets.Core.modifyDefAttr to modify the default
   attribute of the rendering context.

Other changes:
 * Updated AttrDemo to show usage of modifyDefAttr.

0.27
----

API changes:
 * Brick.Widgets.Core: added `hyperlink` combinator (thanks Getty Ritter
   for hyperlinking support)

Other changes:
 * Updated AttrDemo to show how to use hyperlinking
 * README: Added `herms` to featured projects

0.26.1
------

 * Fixed haddock for listHandleEventVi.

0.26
----

API changes:
 * Added Brick.Widgets.List.handleListEventVi to add support for
   vi-style movements to lists (thanks Richard Alex Hofer)

Other changes:
 * Added ListViDemo.hs to demonstrate the Vi-style handler for lists
   (thanks Richard Alex Hofer)

0.25
----

API changes:
 * List: added page movement functions `listMoveByPages`,
   `listMovePageUp`, and `listMovePageDown` (thanks Richard Alex Hofer)

Miscellaneous:
 * Fixed a spelling mistake in the AttrMap haddock (thanks Edward Betts)

0.24.2
------

Miscellaneous:
 * Minor documentation updates including a clarification for #135

0.24.1
------

Bug fixes:
 * vBox/hBox: when there is leftover space and all elements are greedy,
   spread it amongst the elements as evenly as possible instead of
   assigning it all to the first element (fixes #133)

Package changes:
 * Include Sam Tay's brick tutorial files in extra-doc-files

0.24
----

API changes:
 * Added Brick.Widgets.Core.setAvailableSize to control rendering
   context size in cases where the screen size is too constraining (e.g.
   for a floating layer that might be bigger than the screen).

Documentation changes:
 * Samuel Tay has contributed his wonderful Brick tutorial to this
   package in docs/samtay-tutorial.md. Thank you!

0.23
----

API changes:
 * getVtyHandle: always return a Vty handle rather than Maybe
   (Previously, in appStartEvent you'd get Nothing because Vty had
   not been initialized yet. This made various use cases impossible
   to satisfy because appStartEvent is a natural place to get initial
   terminal state from Vty. This change makes it so that a Vty handle is
   always available, even in appStartEvent.)
 * txtWrapWith: added missing haddock

0.22
----

API changes:
 * Core: added txtWrapWith and strWrapWith functions to provide control
   over wrapping behavior by specifying custom wrapping settings.

Other changes:
 * Updated TextWrapDemo.hs to demonstrate customizing wrapping settings.

0.21
----

Package changes:
 * Upgrade to word-wrap 0.2

Other changes:
 * Brick.Types.Internal: improve mouse constructor haddock
 * Add a basic fill demonstration program (FillDemo.hs)

0.20.1
------

Bug fixes:
 * str: fixed an IsString constraint confusion on GHC 7.10.1

0.20
----

Package changes:
 * Added a dependency on "word-wrap" for text-wrapping.
 * Added a new TextWrapDemo demo program to illustrate text wrapping
   support

API changes:
 * Brick.Widgets.Core: added new functions txtWrap and strWrap to do
   wrapping of long lines of text.

Miscellaneous:
 * Guide: fixed event type (#126)

0.19
----

API changes:
 * The editor content drawing function is now passed to renderEditor,
   not the constructor, to improve separation of presentation and
   representation concerns. The corresponding Editor drawing function
   lens and accessor were removed.

0.18
----

Package changes:
 * Added a dependency on data-clist.

API changes:
 * Brick.Focus: removed the Functor instance for FocusRing.
 * Brick.Focus: re-implemented FocusRing in terms of the circular list
   data structure from data-clist. In addition, this change introduced
   "focusRingModify", which permits the user to use the data-clist API
   to directly manipulate the FocusRing's internals. This way brick
   doesn't have to re-invent the wheel on the focus ring behavior.

0.17.2
------

Package changes:
 * Added programs/ReadmeDemo.hs and featured its output and code in the
   README to provide an early demonstration

Library changes:
 * centerAbout now right- and bottom-pads its operand to behave
   consistently with h/vCenter

0.17.1
------

Package changes:
 * Use Extra-Doc-Files instead of Data-Files for documentation files

Bug fixes:
 * List: correctly update selected index in listInsert
 * Update example program in brick.cabal (thanks @timbod7)

0.17
----

Package changes:
* Updated to depend on Vty 5.15.
* Updated to remove dependency on data-default.
* Discontinued support for GHC versions prior to 7.10.1.

API changes:
* Removed Data.Default instances for AttrName, AttrMap, Result, and
  BorderStyle (use Monoid instances instead where possible).
* Added defaultBorderStyle :: BorderStyle.
* Added emptyResult :: Result n.

0.16
----

This release includes a breaking API change:
* Brick now uses bounded channels (Brick.BChan.BChan) for event
  communication rather than Control.Concurrent.Chan's unbounded channels
  to improve memory consumption for programs with runaway event
  production (thanks Joshua Chia)

Other API changes:
* Brick.List got a new function, listModify, for modifying the selected
  element (thanks @diegospd)

Performance improvements:
* hBox and vBox now use the more efficient DList data structure when
  rendering to improve performance for boxes with many elements (thanks
  Mitsutoshi Aoe)

0.15.2
------

Bug fixes:
* viewport: do not cull cursor locations on empty viewport contents
  (fixes #105)
* User guide CounterEvent type fix (thanks @diegospd)

0.15.1
------

Bug fixes:
* List: fixed empty list validation in listReplace (thanks Joshua Chia)

0.15
----

Demo changes:
* MouseDemo: add an editor and use mouse events to move the cursor
* MouseDemo: Enhance MouseDemo to show interaction between 'clickable'
  and viewports (thanks Kevin Quick)

New features:
* Editors now report mouse click events

API changes:
* Rename TerminalLocation row/column fields to avoid commonplace name
  clashes; rename row/column to locationRow/locationColumn (fixes #96)

Bug fixes:
* Core: make cropToContext also crop extents (fixes #101)
* viewport: if the sub-widget is not rendered, also cull all extents and
  cursor locations

Documentation changes:
* User Guide updates: minor fixes, updates to content on custom widgets,
  wide character support, and examples (thanks skapazzo@inventati.org,
  Kevin Quick)

0.14
----

This release added support for wide characters. In particular, wide
characters can now be entered into the text editor widget and used in
'str' and 'txt' widgets.

0.13
----

API changes:
 * Mouse mode is no longer enabled by default.
 * customMain's event channel parameter is now optional
 * FocusRing now provides a Functor instance (thanks Ian Jeffries)

0.12
----

This release primarily adds support for mouse interaction. For details,
see the Mouse Support section of the User Guide. This release also
includes breaking API changes for the App type. Here's a migration
guide:

 * Event handlers now take "BrickEvent n e" instead of "e", where "e"
   was the custom event type used before this change. To recover your
   own custom events, pattern-match on "AppEvent"; to recover Vty input
   events, pattern-match on "VtyEvent".
 * appLiftVtyEvent went away and can just be removed from your App
   record constructor.
 * If you aren't using the custom event type or were just using Vty's
   "Event" type as your App's event type, you can set your event type to
   just "e" because you'll now be able to get Vty events regardless of
   whether you use a custom event type.

API changes:
 * Added the Widget combinator "clickable" to indicate that a widget
   should generate mouse click events
 * Added the Extent data type and the "reportExtent" widget combinator
   to report the positions and sizes of widgets
 * Rendering "Result" values now include reported extents and update
   their offsets (adds "extents" field and "extentsL" lens)
 * Added "lookupExtent", "findClickedExtents", and "clickedExtent" in
   EventM to find extents and check them for mouse clicks
 * Removed appLiftVtyEvent. Instead of wrapping Vty's events in your own
   type, you now get a "BrickEvent" that always contains Vty events but
   has the ability to embed *your* custom events. See the User Guide for
   details.
 * Added demo program MouseDemo.hs
 * Added demo program ProgressBarDemo.hs (thanks Kevin Quick)
 * Added mapAttrname, mapAttrNames, and overrideAttr functions (thanks
   Kevin Quick)
 * Make handleEventLensed polymorphic over event type to allow use with
   custom events (thanks Kevin Quick)
 * Added Ord constraint to some library startup functions

Bug fixes:
 * Added Show instance for Editor, List (fixes #63)

Documentation changes:
 * Updated documentation to use new "resource name" terminology to
   reduce confusion and better explain the purpose of names.
 * Updated user guide with sections on mouse support, the rendering
   cache, resource names, paste mode, and extents

Package changes:
 * Depend on Vty 5.11.3 to get mouse mode support

0.11
----

API changes:
 * Added getVtyHandle in EventM for obtaining the current Vty context.
   It returns Nothing when calling the appStartEvent handler but after
   that a context is always available.

0.10
----

New features:
 * Added a rendering cache. To use the rendering cache, use the 'cached'
   widget combinator. This causes drawings of the specified widget to
   re-use a cached rendering until the rendering cache is invalidated
   with 'invalidateCacheEntry' or 'invalidateCache'. This change also
   includes programs/CacheDemo.hs. This change introduced an Ord
   constraint on the name type variable 'n'.
 * Added setTop and setLeft for setting viewport offsets directly in
   EventM.
 * Dialog event handlers now support left and right arrow keys (thanks
   Grégoire Charvet)

Library changes:
 * On resizes brick now draws the application twice before handling the
   resize event. This change makes it possible for event handlers to
   get the latest viewport states on a resize rather than getting the
   most recent (but stale) versions as before, at the cost of a second
   redraw.

Bug fixes:
 * We now use the most recent rendering state when setting up event handler
   viewport data. This mostly won't matter to anyone except in cases
   where a viewport name was expected to be in the viewport map but
   wasn't due to using stale rendering state to set up EventM.

0.9
---

Package changes:
 * Depend on text-zipper 0.7.1

API changes:
 * The editor widget state value is now polymorphic over the type of
   "string" value that can be edited, so you can now create editors over
   Text values as well as Strings. This is a breaking change but it only
   requires the addition of the string type variable to any uses of
   Editor. (thanks Jason Dagit and Getty Ritter)
 * Added some missing Eq and Show instances (thanks Grégoire Charvet)

New features:
 * The editor now binds Control-U to delete to beginning of line (thanks
   Hans-Peter Deifel)

Bug fixes:
 * List: avoid runtime exception by ensuring item height is always at
   least 1

0.8
---

API changes:
 * Center: added layer-friendly centering functions centerLayer,
   hCenterLayer, and vCenterLayer.

Functionality changes:
 * Dialog now uses new layer-friendly centering functions. This makes it
   possible to overlay a Dialog on top of your UI when you use a Dialog
   rendering as a separate layer.
 * Updated the LayerDemo to demonstrate a centered layer.
 * The renderer now uses a default Vty Picture background
   of spaces with the default attribute, rather than using
   ClearBackground (the Vty default). This is to compensate for an
   unexpected attribute behavior in Vty when ClearBackgrounds (see
   https://github.com/coreyoconnor/vty/issues/95)

0.7
---

NOTE: this release includes many API changes. Please see the "Widget
Names" section of the Brick User Guide for details on the fundamentals!

API changes:
 * The "Name" type was removed. In its place we now have a name type
   variable ("n") attached to many types (including EventM,
   CursorLocation, App, Editor, List, and FocusRing). This change makes
   it possible to:
   * Avoid runtime errors due to name typos
   * Achieve compile-time guarantees about name matching and usage
   * Force widget functions to be name-agnostic by being polymorphic
     in their name type
   * Clean up focus handling by making it possible to pattern-match
     on cursor location names
 * The EditDemo demonstration program was updated to use a FocusRing.
 * Added the "Named" type class to Brick.Widgets.Core for types that
   store names. This type class is used to streamline the Focus
   interface; see Brick.Focus.withFocusRing and EditDemo.hs.
 * The List and Editor types are now parameterized on names.
 * The List widget is now focus-aware; its rendering function now takes
   a boolean indicating whether it should be rendered with focus. The
   List uses the following attributes now:
   * When not focused, the cursor is rendered with listSelectedAttr.
   * When focused, the cursor is rendered with listSelectedFocusedAttr.
 * The Editor widget is now focus-aware; its rendering function now
   takes a boolean indicating whether it should be rendered with focus.
   The Editor uses the following attributes now:
   * When not focused, the widget is rendered with editAttr.
   * When focused, the widget is rendered with editFocusedAttr.
 * The Dialog's name constructor parameter and lens were removed.
 * The 'viewport' function was modified to raise a runtime exception if
   the widget name it receives is used more than once during the
   rendering of a single frame.

Miscellaneous:
 * Many modules now use conditional imports to silence redundancy
   warnings on GHCs with newer Preludes (e.g. including Monoid,
   Foldable, Traversable, Applicative, etc.)

0.6.4
-----

Bug fixes:
 * Add missing Functor instance for Next type (thanks Markus Hauck)

0.6.3
-----

Bug fixes:
 * List: the list now properly renders when the available height is not
   a multiple of the item height. Previously the list size would
   decrease relative to the available height. Now the list renders
   enough items to fill the space even if the top-most or bottom-most
   item is partially visible, which is the expected behavior.

0.6.2
-----

Bug fixes:
 * Editor: the 'editor' initial content parameter is now correctly split
   on newlines to ensure that the underlying editor zipper is
   initialized properly. (fixes #56; thanks @listx)

0.6.1
-----

Package changes:
 * Added lower bound for microlens >= 0.3.0.0 to fix build failure due
   to Field1 not being defined (thanks Markus Hauck)

Documentation changes:
 * Updated user guide and README to link to and mention microlens
   instead of lens

Misc:
 * Fixed a qualified import in the List demo to avoid ambiguity (thanks
   Alan Gilbert)

0.6
---

API changes:
 * Brick now uses the microlens family of packages instead of lens. This
   version of brick also depends on vty 5.5.0, which was modified to use
   microlens instead of lens. This change shouldn't impact functionality
   but will greatly reduce build times.

0.5.1
-----

Bug fixes:
 * Fix negative cropping in hCenter, vCenter, and cropResultToContext
   (fixes #52)
 * Remove unnecessary Eq constraint from listReplace (fixes #48; thanks
   sifmelcara)
 * Mention Google Group in README

0.5
---

Functionality changes:
 * Markup: make markup support multi-line strings (fixes #41)
 * brick-edit-demo: support shift-tab to switch editors
 * Core: improve box layout algorithm (when rendering boxes, track
   remaining space while rendering high-priority children to use
   successively more constrained primary dimensions)
 * Core: make fixed padding take precedence over padded widgets (fixes #42)
   Prior to this commit, padding a widget meant that if there was room
   after rendering the widget, the specified amount of padding would be
   added. This meant that under tight layout constraints padding would
   disappear before a padded widget would. This is often a desirable
   outcome but it also led to unexpected behavior when adding padding
   to a widget that grows greedily: fixed padding would never show up
   because it was placed in a box adjacent to the widget in question,
   and boxes always render greedy children before fixed ones. As a
   result fixed padding would disappear under these conditions. Instead,
   in the case of fixed padding, since we often intend to *guarantee*
   that padding is present, all of the padding combinators have been
   modified so that when the padded widget is rendered with fixed
   padding in the amount V, the widget is given V fewer rows/columns
   when it is rendered so that the padding always has room.

0.4.1
-----

Bug fixes:
* Fixed a bug in the 'visible' combinator: If the size of the visibility
  request was larger than the available space, then the rendering of a
  viewport was toggling between two states, one with aligning on the
  end of the visibility request, and another one aligning on the start.
  This commit fixes it so that a visibility request is always aligned
  on the start if not enough space is available. (thanks Thomas Strobel
  <ts468@cam.ac.uk>)

Behavior changes:
* Honor multiple 'visible' markers in a single viewport with preference
  on the innermost request (thanks Thomas Strobel <ts468@cam.ac.uk>)

0.4
---

API changes:
* Added Brick.Widgets.Core.unsafeLookupViewport to make certain kinds
  of custom widget implementations easier when viewport states are needed
  (thanks Markus Hauck <markus1189@gmail.com>)
* List: added listClear and listReverse functions (thanks Markus Hauck)
* List: Derive instances for Functor, Foldable, Traversable (thanks
  Markus Hauck)

Documentation changes:
* Hyperlink "Data.Text.Markup" inside Brick.Markup haddock (thanks
  Markus Hauck)
* Fix typo in 'Attribute Management' section of user guide (thanks
  Markus Hauck)

0.3.1
-----

Bug fixes:
* EventM newtype again instances MonadIO (thanks Andrew Rademacher)

0.3
---

API changes:
* Made EventM a newtype instead of a type alias
* List: listReplace now takes the new selected index and no longer does
element diffing

Package changes:
* Removed the dependency on the Diff package

Misc:
* Applied some hlint hints (thanks Markus Hauck <markus1189@gmail.com>)
* Fixed a typo in the README (thanks Markus Hauck <markus1189@gmail.com>)
* Improved the renderList documentation (thanks Profpatsch <mail@profpatsch.de>)
* Types: added an explicit import of Applicative for older GHCs

0.2.3
-----

Bug fixes:
* Fixed viewport behavior when the image in a viewport reduces its size
  enough to render the viewport offsets invalid. Before, this behavior
  caused a crash during image croppin in vty; now the behavior is
  handled sanely (fixes #22; reported by Hans-Peter Deifel)

0.2.2
-----

Demo changes:
* Improved the list demo by using characters instead of integers in the
  demo list and cleaned up item-adding code (thanks Jøhannes Lippmann
  <code@schauderbasis.de>)

0.2.1
-----

Bug fixes:
* List:
  * Fixed size policy of lists so that rather than being Fixed/Fixed,
    they are Greedy/Greedy. This resolves issues that arise when the box
    layout widget renders a list widget alongside a Fixed/Fixed one.
    (Closes issue #17, thanks Karl Voelker)
* Scrolling:
  * vScrollPage actually scrolls vertically now rather than horizontally
    (Thanks Hans-Peter Deifel <hpd@hpdeifel.de>)

0.2
---

API changes:
* Added top-level `Brick` module that re-exports the most important
  modules in the library.
* List:
  * Now instead of passing the item-drawing function to the `list` state
    constructor, it is passed to `renderList`
  * `renderList` now takes the row height of the list's item widgets.
    The list item-drawing function must respect this in order for
    scrolling to work properly. This change made it possible to optimize
    the list so that it only draws widgets visible in the viewport
    rather than rendering all of the list's items (even the ones
    off-screen). But to do this we must be able to tell in advance
    how high each one is, so we require this parameter. In addition
    this change means that lists no longer support items of different
    heights.
  * The list now uses Data.Vector instead of [a] to store items; this
    permits efficient slicing so we can do the optimized rendering
    described above.
* The `HandleEvent` type class `handleEvent` method now runs in
  `EventM`. This permits event-handling code implemented in terms of
  `HandleEvent` to do get access to viewport state and to run IO code,
  making it just as powerful as code in the top-level `EventM` handler.
* Many types were moved from `Brick.Widgets.Core` and `Brick.Main` to
  `Brick.Types`, making the former module merely a home for `Widget`
  constructors and combinators.
* The `IsString` instance for `Widget` was removed; this might be
  reinstated later, but this package provides enough `IsString`
  instances that things can get confusing.
* `EventM` is now reader monad over the most recent rendering pass's
  viewport state, in addition to being a state monad over viewport
  requests for the renderer. Added the `lookupViewport` function to
  provide access to the most recent viewport state. Exported the
  `Viewport` type and lenses.
* Now that `handleEvent` is now an `EventM` action, composition with
  `continue` et al got a little messier when using lenses to
  update the application state. To help with this, there is now
  `handleEventLensed`.

Bugfixes:
* Lists now perform well with 10 items or a million (see above; fixes
  #7, thanks Simon Michael)
* Added more haddock notes to `Brick.Widgets.Core` about growth
  policies.
* Forced evaluation of render states to address a space leak in the
  renderer (fixes #14, thanks Sebastian Reuße <seb@wirrsal.net>)
* str: only reference string content that can be shown (eliminates a
  space leak, fixes #14, thanks Sebastian Reuße <seb@wirrsal.net>)

Misc:
* Added a makefile for the user guide.
* List: added support for Home and End keys (thanks Simon Michael)
* Viewports: when rendering viewports, scroll requests from `EventM` are
  processed before visibility requests from the rendering process; this
  reverses this previous order of operations but permits user-supplied
  event handlers to reset viewports when desired.

Package changes:
* Added `deepseq` dependency

0.1
---

Initial release
