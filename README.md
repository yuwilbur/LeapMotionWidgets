#Leap Motion Widgets
There are 3 widgets in this package you can use:

1. Buttons
2. Sliders
3. Scrollers

## Buttons
Buttons only require a script that inherits from ButtonBase.
Take a look at the ButtonDemoBasic example on how to inhereit ButtonBase.

#### ButtonBase
Inspector Values  | Definition
------- | ----------
float string            | Strength of the string, we recommend a value of: 100.
float triggerDistance   | How far the button needs to be pressed before it triggers, we recommend a value of: 0.025.
float cushionThickness  | A cushion used for hysteresis and it's positioned right above the trigger. We recommend keeping this number low, for example: 0.05.

Functions | Definition
--------- | ---------
abstract void ButtonReleased()  | Called when button is released.
abstract void ButtonPressed()   | Called when button is pressed.
float GetPercent()              | Percentage between resting and pressed position.
Vector3 GetPosition()           | Position of the button in local space.
virtual void ApplyConstraints() | Constrains the movement of the button, this can be overriden by your implementation.

## Sliders
Sliders are more complex to integrate than buttons.
Sliders only require a script called SliderBase which inherits from ButtonBase.
Please follow the SliderDemoBasic prefab for an example of how to integrate the sliders.

Sliders require two game objects:
1. SliderUpperLimit
2. SliderLowerLimit
These limits determine how far the slider can move.

#### SliderBase - Inherits from ButtonBase
Inspector Values | Definition
---------------- | ----------
GameObject upperLimit | The position for the upperLimit of the slider. Only localPosition.x will be used.
GameObject lowerLimit | The position for the lowerLimit of the slider. Only localPosition.x will be used.

Functions | Definition
--------- | ----------
abstract void SlidePressed()    | Called when handle is pressed
abstract void SliderReleased()  | Called when handle is released
float GetPercent()              | Percentage for the slider position betweem lower and upper limit.
virtual void UpdatePosition()   | Updates the position of the slider and perform constraints on how far it can go

## Scroll
Scrolling windows are more complex to integrate than sliders.
Please follow the ScrollDemoBasic prefab for an example of how to integrate scrolling window.

Each scrolling window requires three scripts and three gameobjects:
1. ScrollHandle - Responsible for moving the content up/down
2. ScrollViewer - Responsible for displaying the scroll window contents
3. ScrollContent - Responsible for holding the scroll window contents

The ScrollViewer and ScrollContent objects use stencil shaders. You can either create your own stencil shader or you can use the stencil shaders provided with this Unity Package. We provide the following shaders:

For Content:
  * Stencil + Text
  * Stencil + Alpha
  * Stencil + Bloom
  * Stencil + Diffuse

For Viewer:
  * Stencil Window
  
### ScrollHandleBase - Inherits from ButtonBase
Inspector Values | Definition
---------------- | ----------
HandDetector handDetector | HandDetector is used to determine which part of the hand the scrolling window should track.
ScrollViewerBase viewer   | Used to match the handle size to viewer size. 
ScrollContentBase content | Used to move the content as the handle moves.

Functions | Definition
--------- | ----------
None | None

### ScrollViewerBase
Inspector Values | Definition
---------------- | ----------
GameObject scrollWindow       | A quad responsible for displaying the contents.
GameObject scrollWindowFrame  | A gameObject which frames the scrollWindow. This can be set to the same object as the scrollWindow.

Functions | Definition
--------- | ----------
abstract void ScrollActive()    | Gets triggered when the scroll pane becomes active.
abstract void ScrollInactive()  | Gets triggered when the scroll pane becomes inactive.

### ScrollContentBase
Inspector Values | Definition
---------------- | ----------
GameObject scrollViewerBase | Used to determine how far is the content allowed to scroll while remaining visible. 

Functions | Definition
--------- | ----------
float GetPercent() | Top = 0%, Bottom = 100%
