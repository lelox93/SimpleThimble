VR Application: Grasp a Virtual Object through the Use of the Oculus Quest
==========================================================================

The Oculus Quest is a standalone VR headset made by `Meta <https://meta.com/>`_ that does not require a computer to run. It is a great device for VR applications, as it is wireless and has a good tracking system. The Oculus Quest uses inside-out tracking, which means that it uses cameras on the headset to track the position of the user in the physical space. This allows for a more immersive and interactive VR experience, as the user can move around freely without being tethered to a computer.

.. image:: oculus-quest.png
   :alt: pref
   :width: 400 px
   :align: center

|

Install Oculus Software
========================

Prerequisites
-------------

Before you begin, ensure that you have the following:

- A PC with Windows 10 or later (macOS is not supported for Oculus development with Unity).
- An Oculus Quest, Quest 2, or Rift headset.
- A compatible USB cable (e.g., Oculus Link cable or USB 3.0 cable for Quest devices).
- Unity installed on your PC.

Step 1: Install Oculus Software
-------------------------------

Download and install the Oculus PC app (for Oculus Link). This is required for linking your Oculus device to your PC for development.

- **Download link:** `https://www.meta.com/quest/setup/ <https://www.meta.com/quest/setup/>`_

After installation:

1. Open the app and follow the instructions to set up your Oculus device.
2. Enable **Developer Mode** in the Oculus app on your smartphone (instructions in Step 2).

Step 2: Enable Developer Mode
-----------------------------

1. Install the **Meta Quest Developer Hub** on your PC:
   - **Download link:** `https://developer.oculus.com/downloads/ <https://developer.oculus.com/downloads/>`_

2. Log in with your Meta (Oculus) developer account.
   - If you don’t have one, create it here: `https://developer.oculus.com/sign-up/ <https://developer.oculus.com/sign-up/>`_

3. Connect your Oculus device to the Meta Quest Developer Hub and toggle **Developer Mode** on.

Step 3: Install Unity
---------------------

1. From Unity Hub, install a Unity Editor version compatible with the Oculus Integration SDK.
   - Recommended: Unity LTS version (e.g., Unity 2021.3 or later).

2. During installation, add the following modules:
   - **Android Build Support** (for Quest and Quest 2 development)
   - **Windows Build Support (IL2CPP)** (for Rift development)

Step 4: Install Oculus Integration in Unity
-------------------------------------------

1. Open Unity and create a new 3D project.
2. Go to the **Asset Store**:
   - In Unity, click **Window > Asset Store** (or open `https://assetstore.unity.com/ <https://assetstore.unity.com/>`_ in your browser).
3. Search for **Oculus Integration** and download/import it into your project.
   - **Link to Oculus Integration:** `https://assetstore.unity.com/packages/tools/integration/oculus-integration-82022 <https://assetstore.unity.com/packages/tools/integration/oculus-integration-82022>`_

Step 5: Configure Unity for VR Development
------------------------------------------

1. Go to **Edit > Project Settings > XR Plug-in Management** and enable **Oculus**.
2. Set up player settings:
   - Go to **Edit > Project Settings > Player > Other Settings** and enable:
     - **Virtual Reality Supported** (for older Unity versions).
     - Set the scripting backend to **IL2CPP**.

Step 6: Download the SimpleThimble Oculus Project
------------------------------------------------



