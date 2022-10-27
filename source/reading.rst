Loading .ico files
==================

Usage of the utility is pretty simple. There is a static class called 'IconConversion' that you can use to access various methods.
You can load an icon from various sources.

| E.g. you can use one of the following methods
| ``IconConversion.LoadIcon(string fileName)``
| ``IconConversion.LoadIcon(Stream stream)``
| ``IconConversion.LoadIcon(byte[] array)``

| Assuming we load an icon from a byte array 'myIconData', we'll use:
| ``Icon icon = IconConversion.LoadIcon(myIconData);``

| Then we can use an extension method to turn the icon into a Texture2D like so
| ``Texture2D myTexture = icon.ExtractTexture2D(imageIndex: 0);``

As you see, you need to pass the index of the image to this method. An .ico file can contain multiple images, usually each with a different resolution. You can check Icon.NumImages for the total number of images that an icon contains.