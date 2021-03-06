# Template Match

A slghtly rusty alternative to [ImageSearchDll](https://github.com/MyBotRun/Libraries/blob/master/ImageSearchDLL) for AutoIt3.

Relies on [imageproc](https://github.com/PistonDevelopers/imageproc) and a lot of `unsafe`.

### Why?

If you currently rely on ImageSearchDll and want something with a different license, this may interest you.

### Build

Tested with
```
stable-x86_64-pc-windows-gnu / rustc 1.22.1
nightly-x86_64-pc-windows-gnu / rustc 1.24.0-nightly
```

```
cargo build --release
cp target/release/template_match.dll autoit_project_directory
cp au3/template-match.au3 autoit_project_directory
```

### Usage

```AutoIt
; usage.au3

#include <template-match.au3>

Func Main()
    Local $result = TemplateMatch("needle.png")
    ; $error = TemplateMatchRect("needle.png", $x, $y, $w, $h);

    If ($result[3] <> 0) Then
        ConsoleWrite("Error #" & $result[3] & @CRLF)
        Return
    EndIf

    ConsoleWrite("Best X " & $result[0] & @CRLF)
    ConsoleWrite("Best Y " & $result[1] & @CRLF)
    ConsoleWrite("Root Mean Square Error " & $result[2] & @CRLF)

    If ($result[2] < 10.0) Then
        ConsoleWrite("Found a good match!" & @CRLF)
    EndIf
EndFunc

Main()
```

### TODO

* Some way to return multiple matches with a threshold
* Optionally pass a HWND
* What's the situation with multiple displays?
* Transparency
