# andorid.content.BroadcastReceiver #
- 接收snedBroadCast()方法传递的intents对象的基类。
- 如果你不需要在应用程序之间发送广播，考虑和 android.support.v4.content.LocalBroadcastManager一起来使用这个类，而不是和下面描述的几个工具。这样做会给你带来一个更有效的实现，并且允许你不用考虑关于其他应用程序能够接受和发送你的广播的安全性问题。
- 你也可以用Context.registerReceiver()动态地注册这个类的一个实例，或者在androidManifest.xml中通过`<receiver>`来声明一个实现。
- 注意：如果在Activity.onResume()中注册一个接收器，你应该在onPause()中来卸载它。（当暂停的时候不需要接受Intents，这样会减少系统开销)。不要在onSaveInstanceState()中卸载，因为this won't be called if the user moves back in the history stack. 
