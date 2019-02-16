
## [Xcode Server](3-xcode-server.md) | Eric Dudiak | 1535 | p86

3-xcode-server.md


### Overview

- Custom environment variables
- Advanced trigger editing
- Issue tracking and blame
- Upgrade integrations
- Configurable integration user

Custom Environment Variables
New in Xcode 7.3


Advanced Triggers
Integration scripts

Email notifications

Issue Tracking and Blame
We all have issues


- Nobody is perfect
  - Tests will fail
  - Errors will come up
  - Xcode will blame you
- Even if you are perfect
  - SDKs change
  - Language improvements
  - Smarter tools

#### Identifying issue owners

- Lets you know when it’s time to act
- You broke it
  - You introduced an issue
  - Issue is on or near line you modified
  - You are the only committer
- You can help fix it
  - You probably know how to fix an issue
  - You seem to know about the area involved
  - Fuzzy matching

#### Bot configuration changes

- Tracks changes to your bot configuration
- Attributes issues to changes where possible
- Included in email reports

#### Upgrade Integrations

When it’s not your fault

- Re-integrates your project
- Same revision as the last integration
- Any new issues are due to the upgrade
- Prevents blaming you for broken builds


### Configurable Integration User

- Improved visibility into your integrations
- Allows customization
- You own and manage how your integrations run
- Can be any user on the system
- Runs as a menu extra


## Demo - Xcode Server | p145


Configurable Integration User
Improved visibility Customized simulators Normal macOS user Runs as a menu extra


#### Best practices

- Dedicate a new user
- Avoid using administrator accounts
- Stay logged in with Fast User Switching
- Disable screen lock
- Customize for your needs
  - Simulators
  - Networking (VPN and proxies)
  - User data and settings
  - Advanced provisioning