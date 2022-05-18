---
id: 3bfa34fc-5a50-4d06-928a-30c2ce6afbc1
title: Dendron
desc: ''
updated: 1652904161681
created: 1614090590691
---

# Dendron 

## Line wrap for code blocks
* Don't think this is required any more
`F1 => Markdown Preview Enhanced : Customize CSS`
Add in the `style.less`:
```less
.markdown-preview.markdown-preview {
       pre, code {
            white-space: pre-wrap;
       }
}
```

## Self Contained Vaults
* [[Reference | https://wiki.dendron.so/notes/o4i7a81j778jyh7wql0nacb/]]
* [[Migrating to Self Contained Vaults | https://wiki.dendron.so/notes/aikv0yamnfkcowlol7qeldy/]]
### Features
* Self contained vaults include all the files Dendron needs to open the vault and use it
* You can publish any vault you have by itself
* You can share the vault with someone, and Dendron will work immediately when they open it in VSCode without having to set up workspaces
* When you convert your vault to a remote vault, it will include all your settings and everything you need for Dendron
