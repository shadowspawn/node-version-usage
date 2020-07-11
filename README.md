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

Very few of the supporting products document what they expect the file to contain! If you are creating the file, the format with full compatibility across current tests is:

- single line with unix line ending
- three part numeric version e.g. 14.5.0

A leading 'v' is widely supported, so this will work with most implementations:

```bash
node --version > .node-version
```

If you are reading the file in a new implementation, I suggest you also support optional leading `v` and any line ending.
Allowing a leading `v` is common and gives nice symmetry with `node --version`. Allowing any line ending makes it easier
for users and especially Windows users to create a file compatible with your product.

## Compatibility Testing

| Version | asdf | avn | direnv | fnm | nodenv | nvh | nvs |
| ------- | ---- | --- | ------ | --- | ------ | --- | --- |
| simple: 14.5.0  | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| leading v: v14.5.0  | :white_check_mark: | :white_check_mark: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| partial version: 10.2 | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | 🧩 [#1] | :white_check_mark: | :white_check_mark: |

| Line Ending | asdf | avn | direnv | fnm | nodenv | nvh | nvs |
| ----------- | ---- | --- | ------ | --- | ------ | --- | --- |
| unix EOL | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| missing EOL | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Windows EOL  | :x: | :white_check_mark: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

ToDo: `nodist`

## References

For interest, here is a discussion about similar `.ruby-version` file format. The commonly supported format is a simple version, with some products adding fuzzy matching. (Ruby is likely the inspiration for some of the `.node-version` usage, especially `nodenv` which uses `rbenv` syntax.)

- <https://gist.github.com/fnichol/1912050#gistcomment-682506>

Discussion about a standard for `.node-version` was opened in 2016 but got a bit bogged down. No agreement after over 3 years.

- <https://github.com/nodejs/version-management/issues/13>

[#1]: https://github.com/shadowspawn/node-version-usage/issues/1
