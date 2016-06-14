[TOC]

# Overview
- `pacman` will not remove configuration that the application itself creates (for examples "dotfiles" in the home folder).

# User guide
- To install packages: `# pacman -S pkg_name1 pkg_name2 ...`
- To remove a package and leaving all of its dependencies: `# pacman -R pkg_name`
- To remove a package and its dependencies: `# pacman -Rs pkg_name`
- To remove a package, its dependencies and all the packages that depend on the target package: `# pacman -Rsc pkg_name`
- To remove a package, which is required by another package, without removing the dependent package: `# pacman -Rdd pkg_name`
- To synchronize the repository database and update the system's packages (excluding "local" packages that are not in the configured repositories): `# pacman -Syu`
- Remember that pacman's output is logged in `/var/log/pacman.log`
- To query the local package database with the `-Q` flag: `$ pacman -Q --help`
- To query the sync databases with the `-S` flag: `$ pacman -S --help`
- To search for packages: `$ pacman -Ss string1 string2 ....`
- To search for already installed packages: `$ pacman -Qs string1 string2 ...`
- To display extensive information: `$ pacman -Si pkg_name`
- For locally: `$ pacman -Qi pkg_name`
- To retrieve a list of the files installed by a package: `$ pacman -Ql pkg_name` or `$ pacman -Qlq package | grep -v '/$' | xargs du -h | sort -h`
- To list all packages no longer required as dependencies (orphans): `$ pacman -Qdt`
- To list all packages explicitly installed and not required as dependencies: `$pacman -Qet`
- To list a dependency tree of a packages: `$ pactree pkg_name`
- To list all the packages recursively depending on an installed package: `$ pactree -r pkg_name`
- Database structure: the pacman databases are normally located at `/var/lib/pacman/sync`. For each repository specified in `/etc/pacman.conf` there will be a corresponding database file located there.
- pacman stores its downloaded packages in `/var/cache/pacman/pkg/` and does not remove the old or uninstalled versions automatically. To remove the cache version of removed packages: `# pacman -Sc`. To remove all caches: `# pacman -Scc`

Only do this when certain that previous package versions are not required, for example for a later downgrade, if do this when you need downgrade older versions would have to be retrieved through Archive Arch

- To remove all cached versions of uninstalled packages and keep 3 versions of each packages: `# paccache -ruk3`
- Download a package without installing it: `# pacman -Sw pkg_name`
- Install a 'local' package that is not from a remote repository (e.g the package is from the AUR): `# pacman -U /path/to/package/package_name-version.pkg.tar.xz`; `# pacman -U http://www.example.com/repo/example.pkg.tar.xz`
- List installed packages follow time install (use expac): `expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -20`
- List all explicitly installed packages: `$ pacman -Qe`
- List all foreign packages (manually downloaded and installed): `$ pacman -Qm`
- List all native packages (installed from the sync database): `$ pacman -Qn`
- To list all native packages and explicitly installed and not required as dependencies: `$ pacman -Qen`
- To list all installed packages sorted by size: `$ expac -H M '%m\t%n' | sort -h` or `$ pacgraph -c`
	+ expac for more small packages
	+ with pacgraph you can draw image
- Remove all orphan packages: `# pacman -Rns $(pacman -Qtdq)`
- Remove everything but base group: `# pacman -R $(comm -23 <(pacman -Qq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))`

# Easy backup and restore
`pacman -Qqm` lists foreign packages name; which, for must users, means AUR
`pacman -Qqe` lists packages name that were explicitely installed.
that said,
  `pacman -Qqe | grep -v "$(pacman -Qqm)" > pacman.lst`
and
  `cat pacman.lst | xargs pacman -S --needed --noconfirm`
are the best backup/restore lines i've seen (don't remember where i got them tho).
