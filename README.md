# Byte-level care

How to live with zero problems through Total Control.

- 


## CI

How to design and implement continuous integration.

- Run in a premade container or install OS packages
- Display environment information
- Set access credentials
- Version control
  - Git committer
  - Commit message
  - PR title
- Cache OS and programming language library packages
- Check programming language and framework version compatibility
- Check package management configuration (validate & normalize)
- Check outdated packages and known security vulnerabilities
- Build code
- Configure application
- :zero: Byte-level
  - Check execute file mode bit
  - Look for non-ASCII characters
    (non-English alphabets, whitespace characters, control characters)
- :one: Syntax errors
  - Check source code for syntax errors
  - Check template files for syntax errors
- :two: Run unit and functional tests
- :three: Static Analysis
  - Run static analysis: **PHPStan**
  - Magic Number Detector
  - Copy-Paste Detector
- :four: Coding Standards
  - Check coding style
  - Adhere to EditorConfig
- Measure code coverage
- Check route methods (controllers of routes)
- Check list of distributed files
- Check spelling: Codespell
- Custom checks and warnings
- Display logs in CI output or upload logs as artifacts
- Start CD by SSH-ing to own server (`restrict,command` in authorized_keys and `DenyUsers` in sshd.conf)
- Wipe sensitive data

## CD

How to design and implement continuous delivery.

- Possible constrains:
  * successful tests
  * do not run on PR-s
  * our repo
  * specific branch
  * tag in commit message `[deploy:prod]`
  * deploy head commit only
  * optional manual start ([GitLab manual actions](https://gitlab.com/help/ci/yaml/README.md#manual-actions))
- Do not run as root user
- Keep deploy configuration in a file
- Log every output to a file, log start and finish to syslog
- Limit execution time of time-consuming steps (timeout)
- Optionally back up project files before starting to deploy
- Create a bot user on the server for git access with SSH key (`@companybot`)
- List changes in current project files
- [Check for maintenance mode](/webserver/laravel/Commands/IsDownForMaintenance.php),
  Turn on maintenance mode `php artisan down`
  covering static resource, page, AJAX and API requests
- Clear caches (configuration, routes, application, template etc.)
- Wait for to finish and disable cron jobs and background workers after clearing caches (email piped to a program)
- Identify git repository and branch
- Checkout by commit hash (not by branch HEAD)
- At least **lint the source code**
- Don't deploy testing packages
- Enable production optimizations in package manager
- Build code
- Run database migrations
- Turn off maintenance mode
- Populate caches (application, OPcache, `wp rewrite flush`)
- Run at least 1 basic functional or unit test (e.g. log in or display dashboard)
- Check HTML output
- Special sudo configuration for reloading PHP-FPM or Cachetool
- **Alert on failure**
- "Was down for X seconds"
- Send email, Slack, Trello or Google Hangouts notification

## Coding standards

* Tool: squizlabs/php_codesniffer # `phive install phpcs`
* Tool: dealerdirect/phpcodesniffer-composer-installer

- [commenting rules](https://github.com/squizlabs/PHP_CodeSniffer/tree/master/src/Standards/PEAR/Sniffs/Commenting)
- wp-coding-standards/wpcs
- automattic/phpcs-neutron-standard , automattic/phpcs-neutron-ruleset
- slevomat/coding-standard
- object-calisthenics/phpcs-calisthenics-rules
- consistence/coding-standard
- symplify/coding-standard

## Static analysis

* Tool: phpstan/phpstan # `phive install phpstan`
* Tool: dave-liddament/sarb # `phive install sarb`

- ekino/phpstan-banned-code
- phpstan/phpstan-strict-rules
- phpstan/phpstan-deprecation-rules
- ergebnis/phpstan-rules
- thecodingmachine/phpstan-strict-rules
- pepakriz/phpstan-exception-rules
- nunomaduro/larastan
- szepeviktor/phpstan-wordpress
