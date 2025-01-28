VR Application: Oculus Quest
==========================================================================

The Oculus Quest is a standalone VR headset made by `Meta <https://meta.com/>`_ that does not require a computer to run. It is a great device for VR applications, as it is wireless and has a good tracking system. The Oculus Quest uses inside-out tracking, which means that it uses cameras on the headset to track the position of the user in the physical space. This allows for a more immersive and interactive VR experience, as the user can move around freely without being tethered to a computer. The following image shows the application played with the Oculus Quest 2 headset:

.. image:: oculus_app.png
   :alt: pref
   :width: 700 px
   :align: center

|

Prerequisites
-------------

Before you begin, ensure that you have the following:

- A PC with Windows 10 or later (macOS is not supported for Oculus development with Unity).
- An Oculus Quest 2, Quest 3, or Pro headset.
- A compatible USB cable (e.g., Oculus Link cable or USB 3.0 cable for Quest devices).
- Unity Hub installed on your PC.

**Step 1**: Install Oculus Software
-------------------------------

Download and install the Oculus PC app (for Oculus Link). This is required for linking your Oculus device to your PC for development.

- **Download link:** `https://www.meta.com/quest/setup/ <https://www.meta.com/quest/setup/>`_

After installation:

1. Open the app and follow the instructions to set up your Oculus device.
2. Enable **Developer Mode** in the Oculus app on your smartphone (instructions in Step 2).

**Step 2**: Enable Developer Mode
-----------------------------

1. Install the **Meta Quest Developer Hub** on your PC:
   - **Download link:** `https://developer.oculus.com/downloads/ <https://developer.oculus.com/downloads/>`_

2. Log in with your Meta (Oculus) developer account.
   - If you do not have one, create it here: `https://developer.oculus.com/sign-up/ <https://developer.oculus.com/sign-up/>`_

3. Connect your Oculus device to the Meta Quest Developer Hub and toggle **Developer Mode** on.

**Step 3**: Install Unity
---------------------

1. From Unity Hub, install a Unity Editor version compatible with the Oculus Integration SDK.
   - Recommended: Unity LTS version (e.g., Unity ``2021.3.26f1`` or higher, due to ``Meta XR SDK``).

2. During installation, add the following modules:
   - **Android Build Support** (for Oculus Quest development)

**Step 4**: Install Oculus Integration in Unity
-------------------------------------------

1. Open Unity and create a new 3D project.
2. Once the project is created and open, go to **File > Build Settings** and select **Android** as the platform.
3. Go to the **Asset Store**:
   - In Unity, click **Window > Asset Store** (or open `https://assetstore.unity.com/ <https://assetstore.unity.com/>`_ in your browser).
4. Search for **Meta XR All-in-one** and download/import it into your project (Tested with Meta version ``72.0``). 
5. After loading the package, you will see a windows for the ``Meta XR Interaction`` > keep using ``OVR Hand``.
6. Import Samples from Meta XR Interaction in Package Manager ()


.. note::

   We are using the Meta XR All-in-one package because it incluse the Meta Core for visualization, the Meta Interaction modules for physical interaction and other useful demos.

|
   
**Step 5**: Configure Unity for VR Development
------------------------------------------

1. Go to **Edit > Project Settings > XR Plug-in Management** and enable **Oculus**.
2. Set up player settings:
   - Go to **Edit > Project Settings > Meta XR ** and fix all the potential issues.
     
**Step 6**: Download the SimpleThimble Oculus unitypackage
------------------------------------------------

1. **Download the SimpleThimble Oculus unitypackage**: `Download here <SimpleThimble_OculusApp.unitypackage>`_.
2. Import the package into Unity by dragging and dropping it into the Assets folder of your project.
3. In the Project window, go to ``Scenes`` and select the Oculus demo.

.. note::
   This project uses UDP (User Datagram Protocol) for communicating between the virtual scene and the thimbles. In order to set up the communication, you need to upload a different firmware to the thimble (ESP8266). We provide this solution in order to make the project more accessible with a standalone version.  
|

**Step 7**: Connect the SimpleThimble via UDP and run the project
----------------------------------------
1. Download the firmware for standalone version of the SimpleThimble: `Download here <SimpleThimble_standaloneFirmware.rar>`_.
2. Connect the ESP8266 to your computer and upload the firmware trhough Arduino IDE.
3. With the thimble on, connect to the network ``simplethimble`` using the password ``password``.
4. Run the project in Unity and you should see the following scene:


.. image:: oculusApp.gif
   :alt: pref
   :width: 700 px
   :align: center

|

