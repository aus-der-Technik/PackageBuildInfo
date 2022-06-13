![swift-version](https://img.shields.io/badge/swift-5.6-brightgreen.svg?style=for-the-badge)
![Mac OS](https://img.shields.io/badge/-platform-gray?style=for-the-badge)![Mac OS](https://img.shields.io/badge/mac%20os-000000?style=for-the-badge&logo=Apple&logoColor=F0F0F0)![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)
[![License](https://img.shields.io/github/license/yonaskolb/Mint.svg?style=for-the-badge)](LICENSE)

# PackageBuildInfo

#### Automated Swift Package version and build numbering via Git. Swift Package Manager plugin.

Wouldn't it be great if your Swift Package-based projects just take their version and build number automatically from git? Well, now it can!

Using a new amazing feature - Swift Package Manager prebuild plugin, you can generate .swift file with current build info from git. It will never modify your local project.

## Requirements

* SwiftPM 5.6 or later.
* git
* bash

## Usage

* Add to package dependencies:

```
.package(url: "https://github.com/DimaRU/PackageBuildInfo", branch: "master")
```

* Add to target:

```
plugins: [
    .plugin(name: "packageBuildInfoPlugin", package: "PackageBuildInfo")
]
```

## Sample project

Sample project here:
[https://github.com/DimaRU/PackageBuildInfoExample](https://github.com/DimaRU/PackageBuildInfoExample)

## Generated file example:

```swift
/////
//// Package Build info
///  Code generated by PackageBuildInfo. DO NOT EDIT.
//
import Foundation

public struct PackageBuild {
    let isDirty: Bool       // Dirty build - git directory is't clean.
    let timeStamp: Date     // Time of last commit
    let timeZone: TimeZone  // Time Zone
    let count: Int          // Total commit count
    let tag: String?        // Tag, if exist
    let countSinceTag: Int  // Commit count since tag
    let branch: String?     // Git branch name
    let digest: [UInt8]     // Latest commit sha1 digest (20 bytes)

    var commit: String {
        digest.reduce("") { $0 + String(format: "%02x", $1) }
    }
    static let info = PackageBuild(
                              isDirty: false,
                              timeStamp: Date(timeIntervalSince1970: 1651955365),
                              timeZone: TimeZone(secondsFromGMT: 10800) ?? TimeZone.current,
                              count: 6,
                              tag: "1.0.0",
                              countSinceTag: 2,
                              branch: "master",
                              digest: [0x72, 0x75, 0x92, 0xa4, 0x2d, 0xa7, 0x16, 0xb5, 0x9d, 0x2b, 0x0f, 0x06, 0x1d, 0xbc, 0x61, 0x4d, 0xc9, 0xa7, 0x58, 0x92])
}
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](LICENSE)
