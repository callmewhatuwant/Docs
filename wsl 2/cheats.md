# cheats

## To list installed distributions

```sh
wsl -l
wsl --list
```

## To list installed distributions along with its running status and wsl config being 1 or 2

```sh
wsl -l --verbose
wsl -l -v
```

## To run a specific distro

```sh
wsl -d distro_name
wsl --distribution distro_name
```

## To terminate/shutdown a specific distro

```sh
wsl -t distro_name_to_shutdown
wsl --terminate distro_name_to_shutdown
```

## To shutdown all disstros

```sh
wsl --shutdown
```

## Set specific distro as default

```sh
wsl -s my_default_distro
wsl --set-default my_default_distro
```

## To EXPORT a running distro as image

```sh
wsl --export distro_name_to_export windows_path\tar_file_name.tar
```

## To IMPORT an image as distro

```sh
wsl --import new_distro_name install_location_windows_path tar_file_name.tar --version wsl-version-1-or-2
wsl --import Ubuntu-20 D:\VMs\WSL\Ubuntu-20\ Ubuntu-20.04.tar --version 2 # Setting my secondary HDD as storate loc for new distro
```

## To UNREGISTER (also removes the its file storage) a distro

```sh
wsl --unregister distro_name_that_delete
```

## To run a WSL distro as the specified user

```sh
wsl -u username -d distroname
wsl -u root -d Ubuntu-20.04
```

## To change the default user for a distribution

```sh
distributionName config --default-user Username
ubuntu config --default-user my_default_username
ubuntu2004.exe config --default-user johndoe # When you have Ubuntu 20.04 version installed from the Microsoft Store
```