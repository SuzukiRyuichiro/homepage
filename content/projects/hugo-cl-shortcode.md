---
title: "Hugo Cloudinary Shortcode"
date: 2022-10-13T21:40:51+02:00
draft: false
---

# The repo

[Here](https://github.com/SuzukiRyuichiro/hugo-cl-image)

# What I wanted to achieve

I wanted to make it possible to produce Cloudinary image links by just giving the file name to a shortcode.

# Setup

1. make a submodule in your themes folder
2. add the theme in the theme array in your `config.toml`

```toml
theme = ["some other theme", "cl-image"]
```

3. add the following to your params portion of `config.toml`

```toml
[params]
  baseURL = "https://res.cloudinary.com/" # This is the same for everyone
  cloudName = "your cloud name" # You can check your cloud name from cloudinary console page
  folderName = "Portfolio" # if you want to put collection of pictures into a single folder, write the name of the folder (optional)
```

# Usage

The theme adds a shortcode called `cl-image`. You can give following arguments
| argument | description |
| --- | --- |
| src (required) | this is what is your image called on cloudinary. By default, it can be a gibberish so I advice you to change it to something memorable from the Cloudinary console. |
| class | give a string of classes you wish to apply to the `img` element |
| alt | same with the class |
| style | same the class |
| height | This is the pixel height of the image you give to the [Cloudinary Transformation URL API](https://cloudinary.com/documentation/transformation_reference#h_height). If your original image is too large, it is advised to reduce the size matching how large you are displaying on the website. |
| width | same with the height |

## Example

```go
// remove '\'
{{\< cl-image src="ski.jpg" class="rounded center" alt="me in skiing" height="600" style="min-width: 50%; height: 400px; object-fit: cover;" \>}}
```
