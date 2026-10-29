# rljson additions to the gg workflow

These rules win where the development guide says otherwise.

- **Publish:** you run `gg do publish` yourself, once the user has said
  "publish" for the ticket — do not ask the user to run it. Follow
  `/gg-publish`.
- **Pull requests:** CI on a pull request checks that every commit went
  through gg's local checks (`gg one did commit`). The full tests run on
  `main` after the merge: watch them after every publish.
