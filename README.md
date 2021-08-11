# create-release-pr

Creates a pull request for a release. We use this in the Cucumber project to add a manual
approval step before making an automated release from the (protected) `release/*` branch.

This action takes two inputs:

* `current_release`
* `next_version`

Both of these should be of the form `X.Y.Z`, the [semantic version] number of the release.

The action will create two branches: 

* `pre-release/v<next_version>` from the head of the current branch, marking the latest commit to be released
* `release/v<next_version>` from a commit tagged with `v<current_release>`, marking the last commit to have been released.

It then creates a pull request from the `pre-release/v<next_version>` branch to the `release/v<next_version_branch>` branch, containing all the commits to be released.

If either of those branches already exist, they will be force-pushed to match the current state of the repo.

[semantic version]: https://semver.org/