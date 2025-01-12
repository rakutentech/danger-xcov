<h3 align="center">
<img src="/assets_readme/logo.png" alt="xcov Logo" />
</h3>

-------

[![Twitter: @nakiostudio](https://img.shields.io/badge/contact-@nakiostudio-blue.svg?style=flat)](https://twitter.com/nakiostudio)
[![License](https://img.shields.io/badge/license-MIT-green.svg?style=flat)](https://github.com/nakiostudio/xcov/blob/master/LICENSE)
[![Gem](https://img.shields.io/gem/v/danger-xcov.svg?style=flat)](http://rubygems.org/gems/danger-xcov)
[![Gem Downloads](https://img.shields.io/gem/dt/danger-xcov.svg?style=flat)](http://rubygems.org/gems/danger-xcov)

**danger-xcov** is the [Danger](https://github.com/danger/danger) plugin of
[xcov](https://github.com/nakiostudio/xcov), a friendly visualizer for Xcode's
code coverage files.

## Installation

```
sudo gem install danger-xcov
```

## Usage

Simply add `xcov.report` to your `Dangerfile` passing those **xcov** parameters
you need. Click [here](https://github.com/nakiostudio/xcov#parameters-allowed) to
see the updated list of parameters allowed by **xcov**.

```ruby
xcov.report(
   scheme: 'EasyPeasy',
   workspace: 'Example/EasyPeasy.xcworkspace',
   exclude_targets: 'Demo.app',
   minimum_coverage_percentage: 90,
   minimum_coverage_percentage_for_changed_files: 80,
   ignore_list_of_minimum_coverage_percentage_for_changed_files: ['View', 'State']
)
```

The result is as cool as follows:

<h3 align="center">
<img src="/assets_readme/xcov_danger.png" />
</h3>

You can also process the output generated by **xcov** before posting the markdown
report as follows:

```ruby
# Generate report
report = xcov.produce_report(
  scheme: 'EasyPeasy',
  workspace: 'Example/EasyPeasy.xcworkspace',
  exclude_targets: 'Demo.app',
  minimum_coverage_percentage: 90,
  minimum_coverage_percentage_for_changed_files: 80,
  ignore_list_of_minimum_coverage_percentage_for_changed_files: ['View', 'State']
)

# Do some custom filtering with the report here

# Post markdown report
xcov.output_report(report)
```

## Updates in the plugin
- Added `minimum_coverage_percentage_for_changed_files` parameter to allow minimum coverage for new and modified files only.
- Added `ignore_list_of_minimum_coverage_percentage_for_changed_files` parameter to allow skipping files based on the architecture of the project.
   - For example, if the parameter is like `ignore_list_of_minimum_coverage_percentage_for_changed_files: ['View', 'State']`, then any filename which **contains** the word `View` or `State` will be skipped from this coverage check.

## Linking this custom support to your repo
Add this to your gemfile instead of `danger-xcov`, point it to this fork.
```ruby
gem 'danger-xcov', :git => 'https://github.com/rakutentech/danger-xcov.git'
```

## License
This project is licensed under the terms of the MIT license. See the LICENSE file.
