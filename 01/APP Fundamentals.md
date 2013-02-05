android学习，从翻译开始01 
==================

###                                                                 ----App Components之App Fundamentals

闲来无事，想学习学习android开发。官方网站上有比较系统的学习过程，硬着头皮看，看了一段时间觉得光看还不行，不翻译下来总觉得没看明白似的。所以尝试翻译一下，加深自己的理解。

----------

*Android applications are written in the Java programming language. The Android
SDK tools compile the code—along with any data and resource files—into an
Android package, an archive file with an .apk suffix. All the code in a single
.apk file is considered to be one application and is the file that
Android-powered devices use to install the application.*

Android应用程序使用java语言编写，android开发包工具将代码、各种数据和资源文件编译打包成一个andorid包，一个.apk后缀名的归档文件。.apk文件包含了一个应用程序的所有代码并且用来安装应用程序到android设备上。

*Once installed on a device, each Android application lives in its own security
sandbox:  The Android operating system is a multi-user Linux system in which
each application is a different user.  By default, the system assigns each
application a unique Linux user ID (the ID is used only by the system and is
unknown to the application). The system sets permissions for all the files in an
application so that only the user ID assigned to that application can access
them.  Each process has its own virtual machine (VM), so an application's code
runs in isolation from other applications.  By default, every application runs
in its own Linux process. Android starts the process when any of the
application's components need to be executed, then shuts down the process when
it's no longer needed or when the system must recover memory for other
applications. In this way, the Android system implements the principle of least
privilege. That is, each application, by default, has access only to the
components that it requires to do its work and no more. This creates a very
secure environment in which an application cannot access parts of the system for
which it is not given permission.*

一旦安装到设备上，每个APP在专属的受限的安全环境下运行。

-   android系统是一个多用户的系统，每个应用程序代表了一个用户。 -
    系统默认为每个APP分配一个独一无二的linux用户Id，只有系统能使用此ID，并且APP不知道ID的存在。系统为APP中的所有文件设置了访问权限，因此，只有分配给APP的那个用户ID能够访问它们。
    -  每个进程拥有独立的虚拟执行环境，所以APP之间的代码是相互隔离的。 -
    默认情况下，每个app都在自己所属的进程中执行。当一个APP的组件需要被执行，android会启动进程，当不再需要执行或者当系统内存不足，需要恢复内存的时候，会结束进程。

这样，android系统实现了最小特权原则。也就是说，默认情况下，每个APP只能访问它需要的组件来完成任务。这样就建立了一个安全机制，在这种机制下，app不能访问未授权的系统资源。

*However, there are ways for an application to share data with other
applications and for an application to access system services: It's possible to
arrange for two applications to share the same Linux user ID, in which case they
are able to access each other's files. To conserve system resources,
applications with the same user ID can also arrange to run in the same Linux
process and share the same VM (the applications must also be signed with the
same certificate).  An application can request permission to access device data
such as the user's contacts, SMS messages, the mountable storage (SD card),
camera, Bluetooth, and more. All application permissions must be granted by the
user at install time.*

但是，还存在一些方法使得一个APP能够和其他APP分享数据并且能够访问系统服务:  -
为两个APP分配同一个ID是可能的，在这种情况下，它们能够互访彼此的文件。为了节省系统资源，具有相同ID的apps也能够在同一个进程中执行和共享虚拟机。（apps必须拥有相同的数字签名).
- 一个APP可以请求获取访问设备数据的权限，比如：联系人、短信、sd卡、相机、蓝牙等等。所有的权限必须在安装APP的时候获得用户的允许。

*That covers the basics regarding how an Android application exists within the
system. The rest of this document introduces you to: The core framework
components that define your application.  The manifest file in which you declare
components and required device features for your application.  Resources that
are separate from the application code and allow your application to gracefully
optimize its behavior for a variety of device configurations.*

以上包含了andorid app存在于系统的一些基本概念。接下来将介绍：   - 定义APP的核心框架组件 - 组件和设备特征的声明文件，manifest文件。
- 资源文件，和代码分离，允许app尽可能地为一系列的设备配置优化它的表现和行为。

### Application Components 

* Application components are the essential building blocks of an Android
application. Each component is a different point through which the system can
enter your application. Not all components are actual entry points for the user
and some depend on each other, but each one exists as its own entity and plays a
specific role—each one is a unique building block that helps define your
application's overall behavior. *

[^]: **APP
components是android程序的基本组成块。每个component都是系统进入到你的程序的点。对于用户来说，不是所有的组件都是入口点并且相互依赖，但是每个组件都有自己的实体并且扮演者一个具体的角色--每一个组件都是一个独一无二的部件，这些部件定义了app的所有行为。***这一段翻译地很别扭啊。*

* There are four different types of application components. Each type serves a
distinct purpose and has a distinct lifecycle that defines how the component is
created and destroyed.*

有四种类型的组件，每种类型每种组件都提供不同的使用目的和不同的定义组件怎么创建和销毁的生命周期。

*Here are the four types of application components:*

*Activities  An activity represents a single screen with a user interface. For
example, an email application might have one activity that shows a list of new
emails, another activity to compose an email, and another activity for reading
emails. Although the activities work together to form a cohesive user experience
in the email application, each one is independent of the others. As such, a
different application can start any one of these activities (if the email
application allows it). For example, a camera application can start the activity
in the email application that composes new mail, in order for the user to share
a picture.  An activity is implemented as a subclass of Activity and you can
learn more about it in the Activities developer guide.*

以下是四种组件:

Activities：一个activity代表了一个用户界面。例如：邮件APP可能有一个显示新邮件列表的activity，另外一个activity用来写邮件，还有一个activity用来查看邮件内容。尽管在email
app中activities协同工作组成了一个密切相关的用户体验，但是每个activity都是相对独立的。同样的，其他的APP能够启动这些activity中的任何一个，前提是email
APP允许这样做。例如，为了用户能够分享一张照片，相机APP能够启动写email的activity。构建一个activity通常继承Activity类来实现，并且你可以在Activities
Developer Guide中了解更多。

*Services:A service is a component that runs in the background to perform
long-running operations or to perform work for remote processes. A service does
not provide a user interface. For example, a service might play music in the
background while the user is in a different application, or it might fetch data
over the network without blocking user interaction with an activity. Another
component, such as an activity, can start the service and let it run or bind to
it in order to interact with it.  A service is implemented as a subclass of
Service and you can learn more about it in the Services developer guide.*

Service
:一个Service组件在后台运行，执行一个耗时的操作或者执行远程的处理工作。service不提供用户界面。例如:service可能在用户使用别的app的时候在后台播放音乐，或者它可以在不阻塞用户和activity交互情况下通过网络获取数据。其他的组件，比如一个Activity可以启动service并且使他运行或者和它绑定以便和它交互。构建一个Service通常是继承自Service类，你可以在Services
Developer guide中了解更多。

*Content providers  A content provider manages a shared set of application data.
You can store the data in the file system, an SQLite database, on the web, or
any other persistent storage location your application can access. Through the
content provider, other applications can query or even modify the data (if the
content provider allows it). For example, the Android system provides a content
provider that manages the user's contact information. As such, any application
with the proper permissions can query part of the content provider (such as
ContactsContract.Data) to read and write information about a particular person.
Content providers are also useful for reading and writing data that is private
to your application and not shared. For example, the Note Pad sample application
uses a content provider to save notes.*

*A content provider is implemented as a subclass of ContentProvider and must
implement a standard set of APIs that enable other applications to perform
transactions. For more information, see the Content Providers developer guide.*

Content Providers 一个content
provider管理着一组共享的应用程序数据。你可以将数据存储在文件系统中，sqlLite数据库，web存储器或者其他任何你可以访问到的存储位置。通过content
Provider，其他APP能够查询数据，如果contentProvider允许，还可以修改数据。例如，android系统提供了一个管理用户的通讯录的content
provider。任何拥有特有许可的app可以查询content provider中的一部分来读写某个人的信息。Content
provider在读写app私有的数据时很有用。例如Note Pad样例程序使用content provider来保存笔记。要构建一个content
provider通常继承自ContentProvider类，并且必须实现一组标准的api，以便其他应用程序能够处理。参照Content Providers
Developer guide获取更多的信息。



Broadcast receivers  A broadcast receiver is a component that responds to
system-wide broadcast announcements. Many broadcasts originate from the
system—for example, a broadcast announcing that the screen has turned off, the
battery is low, or a picture was captured. Applications can also initiate
broadcasts—for example, to let other applications know that some data has been
downloaded to the device and is available for them to use. Although broadcast
receivers don't display a user interface, they may create a status bar
notification to alert the user when a broadcast event occurs. More commonly,
though, a broadcast receiver is just a "gateway" to other components and is
intended to do a very minimal amount of work. For instance, it might initiate a
service to perform some work based on the event.  A broadcast receiver is
implemented as a subclass of BroadcastReceiver and each broadcast is delivered
as an Intent object. For more information, see the BroadcastReceiver class.

Broadcast receivers:一个broadcast
receiver是一个能够响应系统级的广播通知的组件。许多广播来源于系统--例如，一个通知屏幕关闭的广播，电量过低或者拍摄的照片。APP也能够发起广播--比如，通知其他app数据已经下载完成并且可以使用。虽然broadcast
receivers不显示用户界面，当广播时间发生时，它们可能会建立一个状态条通知来提示用户。

A unique aspect of the Android system design is that any application can start
another application’s component. For example, if you want the user to capture a
photo with the device camera, there's probably another application that does
that and your application can use it, instead of developing an activity to
capture a photo yourself. You don't need to incorporate or even link to the code
from the camera application. Instead, you can simply start the activity in the
camera application that captures a photo. When complete, the photo is even
returned to your application so you can use it. To the user, it seems as if the
camera is actually a part of your application.

When the system starts a component, it starts the process for that application
(if it's not already running) and instantiates the classes needed for the
component. For example, if your application starts the activity in the camera
application that captures a photo, that activity runs in the process that
belongs to the camera application, not in your application's process. Therefore,
unlike applications on most other systems, Android applications don't have a
single entry point (there's no main() function, for example).

Because the system runs each application in a separate process with file
permissions that restrict access to other applications, your application cannot
directly activate a component from another application. The Android system,
however, can. So, to activate a component in another application, you must
deliver a message to the system that specifies your intent to start a particular
component. The system then activates the component for you.

Activating Components Three of the four component types—activities, services,
and broadcast receivers—are activated by an asynchronous message called an
intent. Intents bind individual components to each other at runtime (you can
think of them as the messengers that request an action from other components),
whether the component belongs to your application or another.

An intent is created with an Intent object, which defines a message to activate
either a specific component or a specific type of component—an intent can be
either explicit or implicit, respectively.

For activities and services, an intent defines the action to perform (for
example, to "view" or "send" something) and may specify the URI of the data to
act on (among other things that the component being started might need to know).
For example, an intent might convey a request for an activity to show an image
or to open a web page. In some cases, you can start an activity to receive a
result, in which case, the activity also returns the result in an Intent (for
example, you can issue an intent to let the user pick a personal contact and
have it returned to you—the return intent includes a URI pointing to the chosen
contact).

For broadcast receivers, the intent simply defines the announcement being
broadcast (for example, a broadcast to indicate the device battery is low
includes only a known action string that indicates "battery is low").

The other component type, content provider, is not activated by intents. Rather,
it is activated when targeted by a request from a ContentResolver. The content
resolver handles all direct transactions with the content provider so that the
component that's performing transactions with the provider doesn't need to and
instead calls methods on the ContentResolver object. This leaves a layer of
abstraction between the content provider and the component requesting
information (for security).

There are separate methods for activating each type of component:

You can start an activity (or give it something new to do) by passing an Intent
to startActivity() or startActivityForResult() (when you want the activity to
return a result).  You can start a service (or give new instructions to an
ongoing service) by passing an Intent to startService(). Or you can bind to the
service by passing an Intent to bindService().  You can initiate a broadcast by
passing an Intent to methods like sendBroadcast(), sendOrderedBroadcast(), or
sendStickyBroadcast().  You can perform a query to a content provider by calling
query() on a ContentResolver.  For more information about using intents, see the
Intents and Intent Filters document. More information about activating specific
components is also provided in the following documents: Activities, Services,
BroadcastReceiver and Content Providers.

The Manifest File Before the Android system can start an application component,
the system must know that the component exists by reading the application's
AndroidManifest.xml file (the "manifest" file). Your application must declare
all its components in this file, which must be at the root of the application
project directory.

The manifest does a number of things in addition to declaring the application's
components, such as:

Identify any user permissions the application requires, such as Internet access
or read-access to the user's contacts.  Declare the minimum API Level required
by the application, based on which APIs the application uses.  Declare hardware
and software features used or required by the application, such as a camera,
bluetooth services, or a multitouch screen.  API libraries the application needs
to be linked against (other than the Android framework APIs), such as the Google
Maps library.  And more  Declaring components The primary task of the manifest
is to inform the system about the application's components. For example, a
manifest file can declare an activity as follows:

<?xml version="1.0" encoding="utf-8"?> <manifest ... > <application
android:icon="@drawable/app_icon.png" ... > <activity
android:name="com.example.project.ExampleActivity"
android:label="@string/example_label" ... > </activity> ... </application>
</manifest>In the <application> element, the android:icon attribute points to
resources for an icon that identifies the application.

In the <activity> element, the android:name attribute specifies the fully
qualified class name of the Activity subclass and the android:label attributes
specifies a string to use as the user-visible label for the activity.

You must declare all application components this way:

<activity> elements for activities  <service> elements for services  <receiver>
elements for broadcast receivers  <provider> elements for content providers
Activities, services, and content providers that you include in your source but
do not declare in the manifest are not visible to the system and, consequently,
can never run. However, broadcast receivers can be either declared in the
manifest or created dynamically in code (as BroadcastReceiver objects) and
registered with the system by calling registerReceiver().

For more about how to structure the manifest file for your application, see the
The AndroidManifest.xml File documentation.

Declaring component capabilities As discussed above, in Activating Components,
you can use an Intent to start activities, services, and broadcast receivers.
You can do so by explicitly naming the target component (using the component
class name) in the intent. However, the real power of intents lies in the
concept of intent actions. With intent actions, you simply describe the type of
action you want to perform (and optionally, the data upon which you’d like to
perform the action) and allow the system to find a component on the device that
can perform the action and start it. If there are multiple components that can
perform the action described by the intent, then the user selects which one to
use.

The way the system identifies the components that can respond to an intent is by
comparing the intent received to the intent filters provided in the manifest
file of other applications on the device.

When you declare a component in your application's manifest, you can optionally
include intent filters that declare the capabilities of the component so it can
respond to intents from other applications. You can declare an intent filter for
your component by adding an <intent-filter> element as a child of the
component's declaration element.

For example, an email application with an activity for composing a new email
might declare an intent filter in its manifest entry to respond to "send"
intents (in order to send email). An activity in your application can then
create an intent with the “send” action (ACTION_SEND), which the system matches
to the email application’s “send” activity and launches it when you invoke the
intent with startActivity().

For more about creating intent filters, see the Intents and Intent Filters
document.

Declaring application requirements There are a variety of devices powered by
Android and not all of them provide the same features and capabilities. In order
to prevent your application from being installed on devices that lack features
needed by your application, it's important that you clearly define a profile for
the types of devices your application supports by declaring device and software
requirements in your manifest file. Most of these declarations are informational
only and the system does not read them, but external services such as Google
Play do read them in order to provide filtering for users when they search for
applications from their device.

For example, if your application requires a camera and uses APIs introduced in
Android 2.1 (API Level 7), you should declare these as requirements in your
manifest file. That way, devices that do not have a camera and have an Android
version lower than 2.1 cannot install your application from Google Play.

However, you can also declare that your application uses the camera, but does
not require it. In that case, your application must perform a check at runtime
to determine if the device has a camera and disable any features that use the
camera if one is not available.

Here are some of the important device characteristics that you should consider
as you design and develop your application:

Screen size and density  In order to categorize devices by their screen type,
Android defines two characteristics for each device: screen size (the physical
dimensions of the screen) and screen density (the physical density of the pixels
on the screen, or dpi—dots per inch). To simplify all the different types of
screen configurations, the Android system generalizes them into select groups
that make them easier to target.  The screen sizes are: small, normal, large,
and extra large. The screen densities are: low density, medium density, high
density, and extra high density.

By default, your application is compatible with all screen sizes and densities,
because the Android system makes the appropriate adjustments to your UI layout
and image resources. However, you should create specialized layouts for certain
screen sizes and provide specialized images for certain densities, using
alternative layout resources, and by declaring in your manifest exactly which
screen sizes your application supports with the <supports-screens> element.

For more information, see the Supporting Multiple Screens document.

Input configurations  Many devices provide a different type of user input
mechanism, such as a hardware keyboard, a trackball, or a five-way navigation
pad. If your application requires a particular kind of input hardware, then you
should declare it in your manifest with the <uses-configuration> element.
However, it is rare that an application should require a certain input
configuration.  Device features  There are many hardware and software features
that may or may not exist on a given Android-powered device, such as a camera, a
light sensor, bluetooth, a certain version of OpenGL, or the fidelity of the
touchscreen. You should never assume that a certain feature is available on all
Android-powered devices (other than the availability of the standard Android
library), so you should declare any features used by your application with the
<uses-feature> element.  Platform Version  Different Android-powered devices
often run different versions of the Android platform, such as Android 1.6 or
Android 2.3. Each successive version often includes additional APIs not
available in the previous version. In order to indicate which set of APIs are
available, each platform version specifies an API Level (for example, Android
1.0 is API Level 1 and Android 2.3 is API Level 9). If you use any APIs that
were added to the platform after version 1.0, you should declare the minimum API
Level in which those APIs were introduced using the <uses-sdk> element.  It's
important that you declare all such requirements for your application, because,
when you distribute your application on Google Play, the store uses these
declarations to filter which applications are available on each device. As such,
your application should be available only to devices that meet all your
application requirements.

For more information about how Google Play filters applications based on these
(and other) requirements, see the Filters on Google Play document.

Application Resources An Android application is composed of more than just
code—it requires resources that are separate from the source code, such as
images, audio files, and anything relating to the visual presentation of the
application. For example, you should define animations, menus, styles, colors,
and the layout of activity user interfaces with XML files. Using application
resources makes it easy to update various characteristics of your application
without modifying code and—by providing sets of alternative resources—enables
you to optimize your application for a variety of device configurations (such as
different languages and screen sizes).

For every resource that you include in your Android project, the SDK build tools
define a unique integer ID, which you can use to reference the resource from
your application code or from other resources defined in XML. For example, if
your application contains an image file named logo.png (saved in the
res/drawable/ directory), the SDK tools generate a resource ID named
R.drawable.logo, which you can use to reference the image and insert it in your
user interface.

One of the most important aspects of providing resources separate from your
source code is the ability for you to provide alternative resources for
different device configurations. For example, by defining UI strings in XML, you
can translate the strings into other languages and save those strings in
separate files. Then, based on a language qualifier that you append to the
resource directory's name (such as res/values-fr/ for French string values) and
the user's language setting, the Android system applies the appropriate language
strings to your UI.

Android supports many different qualifiers for your alternative resources. The
qualifier is a short string that you include in the name of your resource
directories in order to define the device configuration for which those
resources should be used. As another example, you should often create different
layouts for your activities, depending on the device's screen orientation and
size. For example, when the device screen is in portrait orientation (tall), you
might want a layout with buttons to be vertical, but when the screen is in
landscape orientation (wide), the buttons should be aligned horizontally. To
change the layout depending on the orientation, you can define two different
layouts and apply the appropriate qualifier to each layout's directory name.
Then, the system automatically applies the appropriate layout depending on the
current device orientation.

For more about the different kinds of resources you can include in your
application and how to create alternative resources for various device
configurations, see the Application Resources developer guide.
