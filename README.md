# What is this?
This is a workaround to prevent GShade from disabling itself when a major update releases, if it can't contact the update server, and disabling update reminders for minor versions.

### IF YOU USE THIS WORKAROUND AND STAY ON AN OUTDATED VERSION BE PREPARED TO FORFEIT ANY SUPPORT YOU MIGHT GET FROM THE GSHADE CONTRIBUTORS/COMMUNITY

# Why?
GShade's policy is to *completely disable* GShade effects on your game every time there is a major update for it until you update. It also completely disables effects if it can't reach their update server. In my opinion this is completely unacceptable. The reasoning for them not supporing turning off the update check is because they don't want to provide support for issues on earlier versions of GShade. Whether or not you think that is sound reasoning is up to you. In my eyes, taking control away from the user and providing a negative experience is not the way to go. If everything works for someone on a certain version of GShade, why shouldn't that person be allowed to just use that version instead of having to go through the update process and then spend hours troubleshooting if something goes wrong? I applaud and thank the team for their continued work on GShade, but this decision combined with how condescending they/the community can be towards any real feedback about this was enough to make me look for a workaround on how to stop it from checking for updates. Please keep in mind that harassing/threatening the GShade team/dev about this issue is NOT the way to go. Feedback can be given without resorting to throwing a tantrum and it's my hope that the GShade team/dev won't try to block this workaround since I'm expecting this will only be used by a small portion of the GShade community.

# Instructions
0. Backup the `dxgi.dll` file in your game's installation folder before you begin in case something goes wrong.
1. Download and install [HxD]( https://mh-nexus.de/en/downloads.php?product=HxD20). This is a hex editor that we will be using to change what url the GShade dll file points to when trying to read what the latest version is. I know that site looks kinda sketch, but it's just an old site for an old program.
2. Run HxD as administrator.
3. Go to `File -> Open` and open the `dxgi.dll` file located in your FFXIV install folder (or whatever game you use GShade with). If you're using steam, your path should look something like this: `C:\Program Files (x86)\Steam\steamapps\common\FINAL FANTASY XIV Online\game\dxgi.dll`
4. Once the file is open, press `Ctrl + F` and type `https` into the search box. The options selected should look like this:

	![image](https://user-images.githubusercontent.com/6508045/212369206-adfc7892-5926-4f73-b805-a27212bc89f5.png)

5. Hit `Select All`. You should see entries on the bottom of the program that look like this:
	
	![image](https://user-images.githubusercontent.com/6508045/212373451-9fc30226-d0a3-42a3-a1da-a104dda97711.png)
	
	Double Click the first row. It should take you straight to where you need to be. You should see this:
	
	![image](https://user-images.githubusercontent.com/6508045/212373600-f7d5a90a-950b-4290-a7e8-c2a7e7da0fac.png)
	
	These are the URLs that we need to configure. Specifically the https://api.github.com/repos/mortalitas/gshade/tags and https://storage.googleapis.com/gshade/tags.json.
6. With your cursor select/highlight the blocks shown on this image:

	![image](https://user-images.githubusercontent.com/6508045/212375610-d45074f4-d940-4343-b67f-c2198328219d.png)
	
	Note: Make sure you select using the *number* blocks like in the image and not the "Decoded text" column that is just a representation of the data. Also worth mentioning is your "Offset (h)" column digits on the left might not match the picture and that's okay. As long as you select the number blocks exactly like in the image and both urls mentioned earlier are included, then you should be fine.
7. Scroll up on this page and click your current version of GShade from the files listed on this repo.
8. Copy the text from that file (should be a bunch of numbers).
9. Go back to HxD and right click the selection you selected in step 6 and click `Paste write`.
10. Save the file and try to run the game, if it worked it will act like you're on the latest version and will stop telling you to update even if new versions come out afterwards.

### Important Notes
- You need to make sure the replacement you're pasting at step 9 is overwriting all the numbers exactly and not adding or removing any. If it does, the alignment for the offsets will be messed up and the game will fail to launch.
- The URL we are redirecting the update check to is just a raw Pastebin with your current version number. If Pastebin happens to go down, GShade will still disable itself since this workaround can't prevent that from happening if GShade receives no data.

# How does this work?

This basically fakes the data that GShade is reading to find what the latest version is. Originally I thought just blocking the update server would be enough, but then I found out GShade disables itself if it can't pull data from the update site. So, the alternative is to have it connect to data, but have the data that it connects to be controlled by us. Since the data it wants is just a text file that literally says what version the latest is, we can just feed it a link to a raw pastebin with whatever version we want.

### Shout out to [this post](https://reshade.me/forum/troubleshooting/7793-how-to-disable-update-notification) for pointing me in the right direction on how to do this.
