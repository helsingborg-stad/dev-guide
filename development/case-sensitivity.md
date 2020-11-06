# Case sensitivity

As our linux servers are case sensitive we need to have that in mind when developing on case insesitive systems as Mac OS and windows.

## Mac OS Create case sensitive image and mount.
To create and mount a case sensitive image follow below steps.
Your case sensitive mount will be present in ~/dev as a symbolic link pointing at the mount point.

```sh
hdiutil create -type SPARSE -fs 'Case-sensitive Journaled HFS+' -size 100g -volname dev-workspace ~/Documents/dev-workspace.sparseimage
hdiutil attach ~/Documents/dev-workspace.sparseimage
mkdir /Volumes/dev-workspace/dev
ln -s /Volumes/dev-workspace/dev ~/dev
```



To remove the disk and mount.
```
hdiutil detach /Volumes/dev-workspace
rm ~/Documents/dev-workspace.sparseimage
rm ~/dev
```

To mount on startup:
TODO