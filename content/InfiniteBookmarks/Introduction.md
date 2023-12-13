## Best local bookmark manager for Mordern Browsers. 

## Dual-layered Tab System

To make better use of the potentially vast number of bookmark folders, I've devised a dual-layered tab system — featuring regular tabs and tab groups.  

In this extension, regular tabs correspond to individual bookmark folders. You can double-click on a tab to switch between single-line and multiline modes. 

The right-click menu can expand regular tabs to a maximum of 6 lines in height, so that you can better decide which folder to add the current browsing page to.  

Tab groups encompass multiple regular tabs, showcased with a single-line scrolling user interface at the top of the extension page.  

At first, only regular tabs were present, but I later realized the need for grouping. To distinguish them from the browser's tabs, the tabs in this extension are referred to as "mini tabs" below.  

![](p1)

The entire interface consists of three parts: tab group bar, mini tab bar, and mini tab content.

As you can see, the tab group can be named arbitrarily (right-click **"Rename"**), and I have added some emojis for easy differentiation.

Right click **"New"** to create a new group. There are multiple templates, two of which are quite unique:


![](p2)

The "**Bookmark Bar**" template will scan top-level bookmark folders during loading. Top-level folders will be automatically added to this group. In chrome top-level folders are the ones on the bookmarkbar, and the address should be: `chrome://bookmarks/?id=1`

The "**Search Engine**" template will initialize some search engines that I have collected, totaling about seventy:


![](p3)


## Different Types of Mini tabs 

Currently, this extension has six types of mini tabs, each of which may have further subdivisions. 

To create them, just click the plus button at the end of the tab bar, or right-click and press <kbd>N</kbd> :

![](p5)


Six types of mini tabs : 
1.  Bookmark folder
2.  Important tabs 
3.  Search Engines
4.  Embeded Iframe
5.  Custom Pagelet
6.  TTS Configuration



Next, we will introduce the bookmark mini tab. We will discuss the rest later~  


## Bookmark Mini Tab

The mini bookmark page comprises an address bar and a list. The address bar (i.e. mini ominibox) is horizontally divided from left to right, featuring the address bar itself, a search box within the folder, a go-to-top button, a go-to-bottom button, a star button, and a reverse order button.  

To utilize the address bar, you can input the bookmark ID (number) and then press the <kdb>Enter</kdb> key, or you can enter the complete bookmark URL, such as chrome://bookmarks/?id=1. The bookmark ID can be obtained by accessing the native bookmark manager.   

Alternatively, you can perform a search by entering characters directly into the address bar and pressing enter. The search function within the folder has not been implemented yet.  

**Next up is the Killer's Mace**: the star button. When it appears hollow, it indicates that the current page is not bookmarked. A left-click allows you to either edit the existing bookmark or create a new one.  

![](p)

**To locate the bookmark folder**, simply right-click on the star button. This action play a highlight animation on the target line.  

The reverse button serves as a toggle, allowing you to switch between reverse or sequential sorting. 



## Right-click Context Menu

**Right-click on the list** enables you to directly add or move favorites below the current line. Manage your bookmarks while you are creating them!  

![Image]()


The right-click menu provides top buttons for seamlessly switching between menu groups. Within the context of bookmark mini tabs, you'll find "Manage" and "Navigate" menus, each serving distinct purposes.

### Manage

**Within the "Manage" menu** you can add separators, an edit/delete/pin-to-top/pin-to-bottom bookmarks. 

If you accidentally delete a bookmark, you can undo the action by opening the native bookmark manager and press <kbd>Ctrl+Z</kbd>. 

**"Pin-Top"** will add an emoji to the title and move it to the top of the list.  

**"Replace with current URL"** option will appear in the management menu if the bookmark URL matches the current domain URL. This function make it easier to update bookmark address for watching video series or reading novels.  

![](p)

### Navigate

**In the "Navigate" menu**, you can open bookmarks in new windows, current windows, new windows in the background, or as iframe-embedded mini tab.

---

### Mini Tab Bar

**Right-click on the mini tab bar** provides additional entries to add favorites, to create a new bookmark folder, and to locate the current bookmark folder.   

Selecting **"New Bookmark Folder"** will create a new bookmark folder alongside the current bookmark folder, automatically appending a numerical suffix to the folder name. It's so convenient!  

The address (and type) of mini tabs can also be altered by right-clicking on **"Copy URL"** option.

![](p)


## Further subdivision of bookmark mini tab and it's addresses.

Bookmark mini tabs can be further divided into three types: 


| Subtype | address format |
|:--------| :---------:|
| 1. bookmark folder |   `chrome://bookmarks/?id={Digital ID}` |
| 2. bookmark search |   `chrome://bookmarks/?q={Search Terms}` |
| 3. recent bookmarks |  `recent={display number, default 1000}` |



## Multiple Selection and Drag to Sort

-   **Multiple Choice**
    
    -   (Similar to Explorer etc. ) : Hold <kbd>Ctrl</kbd> and click to toggle selection.
    -   Hold <kbd>Shift</kbd> and click twice in different positions in list to select between them. 
    -   (Difference) : Use *right-click-drag* to trigger **box-selection**, instead of *left-click-drag*;
	
-   **Drag and Sort**
    
    -   Unlike other programs, drag-and-drop sorting in this extension doesn't require keeping the mouse down all the time. Instead, <u>with a gentle drag</u>, you can release all buttons, scroll the list to the desired position, and finally <u>confirm with a left-click</u> or cancel with a right-click.
	-	Hold <kbd>Ctrl</kbd> before left-click confirmation will duplicate instead of move selected bookmarks.
    -   Immediately after the "gentle drag", you can even switch to mini tab of a different bookmark folder (even in different tab group), and then confirm the modification by a simple click, making cross-folder management very convenient and leading the way.

![](p)


## Bookmark Thumbnails

You have the option to manually add one or more thumbnails to a bookmark. Begin by copying the image to the clipboard or taking a screenshot to the clipboard. Next, right-click on the bookmark list line and press <kbd>V</kbd> to paste the thumbnail. If you want to replace it, right-click on the image and then press <kbd>B</kbd>.

AutohotKey scripts can be employed to facilitate taking and copying screenshots to clipboard.

Please note that the bookmark thumbnail feature is experimental and has a relatively straightforward layout. Horizontal images  may display two columns in one row, while vertical images may display four columns in one row.

The storage mechanism is also relatively simple. Image data is stored in the extension local storage space, with the bookmark ID serving as the key (though not ideal for synchronization). Be cautious during the testing phase, as the data may be lost in the event of storage failure or other bugs. It is advisable to make backups frequently.

The plan is to implement more layout styles that can be combined with user scripts to enable automatic thumbnail generation. Eventually, these thumbnails will be saved on a local server with the URL serving as the key.



That concludes the introduction to the Infinite Bookmark Extensions. I've covered the fundamentals of how to use it for bookmark management. Note that the plural form is used in the last word, "Extensions," signifying that this extension is versatile, and its capabilities will continually strengthen as I continuously use and improve it.
