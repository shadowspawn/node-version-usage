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
- [chnode](https://github.com/tkareine/chnode) Changes shell's current Node.js version by updating $PATH (macOS, Linux)
- [dev](https://docs.pkgx.sh/using-dev/dev) `dev` is built on [pkgx](https://docs.pkgx.sh), a single, standalone binary that can run anything (macOS, Linux)
- [direnv](https://github.com/direnv/direnv) unclutter your .profile. (macOS, Linux)
- [fnm](https://github.com/Schniz/fnm) 🚀 Fast and simple Node.js version manager, built in Rust. (macOS, Linux, Windows)
- [mise](https://github.com/jdx/mise) Polyglot switcher compatible with asdf plugins, built in Rust. (macOS, Linux)
- [n](https://github.com/tj/n) Interactively Manage Your Node.js Versions. (macOS, Linux)
- [nenv](https://github.com/ryuone/nenv) Groom your app’s Node environment with nenv (macOS, Linux)
- [nodeenv](http://ekalinin.github.io/nodeenv/) Virtual environment for Node.js & integrator with virtualenv (macOS, Linux, Windows)
- [nodenv](https://github.com/nodenv/nodenv) Manage multiple NodeJS versions. (macOS, Linux)
- [nodist](https://github.com/nullivex/nodist) Natural node.js and npm version manager for windows. (Windows)
- [nve](https://github.com/ehmicky/nve) Run any command on specific Node.js versions (macOS, Linux, Windows)
- [nvm-rust](https://github.com/BeeeQueue/nvm-rust) A cross-platform node version manager that doesn't suck (macOS, Linux, Windows)
- [nvm.fish](https://github.com/jorgebucaran/nvm.fish) Node.js version manager lovingly made for Fish. (macOS, Linux)
- [nvs](https://github.com/jasongin/nvs) Node Version Switcher - A cross-platform tool for switching between versions and forks of Node.js. (macOS, Linux, Windows)
- [setup-node](https://github.com/actions/setup-node) ([configuration](https://github.com/actions/setup-node/blob/main/docs/advanced-usage.md#node-version-file)) Set up your GitHub Actions workflow with a specific version of node.js

Other products which read `.node-version` include:

- [bitrise](https://bitrise.io) The CI/CD Platform built for Mobile DevOps
- [Cloudflare Pages](https://developers.cloudflare.com/pages/platform/language-support-and-tools/#supported-languages-and-tools) Build fast sites. In record time.
- [Hostman](https://hostman.com) Hosting platform that deploys your web applications
- [netlify](https://docs.netlify.com/configure-builds/manage-dependencies/#node-js-and-javascript) Instantly build and deploy your sites to our global network from Git.
- [paketo](https://paketo.io/docs/howto/nodejs/) Your app, in your favorite language, ready to run in the cloud
- [preferred-node-version](https://github.com/ehmicky/preferred-node-version) Get the preferred Node.js version of a project or user
- [render](https://render.com/docs/node-version) A Cloud for the New Decade
- [Spaceship](https://spaceship-prompt.sh/sections/node/) Minimalistic, powerful and extremely customizable Zsh prompt
- [starship](https://starship.rs/config/#nodejs) ☄🌌️ The minimal, blazing-fast, and infinitely customizable prompt for any shell!
- [Vercel Conformance](https://vercel.com/docs/workflow-collaboration/conformance/rules/REQUIRE_NODE_VERSION_FILE) Conformance provides tools that run automated checks on your code for product critical issues, such as performance, security, and code health.
- [VMware Tanzu](https://docs.vmware.com/en/VMware-Tanzu-Buildpacks/services/tanzu-buildpacks/GUID-nodejs-nodejs-buildpack.html) The Tanzu Node.js Buildpack supports several popular configurations for Node.js apps.

(Note: [nvm](https://github.com/nvm-sh/nvm) does _not_ support reading a `.node-version` file. See [#4] for more.)

## Suggested Compatible Format

If you are creating the file, a format with full compatibility across current tests is:

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

| Utility                                              | simple             | leading `v`        | partial            | Unix EOL           | No EOL             | Win EOL | Notes   |
| :---                                                 | :---:              | :---:              | :---:              | :---:              | :---:              | :---:   |  :---:  |
|                                                      | `10.1.2`           |  `v10.1.2`         | `10.2`             |                    |                    |         |         |
| [asdf](https://github.com/asdf-vm/asdf-nodejs)       | :white_check_mark: | :white_check_mark: | :x:                | :white_check_mark: | :white_check_mark: | :x: | |
| [avn](https://github.com/wbyoung/avn)                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :ghost: [#11] |
| [chnode](https://github.com/tkareine/chnode)         | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [dev](https://docs.pkgx.sh/using-dev/dev)            | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [direnv](https://github.com/direnv/direnv)           | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: | |
| [fnm](https://github.com/Schniz/fnm)                 | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [mise](https://github.com/jdx/mise)                  | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [n](https://github.com/tj/n)                         | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nodeenv](http://ekalinin.github.io/nodeenv/)        | :white_check_mark: | :x:                | :x:                | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nenv](https://github.com/ryuone/nenv)               | :white_check_mark: | 🧩 [#8]            | 🧩 [#8]            | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nodenv](https://github.com/nodenv/nodenv)           | :white_check_mark: | :white_check_mark: | 🧩 [#1]            | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nodist](https://github.com/nullivex/nodist)         | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nve](https://github.com/ehmicky/nve)                | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nvm-rust](https://github.com/BeeeQueue/nvm-rust)    | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [nvm.fish](https://github.com/jorgebucaran/nvm.fish) | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: | |
| [nvs](https://github.com/jasongin/nvs)               | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |
| [setup-node](https://github.com/actions/setup-node)  | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | |

[#1]: https://github.com/shadowspawn/node-version-usage/issues/1
[#4]: https://github.com/shadowspawn/node-version-usage/issues/4
[#8]: https://github.com/shadowspawn/node-version-usage/issues/8
[#11]: https://github.com/shadowspawn/node-version-usage/issues/11#issuecomment-1509992826

The columns show whether the utility supports a file containing:

- simple: three part numeric version, like `10.1.2`
- leading `v`: numeric version with a leading `v`, like `v10.1.2`
- partial: numeric version with less than three parts, like `10.2`
- EOL: end of line characters used in file, Unix `\n` or Windows `\r\n` or none

## References

For interest, here is a discussion about similar `.ruby-version` file format. The commonly supported format is a simple version, with some products adding fuzzy matching. (Ruby is likely the inspiration for some of the `.node-version` usage, especially `nodenv` which uses `rbenv` syntax.)

- <https://gist.github.com/fnichol/1912050>

A discussion about a possible standard format for `.node-version` was started in 2016 initially
covering desirable (new) features and then more focus on existing usage, but did not reach consensus.

- <https://github.com/nodejs/version-management/issues/13>

StackOverflow: What uses / respects the .node-version file?

- <https://stackoverflow.com/questions/27425852/what-uses-respects-the-node-version-file>
