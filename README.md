# Source Code for Kevin's Personal Website

## To start the hugo server

```bash
hugo server -D
```

## To create a new page under a main menu item

```bash
hugo new projects/movieguessr.md
```

## To create a post with only an external link

- Create a new page using the command above
- Add `canonicalUrl: "https://movie.kevinpatel.xyz"` to the frontmatter of the page

## To add a Github card

- Add `githubRepo: "CyberT17/obsidian-day-and-night"` to the frontmatter of the page
