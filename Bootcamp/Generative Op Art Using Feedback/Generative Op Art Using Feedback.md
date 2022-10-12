![[Preview.jpg]]

#### Intro

This tutorial has two benefits: it is an excellent first approach to Cables and shows how to use the feedback method, which is a fundamental technique in the creation of visuals and generative art.

In my patch, all operators are numbered according to the order in which they were created. 

### Links

- [Tutorial Source|noembed](https://www.youtube.com/watch?v=SCFizyJixbA)
- [DR Patch|noembed](https://cables.gl/p/6Xf4cf))

### Recipe

[Youtube Link|fullwidth](https://youtu.be/SCFizyJixbA)

0) Give patch a name and set a square aspect ratio preview.

1) #Main-Loop op. Trigger other ops once every frame to create smooth animations (renderer). This is often the main step in a Cables patch.

1) #Sequence op. Control the order of execution/triggering and let us choose when other ops or actions are triggered, so we can have certain events happen before other event.

3) #Image-Compose op (in my patch is *03-Image-Compose_A*). Compose Images and effects as layers to generate new images.
	>**Image-Compose_A Settings**
	> - Size = manual
	> - Width = 1024 | Heigth = 1024
	> - Pixel Format = RGBA 32 bit float

4) Copy and paste  *03-Image-Compose_A*  to *04-Image-Compose_B*.
	>**Image-Compose_B Settings**
	> - R = 0.5 | G =0.5 | B =0.5 | A = 1

5)  #Full-Screen-Rectangle op. Draws a rectangle using the full WebGL canvas size. We have an output! Later on we're going to switch the connection to *04-ImageCompose_B*.

6) #Circle-Texture op. Draw 2d circle into texture, connect it to *03-ImageCompose_A* (leave space between, well' need it later...) and set 
	> **Circle Texture Settings**
	> - Size = 0.125

7) #Sine-Anim op. Animation in the form of a sine/cosine curve (sinus/cos) It's something similar to an LFO oscillator in Touchdesigner.  In my patch is *07-Sine-Anim_A*. 
	> **Sine-Anim A Settings**
	> - Freq = 0.5
	> - Ampl = 0.8

8) Copy and paste *07-Sine-Anim_A* to clone it in a new *08-Sine-Anim_B*. Switch it to *cosine* and set
	> **Sine-Anim B Settings**
	> - Mode = cosine
	> - Phase = 0.71
	> - Freq = 0.37
	> - Ampl  = 0.45

9) #Relative-Time op. Time since the patch was loaded in seconds. Something similar to te ABSTime trick in Touchdesigner.

10) #HSBtoRGB op. Converts a color from HSB to RGB (conversion, HSV, HSL, colour, mode).

11) #Multiply op.  Multiplies two numbers.
	> **Multiply Settings**
	> - Number 2 = 0.05

12) #Modulo op.  Outputs the remainder after division of one number by another.
	> **Modulo Settings**
	> - Number 2 =1

13) #ChromaticAberration op.  Simulating lens effect by shifting rgb channels.
	> **ChromaticAberration Settings**
	> - Pixel =10
	> - Lens Distort = 0.75
	> - Smooth = ON

	Now disconnect *05-Full-Screen-Rectangle* from *03-Image-Compose_A* and connect it to *04-Image-Compose_B*.

14) #CopyTexture op.  Copy a texture and optionally resize it. Something similar to the feedback TOP in Touchdesigner.
	>**Copy Textures Settings**
	>- HDR = ON

15) #DrawImage op. Draws an image into a composition. In my patch is *15-DrawImage_A*. 

16) Copy and paste  *15-DrawImage_A*  to clone it in a new  *16-DrawImage_B*. 

	Now connect the texture out of *03-Image-Compose_A*  to the texture in of *16-DrawImage_B*.

17) #ScrollTexture op. Scroll image. 
	>**ScrollTexture Settings**
	>- AmountX = -0.0.7

18) Copy and paste  *08-SineAnim_B*  to clone it in a new  *18-SineAnim_C*. 
	>**SineAnim Settings**
	>- Mode = Sine
	>- Amplitude = 0.005

19) #BulgePinch op. Bulge and pinch an image (deform,stretch,distort).
	> **BulgePinch Settings**
	> - Strenght = 0.05
