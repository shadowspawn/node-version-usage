# .node-version File Usage

Q: Is `.node-version` read by multiple Node.js version managers?  
A: Yes.

Q: Does `.node-version` have a defined common or standard file format?  
A: No.

Q: So what compatibility is there across individual products?  
A: Good question! Read on...

## Supporting Products

Version managers for Node.js which read a `.node-version` file include (in alphabetical order):

- [asdf-nodejs](https://github.com/asdf-vm/asdf-nodejs) Node.js plugin for asdf version manager. (macOS, Linux)
- [avn](https://github.com/wbyoung/avn) Automatic Version Switching for Node. (macOS, Linux)
- [chnode](https://github.com/tkareine/chnode) Changes shell's current Node.js version by updating $PATH
- [direnv](https://github.com/direnv/direnv) unclutter your .profile. (macOS, Linux)
- [fnm](https://github.com/Schniz/fnm) 🚀 Fast and simple Node.js version manager, built in Rust. (macOS, Linux, Windows)
- [n](https://github.com/tj/n) Interactively Manage Your Node.js Versions. (macOS, Linux)
- [nenv](https://github.com/ryuone/nenv) Groom your app’s Node environment with nenv (macOS, Linux)
- [nodenv](https://github.com/nodenv/nodenv) Manage multiple NodeJS versions. (macOS, Linux)
- [nodist](https://github.com/nullivex/nodist) Natural node.js and npm version manager for windows. (Windows)
- [nvm.fish](https://github.com/jorgebucaran/nvm.fish) Node.js version manager lovingly made for Fish. (macOS, Linux)
- [nvs](https://github.com/jasongin/nvs) Node Version Switcher - A cross-platform tool for switching between versions and forks of Node.js. (macOS, Linux, Windows)

Other products which read `.node-version` include:

- [Cloudflare Pages](https://developers.cloudflare.com/pages/platform/build-configuration#language-support-and-tools) Build fast sites. In record time.
- [Hostman](https://hostman.com) Hosting platform that deploys your web applications
- [netlify](https://docs.netlify.com/configure-builds/manage-dependencies/#node-js-and-javascript) Instantly build and deploy your sites to our global network from Git.
- [paketo](https://paketo.io/docs/howto/nodejs/) Your app,
in your favorite language,
ready to run in the cloud
- [render](https://render.com/docs/node-version) A Cloud for the New Decade
- [starship](https://starship.rs/config/#nodejs) ☄🌌️ The minimal, blazing-fast, and infinitely customizable prompt for any shell!

## Suggested Compatible Format

If you are creating the file, the format with full compatibility across current tests is:

- single line with unix line ending
- three part numeric version e.g. 14.5.0

A leading 'v' is widely supported, so this will work with most implementations:

```bash
$ node --version
v10.15.3
$ node --version > .node-version
```

If you are reading the file in a new implementation, I suggest you also support optional leading `v` and any line ending.
Allowing a leading `v` is common and gives nice symmetry with `node --version`. Allowing any line ending makes it easier
for users and especially Windows users to create a file compatible with your product.

## Compatibility Testing

| Version Match | asdf | avn | chnode | direnv | fnm | n | nenv | nodenv | nodist  | nvm.fish | nvs |
| ------------- | ---- | --- | ------ | ------ | --- |---| ---- | ------ | ------  | -------- | --- |
| simple: 14.5.0  | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| leading v: v14.5.0  | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :white_check_mark: | :x: |  :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| partial version: 10.2 | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: |  🧩 [#1] | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| **Line Ending** |
| unix EOL | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |  :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| missing EOL | :white_check_mark: | :white_check_mark: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |  :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Windows EOL  | :x: | :white_check_mark: | :x: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: |  :white_check_mark: | :white_check_mark: | :x: | :white_check_mark: |

[#1]: https://github.com/shadowspawn/node-version-usage/issues/1

## References

For interest, here is a discussion about similar `.ruby-version` file format. The commonly supported format is a simple version, with some products adding fuzzy matching. (Ruby is likely the inspiration for some of the `.node-version` usage, especially `nodenv` which uses `rbenv` syntax.)

- <https://gist.github.com/fnichol/1912050>

A discussion about a possible standard format for `.node-version` was started in 2016 initially
covering desirable (new) features and then more focus on existing usage, but did not reach consensus.

- <https://github.com/nodejs/version-management/issues/13>

StackOverflow: What uses / respects the .node-version file?

- <https://stackoverflow.com/questions/27425852/what-uses-respects-the-node-version-file>
