# google-cast-sdk-dynamic

Through version 4.2.x, the `google-cast-sdk` pod referenced the
dynamically-linked version of the Google Cast iOS framework.  This was a ~20MB
download and a ~50MB framework.

Starting with 4.3.1, `google-cast-sdk` now refers to the statically-linked
framework, which is a ~200MB download and a ~600MB framework, and can cause
linker issues when used with other Google dependencies.

This repo includes a podspec for newer versions of the dynamically-linked Google
Cast iOS framework, which circumvents most of these issues by using a copy of
the original podspec, but with changes so that it points at the dynamic
framework files inside of the archive instead of the static library files.

This spec is hosted as a secondary spec repo instead of simply hosting a single
podspec to point to because it appears that's the only reliable way to get
`http`-source specs to work right now.

## Usage:

In your `Podfile`:

```ruby
# This must appear below the CocoaPods CDN source
source 'https://github.com/oreillymedia/google-cast-sdk-dynamic.git'

pod 'google-cast-sdk-dynamic', '4.4.7'
```

then `pod install`.
