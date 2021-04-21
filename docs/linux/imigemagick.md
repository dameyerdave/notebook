# Image Magick

## Crop the image to the visible area

```bash
convert partial-trans.png -flatten -fuzz 1% -trim +repage trimmed.jpg
```

In case of problems with transparency

```bash
convert partial-trans.png -flatten -fuzz 1% -trim +repage trimmed.jpg
```
