# Remote Mapping for Harmony Elite Remote Control with Kodi

The Harmony Elite Remote Control can be connected with Kodi for navigation.
This guide is for Kodi running on top of Raspbian.

### Requirements
- Raspbian installation on Raspberry Pi 4
- Harmony Elite Hub & Remote Control

### Setup
- Install Kodi
```
sudo apt-get update
sudo apt-get install kodi
```

- Register the Raspberry Pi 4 as a Windows PC within the Harmony Remote's devices
- Create an activity for the Harmony Remote to pair the two via Bluetooth

Once the two are paired, Kodi can be started using a custom keypress action.
Edit the file ~/.config/openbox/lxde-pi-rc.xml and add a new keybind under the keyboard section.
###### Example
```
<keybind key="F10">
  <action name="Execute">
    <command>/usr/bin/kodi</command>
  </action>
</keybind>
```

- Update the activity on the Harmony Remote to start Kodi using the specified key bind
- Create an .xml file under ~/.kodi/userdata/keymaps/ to override the existing shortcuts within Kodi
###### Example
```
<keymap>
  <global>
    <keyboard>
      <fastforward>FastForward</fastforward>
      <play_pause>PlayPause</play_pause>
      <rewind>Rewind</rewind>
      <record>Noop</record>
      <stop>Stop</stop>
      <e>ActivateWindow(shutdownmenu)</e>
      <m>ActivateWindow(home)</m>
      <up>Up</up>
      <left>Left</left>
      <down>Down</down>
      <right>Right</right>
      <browser_back>Back</browser_back>
      <r>ActivateWindow(TVRecordings)</r>
      <g>ActivateWindow(contextmenu)</g>
      <i>Info</i>
    </keyboard>
  </global>
</keymap>
```

#### Debugging
To find out which keys are being registered within Kodi from the Harmony Remote
 and which actions are being taken, enable debug logging within Kodi.

Search the log file for the following text: "HandleKey"
###### Example
```
pi@rp4:~ $ grep HandleKey ~/.kodi/temp/kodi.log
2020-02-08 20:31:00.704 T:2972630112   DEBUG: HandleKey: right (0xf083) pressed, action is Right
2020-02-08 20:31:04.672 T:2972630112   DEBUG: HandleKey: down (0xf081) pressed, action is Down
```

Certain button commands within the Harmony Remote will not be correctly recognised by Kodi.
This can be remedied by remapping the buttons within the activity to use a simpler command, e.g. replace "Guide" with "g.".

More information on actions to trigger via commands can be found [**here**](https://kodi.wiki/view/Keymap).
More information on opening windows via commands can be found [**here**](https://kodi.wiki/view/Opening_Windows_and_Dialogs)

