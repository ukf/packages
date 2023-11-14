# `ukf/packages`

This repository acts as a package registry for the other
UK federation projects hosted on GitHub. A single package
registry is used so that consumers do not need to add
a repository reference for each dependency used.

This repository is public; you can download packages freely
using the GitHub user interface even if not logged in.
However, note that GitHub requires that use of the package
registry from tools such as Maven is authenticated. This is
normally done by using a Personal Access Token with the
`read:packages` scope.

For Maven, include a `<repository>` definition like this in
your project's POM:

```xml
<repositories>
    <repository>
        <id>ukf-packages</id>
        <url>https://maven.pkg.github.com/ukf/packages</url>
    </repository>
</repositories>
```

To use a Personal Access Token to provide authentication
for a Maven build, include it in your `~/.m2/settings.xml`
like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0
        http://maven.apache.org/xsd/settings-1.2.0.xsd">

    <servers>

        <server>
            <id>ukf-packages</id>
            <username>your-github-username</username>
            <password>your-personal-access-token</password>
        </server>

    </servers>

</settings>
```

To provide authentication for a CI job using GitHub Actions,
you can build an appropriate `settings.xml` file with an
action like this:

```yaml
    - name: Set up Maven
      uses: s4u/maven-settings-action@v2.8.0
      with:
        servers: |
          [{
              "id": "ukf-packages",
              "username": "${{ github.actor }}",
              "password": "${{ secrets.GITHUB_TOKEN }}"
          }]
```

## Copyright and License

The contents of this repository and the associated package registry
are Copyright (C) the named contributors or their employers, as
appropriate.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use these files except in compliance with the License.
You may obtain a copy of the License at

> <http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
