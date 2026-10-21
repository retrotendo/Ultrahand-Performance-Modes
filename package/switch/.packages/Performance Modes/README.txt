PERFORMANCE MODES v1.0
======================

Performance Modes switches between two Horizon OC setups:
- Battery Mode: stock-clock undervolting / efficiency profile
- OC Mode: normal overclock / performance profile

MENU LAYOUT
-----------
MAIN
  Current Profile

  Change Profile
    Battery Mode
    OC Mode

  Save Settings
    as Battery Mode
    as OC Mode

SETUP
  Initial Setup
    Reset Battery App Profiles -> STOCK
    Mark Current Boot -> Battery
    Mark Current Boot -> OC Mode
    Check Files

  Backup Files
    Create Safety Backup
    Restore Safety Backup

PROFILE STORAGE
---------------
Battery Mode is stored under ./Battery/.
OC Mode is stored under ./OCMode/.

Each mode stores:
  config.ini          = full Horizon OC config, including title-ID app profiles
  hoc.kip             = Horizon OC KIP configuration
  ReverseNX-RT/       = optional complete ReverseNX-RT settings folder

AUTO-SAVE ON MODE SWITCH
------------------------
When leaving OC Mode, the current Horizon config, hoc.kip and ReverseNX-RT
folder are saved to ./OCMode/ before Battery Mode is loaded. When leaving
Battery Mode, the reverse happens. CFW then reboots so the selected hoc.kip
becomes active.

RESET BATTERY APP PROFILES
--------------------------
Reset Battery App Profiles -> STOCK only runs while OC Mode is active.
If Battery Mode is active, nothing is changed and a notification tells you to
switch to OC Mode first.

CHECK FILES
-----------
Check Files verifies Battery config.ini + hoc.kip and OC Mode config.ini +
hoc.kip. If all four exist, it reports:
  All 4 core profile files: OK

SAFETY BACKUP
-------------
Create Safety Backup stores the active files plus both stored modes, including
ReverseNX-RT snapshots when present. Restore Safety Backup restores them and
reboots CFW.

INTERNAL STATE
--------------
The package state remains BATTERY / PERFORMANCE. PERFORMANCE is only the
internal state value used for OC Mode; the actual storage folder is ./OCMode/.
