## The DartPad UI release process

- We follow a normal pull request, review, merge to master github workflow.
- New changes get batched up in master. Our CI bot runs on each PR; we maintain the master branch in an always-shipping state.
- the `web/app.yaml` file for `master` has the `version` set to `dev`. For technical reasons, it also needs to have the `secure: always` line commented out.
- When we're ready to release, we merge all of master into the `prod` branch. We only release production version from this branch.
- We verify that the `web/app.yaml` has it's version set to `prod`, and the `secure: always` line is enabled. The `tool/grind.dart` `deploy` task also does verification of the branch name and `web/app.yaml` settings.
- We then deploy from this branch (`grind deploy`, then a manual push to appengine).
- Between releases, if we have a critical fix, we apply the fix to the master branch. We then do a `git cherry-pick` of the commit(s) into the prod branch, and re-deploy from there.

This release workflow lets us continue to make forward development progress, while at the same time having a stable (and patchable) shipping prod version.

## Pushing to App Engine

- After following the above release process steps, `git checkout prod`
- `grind deploy`; this will create a deployable version of the prod website in `build/web/`
- Deploy the app from the App engine CLI, use the no-promote flag to promote from the cloud console: `gcloud app deploy build/web/app.yaml --project=dart-pad --no-promote`
- From the App Engine cloud console, made that deployed version of the app the default
