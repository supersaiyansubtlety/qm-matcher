# quirky matcher for qm

## setup

In order to match, you must have both [deno](https://deno.com/manual@v1.11.0/getting_started/installation) and java installed.

In this tutorial our old version will be `1.18` and our new version will be `1.19`.

0. Before you start, make sure you've merged all pull requests marked with `final-comment-period` in the QM repo!
1. Clone this repo. We'll be calling the folder you cloned it into our `root` folder.
2. Enter your root folder.
3. Clone QM with `git clone https://github.com/quiltmc/quilt-mappings [your old version name]`. For us, this means we'll have a QM clone in a directory named `1.18`.
4. Repeat, this time naming the clone after your new version.
5. Go into your new version clone and update the `MINECRAFT_VERSION` constant in `buildSrc/src/main/java/quilt/internal/Constants.java` to match your current version.
6. Still in the new version clone, run `git checkout -b [your new version name]` to create a new branch for the new version. (`git checkout -b 1.19` for us)
7. Return to your root folder. You're ready to start matching!

## matching

1. In both the old and new clones, run `./gradlew mapPerVersionMappingsJar`.
2. In the new clone, run `./gradlew dropInvalidMappings`.
3. Run `git add .` and `git commit -m "[your new version name]"` to commit.
4. Return to your root folder and run `deno task match [your old version] [your new version]`.
5. In the new clone, run `./gradlew dropInvalidMappings` again.
6. Run `./gradlew generatePackageInfoMappings` to generate new package info files.
7. Run `./gradlew build javadocJar` to test your build.
8. Run `git add .` and `git commit -m "match [your new version name] to [your old version name]"` to commit.
9. Run `git push`, and you're done!