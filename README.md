What's this?
============

A Microsoft Universal Printer Driver (aka Unidrv) "minidriver" for the [Royal LetterMaster](http://blog.ajf.me/2015-04-08-daisy-wheel-diaries-part-1), a budget 1980s daisy wheel printer. It's supposed to run on Windows 2000 or later.

It doesn't work, unfortunately. Something about the .INF or .GPD file means it won't install. Which is a shame.

It's also pointless. After struggling with it and being unable to get it to work, I discovered that the Windows "Generic / Text Only" driver supports unprintable margins, bold and underline, so long as you tell it the correct commands. Which means this driver is a waste of time, since those were the only problems with Windows's own driver.

Oh well.

Usage
-----

If you want to get this to work, you'll need to [start Windows in the mode where it doesn't check driver signatures](http://revryl.com/2013/02/19/force-driver-windows-8/), because it's unsigned.

Even surmounting that hurdle, though, the driver seems uninstallable: something's wrong with it, but I'm not sure exactly what.

### How you could generate a Security Catalog File if you really wanted to

Add `CatalogFile=LetterMaster.cat` in the `[Version]` section of `LetterMaster.inf`.

To generate `lettermaster.cat` use `Inf2Cat`, available as part of the Windows Driver Kit. The command would look something like this:

    inf2cat /drv:"F:\Projects\2015\Royal LetterMaster\LetterMaster-Unidrv" /os:2000,XP_X86,XP_X64,Server2003_X86,Server2003_IA64,Server2003_X64,Vista_X86,Vista_X64,Server2008_X86,Server2008_IA64,Server2008_X64,7_X86,7_X64,Server2008R2_IA64,Server2008R2_X64,Server8_x64,8_ARM,8_X86,8_X64,Server6_3_X64,6_3_ARM,6_3_X64,6_3_x86

Note that:

* `/drv` is given the name of the *directory* containing the inf file, not the inf file itself
* `/os` here is given every OS inf2cat supports, but there might be more in future

Then you'd need to sign it somehow to make this particularly meaningful.
