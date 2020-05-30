# The Changelog

## 1.7
### The Andrew Release

**Features**
- Gravity Sync will now manage the `custom.list` file that contains the "Local DNS Records" function within the Pi-hole interface.
- If you do not want this feature enabled it can be bypassed by adding a `SKIP_CUSTOM='1'` to your .conf file. 
- Sync will be trigged during a pull operation if there are changes to either file.

**Known Issues**
- No new Star Trek references.

#### 1.7.1
- There is a changelog file now. I'm mentioning it in the changelog file. So meta.
- `./gravity-sync.sh version` will check for and alert you for new versions.

#### 1.7.2
This update changes the way that beta/development updates are applied. To continue receving the development branch, create an empty file in the `gravity-sync` folder called `dev` and afterwards the standard `./gravity-sync.sh update` function will apply the correct updates.
```
cd gravity-sync
touch dev
./gravity-sync.sh update
```
Delete the `dev` file and update again to revert back to the stable/master branch.

**Deprecation**
- Removes `beta` function for applying development branch updates.

## 1.6
### The Restorative Release

**Features**
- New `./gravity-sync.sh restore` function will bring a previous version of the `gravity.db` back from the dead.
- Changes the way that Gravity Sync prompts for data input and how confirmation prompts are handled.
- Adds ability to override verification of 'push', 'restore' or 'config' reset, see `.example` file for details.
- Five new Star Trek references.

**Bug Fixes**
- New functions add consistency in status output.

## 1.5
### The Automated Release

**Features**
- You can now easily deploy the task automation via crontab by running `./gravity-sync.sh automate` which will simply ask how often you'd like to run the script per hour, and then create the entry for you.
- If you've already configured an entry for this manually with a prior version, the script should detect this and ask that you manually remove it or edit it via crontab -e. I'm hesitant to delete existing entries here, as it could potentially remove something unrelated to Gravity Sync.

**Bug Fixes**

- Changes the method for pulling development branch updates via the 'beta' function.
- Cleanup of various exit commands.

## 1.4
### The Configuration Release

**Features**
- Adds new `./gravity-sync config` feature to simplify deployment!
- Adds variables for SSH settings.
- Rearranges functions, which impacts nothing.
- All new and exciting code comments.
- No new Star Trek references.

#### 1.4.1
- Adds variables for custom log locations to `gravity-sync.conf`, see `.example` file for listing.

#### 1.4.2
- Will prompt to create new `gravity-sync.conf` file when run without an existing configuration.

#### 1.4.3
- Bug fixes around not properly utilizing custom SSH keyfile.

## 1.3
### The Comparison Release
1.3 should be called 2.0, but I'll resist that temptation -- but there are so many new enhancements!

**Features**
- Gravity Sync will now compare remote and local databases and only replicate if it detects a difference.
- Verifies most commands complete before continuing each step to fail more gracefully.
- Additional debugging options such as checking last cronjob output via `./gravity-sync.sh cron` if configured.
- Much more consistency in how running commands are processed in interactive mode.

#### 1.3.1
- Changes [GOOD] to [DONE] in execution output.
- Better validation of initial SSH connection.
- Support for password based authentication using SSHPASS.

#### 1.3.2
- MUCH cleaner output, same great features.

#### 1.3.3
- Corrected Pihole bin path issue that cause automated sync not to reload services.

#### 1.3.4
- Moves backup of local database before initiating remote pull.
- Validates file ownership and permissions before attempting to rewrite.
- Added two Star Trek references.

## 1.2
### The Functional Release
- Refactored process to use functions and cleanup process of execution.
- Does not look for permission to update when run.
- Cleanup and expand comments.

#### 1.2.1
- Improved logging functions.

#### 1.2.2
- Different style for status updates.

#### 1.2.3
- Uses a dedicated backup folder for `.backup` and `.last` files.
- Copies db instead of moving to rename and then replacing to be more reliable.
- Even cleaner label status.

#### 1.2.4
- Changes `~` to `$HOME`.
- Fixes bug that prevented sync from working when run via crontab.

#### 1.2.5
- Push function now does a backup, on the secondary PH, of the primary database, before pushing.

## 1.1
### The Pushy Release

- Seperated main purpose of script into `pull` argument.
- Allow process to reverse back using `push` argument.

#### 1.1.2
- First release since move from being just a Gist.
- Just relearning how to use GitHub, minor bug fixes.

#### 1.1.3
- Now includes example an configuration file.

#### 1.1.4
- Added update script.
- Added version check.

#### 1.1.5
- Added ability to view logs with `./gravity-sync.sh logs`.

#### 1.1.6
- Code easier to read with proper tabs.

## 1.0
### The Initial Release

No version control, variables or anything fancy. It only worked if everything was exactly perfect.

```
echo 'Copying gravity.db from HA primary'
rsync -e 'ssh -p 22' ubuntu@192.168.7.5:/etc/pihole/gravity.db /home/pi/gravity-sync
echo 'Replacing gravity.db on HA secondary'
sudo cp /home/pi/gravity-sync/gravity.db /etc/pihole/ 
echo 'Reloading configuration of HA secondary FTLDNS from new gravity.db'
pihole restartdns reload-lists
```

For real, that's it. 6 lines, could provably be done with less.