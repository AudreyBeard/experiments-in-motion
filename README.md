[[_TOC_]]

# Experiments with Motion

## Notes
### Compilation
Most of my experience so far has relied on XCode, since the documentation is only really (and barely) up-to-date for **XCode Version 13.4.1 (13F100)**. In general, the notes I'm taking are relevant to that use case. If I am referring to command-line builds, I will specify that in the text.

#### Project Settings
This project is set to use the "Legacy Build System," which is deprecated. In order to build from the this openFrameworks version (`of_v0.11.2_osx_release`), you need to (for each project):
```
File > Project Settings...
Shared Project Settings:
Build System:
Select "New Build System (Default)"
```

You can also simply change a file from the command line:
`PROJECT_NAME/PROJECT_NAME.xcodeproj/project.xcworkspace/xcshareddata/WorkspaceSettings.xcsettings`

Change the following:
```
<dict> // same in both, included here for context
	<key>BuildSystemType</key>
	<string>Original</string>
</dict>
```
To the following:
```
<dict> // same in both, included here for context
	<key>PreviewsEnabled</key>
	<false/>
</dict>
```
Note that the `<dict>` tag is identical in both cases. It's included here for context

# END of new  notes
--


# About modelNoiseExample
--
![Screenshot of Example](modelNoiseExample.gif)

### Learning Objectives

This openFrameworks example is designed to demonstrate how to load a 3D model and alter its vertices.

After studying this example, you'll understand how to use ofxAssimpModelLoader to load in a 3D model, iterate through its vertices, alter them with perlin noise, and draw them as a mesh.

In the code, pay attention to:

* the usage of the addon ofxAssimpModelLoader, which is used to load in 3D file types including 3ds, .obj, .dae etc. and provide access to their vertices, textures, and materials.
* loading the vertices of the model into a mesh with ```ofVboMesh mesh = model.getMesh(0);```.
* notice how it uses ofVboMesh not ofMesh. A quote from the Advanced Graphics section of ofBook:

	"We can use it [ofVboMesh] exactly the same as an ofMesh, that it 	is actually an ofMesh, but when it's drawn, instead 	of uploading all the vertices to the graphics card 	every time call draw on it, it uploads them once 	when we draw for the first time and only uploads 	them again if they change."

* adding four dimensional perlin noise to each vertice with ```ofSignedNoise();```.




### Expected Behavior

When launching this app, you should see:

* a 3D light pink balloon dog.

Instructions for use:

* move your mouse around to add varrying levels of noise to the model.  
* look in the data folder to see the file being loaded.
* try commenting and uncommenting the lines necessary to draw the original model without noise and the model as a wireframe.
