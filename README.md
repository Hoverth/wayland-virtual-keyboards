# Virtual Keyboards on Wayland

Virtual keyboards, also called on-screen keyboards (OSKs), is a piece of
software that allows a user to input keys via a touchscreen or a mouse
interface, instead of a physical keyboard.

Broadly speaking, OSKs can be split into two categories:

- Mobile keyboards, more focussed on simple text input, like what would be found
on Android or iOS as default.
- Desktop keyboards, more focussed on controlling a computer to it's
fullest extent, including use of modifier keys and keybinds.

In this document I'll outline what each are typically used for, some notes
on what Wayland currently has in place for implementations, some
requirements for both protocol + compositor-side and application-side
developers (application-side devs here being the ones working on OSKs on
Wayland), and finally some examples of those keyboards (mainly Wayland, some X).

## Table of Contents

<!-- vim-markdown-toc GFM -->

- [Mobile Keyboards](#mobile-keyboards)
  - [Mobile OSK Use-cases](#mobile-osk-use-cases)
  - [Mobile OSK Implementation Details](#mobile-osk-implementation-details)
  - [Mobile OSK Requirements](#mobile-osk-requirements)
  - [Mobile OSK Examples](#mobile-osk-examples)
- [Desktop Keyboards](#desktop-keyboards)
  - [Desktop OSK Use-cases](#desktop-osk-use-cases)
  - [Desktop OSK Implementation Details](#desktop-osk-implementation-details)
  - [Desktop OSK Requirements](#desktop-osk-requirements)
  - [Desktop OSK Examples](#desktop-osk-examples)
- [Resources](#resources)
  - [Wayland Protocols](#wayland-protocols)
  - [OSKs](#osks)
  - [Other Tips](#other-tips)
- [Contributing](#contributing)
- [License](#license)
- [Authors](#authors)

<!-- vim-markdown-toc -->

## Mobile Keyboards

Mobile keyboards are typically used to input text in an efficient and
user-friendly manner, with less concern on more specialised input. They
more frequently are found on touchscreen devices.

Android and iOS keyboards are what I would consider to be the gold
standard, and we should probably seek to reproduce how they work.

Note that I don't include something like
[Hacker's Keyboard](https://github.com/klausw/hackerskeyboard), as that
contains more specialised keyboard features, such as modifier keys.

### Mobile OSK Use-cases

- Texting / messaging
- Simple note writing
- Dialling a phone number

### Mobile OSK Implementation Details

- You will want to look into preediting/commiting strings using a protocol
like [input-method-unstable-v1.xml](https://wayland.app/protocols/input-method-unstable-v1)

### Mobile OSK Requirements

- Displays on the lower half of the screen
- Ability to switch layers to access numbers & symbols
- Spell-checking (Optional)
- Mobile keyboards usually appear only when a text input is selected

### Mobile OSK Examples

- Maliit
- Squeekboard

## Desktop Keyboards

Desktop keyboards are typically used to emulate a full keyboard,
including usually having a GUI that shows a keyboard layout, complete
with special keys, modifier keys and levels.

They are usually less focussed on text-specific input, and allow the user
to input keybinds and other specialised input to control their computer.

I find that desktop OSKs are more useful when the input method is a mouse.

### Desktop OSK Use-cases

- Navigating programs using non-text input, e.g. special keys, keybinds
  - Desktop Environments / Compositors
  - Terminal
  - Spreadsheet Program
  - Games (using something like the arrow keys)
- Using the OSK as a GUI keyboard macro pad

### Desktop OSK Implementation Details

- Requires a protocol that enables sending key events
- I have found that the documentation around what keymaps is a tad lacking,
see [the Xkbcommon docs](https://xkbcommon.org/doc/current/xkbcommon-keysyms_8h.html)

### Desktop OSK Requirements

- Ability to float
- Ability to emulate a full hardware keyboard (including modifier keys)
- Ability to change the window's opacity
- Ability to be shown even when there isn't a text input active
(i.e. an always shown setting)

### Desktop OSK Examples

- [Onboard](https://launchpad.net/onboard) (X11,
this is my personal go-to virtual keyboard)
- I have not seen any Wayland desktop OSKs

## Resources

### Wayland Protocols

- [input-method-unstable-v1.xml](https://wayland.app/protocols/input-method-unstable-v1)
- [input-method-unstable-v2.xml](https://wayland.app/protocols/input-method-unstable-v2)
- [text-input-unstable-v3.xml](https://wayland.app/protocols/text-input-unstable-v3)
- KDE's [fake-input.xml](https://wayland.app/protocols/kde-fake-input)
- External [virtual-keyboard-unstable-v1.xml](https://wayland.app/protocols/virtual-keyboard-unstable-v1)

### OSKs

- [Awesome-Wayland's OSK Links](https://github.com/rcalixte/awesome-wayland?tab=readme-ov-file#on-screen-keyboards)
- [Maliit-Keyboard](https://maliit.github.io/)
- [Squeekboard](https://github.com/droidian/squeekboard)
- [QVK](https://invent.kde.org/apol/qvk) (More of a demo in it's current state, 2024/12/06)

### Other Tips

- KDE exposes the [input-method-unstable-v1.xml](https://wayland.app/protocols/input-method-unstable-v1)
(contrary to what the page claims), but it's hidden to applications by
default. You need to add `X-KDE-Wayland-VirtualKeyboard=true` into the
applications `.desktop` file that is installed in the applications directory,
`/usr/share/applications`, for KDE to accept it, and then it'll be available
to select in System Settings.

## Contributing

Got some resources to add or tips other developers should know? Open an issue
or a pull request and it can be added!

By contributing, you agree to license your contribution under the license.

## License

This file is licensed under the
[GNU FDL v1.3](https://www.gnu.org/licenses/fdl-1.3.html).

## Authors

- [Thomas Dickson (Hoverth)](https://github.com/Hoverth)
