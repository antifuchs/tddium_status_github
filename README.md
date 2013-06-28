## What?

Provides [GitHub status notifications](https://github.com/blog/1227-commit-status-api) when running tests through [Tddium](http://tddium.com).

## How?

### Create a GitHub OAuth token

Create a new [GitHub application](https://github.com/settings/applications) and create a new token from that application with the scope "repo:status":
```
$ curl -u {username}:{password} https://api.github.com/authorizations -X POST \
  -d '{"scopes": ["repo:status"], "client_id": "...", "client_secret": "..."}'
```

#### Or

Create a new token using basic authentication and the scope "repo:status":
```
$ curl -u {username}:{password} https://api.github.com/authorizations -X POST \
  -d '{"scopes": ["repo:status"], "note": "tddium status updater"}'
```

### Add the token to Tddium

Add the returned token to your Tddium account or suite configuration:

```
$ tddium config:add account GITHUB_TOKEN {token}
```

### Add tddium_status_github to your project

Add `tddium_status_github` to your Gemfile.

And, in your Rakefile make sure to include:

```ruby
require 'tddium_status_github'
```

#### Or

Add the following to your `tddium.yml` configuration:
```yaml
:tddium:
  # Existing configuration...
  :boot_hook: >
    /usr/bin/env sh -c "gem install --user-install --no-rdoc --no-ri tddium_status_github &&
    echo '$:.concat(Dir.glob(File.join(Gem.user_dir, \"gems\", \"*\", \"lib\"))); require \"tddium_status_github\"' >> Rakefile"
```

## Copyright and license

Copyright 2013 Zendesk

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
