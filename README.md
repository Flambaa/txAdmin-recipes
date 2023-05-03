# txAdmin-recipes 
This repository is the index for the popular txAdmin's Server Deployer Recipes!
Please check the **[Recipe Documentation Page](https://github.com/tabarra/txAdmin/blob/master/docs/recipe.md)** if you wanna know more.

## Popular recipes:
- [CFX Default](https://github.com/tabarra/CFX-Default-recipe)
- [QBCore Framework](https://github.com/qbcore-framework/txAdminRecipe)
- [ESX Legacy](https://github.com/esx-framework/ESX-recipes)
- [ZAP-Hosting ESX Pack](https://github.com/zap-fivem/esx_12_recipe) (deprecated)
- [PlumeESX Legacy](https://github.com/tabarra/PlumeESX-recipe) (deprecated)

## Recipe-making Guidelines and Best Practices:
- Always start your recipe based on the CFX Default recipe. Copy the structure from server.cfg, resources folder, and recipe YAML;
- The recipe must "just work", without the user needing to edit anything before starting the server, like database credentials;
- Database stuff:
    - Preferable use the `{{dbConnectionString}}` placeholder in `server.cfg` instead of writing to some database config file;
    - Put the database stuff at the start of the recipes, as that is the most likely task to fail;
    - The recipe must accept the random database name generated by txAdmin instead of forcing a name like `es_extended`. If needed, you can perform a `replace_string` with the `{{dbName}}` variable;
    - When exporting the database, make sure to not also export player data like admins, bans and etc;
- Your `server.cfg` must contain the following placeholders: `{{maxClients}}`, `{{addPrincipalsMaster}}`, `{{serverEndpoints}}` and `{{svLicense}}`;
- Make sure your scripts/framework recognize users with the `admin` ACE group as script/framework admins. This can be done every time the player joins or even on his first join ([esx-legacy example](https://github.com/esx-framework/esx-legacy/commit/e265976561f6c72c9d95032861638c38b4505d20));
- If your recipe requires `download_github` from an external third party repository, it is recommended that you set the reference parameter, preferably to a commit instead of a tag, since tags can change. This guarantees that no recipe-breaking change will be introduced by some random commit;
- When downloading, extracting and moving Zip files, group the 3 actions so it is easier to find it after;
- Recipes must be onesync compatible, even if just `legacy`;
- Always set `$onesync` to `on` if your recipe supports it;
- Considering that most people are not familiar with what your recipe is installing, guarantee a good onboarding experience with the following:
    - The loading screen must clearly state what that framework is, and how to use it like keys to press and etc ([plume example](https://i.imgur.com/BREZLDW.png));
    - On important files like `server.cfg`, leave plenty of comments instructing the admin how to use or configure your framework;
- Execute a `waste_time` with 10 seconds every 25 `download_github` actions, or 50 if setting the `ref` parameter. Too many GitHub requests in a short amount of time will result in a 403 error;
- If your resources have some kind of inventory or any other NUI that activates on the press of `[TAB]`, it MUST use the [IsNuiFocused()](https://docs.fivem.net/natives/?_0x98545E6D) to prevent it stealing the focus from txAdmin menu when it is open ([example commit](https://github.com/qbcore-framework/qb-inventory/commit/978904e83dd379e44a2370347f311533df707c12)).
- Your framework must be fully compatible with txAdmin:
    - Using menu features like noclip/godmode/teleport/etc should not trigger any negative side effects (like an "anticheat" ban);
    - The txAdmin menu Heal command should also revive the player (eg from [esx_ambulancejob](https://github.com/esx-framework/esx_ambulancejob/blob/9ff01a716e29fffdf3913b15cd554c912a257aa3/server/main.lua#L46));
    - If you need any help or need any kind of integration, open an issue or contact the txAdmin Maintainer;
- Your recipe must not violate or facilitate violation of any license or copyright, so it should only contain resources that are open source (eg GPLv3/MIT/Apache) or sharable (eg Creative Commons). Please make sure it does not contain any leaked content. Although it is hard to find a scenario where a recipe could _directly_ violate any license, this is a headache that we must try to avoid;

****
<p align="center">
    <p align="center">
        <b>Do you have any questions? Things are looking too complicated? Join <code>#recipe-making</code> in our Discord!</b> <br>
        <a href="https://discord.gg/AFAAXzq"><img src="https://discordapp.com/api/guilds/577993482761928734/widget.png?style=banner2" alt="txadmin discord"></img></a>
    </p>
</p>
