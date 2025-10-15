### README for files/ directory
#### But why? 
In the event you don't want to expose your custom files publicly in a repository, you can place them here.
#### Info
- Directory for placing local customized [vulhub](https://github.com/vulhub/vulhub) files/directories to be used by the ludus_vulhub role.
- These files will be copied to /opt/vulhub (or the path specified by `vulhub_install_path`) on the target host.
- If you want to use a local copy of vulhub files instead of cloning from GitHub, set `use_local_vulhub_files` to true.