# Gradient's Blog Code.

![Hugo Build](https://github.com/Gradient-IIITS/Gradient-s-Blog/workflows/Hugo%20Build/badge.svg)

[![Gradient Blogs](https://img.shields.io/badge/Gradient%20IIITS-Blogs-blue?style=for-the-badge)](https://gradient-iiits.github.io)

The blog has been created using [Hugo](https://gohugo.io/), a static site generator.

## To Contribute:

Just send us a pull request or add an issue.

## Steps:

- Fork [this](https://github.com/Gradient-IIITS/Gradient-s-Blog) repository.
- Run `git clone <URL-of-your-fork>` in your local machine.
- Run `cd Gradient-s-Blog`.
- Run `git submodule update --init --recursive` (This step is important).
- Add your post by following instructions given below.
- Push the changes by following `add-commit-push` pattern.
- Open a PR.

## To Add a post:

- Install [Hugo](https://gohugo.io/getting-started/installing/).
- Run `hugo new posts/<YOUR POST NAME>.md`.
- Add the content in markdown format.
- If you have images and/or code-snippets put them under `static/images` or `static/code` folders respectively.
- Run `hugo server -D`. You will get something like `Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)`
- Check if your post has the proper look, content, feel or not.

## Guide for adding images/code-snippets in your post:

- Make a subfolder under `static/code` or `static/images` folder. (Name them same as your post's name)
- Put files under your subfolders.
- Use them in MD files as `images/<YOUR POST NAME>/<image>` or `code/<YOUR POST NAME>/<code-file>`.
