# BaiGfe
Remove Mandatory Login of Geforce Experience - [support: v3.14.x to v3.27.x(current)]
# How to Remove Mandatory Login  

make a backup of every files you edit !

# Easy copy/paste fix :  

Download pre-moded app.js : [https://github.com/Moyster/BaiGfe/raw/master/app.js](https://github.com/Moyster/BaiGfe/raw/master/app.js)

Copy/paste to :

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

# Auto-install easy fix :

**Right-click Install-Fix.ps1 and choose Run as Administrator**

&#x200B;

You may need to allow the script to run on your system. To do this: 

1. Run powershell as administrator, then run this powershell call : 
```
Set-ExecutionPolicy RemoteSigned
```
 2. Type "A" then hit enter and re-run Install-Fix.ps1

&#x200B;

# Manual way :  

Open `app.js` found in :  

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

1. Skip displaying login dialog

Find:

``` JavaScript
.selectView()}
```

Replace:

``` JavaScript
}
```

&#x200B;

2. Spoof email verification status

Find:

``` JavaScript
isLeftPaneVisible=function()
```

Replace:

``` JavaScript
handleLoggedIn({sessionToken:"1",userToken:"1",user:{core:{displayName:"",primaryEmailVerified:!0}}});
```

&#x200B;

3. Skip email verification prompt for previously logged-in accounts

Find:

``` JavaScript
domains.list){
```

Replace:

``` JavaScript
domains.list){return!0}else{return!0}{
```

Find:

``` JavaScript
showEmailVerification=
```

Replace:

``` JavaScript
showEmailVerification=function(){},
```

&#x200B;

4. (Optional) Force-enable in-game overlay button (ShadowPlay)

Find every instance of:

``` JavaScript
isShareSupported=
```

Replace each instance with:

``` JavaScript
isShareSupported=!0,
```

# How to Block Data Collection / Telemetry (block all or keep Games Optimisations)

Step 1 - Open the hosts file in a text editor (notepad++) :

    C:\Windows\System32\drivers\etc\hosts 

(copy-paste the file on your desktop to edit, copy back to "etc" folder if you have permission errors)

Step 2 - Add at the end of the file (CHOOSE ONE OR THE OTHER LIST, NOT BOTH) :  
> Full blocklist: blocks telemetry / driver & Gfe updates (Keeps Game Optimisations and all "offline" features working)
> Lite blocklist : only blocks telemetry (might break Game Optimisations in some cases, fix/workaround pending)

- FULL BLOCKLIST : (as of 04/17/2020 - GFE 3.20.3.63)  

`0.0.0.0 telemetry.gfe.nvidia.com`  
`0.0.0.0 gfe.nvidia.com`  
`0.0.0.0 gfwsl.geforce.com`  
`0.0.0.0 services.gfe.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.cn`  
`0.0.0.0 events.gfe.nvidia.com`  
`0.0.0.0 img.nvidiagrid.net`  
`0.0.0.0 images.nvidiagrid.net`  
`0.0.0.0 images.nvidia.com`  
`0.0.0.0 ls.dtrace.nvidia.com`  
`0.0.0.0 ota.nvidia.com`  
`0.0.0.0 ota-downloads.nvidia.com`  
`0.0.0.0 rds-assets.nvidia.com`  
`0.0.0.0 assets.nvidiagrid.net`  
`0.0.0.0 nvidia.tt.omtrdc.net`  
`0.0.0.0 api.commune.ly`  
`0.0.0.0 login.nvgs.nvidia.com`  
`0.0.0.0 login.nvgs.nvidia.cn`  


- LITE BLOCKLIST (keep GFE / Drivers Update working) : (as of 04/17/2020 - GFE 3.20.3.63)  

    might break Game List for now, use the full blocklist if it does

`0.0.0.0 ls.dtrace.nvidia.com`  
`0.0.0.0 telemetry.gfe.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.cn`  
`0.0.0.0 nvidia.tt.omtrdc.net`  
`0.0.0.0 api.commune.ly`  
`0.0.0.0 login.nvgs.nvidia.com`  
`0.0.0.0 login.nvgs.nvidia.cn`  

("[0.0.0.0](https://0.0.0.0)" is preferred to "[127.0.0.1](https://127.0.0.1)" but both works)  
( If you previously blocked all nvidia domains, you need to flush your dns cache to restore "Game Optimizations" functionality :  
open "CMD" > `ipconfig /flushdns` )

Save and forget :)  

&#x200B;

PS: The "beautified" version of app.js will work just fine, you can minify it back, but it's not mandatory (just like login :) ).

*Post and fix based off the previous mod author(s), mainly :* [*https://www.reddit.com/r/nvidia/comments/8b5nej/updated\_remove\_mandatory\_login\_of\_geforce/*](https://www.reddit.com/r/nvidia/comments/8b5nej/updated_remove_mandatory_login_of_geforce/)
