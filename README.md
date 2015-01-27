# autorandr 
Automatically select a display configuration based on connected devices

## Branch information

This is a compatible Python rewrite of
[wertarbyte/autorandr](https://github.com/wertarbyte/autorandr).

The original [wertarbyte/autorandr](https://github.com/wertarbyte/autorandr)
tree is unmaintained, with lots of open pull requests and issues. I forked it
and merged what I thought were the most important changes. If you are searching
for that version, see the [`legacy` branch](https://github.com/phillipberndt/autorandr/tree/legacy).
Note that the Python version is better suited for non-standard configurations,
like if you use `--transform` or `--reflect`. If you use `auto-disper`, you
have to use the bash version, as there is no disper support in the Python
version (yet). Both versions use a compatible configuration file format, so
you can, to some extent, switch between them.  I will maintain the `legacy`
branch until @wertarbyte finds the time to maintain his branch again.

If you are interested in why there are two versions around, see
[#7](https://github.com/phillipberndt/autorandr/issues/7),
[#8](https://github.com/phillipberndt/autorandr/issues/8) and
especially
[#12](https://github.com/phillipberndt/autorandr/issues/12)
if you are unhappy with this version and would like to contibute to the bash
version.

## License information and authors

autorandr is available under the terms of the GNU General Public License
(version 3).

Contributors to this version of autorandr are:

* Alexander Wirt
* Chris Dunder
* Maciej Sitarz
* Matthew R Johnson
* Phillip Berndt
* Rasmus Wriedt Larsen
* Stefan Tomanek
* Timo Bingmann
* Tomasz Bogdal
* stormc
* tachylatus

## How to use

Save your current display configuration and setup with:
```
autorandr --save mobile
```

Connect an additional display, configure your setup and save it:
```
autorandr --save docked
```

Now autorandr can detect which hardware setup is active:
```
 $ autorandr
   mobile
   docked (detected)
```

To automatically reload your setup, just append `--change` to the command line

To manually load a profile, you can use the `--load <profile>` option.

autorandr tries to avoid reloading an identical configuration. To force the
(re)configuration, apply `--force`.

To prevent a profile from being loaded, place a script call _block_ in its
directory. The script is evaluated before the screen setup is inspected, and
in case of it returning a value of 0 the profile is skipped. This can be used
to query the status of a docking station you are about to leave.

If no suitable profile can be identified, the current configuration is kept.
To change this behaviour and switch to a fallback configuration, specify
`--default <profile>`.

Another script called `postswitch` can be placed in the directory
`~/.autorandr` as well as in all profile directories: The scripts are executed
after a mode switch has taken place and can notify window managers or other
applications about it.

To install autorandr call `make install`, define your setup and then call
`make hotplug` to install hotplug scripts.
