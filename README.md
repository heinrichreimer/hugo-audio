# 🎧 hugo-audio

A Hugo theme component to embed sounds using the HTML audio element.

## Features

This [Hugo](https://gohugo.io) theme component provides a shortcode `audio` for embedding sounds using the [HTML audio element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio).

- Languages: English and German ([more languages](https://github.com/janheinrichmerker/hugo-audio/pulls) are welcome!)
- Fallback to a localized download notice if the browser doesn't support the [HTML audio element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)
- Supported audio formats:
  - MP3 (extension `.mp3`)

## Installation

The best way to install this component is as a Hugo module:

1. Initialize your existing site as Hugo module:

    ```shell
    hugo mod init github.com/<USERNAME>/<REPO>
    ```

2. Add the hugo-audio component as a Hugo module:

    ```shell
    hugo mod get github.com/janheinrichmerker/hugo-audio
    ```

3. In your site's or theme's configuration file, add a `module` section and define both `hugo-audio` and your currently used theme as modules to be imported.

    Here is an example, with a YAML configuration file:

    ```yaml
    module:
      imports:
        - path: github.com/janheinrichmerker/hugo-audio
        - path: my-theme
    ```

    With a TOML configuration file, it should look like this:

    ```toml
    [module]
      [[module.imports]]
        path = "github.com/janheinrichmerker/hugo-audio"
      [[module.imports]]
        path = "my-theme"
    ```

<details><summary>But it can also be installed as a Git module.</summary>

1. Add this repository as a submodule like this:

    ```shell
    git submodule add https://github.com/janheinrichmerker/hugo-audio.git themes/hugo-audio
    ```

2. Add `hugo-audio` as the leftmost element of the `theme` list in your site's or theme's configuration file:

    Here is an example, with a YAML configuration file:

    ```yaml
    theme: ["hugo-audio", "my-theme"]
    ```

    With a TOML configuration file, it should look like this:

    ```toml
    theme = ["hugo-audio", "my-theme"]
    ```

</details>

## Usage

This shortcode uses Hugo [Page Resources](https://gohugo.io/content-management/page-resources/).

So first place the audio to be played in the [page bundle](https://gohugo.io/content-management/page-bundles/) of the page where you want to use the shortcode.

In the page source file, then use the shortcode like this, indicating the audio filename _without_ its extension:

```go
{{< audio src="my-cool-sound" >}}
```

This will reference the file `my-cool-sound.mp3`, for example.
... or with a fixed width:

```go
{{< audio src="my-cool-sound" width="600px" >}}
```

The shortcode takes one mandatory argument: the filename of the audio file to play _without_ the extension.
The component automatically detects if several versions of the file exist in the page bundle and accordingly adds multiple `src` tags.
If no audio file of the given name is found in the supported format (see above), the shortcode _intentionally fails_ with a `No valid audio file with filename <filename> found.` error.

### Defaults

- The web browser's default audio controls are displayed (`controls` attribute is always included).
- Audio can be preloaded (`preload="auto"` attribute is always included).
- Audio width is 100% (`width="100%"` attribute is included). Can be changed by explicitly specifying the width in the shortcode.
- The following other audio attributes can be set: `muted="true"`, `autoplay="true"` and `loop="true"`.
- Default settings are used for all other audio attributes.

## Acknowledgments

- [Nicolas Martignoni](https://github.com/martignoni), for the [hugo-video](https://github.com/martignoni/hugo-video) shortcode on which this shortcode is based.
- [Tom McKenzie](https://github.com/grrowl), for implementing `muted`, `autoplay` and `loop` audio attributes support.
- [Olaf Haag](https://github.com/OlafHaag), [Paul Lettington](https://github.com/plett) and [Christian Mahnke](https://github.com/cmahnke), for raising and fixing some bugs.
- [Arsenii Lyashenko](https://github.com/ark0f), for implementing `controls` disabling option.

## License

All the source code is licensed under GPL 3 or any later version

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version. This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
