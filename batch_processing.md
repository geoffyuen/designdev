# Batch Processing

Here are useful terminal commands to automate repetitive tasks.

## PDF pages to jpg

Requires Ghostscript: `brew install ghostscript`

`gs -dNOPAUSE -sDEVICE=jpeg -r144 -sOutputFile=p%03d.jpg file.pdf`

## Resize images to 320px wide using SIPS (MacOS only?)

`sips --resampleWidth 320 *.png`

```
--resampleWidth <width in pixel>
--resampleHeight <height in pixels>
-Z <x y dimensions>
```
