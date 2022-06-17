# Test repo for [woorelease](https://github.com/woocommerce/woorelease)

This repo showcases how the entries are being built, how to exclude them, and how to specify a type. With `woorelease` and GitHub Release notes.

## Steps to reproduce
1. Release `1.0.0` from `develop` (manually, as you [cannot do that with the woorelease either](https://github.com/woorelease-bugs/initial-release))
2. `git co -b release/1.0.1`, make a commit there, tag `1.0.1`, and release, but don't make a PR yet!
### Woorelease
Create and merge a PR
1. (set type) with a body containing 
	```md
	### Changelog entry

	> Add - Added entry.
	```
2. (exclude) with a body finishing with
	```md
	### Changelog entry
	```
1. (multiple entries) with a body containing 
	```md
	### Changelog entry

	> Add - One change.
	> Fix - Second change.
	```
3. with a body containing
	```md
	### Changelog entry
	some leftover text
	```
4. (fall back to PR name) without any `### Changelog entry` section in the body
5. (problematic fallback) merging `release/1.0.1` branch with `Release 1.0.1` as a title, and no `### Changelog entry` section in the body
6. Generate chengelog with
	```
	woorelease cl:generate --product_version=1.0.2 https://github.com/woorelease-bugs/types-excludes/tree/develop
	```

### GitHub config
Create and merge a PR
1. (set type - automatic) from a branch prefixed `add/`, `fix/`, `remove/`, `update/`, or `tweak/`
1. (set type - manual) from any branch and assign a GH label `changelog: fix|add|update|tweak`
2. (exclude) and assign a GH label `changelog: none`
4. (fall for no label) from a non-prefixed branch and without any label
5. (automatically excluded releases) merging `release/*`
6. Go to https://github.com/woorelease-bugs/types-excludes/releases/new?tag=1.0.2 and click "Generate release notes"

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
