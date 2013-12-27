---
title: How to Enable WP8 Emulator on Mac
author: Tomomi Imura
layout: post
permalink: /blog/2013/01/09/how-to-enable-wp8-emulator-on-mac/
topsy_short_url:
  - http://is.gd/jj85w1
  - http://is.gd/jj85w1
dsq_thread_id:
  - 2067765977
categories:
  - IE
  - Mobile
  - Nokia
  - WindowsPhone
---
It appears to be that many Mac users, including myself, has had some trouble setting up Windows Phone SDK and run an WP emulator. I once gave up, but after spending some time searching and asking my coworkers around, I finally make Windows Phone 8 emulator runnable on my MacBook Pro, so before I totally forget how I did, I decide to blog and share it with you. (Notes: I am still on OS 10.7.5, on 2.4 GHz Intel Core MacBook Pro, with 8GB memory. and VMWare Fusion 4.1.4, not the latest.)

## Install VMWare

First of all, Windows Phone 8 SDK is not available for Mac, so you need to create a virtual machine and install Windows 8 on your Mac. My choice is <a href="http://www.vmware.com/products/fusion/overview.html" target="_blank">VMWare Fusion for Mac</a>. Download and install it to get started.

## Download Windows 8

You need to download **Windows 8 *64 bits* ISO**. You should be able to download the 90 days evaluation for developers from <a href="http://msdn.microsoft.com/en-us/evalcenter/jj554510.aspx" target="_blank">Microsoft MSDN</a>.

## Create a virtual machine

Launch VMWare Fusion, and go to menu, **File > New**. You should see a new dialog:  
[<img src="/assets/images/wp-content/uploads/2013/01/vm01.png" alt="" title="vm01" width="600" class="aligncenter size-full wp-image-633" />][1]

<img src="/assets/images/wp-content/uploads/2013/01/iso-icon.png" alt="" title="iso-icon" width="134" height="124" align="left" size-full style="margin-right:1em" wp-image-638" />Go back to Finder, where you have downloaded Windows 8 iso, grab the iso icon and drag it into the dialog.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2013/01/vm02.png" alt="" title="vm02" width="600" class="aligncenter size-full wp-image-641" />][2]

Then click **Continue**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm03.png" alt="" title="vm03" width="600" class="aligncenter size-full wp-image-644" />][3]

Leave them as-is, and click **Continue**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm04a.png" alt="" title="vm04a" width="600" class="aligncenter size-full wp-image-646" />][4]

Click **Customize Settings** before finishing.

[<img src="/assets/images/wp-content/uploads/2013/01/vm05.png" alt="" title="vm05" width="600" class="aligncenter size-full wp-image-647" />][5]

Name the virtual machine. e.g. &#8220;Windows 8&#8243;, and click **Save**. You should see the Setting dialog now.

[<img src="/assets/images/wp-content/uploads/2013/01/vm06a.png" alt="" title="vm06a" width="650" class="aligncenter size-full wp-image-648" />][6]

First, let&#8217;s click the **Processors &#038; Memory**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm07.png" alt="" title="vm07" width="650" class="aligncenter size-full wp-image-651" />][7]

Confugure the CPU by choosing **2 Processor Cores** from the first pull-down menu.  
Then increase memory. I chose 4096MB.

<em>Note: If you&#8217;re on VMWare Fusion 5, select <strong>Preferred virtualization engine: Intel VT-x with EPT option</strong> at the Advanced setting below the memory setting, and skip the next step. <a href="http://blogs.msdn.com/b/interoperability/archive/2012/12/21/how-to-develop-for-windows-phone-8-on-your-mac.aspx" target="_blank">See this article on MSDN</a>.  
If you're on VMWare Fusion 4.x like I do, follow the next step.</em>

Click **Show All** from top left to go back to the Setting menu, then click **Advanced**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm08a.png" alt="" title="vm08a" width="650" class="aligncenter size-full wp-image-652" />][8]

For **Preferred Virtualization Engine**, choose **Intel VT-x with EPT**.  
Close the Settings.

## Configure VM

Now, before launching Windows 8, you need to tweak some Virtual Machine configuration.  
Exit VMWare.

Then find your virtual machine, probably under `yourname/Documents/Virtual Machines/`. It may or may not has the `.vmwarevm` extension depending on your Mac setting.  
Ctrl-click and select **Show Package Contents**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm09a.png" alt="" title="vm09a" width="656" height="602" class="aligncenter size-full wp-image-679" />][9]

Now you should find a `.vmx` file.

[<img src="/assets/images/wp-content/uploads/2013/01/vm10.png" alt="" title="vm10" width="600" class="aligncenter size-full wp-image-653" />][10]

Open the file with a text editor of your choice.  
Then add these lines:

```bash
hypervisor.cpuid.v0 = "FALSE"
mce.enable = "TRUE"
vhv.enable = "TRUE"
```

[<img src="/assets/images/wp-content/uploads/2013/01/vm11.png" alt="" title="vm11" width="650"  class="aligncenter size-full wp-image-657" />][11]

Save it, then run the virtual machine.

## Launch Windows 8

[<img src="/assets/images/wp-content/uploads/2013/01/vm12.png" alt="" title="vm12" width="650"  class="aligncenter size-full wp-image-658" />][12]

Now, you are going to need to set up your Windows 8. Go ahead and finish them all.

## Install Windows Phone SDK

Once you&#8217;re done with the initial setups, open Internet Explorer and go to <a href="http://www.microsoft.com/en-us/download/details.aspx?id=35471" target="_blank">Microsoft Download Center</a>, then download and install **Windows Phone SDK 8.0** on your Windows 8.

<em>Notes: if you are ever asked to press Ctrl-Alt-Delete on Windows on VMWare, and if you're on MBP like I am, press <strong>Fn-Ctrl-Option-Delete</strong> combo.</em>

## Use Visual Studio Express

<img src="/assets/images/wp-content/uploads/2013/01/vm13.png" alt="" title="vm13" width="113" height="113" align="left" size-full style="margin-right:1em" wp-image-663" /> Now you should have **Visual Studio Express 2012 for Windows Phone** installed, so launch it!  
<br clear="all" />

Now go to **FILE > New Project&#8230;**  
Once you get the dialog, pick a project type. If you are reading my blog, you are very likely to be a web developer, so pick *Windows Phone HTML5 App* may be good! (but it does not really matter for now, because the ultimate purpose here is launching an emulator!)

[<img src="/assets/images/wp-content/uploads/2013/01/vm14a.png" alt="" title="vm14a" width="650"  class="aligncenter size-full wp-image-664" />][13]  
You get a bunch of stuff here &#8211; XAML template, visual editor etc, etc. 

## Launch emulator from Visual Studio Express

Click the emulator button.

[<img src="/assets/images/wp-content/uploads/2013/01/vm15a.png" alt="" title="vm15a" width="650" class="aligncenter size-full wp-image-665" />][14]

It should launch an WP emulator! Ta-da!

[<img src="/assets/images/wp-content/uploads/2013/01/vm16.png" alt="" title="vm16" width="650"  class="aligncenter size-full wp-image-666" />][15]

Unfortunate things can happen. If you get this error message and fail to launch the emulator,

<img src="/assets/images/wp-content/uploads/2013/01/vm17a.png" alt="" title="vm17a" width="374" height="165" class="aligncenter size-full wp-image-667" />

You probably did not configure the **.vmx** file correctly. Go to the top menu, **Virtual Machine > Shut down** (not Suspend) and shut down the VM completely first then re-edit and save the .vmx file. Re launch the VM and try again.

## Launch the emulator as stand-alone

OK, cool, but as a Mac-using web developer, you may not want to use Visual Studio as an IDE. But the WP8 emulator seems only running within Visual Studio. Do you need to open a dummy project all the time? 

No, you can hack it so the emulator can run as a stand-alone.

Go to Desktop, and Ctrl-click. Then **New > Shortcut**.

[<img src="/assets/images/wp-content/uploads/2013/01/vm18.png" alt="" title="vm18" width="650" class="aligncenter size-full wp-image-668" />][16]

To create a shortcut for **WVGA/512MB RAM** emulator, copy this and paste it into the field:  

```bash
"C:\Program Files (x86)\Microsoft XDE\8.0\XDE.exe" -createDiffDisk "%LOCALAPPDATA%\Microsoft\XDE\dd.480x800.512.vhd" -vhd "C:\Program Files (x86)\Microsoft SDKs\Windows Phone\v8.0\Emulation\Images\Flash.480x800.vhd"
```  
(All in one line, with the double-quotes).

<img src="/assets/images/wp-content/uploads/2013/01/vm19a.png" alt="" title="vm19a" width="624" height="463" class="aligncenter size-full wp-image-670" />

Then click **Next**. Name the shortcut. Then **Finish**.  
Now you should have the shortcut icon on desktop.  
Double-click to launch the WP8 emulator!

[<img src="/assets/images/wp-content/uploads/2013/01/vm20.png" alt="" title="vm20" width="650" class="aligncenter size-full wp-image-675" />][17]

For other emulators:

**WVGA**  

```bash
"C:\Program Files (x86)\Microsoft XDE\8.0\XDE.exe" -memsize 1024 -createDiffDisk "%LOCALAPPDATA%\Microsoft\XDE\dd.480x800.1024.vhd" -vhd "C:\Program Files (x86)\Microsoft SDKs\Windows Phone\v8.0\Emulation\Images\Flash.480x800.vhd"
```

**WXGA**  

```bash
"C:\Program Files (x86)\Microsoft XDE\8.0\XDE.exe" -memsize 1024 -createDiffDisk "%LOCALAPPDATA%\Microsoft\XDE\dd.768x1280.1024.vhd" -vhd "C:\Program Files (x86)\Microsoft SDKs\Windows Phone\v8.0\Emulation\Images\Flash.768x1280.vhd"
```

**720P**  

```bash
"C:\Program Files (x86)\Microsoft XDE\8.0\XDE.exe" -memsize 1024 -createDiffDisk "%LOCALAPPDATA%\Microsoft\XDE\dd.720x1280.1024.vhd" -vhd "C:\Program Files (x86)\Microsoft SDKs\Windows Phone\v8.0\Emulation\Images\Flash.720x1280.vhd"
```

## References

Nokia Developer Wiki:  
<a href="http://www.developer.nokia.com/Community/Wiki/Windows_Phone_8_SDK_on_a_Virtual_Machine_with_Working_Emulator" target="_blank">Windows Phone 8 SDK on a Virtual Machine with Working Emulator</a>

NSDN Blog:  
<a href="http://blogs.msdn.com/b/interoperability/archive/2012/12/21/how-to-develop-for-windows-phone-8-on-your-mac.aspx" target="_blank">How to develop for Windows Phone 8 on your Mac</a>

<a href="http://blogs.msdn.com/b/shintak/archive/2012/11/06/10366015.aspx" target="_blank">WP8 のエミュレーターを単体起動するためのショートカット</a>

 [1]: /assets/images/wp-content/uploads/2013/01/vm01.png
 [2]: /assets/images/wp-content/uploads/2013/01/vm02.png
 [3]: /assets/images/wp-content/uploads/2013/01/vm03.png
 [4]: /assets/images/wp-content/uploads/2013/01/vm04a.png
 [5]: /assets/images/wp-content/uploads/2013/01/vm05.png
 [6]: /assets/images/wp-content/uploads/2013/01/vm06a.png
 [7]: /assets/images/wp-content/uploads/2013/01/vm07.png
 [8]: /assets/images/wp-content/uploads/2013/01/vm08a.png
 [9]: /assets/images/wp-content/uploads/2013/01/vm09a.png
 [10]: /assets/images/wp-content/uploads/2013/01/vm10.png
 [11]: /assets/images/wp-content/uploads/2013/01/vm11.png
 [12]: /assets/images/wp-content/uploads/2013/01/vm12.png
 [13]: /assets/images/wp-content/uploads/2013/01/vm14a.png
 [14]: /assets/images/wp-content/uploads/2013/01/vm15a.png
 [15]: /assets/images/wp-content/uploads/2013/01/vm16.png
 [16]: /assets/images/wp-content/uploads/2013/01/vm18.png
 [17]: /assets/images/wp-content/uploads/2013/01/vm20.png