# Test repo for [woorelease](https://github.com/woocommerce/woorelease)

This repo showcases how the entries are being built, how to exclude them, and how to specify a type. With `woorelease` and GitHub Release notes.

## Steps to reproduce
1. Release `1.0.0` from `develop` (manually, as you [cannot do that with the woorelease either](https://github.com/woorelease-bugs/initial-release))
2. `git co -b release/1.0.1`, make a commit there, tag `1.0.1`, and release, but don't make a PR yet!
### Woorelease
Create and merge a PR
1. [(set type - manual)](https://github.com/woorelease-bugs/types-excludes/pull/2) with a body containing 
	```md
	### Changelog entry

	> Add - release.yml
	```
2. [(exclude)](https://github.com/woorelease-bugs/types-excludes/pull/6) with a body finishing with
	```md
	### Changelog entry
	```
1. [(multiple entries)](https://github.com/woorelease-bugs/types-excludes/pull/7) with a body containing 
	```md
	### Changelog entry

	> Update - PR links
	> Add - changelog results
	```
3. [(problematic exclude)](https://github.com/woorelease-bugs/types-excludes/pull/1) with a body containing
	```md
	### Changelog entry
	some leftover
	```
4. [(fall back to PR name)](https://github.com/woorelease-bugs/types-excludes/pull/5) without any `### Changelog entry` section in the body
5. [(problematic fallback)](https://github.com/woorelease-bugs/types-excludes/pull/3) merging `release/1.0.1` branch with `Release 1.0.1` as a title, and no `### Changelog entry` section in the body
6. Generate chengelog with
	```
	woorelease cl:generate --product_version=1.0.2 https://github.com/woorelease-bugs/types-excludes/tree/develop
	```
	```diff
	= 1.0.2 - 2022-06-17 =
	* Add - One change.
	* Add - release.yml.
	* Fix - Add links to PRs.
    ⚠️* Fix - Release 1.0.1.
	* Fix - Second change.
	⚠️* Fix - some leftover.
	* Tweak - Update README.md.
	```

### GitHub config
Create and merge a PR
1. [(set type - automatic)](https://github.com/woorelease-bugs/types-excludes/pull/2) from a branch prefixed `add/`, `fix/`, `remove/`, `update/`, or `tweak/`
1. [(set type - manual)](https://github.com/woorelease-bugs/types-excludes/pull/4) from any branch and assign a GH label `changelog: fix|add|update|tweak`
2. [(exclude)](https://github.com/woorelease-bugs/types-excludes/pull/6) and assign a GH label `changelog: none`
4. [(fall back for no label)](https://github.com/woorelease-bugs/types-excludes/pull/5) from a non-prefixed branch and without any label
5. [(automatically excluded releases)](https://github.com/woorelease-bugs/types-excludes/pull/3) merging `release/*`
6. There is no way to [specify multiple entries per single PR](https://github.com/woorelease-bugs/types-excludes/pull/7) (yet?)
7. Go to https://github.com/woorelease-bugs/types-excludes/releases/new?tag=1.0.2 and click "Generate release notes"
	```
	## What's Changed
	### New Features 🎉
	* Add a workflow to attach label based on PR branchname by @tomalec in https://github.com/woorelease-bugs/types-excludes/pull/1
	* Add release.yml by @tomalec in https://github.com/woorelease-bugs/types-excludes/pull/2
	⚠️* Update links & add results by @tomalec in https://github.com/woorelease-bugs/types-excludes/pull/7
	### Tweaked
	* Update README.md by @tomalec in https://github.com/woorelease-bugs/types-excludes/pull/4
	### Other Changes
	* Add links to PRs by @tomalec in https://github.com/woorelease-bugs/types-excludes/pull/5
	```

## Prerequisites

We aim to support the latest two minor versions of WordPress, WooCommerce, and PHP. (L-2 policy)

-   WordPress 5.7+
-   WooCommerce 6.0+
-   PHP 7.3+

<p align="center">
	<br/><br/>
	Made with 💜 by <a href="https://woocommerce.com/">WooCommerce</a>.<br/>
	<a href="https://woocommerce.com/careers/">We're hiring</a>! Come work with us!
</p>
