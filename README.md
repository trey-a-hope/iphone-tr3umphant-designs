# Tr3umPHant Designs for iPhone

A native iPhone companion to the [Tr3umPHant Designs website](https://github.com/trey-a-hope/website-tr3umphant-designs): Trey Hope's 2015 portfolio app where people can read about him, browse his flyers, logos and illustrations, and fill in a design request or contact form. Written in early Swift (1.2) with a single storyboard.

## Features

- **Animated home screen** (`ViewController.swift`): a full-screen gradient whose top and bottom colors drift continuously on a 0.1-second timer, with buttons for About Me, Graphic Work, Requests and Contact Me.
- **About Me** (`AboutMe.swift`): bio and photo plus buttons that open Trey's Google+, Instagram, Facebook, Twitter and LinkedIn profiles in their native apps through URL schemes (`SocialNetworkURL.swift`). If the app isn't installed, an alert says so.
- **Graphic Work** (`GraphicWork.swift`): a tab bar with three tabs, Flyers, Logos and Illustrations, each its own view controller.
- **Requests** (`Requests.swift`): a table-based form for first name, last name, phone, email, design type and date needed.
- **Contact** (`Contact.swift`): first name, last name, phone, email and a message field.
- **Custom transitions**: `TransitionManager.swift` swings screens in and out with a spring-damped rotation, and `CustomSegue.swift` provides a zoom-from-center segue.

## How it works

Every screen is laid out in `MyApp/Base.lproj/Main.storyboard` and backed by a small view controller class. Each controller sets a shared `TransitionManager` as the transitioning delegate in `prepareForSegue`, so all navigation uses the same rotation animation. `AlertMessages.swift` centralizes the `UIAlertView` messages ("Sent!", "This app must be installed first.", and so on). Images live in `MyApp/Images.xcassets`, and the three 64×64 PNGs at the repo root are the tab bar icons.

## Tech stack

- Swift 1.2 and UIKit (storyboards, `UITableViewController`, `UITabBarController`)
- Core Animation (`CAGradientLayer`, `CGAffineTransform`) for the background and transitions
- iOS 8.2 deployment target
- No third-party dependencies

## Getting started

### Prerequisites

The project was written for **Xcode 6.3** and Swift 1.2. Current Xcode releases can't compile Swift 1.x, so you'll need either an old Xcode on a matching macOS, or to migrate the code (for example `as!` casts, `++`/`--`, `NSTimer`, `UIAlertView` and `UIApplication.sharedApplication()` all changed in later Swift and iOS versions).

### Running

1. Clone the repo:
   ```bash
   git clone https://github.com/trey-a-hope/iphone-tr3umphant-designs.git
   ```
2. Open `MyApp.xcodeproj` in Xcode.
3. Pick the `MyApp` scheme and an iPhone simulator, then press **Run**.

### Testing

`MyAppTests/MyAppTests.swift` contains only Xcode's template test case. Run it with **Product → Test** (⌘U).

## Project structure

```
iphone-tr3umphant-designs/
├── MyApp/
│   ├── AppDelegate.swift
│   ├── ViewController.swift      # Home screen with animated gradient
│   ├── AboutMe.swift             # Bio and social links
│   ├── SocialNetworkURL.swift    # Deep-link URLs for each social app
│   ├── GraphicWork.swift         # Tab bar for the portfolio
│   ├── Flyers.swift, Logos.swift, Illustrations.swift
│   ├── Requests.swift            # Design request form
│   ├── Contact.swift             # Contact form
│   ├── AlertMessages.swift       # Shared alert helpers
│   ├── TransitionManager.swift   # Rotating spring transition
│   ├── CustomSegue.swift         # Zoom segue
│   ├── Base.lproj/               # Main.storyboard, LaunchScreen.xib
│   └── Images.xcassets/          # App icon, portfolio and social images
├── MyAppTests/
├── MyApp.xcodeproj/
└── flyers@3x.png, logos@3x.png, illustrations.png   # Tab bar icons
```

## Known limitations

- The Requests and Contact forms don't send anything yet: **Submit** only shows the "Sent!" alert.
- The home screen adds a new gradient layer and re-adds its subviews every 0.1 seconds, so memory use grows the longer it stays open.
- `UIAlertView` and the Google+ URL scheme are long retired.
- Per-user Xcode state (`xcuserdata/`) is committed and can be removed.
- There's no license file in the repo.
