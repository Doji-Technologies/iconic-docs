Encoding .ico files
===================

Fire & Forget
-------------

| It only takes one simple method call to generate an .ico file from a Texture2D:
| ``IcoConversion.EncodeToICO(myTexture);``

Some prerequisites for the textures:

* must be in a non-compressed format (RGBA32, ARGB32, RGB24)
* .ico only supports resolutions up to 256x256


Customizing Multi-Resolution Behaviour
--------------------------------------

By default, the ``EncodeToICO()`` methods automatically create a multi-resolution .ico file. (Visual Studio is a decent tool to inspect .ico files by the way. If you want to know which images are embedded in an .ico file just drag and drop it into an open instance of VS.)

Configuring this behaviour can be achieved by passing an IcoRescaleSettings object.
This is best explained with a few examples. Imagine we have the following image with a resolution of 200x200 as an uncompressed Texture2D object in Unity:

.. figure:: /_static/images/baboon.jpg
   :width: 40%
   :align: center


Example 1: Default Values
~~~~~~~~~~~~~~~~~~~~~~~~~

If you just call ``IcoConversion.EncodeToICO(myTexture);`` without specifying any settings, the resulting .ico file will contain the following 5 images with the resolutions 256x256, 128x128, 64x64, 32x32 and 16x16:

.. figure:: /_static/images/baboon_ico.jpg
   :width: 60%
   :align: center


Example 2: One Single Resolution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you do not wish to create a multi-resolution icon you can simply set MultiResolutionIcon to false:

   .. code-block:: C#
      :linenos:

      settings = new IcoRescaleSettings() {
         MultiResolutionIcon = false
      };

This will result in an .ico file that contains one single 200x200 image.

.. note::
   When MultiResolution is set to false, the asset will attempt to turn your texture into an .ico file without modifications. This means, you have to ensure yourself, that your texture is within the maximum resolution supported by .ico files (256x256). Otherwise you will encounter a runtime exception like: "Invalid texture resolution. ICO files support a maximum resolution of 256x256."

.. raw:: latex

    \newpage
    
Example 3: Different Scaling Modes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In example 1 you might have noticed, that the largest image used a resolution of 256x256 even though the initial texture has a resolution of 200x200. The reason is, that IcoRescaleSettings.DownscaleMode is set to 'DownscaleMode.ToNearest' by default. Thus the texture will be rescaled to the nearest power-of-two. If you wish to change this behaviour, you can specify a different mode like so:

   .. code-block:: C#
      :linenos:

      settings = new IcoRescaleSettings() {
         MultiResolutionIcon = true,
         DownscaleMode = DownscaleMode.None
      };

When specifying 'DownscaleMode.None', the resulting .ico file will contain the following 4 images with the resolutions 200x200, 100x100, 50x50, 25x25:

.. figure:: /_static/images/baboon_ico_200.jpg
   :width: 60%
   :align: center


The other modes 'DownscaleMode.ToLarger' and 'DownscaleMode.ToSmaller' work similar to the default 'DownscaleMode.ToNearest', but you can choose to always scale up or down to the next power-of-two respectively. 

.. note::
   | IcoRescaleSettings.DownscaleMode only has an effect if IcoRescaleSettings.MultiResolutionIcon is set to true.
   | Irrespective of which downscale mode is used, the largest image will always be clamped to the maximum supported resolution of 256x256 pixels.
