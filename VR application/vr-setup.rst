VR application: how to setup our virtual reality software
+++++++++++++++++++++++++++++++++++++++++++++

Here we will see how to setup softwares to work together. Those softwares all come for free at the price to create a personal account on their websites.

Install Unity softwares
========================

The first step is to install the Unity IDE. We will do it by using the Unity Hub, which is a software which allows us to mange Unity installations 
supporting also several version in the same computer. You can download the Unity Hub for windows by 
clicking `here <https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.exe?_ga=2.85170649.1955100606.1682932923-1536020329.1682932923>`_, and 
for Mac by clicking `here <https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.dmg?_ga=2.55320299.1955100606.1682932923-1536020329.1682932923>`_

After the installations is done, you can install the specific version of Unity which we used to develope this VR application, which is the 
Unity **2020.3.28f1** (64-bit). You can download this specific version by opening the Unity Hub and clicking `here <unityhub://2020.3.28f1/f5400f52e03f>`_.

That's it for now!


Install Leap Motion softwares
==============================

We will need a specific version of the Leap Motion called Orion, since this developer kit is known to work beatifully with the Unity packages.
To download **Leap Motion Orion 4.1.0** click `here <https://developer-archive.leapmotion.com/downloads/external/v4-1-hand-tracking/windows?version=4.1.0>`_.

Now you can attach your Leap Motion to the PC and launch the Leap Motion visualizer to chech that is woking properly.
You should see this:

.. image:: leap-visual.gif
   :alt: pref
   :width: 700 px
   :align: center

|

Install Leap Motion Unity modules 
===================================

What is an asset in Unity
--------------------------
Unity Asset refers to any digital resource, such as 3D models, textures, audio files, scripts, or plugins, that can be 
imported into the Unity game engine to enhance or create a game or interactive experience. These assets are created by 
developers, artists, and designers and can be purchased or downloaded from the `Unity Asset Store <https://assetstore.unity.com/>`_ 
or other online marketplaces.

Unity assets allow game developers to save time and resources by using pre-built components to create games more efficiently. 
They can also be used to improve the quality of a game, as they can provide access to high-quality resources that might be 
difficult or time-consuming to create from scratch. Additionally, Unity assets can be modified or combined to create unique 
game experiences, giving developers more creative freedom and flexibility.

The Motion Unity modules 
-------------------------
The Leap Motion Unity Modules are a collection of pre-built scripts, prefabs, and examples that can be used to quickly 
integrate Leap Motion hand tracking into Unity projects. These modules are designed to simplify the development process 
and provide a starting point for developers to build on.
The Leap Motion Unity Modules include a variety of features, such as hand and finger tracking, gesture recognition, 
physics-based interactions, and virtual reality support. These features are implemented through a set of pre-built 
scripts and prefabs that can be easily added to a Unity project.
For example, the HandController prefab is a pre-built object that includes the necessary components and scripts to 
track hands and fingers using the Leap Motion controller. Similarly, the Interaction Engine module provides a set of 
physics-based tools and components that can be used to create realistic object interactions, such as grabbing and throwing objects.
Now to link our Unity scene and the Leap Motion output we need to download the **Leap Motion Unity modules**, specifically the version **4.8.0** which 
you can download by clicking `here <https://www2.leapmotion.com/downloads/unity-modules/v4.8.0>`_.

The Leap Motion core asset
---------------------------
The core asset for the Leap Motion is a Unity package that provides a set of tools and APIs for developers to integrate hand tracking into their Unity projects.

The core asset for Leap Motion includes a variety of features, such as hand and finger tracking, gesture recognition, and virtual reality support. 
The hand and finger tracking features allow developers to track the position, orientation, and movement of hands and fingers in real-time, 
which can be used to create natural and intuitive user interfaces for games and applications.
You will need to install also the **Core Assets** to visualize properly the animation of the hands in Unity. We will need the version **4.3.4** which 
you can download by clicking `here <https://github.com/ultraleap/UnityPlugin/releases/download/Release-CoreAsset-4.3.4/Leap_Motion_Core_Assets_4.3.4.unitypackage>`_.

The Leap Motion interaction engine
-----------------------------------
The Interaction Engine is a physics-based tool and module for the Leap Motion Unity Modules that allows developers to create realistic object interactions 
in virtual reality and other interactive applications. It includes a set of scripts and prefabs that simulate real-world physics and collision detection, 
enabling complex object interactions such as grabbing and manipulating objects with multiple points of contact. The module also supports VR-specific 
features such as haptic feedback and two-handed interactions. 
You will need the interaction engine version **1.1.1** which you can download  `here <https://github.com/ultraleap/UnityPlugin/releases/download/Release-InteractionEngine-1.1.1/Leap_Motion_Interaction_Engine_1.1.1.unitypackage>`_

DAJE LELLO