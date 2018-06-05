# Android 2D Game Development Notes 3

Random how to examples... continued.


## How to clear canvas?

```java
canvas.drawRGB(0, 0, 0);
```

## How to draw that f*king annoying rectangle?

```java
canvas.drawRect(x, y, RIGHT, BOTTOM, paint);
```

## How to draw image?

```java
canvas.drawBitmap(bitmap, x, y, paint);
```

## How to keep screen on?

```java
import android.view.WindowManager;

getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);

// To disable:
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
```

## How to draw text?

```java
canvas.drawText("Hello world!", x, y, paint);
```

## How to load a font?

```java
import android.graphics.Typeface;

try {
  Typeface t = Typeface.createFromAsset(getAssets(), "Quirlycues.ttf");
  paint.setTypeface(t);
} catch (Exception e) {
}
```

