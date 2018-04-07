[ElectronJS: Beginner To Pro](https://www.youtube.com/watch?v=iyjM39a0MWE&list=PLXB3WIVcnsH1hAZg9jngLp10mbBhYG40a&index=1&t=0s)

### MENU ACCELERATORS & ROLES

```
let template = [{
	label: 'Edit App',
	submenu: [{
		label: 'Undo',
		accelerator: 'CmdOrCtrl+z',
		role: 'undo'
	}, {
		label: 'Redo',
		accelerator: 'Shift+CmdOrCtrl+z',
		role: 'redo'
	}, {
		type: 'separator'
	}, {
	 ....
	}]
}]
```

### Context Menu

Inter-Process Communication
Main Process <-- IPC --> Renderer Process

IPC Sync
```
const ipc = require('electron').ipcRenderer;
syncMsgBtn.addEventListener('click', function() {
	const reply = ipc.sendSync('synchronous-message', 'Mr, Watson, Come here');
});

const ipc = electron.ipcMain;
ipc.on('synchronous-message', function(event, arg) {
	event.returnValue = 'I heard you!';
});
```

IPC Async

```
const ipc = require('electron').ipcRenderer;
asyncMsgBtn.addEventListener('click', function() {
	ipc.send('asynchronous-message', 'Thats one small step for man');
});
ipc.on('asynchronous-reply', function(event, arg) {
	const message = `Asynchronous message reply: ${arg}`;
	document.getElementById('asyncReply').innerHTML = message;
});

const ipc = electron.ipcMain;
ipc.on('asynchronous-message', function(event, arg) {
	if(arg === 'Thats one small step for man') {
		event.sender.send('asynchronous-reply', ', one giant leap for mankind.');
	}
});
```

### Native Dialogs
Dialog types
- File Open
- File Save
- Message Box
- Error Box <br/><br/>

File Open
```
const dialog = electron.dialog;
ipc.on('open-directory-dialog', function(event) {
	dialog.showOpenDialog({
		properties: ['openDirectory']
	}, function(files) {
		if(files) {
			event.sender.send('selectedItem', files);
		}
	});
});

- openFile
- openDirectory
- multiSelections
- createDirectory
- showHiddenFiles
- promptToCreate (Windows Only)
```

Message Box

```
dialog.showMessage({
	type: info,
	buttons: ['Save', 'Cancel', 'Don\'t Save'],
	defaultId: 0,
	cancelId: 1,
	title: 'Save Score',
	message: 'Backup your score file?',
	detail: 'Message detail'
});

- info
- error
- question
- none

Custom icons
let warningIcon = nativeImage.createFromPath('images/warning.png');

```

### Debugging Your Electron Application
- Debugging Renderer Process
	- Chromium's Dev Tools
- Debugging Main Process
	- VS Code's Tools
	- node-inspector
- Devtron

### Testing with spectron
- Spectron

### Building Your Application
```
npm install electron-builder

--mac, --win, --linux
```

Updating the package.json file
```
"scripts": {
	"start": "electron .",
	"dist": "build -mwl --x64 --ia32"
},
"build": {
	"appId": "com.your-company.electron-app-name",
	"copyright": "Copyright ...",
	"productName": "My Electron App",
	"electronVersion": "1.4.1",
	"mac": {
		"category": "public.app-category.developer-tools"
	},
	"win": {
		"target": ["nsis"]
	},
	"linux": {
		"target": ["AppImage", "deb"]
	}
},
"main": "./app/main.js"


App Icons
- 16px
- 32px
.... 

```

Configuring the MACOS DMG

### Auto Updating
Built-In
Platform Update Method
Mac OS   Squirrel.Mac
Windows  Squirrel
Linux    None

#### Electron-Updater
Install electron-updater as an app dependency.
```
npm i --save electron-updater
```
Use autoUpdater from electron-updater instead of electron
```
import { autoUpdater } from "electron-updater"

Update Events
autoUpdater.on('checking-for-update', () => {})
autoUpdater.on('update-available', () => {})
autoUpdater.on('update-not-available', () => {})
autoUpdater.on('update-downloaded', () => {})
autoUpdater.on('error', (event, error) => {})
```

### Electron Forge
- A complete tool for building modern Electron <br />
https://electronforge.io/forge
