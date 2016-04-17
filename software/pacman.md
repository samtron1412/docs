[TOC]

# Overview

# User guide
1. To install packages:
# pacman -S pkg_name1 pkg_name2 ...
2. To remove a package and leaving all of its dependencies
# pacman -R pkg_name
3. To remove a package and its dependencies
# pacman -Rs pkg_name
4. To remove a package, its dependencies and all the packages that depend on the target package
# pacman -Rsc pkg_name
5. To remove a package, which is required by another package, without removing the dependent package
# pacman -Rdd pkg_name
6. pacman will not remove configuration that the application itself creates (for examples "dotfiles" in the home folder).
7. To synchronize the repository database and update the system's packages (excluding "local" packages that are not in the configured repositories)
# pacman -Syu
8. Remember that pacman's output is logged in /var/log/pacman.log
9. pacman queries the local package database with the -Q flag
$ pacman -Q --help
10. pacman queries the sync databases with the -S flag
$ pacman -S --help
11. search for packages
$ pacman -Ss string1 string2 ....
12. search for already installed packages
$ pacman -Qs string1 string2 ...
13. To display extensive information
$ pacman -Si pkg_name
14. For locally
$ pacman -Qi pkg_name
15. To retrieve a list of the files installed by a package
$ pacman -Ql pkg_name
$ pacman -Qlq package | grep -v '/$' | xargs du -h | sort -h
16. To list all packages no longer required as dependencies (orphans)
$ pacman -Qdt
17. To list all packages explicitly installed and not required as dependencies
$pacman -Qet
18. To list a dependency tree of a packages
$ pactree pkg_name
19. To list all the packages recursively depending on an installed package,
$ whoneeds pkg_name
$ pactree -r pkg_name
20. Database structure: the pacman databases are normally located at /var/lib/pacman/sync. For each repository specified in /etc/pacman.conf there will be a corresponding database file located there.
21. pacman stores its downloaded packages in /var/cache/pacman/pkg/ and does not remove the old or uninstalled versions automatically:
# pacman -Sc

Only do this when certain that previous package versions are not required, for example for a later downgrade, if do this when you need downgrade older versions would have to be retrieved through Archive Arch

To remove all cached versions of uninstalled packages,, except fro the most recent 3
# paccache -ruk0
22. Download a package without installing it
# pacman -Sw pkg_name
23. Install a 'local' package that is not from a remote repository (e.g the package is from the AUR)
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

# pacman -U http://www.example.com/repo/example.pkg.tar.xz
23. To keep a copy of the local package in pacman's cache, use:
# pacman -U file:///path/to/package/package_name-version.pkg.tar.xz
24. List installed packages follow time install (use expac)
expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -20
25. List all explicitly installed packages
$ pacman -Qe
26. List all foreign packages (manually downloaded and installed)
$ pacman -Qm
27. List all native packages (installed from the sync database)
$ pacman -Qn
To list all native packages and explicitly installed and not required as dependencies
$ pacman -Qen
28. To list all installed packages sorted by size
$ expac -H M '%m\t%n' | sort -h
$ pacgraph -c
expac for more small packages
with pacgraph you can draw image
29. Remove all orphan packages
# pacman -Rns $(pacman -Qtdq)
30. Remove everything but base group
# pacman -R $(comm -23 <(pacman -Qq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))

pacman -Qqm lists foreign packages; which, for must users, means AUR
pacman -Qqe lists packages that were explicitely installed.
that said,
  pacman -Qqe | grep -v "$(pacman -Qqm)" > pacman.lst
and
  cat pacman.lst | xargs pacman -S --needed --noconfirm
are the best backup/restore lines i've seen (don't remember where i got them tho).
