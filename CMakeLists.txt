#this cmake is only used for installing scripts to target)
cmake_minimum_required(VERSION 2.8.9)
set(BRDISKSCR brdskmgr) #update-script helper
set(UPDATESCR update)   #update script
set(FINDDEVSCR find-devtype)  #device detction scrtipt
set(STARTUP_SCR_MOUNT S02MountSettings)  #settings partition mount script
set(STARTUP_SCR_DEVFIND S01FindDevType)  #device detection startup script
set(STARTUP_SCR_DROPBEAR S50dropbear)  #ssh service customized-startup script
set(FSTAB_FILE fstab)  #fstab

file(GLOB UPDATE_SCRIPTS ${BRDISKSCR} ${UPDATESCR} ${FINDDEVSCR})
install(PROGRAMS ${UPDATE_SCRIPTS} DESTINATION usr/sbin)

file(GLOB STARTUP_SCRIPTS ${STARTUP_SCR_MOUNT} ${STARTUP_SCR_DEVFIND} ${STARTUP_SCR_DROPBEAR})
install(PROGRAMS ${STARTUP_SCRIPTS} DESTINATION etc/init.d)

file(GLOB OTHER_SCRIPTS ${FSTAB_FILE})
install(FILES ${OTHER_SCRIPTS} DESTINATION etc)

#for cross compiling
#cmake -H. -BOutput -DCMAKE_TOOLCHAIN_FILE=/path/to/toolchain-arm-backup.cmake -DCMAKE_INSTALL_PREFIX=/home/user/tmp/
#cmake --build Output -- all
#cmake --build Output -- install

#for local compiling
#cmake -H. -BOutput
#cmake --build Output -- all

#for cleaning make generated output
#rm -rf Output

