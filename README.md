# How to release an old version of an NPM module

Let's assume we are currently at version 1.0.0 and need to make a security release for 0.1.x branch, 0.1.1. Here's how to do this without overriding the `latest` tag on NPM, which is on by default when running `npm publish`. This makes the assumption that you have properly released via git tags, otherwise you'll have to find proper GitShas.

1. Fetch all git tags and checkout a new branch from the v0.1.0 release/tag `git checkout -b 0.1.x v0.1.0`
1. Create a new branch for the 0.1.x series `git checkout -b 0.1.x` and push to GitHub
1. Checkout a new branch (named whatever you want) for the 0.1.x security fix `git checkout -b security-fix`
1. Make your changes and push the branch to GitHub
1. Make a pull request to the 0.1.x branch
1. Once approved, merge those changes
1. Checkout the 0.1.x branch on your local and update the package.json to 0.1.1, update the CHANGELOG, and push directly to the 0.1.x branch
1. Create a new tag `git tag -a v0.1.1 -m 'v0.1.1'` and push that tag `git push --tags`
1. Publish to NPM with with the `--tag` flag `npm publish --tag previous` - this will prevent the 0.1.1 release from being marked as `latest` and installing in new projects rather than the 1.0.x release. (The usage of `previous` is arbitrary, as long as you don't type `latest` this can be whatever string you want)
