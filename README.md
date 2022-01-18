# Ansible Role: Googler, google from the terminal

An Ansible Role that installs [Googler](https://github.com/jarun/googler) on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

If no version is specified, the latest version will be installed. Available [Googler releases](https://github.com/jarun/googler/releases).

    googler_version: 4.3.2

If no prefix is specified for the `bin/googler` binary placing, `/usr/local` is used.

    googler_prefix_dir: $HOME/.local

If the directory for downloading and extracting the release archive is not specified, `/tmp` is used.

    googler_download_dir: $HOME/Downloads

Search keyword and option completion scripts for Bash, Fish and Zsh can be copied to the specified locations.
<br />Paths from which autocompletions are usually loaded automatically:

    googler_bash_completions_dir: /etc/bash_completion.d
    googler_fish_completions_dir: /etc/fish/completions
    googler_zsh_completions_dir: /usr/share/zsh/functions/Completion/Zsh

You can also may want to use [googler @t](https://github.com/jarun/googler#googler-t) add-on, in which case specify where to copy the `google_at` file with convenient aliases:

    googler_at_aliases_dir: $HOME/.googler

To source it after installation, run:

    $ source $HOME/.googler/google_at

List of user environment files to add conditional export to the system PATH of a directory with the app binary.
<br />Only existing files with write access for the current ansible_user will be processed.
<br />If not specified, empty list is used.

    googler_env_files_to_modify:
      - $HOME/.profile
      - $HOME/.bashrc
      - $HOME/.zshenv

**NOTE:** By default, the base tasks of a role are skipped if the application is already installed in the desired
<br />bin directory and no version upgrade is required.
<br />&nbsp;&nbsp;&nbsp;&nbsp;If you want to add a conditional export to the system `PATH` of a directory with the app binary, or copy completion scripts,
<br />after the Playbook has already been run once, you can force the launch base role tasks by defining the `update_apps` variable
<br />and adding `googler` to the list. For example:
``` bash
$ ansible-playbook main.yaml -e "update_apps=[googler]"
```
This approach is also used to force an update to the latest available release.

## Dependencies

`make`, `Python 3.6` or later.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: ansible-role-googler
      googler_prefix_dir: $HOME/.local
      googler_bash_completions_dir: /etc/bash_completion.d
      googler_zsh_completions_dir: $HOME/.oh-my-zsh/completions
      googler_at_aliases_dir: $HOME/.oh-my-zsh/completions
```

## License

MIT
