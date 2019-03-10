# Udacity VR Maze

Complete the maze project in the [Udacity VR Curriculum](https://classroom.udacity.com/nanodegrees/nd105/parts/59ea77f3-dc80-4fa1-b7e9-67c14a69b774/modules/c9d6e8a9-09d7-44a3-868c-7d99c037ec0a/lessons/a5debf44-b201-408f-bf32-9caccbfd4c73/concepts/4c5cb54a-9faa-4cfc-a984-e579fb5cedeb)

You need to download [Unity Hub](https://unity3d.com/get-unity/download) and download Unity 2017.4.22f1 to work on the project

You also need to add iOS Build Support / Android Build Support according to what phone you have. 

Don't forget to add [Unity for Github](https://unity.github.com/), create a development branch and make consistent commits. 


## Project Overview
You'll be creating a fully interactive VR experience in the form of a maze.

This gives you a chance to apply what you've learned with scripting to bring a full audio visual experience together.

## What will I learn?
This project is focused on learning to code the scripts that bring everything to life. Skills include:

- Creating new C# scripts in Unity
- If then, loops, arrays, and other programming constructs
- Attaching scripts to objects
- Using the built-in Monobehaviour methods
- Triggers and Gaze Based Interaction
- Creating, moving and animating objects procedurally
- Familiarization with the Unity documentation
- Scripting Dynamic UI Objects
- Debugging
- The Unity Event System.
- Managing and Reloading scenes.
- Controlling particle systems.
- Create an Audio Clip and playing sounds.
- Waypoint Navigation System.
- Profiling scenes for performance.

Outlined below is a suggested approach to building your project that will help you systematically meet all the requirements for this project.

**Note:** As long as your project submission meets all the requirements specified in the Project Rubric, you can build your project any way you like and also use different assets than the ones provided with the starter project.

## 01. Understanding the Project Requirements
During this step we will make sure we understand the scope of the project and what is required from our project submission. First make sure you read through all the [project rubric](./project_rubric.pdf) to fully understand what is expected of you.

Make a plan using the project plan sheet and submit it to your teacher for feedback.

## 02. Downloading and Opening the Starter Project
During this step we will download the starter project, verify that we have the recommended Unity version installed, and get to know the project and the scene.

- Go to the [VR Software Development](https://github.com/udacity/VR-Software-Development_A-Maze/releases) - A Maze repository release page and read the release notes and the README.
- Download the Source code (zip) for the most recent release version which will be noted as the Recommended Version in the Release Status section of the release notes.
- Unzip the repository to a convenient location on your computer.
- Open the Unity project named A Maze.
- Set up Unity for Github and link this repository as the remote 
- Create a development branch, switch to it, and make an initial commit with the starter project files.
- Open the scene Assets > UdacityVR > Scenes > Main.
- Spend some time exploring the scene and the assets.
- Enter game mode.

Notice that there is no VR functionality yet. We will set that up in the next step when we create the GVR camera rig.

**Note:** When you enter game mode, you will see a NullReferenceException error thrown from the Waypoint.cs script. This is expected and is caused by the code referencing the main camera's parent game object which doesn't exist yet, we will set it up in the next step.

## 03. Creating the GVR Camera Rig
During this step we will create the VR camera by including the `GvrEditorEmulator` in the scene and configuring the camera.

- Add the `GvrEditorEmulator` prefab to the scene.
- Make the `Main Camera` game object a child of the `GvrEditorEmulator` game object.
- Reset the `Main Camera` game object's **Transform** component.
- Verify that the `Main Camera` game object has the **Tag** `MainCamera`.
- Move the `GvrEditorEmulato`r game object to a convenient location for development, for example, **Position:** `0, 3, 35` and **Rotation:** `0, 180, 0`.
- Enter game mode and use **Alt + Mouse** movement and **Ctrl + Mouse** movement to rotate and tilt the camera viewing angle.

Notice that there is no interactivity yet. We will set that up in the next step when we prepare the scene for interaction.

**Tip:** If the view seems 'off' when you rotate and tilt the camera viewing angle during game mode, verify that the `Main Camera` game object's **Transform** component properties are set to the default values, i.e. **Position:** `0, 0, 0,` **Rotation:** `0, 0, 0,` and **Scale:** `1, 1, 1`.

## 04. Preparing the Scene for Interaction
During this step we will prepare the scene for interaction by setting up the reticle pointer, physics raycaster, and event system, and then test the included waypoint system.

**Note:** The Waypoint game objects in the scene are instances of the Waypoint prefab which has already been completed for you.

- Add the `GvrReticlePointer` prefab to the scene as a child of the Main Camera game object.
- Increase the Max Reticle Distance value for the `GvrReticlePointer` from the default 10 to 20.
- Add the `GvrPointerPhysicsRaycaster` script as a component on the Main Camera game object.
- Add the `GvrEventSystem` prefab to the scene.
- Enter game mode and navigate the scene by clicking on the waypoints.

Notice that when you move the reticle pointer over any of the other game objects such as the Coin, Key, or Door, the reticle pointer does not expand and the game objects cannot be interacted with. We will set that up in the next step when we make the game objects interactive.

**Tip:** If the reticle pointer seems 'off' when you rotate and tilt the camera viewing angle during game mode, verify that the `GvrReticlePointer` game object's Transform component properties are set to the default values, i.e. Position: 0, 0, 0, Rotation: 0, 0, 0, and Scale: 1, 1, 1.

## 05. Making the Game Objects Interactive
During this step we will make the Coin, Key, and Door interactive by adding script and event trigger components to them.

- Locate and select the Coin game object in the hierarchy.
- Verify that it has a Collider component.
- Add the provided Coin script as a component.
- Add an Event Trigger as a component.
- Add the PointerClick event to the Event Trigger component.
- Assign the Coin object from the project hierarchy to the object field of the Pointer Click event.
- Assign the Coin.OnCoinClicked() method as the function for the Pointer Click event.
- Enter game mode, click on the coin and verify that the message `Coin.OnCoinClicked()` was called is printed to the Console window.
- Repeat the same process for the Key game object but use the Key script and the `Key.OnKeyClicked()` method.
- Repeat the same process for the first parent Door game object but use the Door script and the `Door.OnDoorClicked()` method.

Notice that when you click, for example, the Coin the triggered event is not visible in the game view, but each time you click the Coin, the 'Coin.OnCoinClicked()' was called message is printed to the console window. This is because the `OnCoinClicked()` method has only been declared and  currently only contains `Debug.Log()`.

## 06. Making the UI Interactive
During this step we will make the SignPost interactive by adding script and event trigger components to it. The process is almost identical to what we did with the Coin, Key, and Door in the previous step, but we don't need a collider to interact with UI game objects. Instead, we need to verify that the Canvas game object has a Graphic Raycaster component, and because we are using GVR, we will replace Unity's Graphic Raycaster with Google VR's `GvrPointerGraphicRaycaster`.

**Tip:** Temporarily disable the The_Temple, the Door, and the Post_Sign game objects so you can easily see and navigate to the SignPost.

- Locate and select the SignPost game object in the hierarchy.
- Remove the Graphic Raycaster component that is automatically added when creating a new canvas game objects.
- Add the `GvrPointerGraphicRaycaster` script as a component.
- Add the provided SignPost script as a component.
- Add an Event Trigger as a component.
- Add the PointerClick event to the Event Trigger component.
- Assign the SignPost script component from the inspector to the object field of the Pointer Click event.
- Assign the SignPost.ResetScene() method as the function for the Pointer Click event.
- Enter game mode, click on the SignPost and verify that the message 'SignPost.ResetScene()' was called is printed to the Console window.

At this point you have a scene with several game objects that when clicked will call the specified method in the script assigned to the Pointer Click event trigger. During the next four steps we will write code to create 'behaviours' for the Coin, Key, Door, and SignPost game objects.

## 07. Programming the Coin Behaviour
During this step we will program the Coin behaviour so that when a Coin is clicked it plays a sound, displays a 'poof' effect, and disappears.

- Review the Coin Behaviour section of the [Project Rubric](./project_rubric.pdf).
- Open the Coin script and read through the entire script including all the comments.
- Spend some time understanding the behaviour of the provided CoinPoof prefab. You can do this by, for example, entering game mode and dragging a CoinPoof prefab into the scene.
- Program the Coin behaviour by completing all the TODO comments in the script.

**Tip** The Unity documentation on [Instantiate](https://docs.unity3d.com/2017.4/Documentation/ScriptReference/Object.Instantiate.html) and [Destroy](https://docs.unity3d.com/2017.4/Documentation/ScriptReference/Object.Destroy.html) might be helpful for completing. Also, remember to convert your decimal to a float for the Destroy function (i.e. append an f to your decimal number).

**Note:** The provided CoinPoof prefab has already been completed and does not need to be modified.

## 08. Programming the Key Behaviour
During this step we will program the Key behaviour so that when the Key is clicked it plays a sound, displays a 'poof' effect, and disappears.

- Review the Key Behaviour section of the [Project Rubric](./project_rubric.pdf).
- Open the Key script and read through the entire script including all the comments.
- Spend some time understanding the behaviour of the provided KeyPoof prefab. You can do this by, for example, entering game mode and dragging a KeyPoof prefab into the scene.
- Program the Key behaviour by completing all the TODO comments in the script.

**Note:** The provided KeyPoof prefab has already been completed and does not need to be modified.

## 09. Programming the Door Behaviour
During this step we will program the Door behaviour so that when the Key is clicked the Door is unlocked and when the Door is clicked it plays a sound and starts rotating to an open position.

- Review the Door Behaviour section of the [Project Rubric](./project_rubric.pdf).
- Open the Door script and read through the entire script including all the comments.
- Add an AudioSource component to the first parent Door game object and disable Play On Awake.
- Assign the Door_Opening audio to the AudioClip field.
- Program the Door behaviour by completing all the TODO comments in the script.

## 10. Programming the SignPost Behaviour
During this step we will program the SignPost behaviour so that when the SignPost is clicked it restarts the game.

- Review the SignPost Behaviour section of the [Project Rubric](./project_rubric.pdf).
- Open the SignPost script and read through the entire script including all the comments.
- Program the SignPost behaviour by completing all the TODO comments in the script.

**Note:** If you haven't already, now is a good time to disable Auto Generate and manually Generate Lighting (located at the bottom of the Lighting window).

**Bonus:** For extra practice with animations, you might want to make the Chest interactive and animate the lid opening when the user clicks it. You can create the animation using only code or use an animation and animator controller. If you want to use an animator controller, you can either create your own animation clip or import the animation from the Chest model.

## 11. Creating the Gameplay Functionality
During this step we will put everything together and turn our project into an actual game.

- Review the Gameplay Functionality section of the [Project Rubric](./project_rubric.pdf).
- Use the child game objects of the Maze game object to design a Maze.
- Move the player, i.e. the `GvrEditorEmulator` game object, to your desired start location.
- Add more Waypoints so the player can navigate to all parts of the Maze.
- Add more Coins so the player have plenty of Coins to collect.
- Move the Key to a location so it is somewhat difficult for the player to find it.
- Add walls (cubes) to ensure that users have to navigate around to find the key and coins.

**Tip:** Any time you have a game object that you want to reuse multiple times such as for example the Coin game object and the game objects you use to build the Maze, you want to turn the game object into a Prefab before duplicating it because this allows you to make changes to all the copies at the same time.

## 12. Improve, Deploy, Test, and Optimize
It is extremely important to create experiences that people actually enjoy. At a minimum, this includes making sure the app runs smoothly on the target device but we can also do some other enhancements to our scene. Here are some suggestions:

- Replace the default Skybox (a Skybox material is provided in the Assets folder).
- Add ambient sound (an audio clip is provided in the Assets folder).
- Add lights to highlight important parts of the scene.
- Adjust lights, materials, and lighting settings to reflect the atmosphere you want the game to convey.
- Optimize game objects, lights, materials, lighting settings and quality settings for mobile VR