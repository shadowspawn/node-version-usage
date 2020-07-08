# .node-version File Usage

Q: Is `.node-version` read by multiple node version managers?  
A: Yes.

Q: Does `.node-version` have a defined common or standard file format?  
A: No.

Q: So what compatibility is there across individual products?  
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

Very few of the supporting products document what they expect the file to contain! From what I have seen most just read it and process it as normal for _their_ version support. This is an educated guess based on what I have seen.

- single line
- three part numeric version e.g. 14.5.0
- optional leading 'v' e.g. v14.5.0

So for example, this is likely to produce a widely compatible file:

```bash
node --version > .node-version
```

## Compatibility/Support

🚧Work in progress! 🚧

| Version  | fnm | nodenv | nvh | nvs |
| -------- | --- | ------ | --- | --- |
| simple: 14.5.0  | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  |
| leading v: v14.5.0  | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  |
| partial version: 10.2 | :white_check_mark:  | :x: | :white_check_mark:  |  ? |

| Line Ending  | fnm | nodenv | nvh | nvs |
| -------- | --- | ------ | --- | --- |
| Windows EOL  | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  | ? |
| missing EOL | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  | ? |
| Linux/Mac EOL | :white_check_mark:  | :white_check_mark:  | :white_check_mark:  | ? |

## References

For interest, here is a discussion about similar `.ruby-version` file format. The commonly supported format is a simple version, with some products adding fuzzy matching. (This is likely the inspiration for some of the `.node-version` usage, especially `nodenv` which uses `rbenv` syntax.)

- <https://gist.github.com/fnichol/1912050#gistcomment-682506>

Discussion about a standard for `.node-version` was opened in 2016 but got a bit bogged down. No agreement after over 3 years.

- <https://github.com/nodejs/version-management/issues/13>
