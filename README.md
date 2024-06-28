# Source Code for Kevin's Personal Website

Using a modified version of [Hugo PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

## To start the hugo server

```bash
hugo server -D
```

## To create a new page under a main menu item

```bash
hugo new --kind post posts/url-path.md
```

## To add a Github card

- Add `{{< github-repo url="CyberT17/secblogs" >}}` to the markdown of the page
