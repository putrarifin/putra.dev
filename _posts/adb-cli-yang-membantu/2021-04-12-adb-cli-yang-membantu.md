---
layout: post
title: "Perintah ADB 🤖"
date: 2023-02-28" "09:46:55
categories: android
emoticon: 🤖
---

Mendapatkan nama `activity class` yang saat ini sedang aktif:
```bash
adb shell dumpsys window windows | grep -E 'mCurrentFocus'
```

Menjalankan `activity` berdasarkan nama `class`:
```bash
adb shell am start 
    -a android.intent.action.MAIN 
    -n dev.putra.sample/.MainActivity
```

Menjalankan `activity` berdasarkan nama `applink`:
```bash
adb shell am start 
    -a android.intent.action.VIEW 
    -d "host://domain/param" dev.putra.sample
```