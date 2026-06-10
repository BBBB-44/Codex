---
---

## how to make a character follow a path :

step 1 : 

make a bezier curve 
Add/curve/bezier curve

then go in edit mode to make the curve you want.

(tips : put yourself in z view to have a flat curve)

step 2 : make the character follow the path

select the character rig

go in object constraint property

add an object constraint : follow path

then select the bezier curve.

click animate path.


step 3 : make the walk animation loop

select the character rig

go in animation tab

click on editor type, then select graph editor.

press : shft + e

then select : Make Cyclic

## transparency / depth sorting problem caused by “image as plane” materials.

Fix (this usually solves it immediately)
1. Select the sewer plane

Go to Material Properties → Settings

2. Change:
Blend Mode → Alpha Hashed (best quick fix)
or → Alpha Clip (if you want sharp edges)
3. Also set:
Shadow Mode → match the above (Hashed or Clip)


## Import an image as a texture, you can use the Shading workspace for a node-based approach or the Material Properties panel for a quick setup. 

Method 1: Drag-and-Drop (Fastest)

Open the Shading workspace or the Node Editor. 
Locate your image file in your computer’s file browser.
Drag and drop the image file directly into the Node Editor. This automatically creates an Image Texture node. 
Connect the Color output of the Image Texture node to the Base Color input of the Principled BSDF node.


## How to Import Animation (FBX) to Switch Character Animations (Blender 3.4)
1. Select your character's armature (rig) in the viewport.
2. Switch to the Animation workspace or change an area to the Dope Sheet editor.
3. At the top of the Dope Sheet, change the mode from "Dope Sheet" to Action Editor.
4. In the Action Editor, you will see a dropdown menu containing all actions currently in the scene. Select a different animation to apply it to the rig.

# Fly/Walk Navigation for camera view
1. Activate Fly Mode: Press Shift +  ` (tilde key).
2. Navigate: Use your mouse to aim, and W, A, S, D keys to move forward, left, backward, and right.


# how to extrude svg
1. import svg file
2. go in object data. (green sideway U icon)
3. geometry >extrude

## optional : facing upward position
press r
press x
press 90

## optional : change the svg center point
edit mode
press g

# How to rotate object
1. transform panel > z > insert keyframe
2. 1st keyframe z = 0
3. last keyframe z = 360
4. rightclick keyframe > interpolation mode > linear
