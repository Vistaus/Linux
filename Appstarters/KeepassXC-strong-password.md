## How to open KeepassXC (Flatpak) and auto-entering password stored in Kwallet.

Use-case: you have a complex password and a strong user password and/or LUKS encrypted drive.
KWallet sucks, so you want to integrate KeepassXC into your KDE system. This is not natively existing, so you need this workaround:

1. Open "KWalletManager"
2. If not existent, create a new folder called "Passwords" by clicking on the clear area and then "New"
3. Open that folder, in here you find multiple folders, one is called "Passwords" in your systems language
4. Right click the "Passwords" subfolder and press "new"
5. Enter the name of your Entry, click on the entry and "show content", enter your Keepass Password
6. Create an appstarter for quick-opening your password storage!

This is the base command (The entry is called "KeepassXC-main", encouraging the use of multiple password files):

```
kwallet-query -r KeepassXC-main kdewallet | /usr/bin/flatpak run --branch=stable --arch=x86_64 --command=keepassxc --file-forwarding org.keepassxc.KeePassXC --pw-stdin ~/passwords.kdbx
```

You can create an appstarter by right-clicking on the Menu icon, going to "edit menu entries", creating a new Entry and setting the Command as the previous one.

Or you can use this command:

```printf """[Desktop Entry]
Comment= Opens Your password storage and enters the password stored in KWallet
Exec='kwallet-query -r KeepassXC-main kdewallet | /usr/bin/flatpak run --branch=stable --arch=x86_64 --command=keepassxc --file-forwarding org.keepassxc.KeePassXC --pw-stdin ~/passwords.kdbx'
GenericName=
Icon=emblem-encrypted-unlocked
MimeType=
Name=Keepass-unlock
NoDisplay=false
Path=
StartupNotify=true
Terminal=false
TerminalOptions=
Type=Application
""" > ~/.local/share/applications/KeepassXC-open.desktop
```

---

## Have a really strong password
now you can store a really long password for your possibly cloud-synced database!

### KeepassDX on Android 

Depending on your threat model, if you use Android and KeepassDX, you can now once enter the password and save it using your fingerprint.

Transfer the password:
- USB
- Use a privacy friendly QR Scanner (not Google lens), copy the password on your Laptop and in the Klipper menu you can show a QR Code
- scan the QR code and copy the password to the draft
- Insert the password to your storage, empty your draft (Florisboard recommended keyboard)

Warning: in many states a Fingerprint is less secure than a password. Law enforcement can "enforce" you to touch your fingerprint sensor, while they can't force you to say your password.
