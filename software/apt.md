- `apt-add-repository` and `add-apt-repository` is the same.
- Remove ppa: `apt-add-repository --remove ppa:whatever/ppa`
- View list of ppa: `ls /etc/apt/sources.list.d`
- List of packages installed locally: `dpkg --get-selections | grep -v deinstall`

