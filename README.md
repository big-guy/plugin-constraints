# Example plugin with dependency constraints

This template is based on `gradle init`, but adds contraints against other plugins that may be applied.

The plugin build is defined in `build-logic`. In `build-logic/build.gradle`, we define an implementation constraint on the Spotbugs plugin. We reject any 4.6.x version of the plugin. 

In `app/build.gradle`, we try to apply the Spotbugs plugin version 4.6.2. You can see the classpath for the `app` project by running `app:buildEnvironment`. 

The [build fails](https://scans.gradle.com/s/ccm2622rhlyvk/failure#1) because a plugin cannot be found that passes the constraints.
https://scans.gradle.com/s/ccm2622rhlyvk/build-dependencies?focusedDependency=WzEsMCwxLFsxLDAsWzFdXV0&focusedDependencyView=dependencies_or_failure&toggled=W1sxXSxbMSwwXV0

These constraints won't work with `buildSrc` currently because of the way we resolve dependencies for a `buildSrc` build. The failure message could be made better by focusing more on the build script classpath aspect of the failure. The failure is very similar to failures you would see with just project dependencies.