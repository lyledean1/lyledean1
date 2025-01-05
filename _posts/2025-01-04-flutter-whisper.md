---
layout: post
title:  "Flutter Whisper.cpp"
date: 2024-01-04
---
# Flutter Whisper.cpp

[Flutter Whisper.cpp](https://github.com/lyledean1/flutter_whisper.cpp) allows offline/on device - fast and accurate automatic speech recognition (ASR) using OpenAI's Whisper ASR model. Built on top of ggerganov's Whisper.cpp, the app uses flutter_rust_bridge to bind Flutter to Rust via FFI, and whisper-rs for Rust C bindings to Whisper.cpp. The app also utilizes the Record Dart library for recording .m4a in iOS which is then converted to a .wav file.

[Click here to see my talk at Fluttercon 2023 on using Rust with Flutter](https://www.droidcon.com/2023/08/07/supercharging-your-flutter-apps-with-rust/)

## Video
The example below took < 1 second to process the audio on an iPhone 12

![Video](https://user-images.githubusercontent.com/20296911/229925629-9f4e9fa0-6165-4d96-b61b-a04f8105a1f6.MOV)
