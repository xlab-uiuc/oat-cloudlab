# Profile for Acto on CloudLab

## Usage

### Fetch the profile

First, obtain the profile, by either accessing this link https://www.cloudlab.us/p/Sieve-Acto/acto-cloudlab?refspec=refs/heads/main, or creating a new one from this repository following the instructions below:

<details><summary>Click to show details</summary>

On the web dashboard of CloudLab, click "Experiments" -- "Create Experiment Profile"

1. Give your profile a name, e.g. `acto-cloudlab`.
2. Click the "Git Repo" button and enter the URL `https://github.com/xlab-uiuc/acto-cloudlab`. "Confirm".
3. Preview the information loaded from the repo, e.g. source code, XML, description, instructions etc.
4. Optionally configure the permissions as per your needs. "Create".

After the creation procedure is done, click the "Instantiate" button.

</details>

### Instantiate the profile

Either way, you should now be landing on the page of instantiating the profile, i.e. create an experiment based on it.

1. **Select a Profile**: This profile (`acto-cloudlab`, or your provided name if you manually imported it) should be automatically selected. You may want to read the description on screen.
2. **Parameterize**: All parameters are hardwired and this step will be skipped automatically.
3. **Finalize**: Optionally give your experiment a name. If you are a member of multiple CloudLab projects, choose the proper one for running the experiment also on this screen.
4. **Schedule**: Generally you would leave this screen as default and extend the experiment afterwards if needed. Click the "Finish" button.

Wait for the experiment to be created and set up. **Note that there can be such a stage where the progress bar indicates completeness, but the "State" is `booted (startup services are still running)`. Please be patient and wait for "State" to become `ready`** -- because at this time, the machine is still running the [startup scripts](scripts) and the environment isn't fully set up yet.

Once the startup scripts also complete, you can log in to the machine and begin your tests.

### Alternative machine types

The default hardware type `c6420` is recommended for the best reproduced results. However, if that type is not currently available, you may choose another one following the instructions below. You can check the current resource availability on [this page](https://www.cloudlab.us/resinfo.php).

<details><summary>Click to show details</summary>

The `main` branch of this repository always uses `c6420` as the hardware type. In addition, this repository provides profiles that use other hardware types in their corresponding branches. Instantiate them via the following links:

- `c6420` (the same as `main`): https://www.cloudlab.us/p/Sieve-Acto/acto-cloudlab?refspec=refs/heads/c6420
- `c8220`: https://www.cloudlab.us/p/Sieve-Acto/acto-cloudlab?refspec=refs/heads/c8220
- `c6320`: https://www.cloudlab.us/p/Sieve-Acto/acto-cloudlab?refspec=refs/heads/c6320

Or if you imported the profile by yourself in previous sections:

1. Go to "Experiments" -- "My Profiles" and find the profile.
2. Go the detail page of that profile, scroll to the page bottom and find "Repository Branches and Tags".
3. Click the "Instantiate" button for the particular branch/hardware type you wish to launch an experiment with.

</details>

## Development

- When this repository gets updated, the imported CloudLab profile won't synchronize automatically. You should:
    1. Go to "Experiments" -- "My Profiles" and find the profile.
    2. Click the edit icon.
    3. Click the "Update" button next to the "Repository" field.
    4. When it gets done, verify that the commit hashes are the desired values.
- Some of the startup script internals were discussed in https://github.com/xlab-uiuc/acto/pull/257.
- The Ansible scripts were moved out of tree from [the other repo](https://github.com/xlab-uiuc/acto). Some of the internals were discussed there, e.g. https://github.com/xlab-uiuc/acto/pull/247
- When you see `Oops! No parameter bindings in the rspec; did you call bindParameters()?`, the possible reason is:
    - In your default branch like `main`, some parameters are left adjustable.
    - Meanwhile, in the branch you are currently instantiating, you have hardwired everything.

    Looks like a bug of CloudLab? A workaround is to also hardwire everything in the default branch.

- Git practice: let's always rebase `c8220` onto the tip of `main`/`c6420`?
