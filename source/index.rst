Iconic (.ico Utilities)
=======================

.. meta::
   :description lang=en: A Cross-platform Unity utility for reading and writing .ico files.

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Overview:

   Introduction <self>
   
This documentation is currently in progress and will evolve as times goes on...

Usage
=====

Usage of the utility is pretty simple. There is a static class called 'IconConversion' that you can use to access various methods.

Loading .ico files
------------------

You can load an icon from various sources.

E.g. you can use
IconConversion.LoadIcon(string fileName)
IconConversion.LoadIcon(Stream stream)
IconConversion.LoadIcon(byte[] array)

Assuming we load an icon from a byte array 'myIconData', we'll use:
Icon icon = IconConversion.LoadIcon(myIconData);

Then we can use an extension method to turn the icon into a Texture2D like so
Texture2D myTexture = icon.ExtractTexture2D(imageIndex: 0);

As you'll see, you need to pass the index of the image to this method. An .ico file can contain multiple images, usually each with a different resolution. You can check Icon.NumImages for the total number of images that an icon contains.