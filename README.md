# SecureVault

Desktop application for Windows that stores files and folders in an encrypted container. The container can be a file on your computer, USB drive or external disk. The app provides its own file interface for working with data inside storage.


## Opportunities

- Create a new storage, select an existing container, and delete the container.
- Connect and disable the storage.
- Set, change, and delete the storage password.
- Automatic locking after 10 minutes of inactivity if no operations are in progress.
- View files and folders, navigate through directories, and drag files and folders to the app window.
- Add files and folders, create folders, extract, rename, and delete items.
- Sequential operations background queue: the interface remains visible and navigable Operations are performed in turn to avoid changing a container from multiple tasks at once.
- The runtime indicator with percentages and a sample remaining time. You can cancel an existing import or extraction operation.
- A tabular view sorted by name, size, and date of change, plus the view of three-size icons.
- Sketches of images and videos in the form of icons; Typical icons for other files
- Preview images in the app. Other files are opened by default by Windows after temporary extraction.
- Seal the container after data is deleted, so that the freed space is returned to the storage file.
- A acrylic style interface with light and dark design support Windows 11 uses the Mica effect, if available.

## Get Started

### Requirements

- Windows 10 build 1809 or newer / Windows 11.
- . NET 10 to run the app.
- To build from source - . NET 10 SDK. You can also use Visual Studio with a classic app development component, NET and WPF support.

### Run app

1. Open `SecureVault.exe'.
2. Create secure storage.
3. Enjoy.
   
### First storage

1. Open the setup menu and select **Create Disk... **.
2. Specify the location and file name of the container, then set a password.
3. Connect the storage you created.
4. Add the data by clicking **Add** or drag and drop files and folders into the window.
5. Select the item to retrieve and click **Extract**. Use the create, rename, and delete buttons to manage the content.
6. Before retrieving the USB drive, disable storage in the app.

For a container that’s already created, use **Select disk... **, then connect it with your password.

## Work with Files

Import, extract, rename, and delete in sequence in the background queue. During operations, you can continue to view the storage and switch between folders. The progress of the current operation is displayed at the bottom of the window. The **Undo** button is active when an operation that you can undo is in progress.

In tabular mode, click the **Name**, **Size** or **Changed** titles to sort the list. In icon mode, size is selected in the settings and applied immediately.

When an image is opened, the app displays a built-in preview. For all other file types, the application retrieves a temporary copy to the `%TEMP% SecureVault` folder and then opens its default Windows program. The app waits for open time files to be closed before finishing work and deletes temporary copies after closing. The temporary copy is outside the encrypted container while it’s open.

Deleting files frees up the blocks they occupy and tightens the container. Therefore, the delete operation may take time and the size of the container file decreases after it.

## Data protection

- The contents of the container are encrypted by an algorithm **AES-256-GCM**.
- To protect the master key, use **Argon2id** with default settings: 256 MiB memory, 3 iterations and 4 parallelization.
- Data is stored in encrypted blocks of 64 KiB; The block uses separate nonce and authenticated data.
- The container’s index is stored in two slots. When opened, the correct slot with the largest generation is selected.
- When you delete an app password, the access key is saved using **Windows DPAPI** and is only available to the current Windows user. This convenience is not a substitute for password protection against access to the user account.

**Important:** Remember your password and keep a backup copy of the container file. Deleting or damaging a container can result in data loss. Before retrieving the storage device, turn off the storage and wait until operations are complete. Deleting your password reduces the container’s protection to the level of the current Windows account.


## Limitations

- The container can't connected to the Explorer as a disc with a letter.
- Files opened by external applications are temporarily decrypted in the `%TEMP%' system folder. Don’t leave such files open on devices you don’t trust.
- Deleting a container destroys the data stored in it; Make sure that you have selected the correct file and saved the necessary backups.

## Technology

- C#, .NET 10 и WPF.
- AES-GCM и Argon2id.
- Windows DPAPI for local key storage when the password is removed.
- Win32 Shell API to get file thumbnails


