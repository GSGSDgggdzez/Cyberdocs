# Recon-ng

Allows automating OSINT work

[Recon-ng](https://github.com/lanmaster53/recon-ng) 

Create a workspace

```sh
workspaces create WORKSPACE_NAME
```

Start reconnaissance with the specific workspace.

```sh
recon-ng -w WORKSPACE_NAME
```

Check the names of the tables in our database

```sh
db schema
```

Insert the domain name `target-domain.com` into the domains table

```sh
db insert domains
#domain (TEXT): target-domain.com
```

Search, install, remove and get information about modules

```sh
marketplace {search | install | remove | info} KEYWORD*
```

Working with installed modules

```sh
modules search
modules {load | search} MODULE
```

To set option values

```sh
options list
options set Name VALUES
run
```

### Keys

Some modules cannot be used without a key for the corresponding service API. `K` indicates that you must provide the appropriate service key to use the module in question.

- `keys list` list keys
- `keys add KEY_NAME KEY_VALUE` adds a key
- `keys remove KEY_NAME` removes a key

Once all modules are installed, you can proceed to load and run them.

- `modules load MODULE` loads an installed module
- `CTRL + C` unloads the module.
- `info` to view the loaded module information.
- `options list` lists the available options for the chosen module.
- `options set NAME VALUE`
- `run` to execute the loaded module.

