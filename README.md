# Bypass GFE Login

Remove mandatory login for GeForce Experience

Works as of version 3.28.0.412

## How to Remove Mandatory Login

There are two methods for modifying the target file. Before replacing or
modifying this file, create a backup.

In File Explorer, go to:

``` Text
C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\
```

Backup `app.js` by creating a copy and renaming it something like
`app.js.backup`

### Method 1: Copy and paste pre-patched file

Download [pre-patched app.js](app.js) and move it into the `www` folder.

### Method 2: Manually patch file

1. Open `app.js` in a text editor that has find-and-replace functionality
(usually activated with `Ctrl`+`F` by default)

2. Skip displaying login dialog
    - Find:
        ``` JavaScript
        .selectView()}
        ```
    - Replace with:
        ``` JavaScript
        }
        ```

3. Spoof email verified status
    - Find:
        ``` JavaScript
        isLeftPaneVisible=function()
        ```
    - Replace with:
        ``` JavaScript
        handleLoggedIn({sessionToken:"1",userToken:"1",user:{core:{displayName:"",primaryEmailVerified:!0}}});
        ```

4. Spoof email verification for previously logged-in users
    - Find:
        ``` JavaScript
        domains.list){
        ```
    - Replace with:
        ``` JavaScript
        domains.list){return!0}else{return!0}{
        ```

5. Skip email verification prompt for previously logged-in users
    - Find:
        ``` JavaScript
        showEmailVerification=
        ```
    - Replace with:
        ``` JavaScript
        showEmailVerification=function(){},
        ```

6. (Optional) Force-enable in-game overlay button (ShadowPlay)
    - Find every instance of:
        ``` JavaScript
        isShareSupported=
        ```
    - Replace each instance with:
        ``` JavaScript
        isShareSupported=!0,
        ```

## How to Block Data Collection / Telemetry

1. Open the hosts file in a text editor:
    ``` Text
    C:\Windows\System32\drivers\etc\hosts
    ```
    - (copy-paste the file on your desktop to edit, copy back to "etc" folder
      if you have permission errors)

2. Add these lines to the bottom of the file only from one of the lists
    - Full blocklist
        : blocks telemetry / driver & GFE updates
    - Lite blocklist
        : only blocks telemetry (might break Game Optimizations in some cases)

3. If you previously blocked all nvidia domains, you need to flush your dns
cache to restore "Game List" and "Optimizations" functionality
    - Open Command Prompt and run the command `ipconfig /flushdns`

### Full Blocklist (as of GFE 3.20.3.63)

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

### Lite Blocklist (as of GFE 3.20.3.63)

`0.0.0.0 ls.dtrace.nvidia.com`  
`0.0.0.0 telemetry.gfe.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.cn`  
`0.0.0.0 nvidia.tt.omtrdc.net`  
`0.0.0.0 api.commune.ly`  
`0.0.0.0 login.nvgs.nvidia.com`  
`0.0.0.0 login.nvgs.nvidia.cn`  
