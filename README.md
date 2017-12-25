# mattermost-github-integration

This role sets up a mattermost github integration service which posts changes of an organization or repository to a mattermost channel.


## Requirements

This role works standalone


## Role Variables

| Name                                           |         Required         | Default                              | Description                                                         |
|:-----------------------------------------------|:------------------------:|:-------------------------------------|:--------------------------------------------------------------------|
| `global_cache_dir`                             |    :heavy_check_mark:    |                                      | Cache directory to download roundcube files to                      |
| `mattermost_github_integration_install_path`   | :heavy_multiplication_x: | `/opt/mattermost-github-integration` | Path to install the server on                                       |
| `mattermost_github_integration_secret`         | :heavy_multiplication_x: | `None`                               | Secret that is used to authenticate between github and your server. |
| `mattermost_github_integration_server_hook`    | :heavy_multiplication_x: | `/`                                  | The relativ url where the server is listing.                        |
| `mattermost_github_integration_server_address` | :heavy_multiplication_x: | `0.0.0.0`                            | Adress of the server                                                |
| `mattermost_github_integration_server_port`    | :heavy_multiplication_x: | `5000`                               | Port under which the server listens to webooks from github          |
| `mattermost_github_integration_username`       | :heavy_multiplication_x: | `Github`                             | Name under which username the post should show up in mattermost     |
| `mattermost_github_integration_icon_url`       | :heavy_multiplication_x: | ` `                                  | Url to icon file which should show up in mattermost                 |
| `mattermost_github_integration_webhook_urls`   | :heavy_multiplication_x: | `[]`                                 | List of webhooks to post to. See below for more information         |
| `mattermost_github_integration_show_avatars`   | :heavy_multiplication_x: | `true`                               | show github avatars in the message that is posted                   |
| `mattermost_github_integration_ignore_actions` | :heavy_multiplication_x: | `[]`                                 | List of actions to ignore- See below for more information           |

### Webhooks

| Name      |      Required      | Default | Description                   |
|:----------|:------------------:|:--------|:------------------------------|
| `name`    | :heavy_check_mark: |         | Name of the repository/team where this information should go to |
| `url`     | :heavy_check_mark: |         | Url of the mattermost webhook |
| `channel` | :heavy_check_mark: |         | Channel id like town-square from mattermost. This is where the information gets posted to. |

When using `name` you can add `default` as a variable where everything is send to if it finds no other match. Also you can use `teamname` or `teamname/repositoryname` to have a better controll over the information like `stuvusIT` or `stuvusIT/mattermost-github-integration`

### Ignore actions
| Name       |      Required      | Default | Description                                             |
|:-----------|:------------------:|:--------|:--------------------------------------------------------|
| `category` | :heavy_check_mark: |         | Path to install the server on                           |
| `actions`  | :heavy_check_mark: |         | List of actions to be ignored e.g `labeled`, `assigned` |

## Example Playbook

```yml
hosts: all
  become: true
  vars:
    mattermost_github_integration_install_path: /opt/mattermost-github-integration
    mattermost_github_integration_secret: 0mHdpBa6SQdv5OUm
    mattermost_github_integration_webhook_urls:
      - name: default
        url: https://chat.stuvus.de/hooks/0mHdpBa6SQdv5OUm
        channel: it-bots
      - name: teamname
        url: https://chat.stuvus.de/hooks/0mHdpBa6SQdv5OUm
        channel: it-bots
    mattermost_github_integration_ignore_actions:
      - category: issues
        actions:
          - labeled
          - assigned
  roles:
    - mattermost-github-integration
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
