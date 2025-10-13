# How to contribute

## General terms

1. By contributing to this project you grant the repository owner the full copyright to the contribution.
2. Generally small changes and fixes are more likely to be merged as large changes can easily lead to conflicts in the future.
3. A change in the common codebase must not cause additional issues in target subprojects. It must compile for all subprojects.
4. Changes to pins, interrupts, task priorities, heap/stack sizes must be carefully examined for side effects as they can have unintended consequences in seemingly unrelated modules. Generally do not change these unless absolutely required and tested.
5. Read the [wiki](https://github.com/Ultrawipf/OpenFFBoard/wiki) for additional information about [pinouts](https://github.com/Ultrawipf/OpenFFBoard/wiki/Pinouts-and-peripherals), features, [commands](https://github.com/Ultrawipf/OpenFFBoard/wiki/Commands) and contribution info

### Simplified steps for contribution
1. Clone/Fork the projects master branch
2. Make your changes and create a commit (If it requires GUI features to be changed it is recommended to do the same with the [configurator repo](https://github.com/Ultrawipf/OpenFFBoard-configurator) or if its just a small change detail what the effect is and request a change)
3. Create a pull request for your fork against master and describe your contribution in a detailed way. What bug does it fix? Which feature is added?
4. Wait for approval and append requested changes to your branch
5. Your code gets squash/rebase merged if approved

### Release workflow
Changes should be added in the CHANGELOG.md file.
This will be used to generate release notes.

The release workflow runs automatically on every push to master to verify that releases can be built successfully.
When pushing to master, if a new version is detected in CHANGELOG.md, a GitHub release is automatically created. A tag with a "-" (e.g., v1.x.x-beta) generates a prerelease.

To create a new release:
1. Update CHANGELOG.md with the changes in a new version section (e.g., "### Changes in 1.17:")
2. Commit and push to master
3. The workflow will automatically create a tag and release based on the version in CHANGELOG.md

A release is triggered automatically when a new version section is added to CHANGELOG.md and pushed to master.

### Submodules
The configurator is an important part of the project and should be kept up to date with any changes required to support a firmware and the submodule should if possible point to a commit that works with the corresponding firmware version.

Pull the submodules with `git submodule update --init`.

### Branches
If you directly push a branch to the project as a developer your branch name should contain your username or the type of feature. Like `ultrawipf/warpspeed` or `feature/pwmdriver`.
Set your git author name correctly before committing.

### Code style
The code should follow the same style as the other parts of the project and you should use easy to understand comments for complex statements and new functions.

### Flash storage
If you require a variable to be stored in flash check the eeprom emulation functions and choose an address according to `scripts/memory_map.csv` and add it to the list in [`scripts/memory_map.csv`](../../Firmware/scripts/memory_map.csv). 

The script `scripts/generate_memory.py` is used to generate `eeprom_addresses.c` and `eeprom_addresses.h` from the csv file to keep track of used addresses and automatically set the right defitions.

In general you should use a block of addresses per class and use the space efficiently. If you have 5 bools and an 8 bit int to store don't use 6 full addresses but pack them into a single uint16_t.
