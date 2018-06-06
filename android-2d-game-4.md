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

## How to handle single touch input?

```java
import android.view.MotionEvent;

private int touchState;
private float touchX;
private float touchY;

@Override
public boolean onTouchEvent(MotionEvent e) {
  switch (e.getActionMasked()) {
    case MotionEvent.ACTION_DOWN:
      touchState = 1;
      break;
    case MotionEvent.ACTION_MOVE:
      touchX = e.getX();
      touchY = e.getY();
      break;
    case MotionEvent.ACTION_UP:
    case MotionEvent.ACTION_CANCEL:
      touchState = 0;
      break;
  }
  return true;
}

private void onGameLoop() {
  // here:
  //   touch is pressed (similar to click): touchState == 1
  //   touch is down: touchState == 2
  if (touchState == 1) {
    touchState = 2;
  }
}
```

## How to handle multitouch input?

```java
import android.view.MotionEvent;

@Override
public boolean onTouchEvent(MotionEvent e) {
  int index = e.getActionIndex();
  int id = e.getPointerId(index);
  float x = e.getX(id);
  float y = e.getY(id);
  switch (e.getActionMasked()) {
    case MotionEvent.ACTION_DOWN:
    case MotionEvent.ACTION_POINTER_DOWN:
      // touch down
      break;
    case MotionEvent.ACTION_MOVE:
      // touch move
      break;
    case MotionEvent.ACTION_UP:
    case MotionEvent.ACTION_POINTER_UP:
    case MotionEvent.ACTION_CANCEL:
      // touch up
      break;
  }
  return true;
}
```

## How to play sounds?

```java
import android.media.MediaPlayer;
import android.content.res.AssetFileDescriptor;

private MediaPlayer player;

try {
  AssetFileDescriptor afd = getAssets().openFd("shoot.wav");
  player = new MediaPlayer();
  player.setDataSource(afd.getFileDescriptor(), afd.getStartOffset(), afd.getLength());
  afd.close();
  player.prepare();
} catch (Exception e) {
}

private void onGameLoop() {
  if (touchState == 1) {
      player.seekTo(0); // player.setLooping(true) for bgm
      player.start();
  }
}
```
