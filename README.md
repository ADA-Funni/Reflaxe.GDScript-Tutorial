# Reflaxe (GDScript)
Reflaxe (GDScript) is a tool used for programming Godot Engine projects in Haxe.
It works by transpiling your Haxe code into GDScript, to be cleanly used within Godot Engine.
## Setup
> [!IMPORTANT]
> Install Haxe and Godot Engine before following this tutorial!
### Add Godot Engine to your system PATH
> [!WARNING]
> This step differs depending on your OS. Just follow the same principles, and Google how to create environment variables on your OS if it isn't Windows.
1. Search for "System environment variables" in the Start Menu.
2. Click "Environment variables".
3. Go to "System variables", and click "New".
4. Set the variable name to "GODOT_PATH", and set the variable value to where your Godot Engine's exe file is.
5. Restart Command Prompt.
### Set up your project
1. Run `cd (your project folder)` in the terminal.
2. Copy the following to a file named "hmm.json".
```json
{
  "dependencies": [
    {"name": "gdscript", "type": "haxelib", "version": "1.0.0-beta"},
    {"name": "godot-api-generator", "type": "git", "dir": null, "ref": null, "url": "https://github.com/senioritaelizabeth/Haxe-GodotBindingsGenerator"},
    {"name": "godot-extension-api-typings", "type": "haxelib", "version": "1.1.2"},
    {"name": "reflaxe", "type": "haxelib", "version": "4.0.0-beta"}
  ]
}
```
3. Run `haxelib install hmm` in the terminal.
4. Run `haxelib run hmm setup` in the terminal.
5. Run `hmm install` in the terminal.
6. Copy [this](https://raw.githubusercontent.com/godotengine/godot-headers/refs/heads/master/extension_api.json) to a file named "extension_api.json".
7. Make three folders, "assets", "assets/haxe", and "assets/gdscript".
8. Install the VSCode extension "Run On Save" by emeraldwalk.
9. Copy the following into your "vscode/settings.json" file.
```json
{
    "emeraldwalk.runonsave": {
        "commands": [
            {"cmd": "cd assets/haxe; haxelib run godot-api-generator extension_api.json assets/haxe; cd ../../", "isAsync": true},
            {"cmd": "haxe build.hxml", "isAsync": false}
        ]
    }
}
```
10. Copy the following into a file named "build.hxml".
```hxml
-cp assets/haxe
-lib gdscript
-D gdscript-output=assets/gdscript

# Stops the "cug" package from being buttfucked by DCE.
cug
```
11. Copy the following into a file named "MyClass.hx" in "assets/haxe/game". (That folder is where you will put ALL of your Haxe code.)
```haxe
package game;

class MyClass extends godot.Node {
    public override function _ready() {
        super.ready();
        trace("Hello, World!");
    }
}
```
12. Save the file. The VS Code extension should convert it to GDScript instantly. (The exported GDScript files will be in assets/gdscript.)