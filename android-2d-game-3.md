# Android 2D Game Development Notes 3

Random how to examples.

## How to make your app fullscreen?

Add `android:theme="@android:style/Theme.NoTitleBar.Fullscreen"`.

```xml
<application android:label="@string/app_name" android:icon="@drawable/ic_launcher"
  android:theme="@android:style/Theme.NoTitleBar.Fullscreen">
```

## How to target specific screen orientation?

Add `android:screenOrientation="landscape"`, for example.

```xml
<activity android:name="HelloWorld"
  android:label="@string/app_name"
  android:screenOrientation="landscape">
```

## How to avoid that f*king blurry screen?

Add this under the `<manifest>` tag.

```xml
<supports-screens android:xlargeScreens="true" android:largeScreens="true" />
```

## How to make a game loop?

On android `Activity` class body:

```java
private volatile boolean running;

@Override
protected void onResume() {
  super.onResume();
  running = true;
  new Thread(new Runnable() {
    public void run() {
      long last = 0;
      while (running) {
        if (System.currentTimeMillis() - last > 1000 / 60) {
          // call onGameLoop() or do something...
          last = System.currentTimeMillis();
        }
      }
    }
  }).start();
}

@Override
protected void onPause() {
  super.onPause();
  running = false;
}
```

## How to load bitmap from assets?

Here I have `assets/a.png`. The following code is **inside** an `Activity` class.

```java
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;

try {
  Bitmap b = BitmapFactory.decodeStream(getAssets().open("a.png"));
} catch (Exception e) {
}
```

## How to double buffer?

```java
import android.graphics.Bitmap;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.view.SurfaceView;
import android.view.SurfaceHolder;

private Bitmap bitmap;
private Canvas canvas;
private Paint paint;
private SurfaceView view;
private SurfaceHolder holder;

@Override
public void onCreate(Bundle bundle) {
  super.onCreate(bundle);
  bitmap = Bitmap.createBitmap(569, 320, Bitmap.Config.ARGB_8888);
  canvas = new Canvas(bitmap);
  paint = new Paint();
  paint.setAntiAlias(false); // disable antialias
  paint.setFilterBitmap(false); // disable bitmap smoothing
  view = new SurfaceView(this);
  holder = view.getHolder();
  setContentView(view);
}

private void onGameLoop() {
  // draw to **this**.canvas here...
  // then draw to scaled back buffer to surface view:
  Canvas canvas = holder.lockCanvas();
  canvas.drawBitmap(bitmap, null, new RectF(0, 0, view.getWidth(), view.getHeight()), paint); 
                              // this RectF should be cached somehow to avoid GC
  holder.unlockCanvasAndPost(canvas);
}
```

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
