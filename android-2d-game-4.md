# Android 2D Game Development Notes 4

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

# How to handle single touch input?

```java
import android.view.MotionEvent;

private int state;
private float touchX;
private float touchY;

@Override
public boolean onTouchEvent(MotionEvent e) {
  switch (e.getActionMasked()) {
    case MotionEvent.ACTION_DOWN:
      state = 1;
      break;
    case MotionEvent.ACTION_MOVE:
      touchX = e.getX();
      touchY = e.getY();
      break;
    case MotionEvent.ACTION_UP:
    case MotionEvent.ACTION_CANCEL:
      state = 2;
      break;
  }
}

private void onGameLoop() {
  // here:
  //   isPressed = state == 1
  //   isDown = state == 2
  if (state == 1) {
    state = 2;
  }
}
```
