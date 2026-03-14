https://drive.google.com/file/d/1_Y41VA3dhHvfYw0oAvjMbD2RT7PePfiY/view?usp=drivesdk got the model from elsewhere, then you need to import it and any related textures into your 'Assets' folder.

If you are importing your model from a 3D editor, please ensure you keep in mind the difference between coordinate systems. For example, [**Blender**](https://blender.org)'s default coordinate and unit system differs from Unity's. You must export FBX files from Blender and define the exporter as such:

![image](/img/avatars/creating-your-first-avatar-b066a1b-2022-05-27_11-13-48_blender.png)

After you get the model in your assets, select it, you'll want to ensure it has the correct settings in the rig tab in the inspector. Make sure the Animation Type is set to Humanoid.

## Step 4 - Get the model into a scene
Now that you have the model in your Assets folder, with the correct settings applied, you need to put it into a scene. To do so, either drag it into your [Hierarchy](https://docs.unity3d.com/Manual/Hierarchy.html) or directly into the Scene View window. We recommend having one scene per avatar and placing it at the coordinates (0, 0, 0). If needed, rotate the avatar so it is standing up straight, and ensure that its size is what you expect. You can add a Cube to your scene to compare - the cube will be 1 meter on each side and your Avatar will best function between about 0.5-5m tall. The average person is around 1.65 meters tall.
:::caution Avatar Optimization

It is very important that your avatar is optimized so that you do not cause low FPS for yourself and others. The SDK will inform you if something looks wrong. Check out our [Avatar Optimization Tips](/avatars/avatar-optimizing-tips) to check out methods to improve your avatar's Performance Rank.
:::
## Step 5 - Adding an Avatar Descriptor 
The next step is to add a 'VRC Avatar Descriptor' component and prepare its settings.
1. Select the avatar in your hierarchy.
2. Click 'Add Component' in the inspector.
3. Search for the 'VRC Avatar Descriptor' component and add it.
4. Customize its settings, as explained below.

![Add a `VRC Avatar Descriptor` to get started with your avatar.](/img/avatars/creating-your-first-avatar-fd027ea-Unity_qH7NJfAzzn.png)
### View position
First, you'll want to set the view position. This will be where your camera will be positioned in VRChat. You can see a visual representation of it as a small white sphere in the scene.

If your avatar has a head, place the view position between the avatar's eyes. If your avatar's head is unusually large, its feet may lift off the ground when looking up and down. To avoid this, place the view position closer to where a regular-sized head would be.

If your avatar doesn't have a head, place the view position wherever you think it's appropriate.

![Use the Avatar Descriptor to configure your avatar for VRChat. Make sure to adjust the view position!](/img/avatars/creating-your-first-avatar-5afcbf1-Unity_lsTjP8qDqO.png)
### Lip sync mode
When you talk, you can make your avatar's mouth (or anything else) react automatically.  Open your `VRC Avatar Descriptor` and expand the `LipSync` dropdown. You can choose one of five lip sync modes:

#### Default
![Pressing 'Auto Detect!' is usually enough to let your VRChat avatar react to your speech.](/img/avatars/creating-your-first-avatar-d69289f-Unity_FgsAtEU75F.png)

Press 'Auto Detect!' to let the VRChat SDK automatically detect the appropriate lip sync mode. The mode will then switch to one of the modes below.

#### Jaw Flap Bone
If your avatar uses a single bone to animate the jaw, you can specify it here. Your character's jaw will open depending on how loudly you speak in VRChat. Ensure you've configured the jaw bone in Unity's Humanoid rig for your avatar.

#### **Viseme Blend Shape** (recommended)
Blend shapes/shape keys (named depending on what software you're using) modify the mesh based on vertex positions.  Many models use this for detailed animations for speaking. If your model has these, you should use them!

We use the Oculus Audio library to detect and set visemes. [You can see a reference to what all the visemes should look like and what sound triggers them here](https://developer.oculus.com/documentation/unity/audio-ovrlipsync-viseme-reference). 

VRChat can usually detect your avatar's visemes automatically. If not, you can choose visemes from the dropdown list.

![The 'Viseme Blend Shape' mode is the most common method of making your character's face move when you speak.](/img/avatars/creating-your-first-avatar-6272723-Unity_w5nQONGtcb.png)

:::caution SIL shape

Unity will delete shape keys/blend shapes that are empty on import, so make sure your "SIL" shape (the shape your mouth makes when no sound is detected, but the mic is active - such as the space between words) moves a single vertex a very small, imperceptible amount. This will prevent Unity from deleting that key.
:::

:::note Viseme Performance Tip!

If you're an avatar creator, consider splitting your avatar into two skinned meshes - one for your body, and one for your head/face.
The performance cost of blend shapes depends on how much of your 3D model they affect. Keeping blend shapes on a separate head mesh and having fewer blend shapes on your body mesh may improve your avatar's performance.
:::

##### Jaw Flap Blend Shape
If your avatar only uses a single blend shape to animate its mouth, configure it here. It will behave similarly to 'Jaw Flap Bone' by animating the jaw blend shape instead of a jaw bone.

##### Viseme Parameter Only
If you're an advanced creator, you can use this mode to control how your avatar reacts to speech with VRChat's built-in [Animator Parameters](/avatars/animator-parameters).

## Step 6 - Going to the build tab / Checking if the avatar is ok
Next, we'll want to check that everything is good in the build window. To do that, use the menu item `VRChat SDK > Show Control Panel`, which opens the VRChat SDK Control panel. After signing in, switch to the "Builder" tab to see the avatar's GameObject mentioned with a "Build" section below. You also see settings, content tags, the avatar's performance rank, errors, and warnings.

![The VRChat SDK build panel.](/img/avatars/build-panel-avatars-2025.png)

Simply follow the steps in VRChat's SDK build panel: 
1. Give your avatar a name.
	- You can add a description, too.
2. Choose your avatar's visibility.
	- Public avatars can be cloned by other VRChat users or shared via pedestals in worlds.
	- Private avatars can only be used by you.
3. Select appropriate content warnings for your avatar to comply with VRChat's  [content gating system](https://hello.vrchat.com/blog/content-gating).
4.  Select a thumbnail image.
	- You can select a file or capture an image from your Unity scene.
5. Read the 'Validations' section. It contains many useful errors and warnings.
	- For example, the SDK may warn you about your avatar having too many triangles, which you can fix by optimizing mesh(es). If you're unable to optimize the mesh, you may need to go back and choose another model.
6. Choose the build type.
	- **Build & Publish Your Avatar Online** uploads your avatar to VRChat and allows other users to see it.
	- **Build & Test Your Avatar** allows you to quickly test your avatar without uploading it.
		- You can find your test avatar in the "Other" avatars section in VRChat.
		- You can use [Build & Test on Android](/platforms/android/build-test-mobile/).
7. Choose which platforms to build your [platform](/platforms/) on.
8. Confirm that the avatar's information is accurate and thatn you have the rights to upload the content to VRChat.
9. When you're ready, click the "Build & Publish" button.


## Step 7 - Building and uploading the avatar!
Now everything is ready. Press the "Build & Publish" button, and the SDK will start building and uploading your avatar. Before uploading your avatar, you should double-check that it complies with VRChat's [Terms of Service](https://hello.vrchat.com/legal) and [Community Guidelines](https://hello.vrchat.com/community-guidelines).

After uploading your avatar, it should be available in VRChat. You can also see your avatar in  `VRChat SDK > Show Control Panel > Content Manager`.

You can also test your avatar without uploading it. To do this, click "Build & Test" instead. Your avatar will appear in the "Other" section of your VRChat Avatars menu. Test avatars can only be seen by you. In order for other players to see your avatar, you need to upload it.

Additionally, you can launch with the `--watch-avatars` launch option that will make it so that if you're wearing an avatar from the "Other" section, any future tests will immediately switch you to the new version of the avatar.

## Step 8 - Enjoy your avatar!

Congratulations on creating your first avatar! We hope everything went smoothly. If you need any help, consider visiting our [Ask Forum](https://ask.vrchat.com/) or our [Discord server](https://discord.com/invite/vrchat).

Creating and uploading VRChat avatars can be fun and creatively fulfilling. If you'd like to improve your avatar creation skills, take a look at the rest of our [Avatars documentation](https://creators.vrchat.com/avatars/).

## Learn more

If you'd like to become better at avatar creation, check out these pages:
- [Android Content Optimization](/platforms/android/quest-content-optimization) - Learn how to create avatars that work well on Android and Quest.
- [Avatar Optimization Tips](/avatars/avatar-optimizing-tips) - Learn general advice on creating optimized PC or Android avatars.
- [Performance Ranks](/avatars/avatar-performance-ranking-system) - Learn why certain avatars are visible or hidden to other players by default.
- [Avatar Components](/avatars/avatar-components/) - Learn how to create immersive interactions on your avatar. 

