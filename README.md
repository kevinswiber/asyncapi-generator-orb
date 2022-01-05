# swiberdev/asyncapi-generator Orb

[![CircleCI Build Status](https://circleci.com/gh/kevinswiber/asyncapi-generator-orb.svg?style=shield 'CircleCI Build Status')](https://circleci.com/gh/kevinswiber/asyncapi-generator-orb) [![CircleCI Orb Version](https://badges.circleci.com/orbs/swiberdev/asyncapi-generator.svg)](https://circleci.com/orbs/registry/orb/swiberdev/asyncapi-generator) [![GitHub License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://raw.githubusercontent.com/kevinswiber/asyncapi-generator-orb/master/LICENSE) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

## Example

```yaml
version: 2.1
orbs:
  ag: swiberdev/asyncapi-generator@1.0.0
  aws-s3: circleci/aws-s3@3.0
jobs:
  sync-s3:
    docker:
      - image: cimg/python:3.6
    steps:
      - attach_workspace:
          at: /tmp/asyncapi-generator
      - aws-s3/sync:
          from: /tmp/asyncapi-generator
          to: 's3://my-s3-bucket-name/prefix'
          arguments: |
            --acl public-read \
            --cache-control "max-age=86400"
workflows:
  asyncapi-generator-example:
    jobs:
      - ag/run:
          arguments: -p baseHref=/test-experiment/ -p sidebarOrganization=byTags
          filepath: docs/api/my-asyncapi.yml
          output: generated-html
          template: '@asyncapi/html-template@0.15.4'
      - sync-s3
```

## Resources

[CircleCI Orb Registry Page](https://circleci.com/orbs/registry/orb/swiberdev/asyncapi-generator-orb) - The official registry page of this orb for all versions, executors, commands, and jobs described.
[CircleCI Orb Docs](https://circleci.com/docs/2.0/orb-intro/#section=configuration) - Docs for using and creating CircleCI Orbs.

### How to Contribute

We welcome [issues](https://github.com/kevinswiber/asyncapi-generator-orb/issues) to and [pull requests](https://github.com/kevinswiber/asyncapi-generator-orb/pulls) against this repository!

### How to Publish

- Create and push a branch with your new features.
- When ready to publish a new production version, create a Pull Request from _feature branch_ to `master`.
- The title of the pull request must contain a special semver tag: `[semver:<segment>]` where `<segment>` is replaced by one of the following values.

| Increment | Description                       |
| --------- | --------------------------------- |
| major     | Issue a 1.0.0 incremented release |
| minor     | Issue a x.1.0 incremented release |
| patch     | Issue a x.x.1 incremented release |
| skip      | Do not issue a release            |

Example: `[semver:major]`

- Squash and merge. Ensure the semver tag is preserved and entered as a part of the commit message.
- On merge, after manual approval, the orb will automatically be published to the Orb Registry.

For further questions/comments about this or other orbs, visit the Orb Category of [CircleCI Discuss](https://discuss.circleci.com/c/orbs).

## License

MIT
