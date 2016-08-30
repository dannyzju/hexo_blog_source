---
title: Android中的Threads的实现
date: 2016-08-25 00:33:19
tags:
- Android
---
在Android想要创建后台任务时该怎么做呢？最简单粗暴的方法就是通过创建一个background thread来实现，这里我们以后台下载音乐为例。

首先建立一个Playlist的类，添加需要下载的曲目:
```java
public class Playlist {
    public static String[] songs = {"He’s the Greatest Dancer", "Cut the Cake", "The Groove Line", "Stayin’ Alive", "Give Up the Funk"};
}
```


### 1. 通过Runnable实现
```java
mDownloadButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                downloadSong();
            }
        };

        Thread thread = new Thread(runnable);
        thread.setName("DownloadThread");
        thread.start();
    }
}
```


### 2. 通过继承Thread实现
首先创建一个DownloadThread如下所示：
```java
public class DownloadThread extends Thread {
    @Override
    public void run() {
        downloadSong();
    }
    ...
}
```

然后再创建一个新的DownloadThread实例，调用start()方法即可。
```java
mDownloadButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        DownloadThread thread = new DownloadThread();
        thread.setName("DownloadThread");
        thread.start();
    }
}
```


通过以上两种形式，我们成功实现了在background thread下载歌曲。然而新的潜在问题是，若开始下载后Playlist中的曲目被误改，则很可能错误的曲目会被下载下来。那么如何避免这种情况呢？

### 3. Handler, Looper和Message

首先创建一个DownloadHandler类
```java
import android.os.Handler;
public class DownloadHandler () extends Handler {
    @Override
    public void handleMessage(Message msg) {
        downloadSong(msg.obj.toString());
    }

    private void downloadSong(String song) {
        long endTime = System.currentTimeMillis() + 10 * 1000;
        while (System.currentTimeMillis() < endTime) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        Log.d(TAG, song + " downloaded!");
    }
}
```

其次修改DownloadThread中的run 方法
```java
import android.os.Looper;
public class DownloadThread extends Thread {
    public DownloadHandler mHandler;

    @Override
    public void run() {
        Looper.prepare();
        mHandler = new DownloadHandler();
        Looper.loop();
    }
}
```

最后在点击Button时把要下载的曲目通过Message的形式送到DownloadThread的handler中即可。
```java
DownloadThread thread = new DownloadThread();
thread.setName("DownloadThread");
thread.start();
mDownloadButton = (Button) findViewById(R.id.downloadButton);
mDownloadButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        for (String song : Playlist.songs) {
            Message message = Message.obtain();
            message.obj = song;
            thread.mHandler.sendMessage(message);
        }
    }
}
```

当app被关掉之后，我们创建的DownloadThread也就同时被kill了。但如果我们想要在app被关闭之还能在后台继续下载歌曲怎么办呢？这就要引入Android Service了，且看下回分解。