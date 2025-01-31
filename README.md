This test project showcases how a very simple scenario with MSBuild's latest containerization SDK fails with Playwright.

Requirements:
- .NET 8 SDK
- Docker (or equivalent container technology)

Reproduce Steps:
- dotnet build
- dotnet publish /t:PublishContainer
- docker run -it --entrypoint bash playwrightexamplecontainer:latest

Observe that the test project cannot find the drivers.

```
PS C:\Github\PlaywrightContainerExample> docker run -it --entrypoint bash playwrightcontainerexample:latest
root@00df428ce03c:/app# printenv
NUGET_XMLDOC_MODE=skip
platformOptions__resultDirectory=/tmp/TestResults
HOSTNAME=00df428ce03c
DOTNET_VERSION=8.0.11
APP_UID=1654
PWD=/app
POWERSHELL_DISTRIBUTION_CHANNEL=PSDocker-DotnetSDK-Ubuntu-24.04
HOME=/root
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
PLAYWRIGHT_BROWSERS_PATH=/ms-playwright
DOTNET_SDK_VERSION=8.0.404
ASPNETCORE_HTTP_PORTS=8080
TERM=xterm
DOTNET_GENERATE_ASPNET_CERTIFICATE=false
SHLVL=1
ASPNET_VERSION=8.0.11
DOTNET_NOLOGO=true
DOTNET_RUNNING_IN_CONTAINER=true
DOTNET_USE_POLLING_FILE_WATCHER=true
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
_=/usr/bin/printenv
root@00df428ce03c:/app# dotnet test PlaywrightContainerExample.dll
VSTest version 17.11.1 (x64)

Starting test execution, please wait...
A total of 1 test files matched the specified pattern.
  Failed HomepageHasPlaywrightInTitleAndGetStartedLinkLinkingToTheIntroPage [13 ms]
  Error Message:
   Initialization method PlaywrightContainerExample.Test1.PlaywrightSetup threw exception. System.NullReferenceException: Object reference not set to an instance of an object..
  Stack Trace:
      at Microsoft.Playwright.Helpers.Driver.GetExecutablePath() in /_/src/Playwright/Helpers/Driver.cs:line 90
   at Microsoft.Playwright.Transport.StdIOTransport.GetProcess(String driverArgs) in /_/src/Playwright/Transport/StdIOTransport.cs:line 116
   at Microsoft.Playwright.Transport.StdIOTransport..ctor() in /_/src/Playwright/Transport/StdIOTransport.cs:line 46
   at Microsoft.Playwright.Playwright.CreateAsync() in /_/src/Playwright/Playwright.cs:line 43
   at Microsoft.Playwright.MSTest.PlaywrightTest.PlaywrightSetup() in /_/src/Playwright.MSTest/PlaywrightTest.cs:line 43


Failed!  - Failed:     1, Passed:     0, Skipped:     0, Total:     1, Duration: 21 ms - PlaywrightContainerExample.dll (net8.0)
```