# .node-version

Q: Is `.node-version` read by multiple node version managers?  
A: Yes.

Q: Does `.node-version` have a common or standard file format?  
A: No.

Q: So what compatibility is there?  
A: Good question! Read on...

## Supporting Products

Products which read a `.node-version` file include (in alphabetical order):

- [asdf-nodejs](https://github.com/asdf-vm/asdf-nodejs) Node.js plugin for asdf version manager
- [avn](https://github.com/wbyoung/avn) Automatic Version Switching for Node
- [direnv](https://github.com/direnv/direnv) unclutter your .profile
- [fnm](https://github.com/Schniz/fnm) 🚀 Fast and simple Node.js version manager, built in native ReasonML
- [nodenev](https://github.com/nodenv/nodenv) Manage multiple NodeJS versions.
- [nodist](https://github.com/nullivex/nodist) Natural node.js and npm version manager for windows.
- [nvh](https://github.com/shadowspawn/nvh) Easily install Node.js versions
- [nvs](https://github.com/jasongin/nvs) Node Version Switcher - A cross-platform tool for switching between versions and forks of Node.js

## Suggested Compatible Format

Very few of the supporting products specify what they expect the file to contain, and I expect most just read it and process it as normal for _their_ version support. I would like to fill out the details on which products support which features, but for now here is an educated guess based on what I have seen.

- single line
- three part numeric version e.g. 14.5.0
- optional leading 'v' e.g. v14.5.0

So for example, this is likely to produce a widely compatible file (`sh`):

```
node --version > .node-version
```

## .ruby-version

For interest, here is a discussion about similar `.ruby-version` file format:

- https://gist.github.com/fnichol/1912050#gistcomment-682506