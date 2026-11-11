Soulcalibur II HD Online for PS5 (homebrew port)

This is a native PS5 build of the PS3 game Soulcalibur II HD Online, made with static recompilation. It runs as an ordinary PS5 homebrew app on a jailbroken console, at 60 fps with full audio. It’s based on the PC recompilation by n0madic and the ps3recomp toolchain, carried over to the PS5’s FreeBSD-based system and Vulkan graphics.

How it’s a port, not emulation

An emulator like RPCS3 runs the original PS3 program as-is. It reads the game’s PowerPC machine code while the game is playing and translates or interprets it on the fly, pretending to be a PS3 the whole time.

This build works differently:

The game’s code was translated before it ever runs. The PS3 executable’s PowerPC code was converted ahead of time into C code. That code was then compiled with a normal compiler into x86-64 code for the PS5’s AMD CPU. What runs on your PS5 is a native program; no PowerPC code is decoded during play.
The Cell co-processor (SPU) programs got the same treatment. The game uses them for sound mixing and other jobs, and they were translated into native code as well.
The PS3’s system libraries are rewritten, not emulated. When the game calls PS3 system functions for audio output, file access, controllers, threads and so on, those calls go straight to new implementations built on the PS5’s own system. There’s no PS3 operating system or firmware underneath, and no PS3 BIOS is needed.
Graphics are translated to Vulkan. The game still builds PS3-style graphics command lists. A renderer reads those lists and draws them with Vulkan on the PS5’s GPU, using shaders converted from the PS3 originals. This is the one part that works like a compatibility layer, closer to how Proton translates DirectX on Linux than to emulating a CPU.

The game logic is the original game’s, translated into native code, and everything it talks to has been rebuilt around it for the PS5. This is also why it can run at full speed where emulating the Cell processor would be far heavier.

What it needs

You must supply your own copy of the game. The build contains none of the game’s data, and it’s for personal use only.

Extract the PPSA77069 contents to your /data directory

copy game files into /data/sc2hd/ on the PS5
  - your game package  UP0700-NPUB31366_00-SC2HDONLINEGAME1*.pkg (Rename it to game.pkg)
  - the 01.01 update package (UP0700-NPUB31366_00-SC2HDONLINEGAME1-A0101-V0100-PE.pkg), if you have it
  - the license (UP0700-NPUB31366_00-SC2HDONLINEGAME1.rap)
The title installs and decrypts them into /data/sc2hd/hdd0 (once; several
minutes), then starts the game.

Status

Story and arcade modes, versus and character select all play at full speed with correct audio and graphics. Online mode isn’t available yet, same as in the PC port.
