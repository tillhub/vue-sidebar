# 1.0.0 (2018-12-03)


### Bug Fixes

* fixed padding not being applied + watchers being called in wrong `this` context ([1678f9c](https://github.com/tillhub/vue-sidebar/commit/1678f9c))
* fixed sidebar component name ([f0daf6e](https://github.com/tillhub/vue-sidebar/commit/f0daf6e))


### Features

* initial commit ([9ef14ef](https://github.com/tillhub/vue-sidebar/commit/9ef14ef))
* reimplemented sidebar by reusing dialog's code instead of extending it ([1e22fc1](https://github.com/tillhub/vue-sidebar/commit/1e22fc1))


### BREAKING CHANGES

* `showTitle` prop has been inverted and is now named `hideTitle`. Title is still
visible by default.
