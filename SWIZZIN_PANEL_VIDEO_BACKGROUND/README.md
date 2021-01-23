![](https://user-images.githubusercontent.com/77786782/105615322-a7b77980-5d9d-11eb-925d-e05cca68540b.png)

# VIDEO EXAMPLES:  
 

## \-BACKUP YOUR EXISTING "/templates" & "/imgs" FOLDERS-  
\-BACKUP YOUR EXISTING "/templates" & "/imgs" FOLDERS-  
\-BACKUP YOUR EXISTING "/templates" & "/imgs" FOLDERS-

## Backup versions of all files for the Swizzin panel can be found here (JUST IN CASE):  
[https://github.com/liaralabs/swizzin_dashboard](https://github.com/liaralabs/swizzin_dashboard)

​

To keep it easy on everyone, I went ahead and made three different _**premade**_ _**login.html**_ pages, each with their own different video background (see examples above). I hope it provides a solid start for anyone wanting to branch out and create their own.. I already optimized the mp4 files (bitrate/resolution/file size/etc), and I also created background images from the first frame of each video. These background images (posters) load first so the page isn't blank for individuals on slower connections.

_**AT THE END OF THIS GUIDE, I INCLUDED SOME EASY PEASY INFO ON MAKING YOUR OWN VIDEO BACKGROUND...**_

~**VIRUSTOTAL.COM**~ ~(0/61 AKA IT'S CLEAN LOL)~[~https://www.virustotal.com/gui/file/e366440830dc57ef3e803eb351979cfa4f930b27976c1af8236cf4c7c8d5ba86/detection~](https://www.virustotal.com/gui/file/e366440830dc57ef3e803eb351979cfa4f930b27976c1af8236cf4c7c8d5ba86/detection)

~**DOWNLOAD THE ZIP:**~[~https://mega.nz/file/HTIDgaSZ#e76W-Pm8z2Ivl04YCsJfT1RPN9zs2rSQx_jdqZs9ZRU~](https://mega.nz/file/HTIDgaSZ#e76W-Pm8z2Ivl04YCsJfT1RPN9zs2rSQx_jdqZs9ZRU)

**Virus Scan:**[**VIRUSTOTAL SCAN (0/60)**](https://www.virustotal.com/gui/file/77f7ef64347bec1089b7b694281a5c055bd66d8e25bbc17614cd5cbc52851fa9/detection)

**Download v2:**[**MEGA LINK TO V2 ZIP**](https://mega.nz/file/aSIw3brY#rPAclB4f2d388vkjCQ9GJF-b13II09qucJODwukpFmI)

**I tried to structure the ZIP folder to mimic the swizzin directories...once you've downloaded the zip from mega, go ahead and extract the zip file.**

**Once extracted, it will look like the tree below...hopefully this tree helps make sense of things....and the folders where these new files need to go:**

**You can either copy everything over at once, or just one set at a time.Just make sure you copy over the jpg/mp4 files that match the xxxxx\_login.html file**

\*\*\*For example..if you just wanted the "neon\_retro" version.. make sure to copy over all three matching items in to their designated dirs:\*\*\*

**Once you have your .mp4/.jpg in the** `/opt/swizzin/swizzin/img` **dir....and your xxxxxx\_login.html file in the** `/opt/swizzin/swizzin/templates` **dir (AND BACKUPS MADE) it's finally time to rename the custom xxxxx\_login.html page, making it your NEW login.html...so if you have been following along, you will have put the new xxxxxx\_login.html page inside of the /templates dir..**

**Go to the** `/opt/swizzin/swizzin/templates` **DIR if you're not already in there..**

**You're going to make the new video background login page THE NEW login.html page**...

**An example would be:**`sudo cd /opt/swizzin/swizzin/templatessudo mv ./neon_retro_login.html ./login.html`

**LET'S BE SAFE AND SET THE PROPER PERMISSIONS FOR THE NEW FILES, JUST IN CASE THEY CHANGED DURING THE PROCESS..**

**..RUN THESE COMMANDS BELOW, I'M USING THE "neon\_retro\_login" version in the example here:**`sudo chown swizzin:swizzin /opt/swizzin/swizzin/templates/login.htmlsudo chmod /opt/swizzin/swizzin/templates/login.htmlsudo chown swizzin:swizzin /opt/swizzin/swizzin/img/neon_retro.*sudo chmod /opt/swizzin/swizzin/static/img/neon_retro.*`

**VERIFY THAT THE PERMISSIONS HAVE BEEN SET..RUN:**`sudo ls -lshR /opt/swizzin/swizzin/`

**You should see the following:**(`swizzin:swizzin -rw-r--r--`)

**Alright the last thing we have to do is restart the systemd service for the swizzin panel....**

**RUN THE FOLLOWING COMMAND TO RESTART THE PANEL SERVICE:**`sudo systemctl restart panel.service`

**...and there ya go! Go to your swizzin install and your new login page is alive!**

**NOTE ANY TIME YOU MAKE ANY CHANGES TO THE LOGIN.HTML FILE OR FILES SOURCED IN THE LOGIN.HTML YOU MUST RESTART THE SYSTEMD PANEL SERVICE. THE FILES ARE IN A CACHE, AND UNLESS YOU RUN A RESTART ON THE SERVICE, YOU WON'T SEE ANY CHANGES.If you want to make your own video background, below I've included a site with a ton of free video loops:**[https://pixabay.com/videos/search/looping/](https://pixabay.com/videos/search/looping/)

​

**I'VE MADE THIS SIMPLE ONE LINER THAT WILL CONVERT ALL THE .MP4 FILES INSIDE OF A DIR TO THE PROPER FORMAT, AS WELL AS CREATE THE BACKGROUND IMAGES OF THE FIRST FRAME OF EACH VIDEO...MAKE SURE YOU HAVE FFMPEG INSTALLED!**`mkdir ./OG_VIDZ; for i in *.mp4; do ffmpeg -i "$i" -c:v h264 -an -r:v 24 -b:v 1500k "${i%%.*}_24fps.mp4" && ffmpeg -ss 00:00:1 -i "$i" -vframes 1 -q:v 2 "${i%%.*}.jpg" && mv "$i" ./OG_VIDZ ; done`

**UPDATE:MORE ONE LINERS:**

_This line cmd is the same as above, except it doesn't add the \_24fps...basically it backups up the OG mp4 files to a folder called OG\_VIDZ, converts them to a proper file size, makes a jpg for the first frame, and then renames the new mp4 files back to the original name:_`mkdir ./OG_VIDZ; for i in *.mp4; do ffmpeg -i "$i" -c:v h264 -an -r:v 24 -b:v 1500k "${i%%.*}_24fps.mp4" && ffmpeg -ss 00:00:1 -i "$i" -vframes 1 -q:v 2 "${i%%.*}.jpg" && mv "$i" ./OG_VIDZ ; done && rename 's/_24fps//' ./*.mp4`

_This cmd converts any .mov files in the current directory to mp4:_`for i in *.mov; do ffmpeg -i "$i" -vcodec h264 -acodec aac ${i%%.*}.mp4 ; done`

..let me know if this guide was of any help lol
