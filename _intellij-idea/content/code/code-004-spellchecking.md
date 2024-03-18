---
title: "拼写检查"
sequence: "104"
---

[UP](/intellij-idea.html)


```text
Configure: Settings/Preferences | Editor | Natural Languages | Spelling
Inspection: Settings/Preferences | Editor | Inspections | Proofreading | Typo
```

IntelliJ IDEA helps you make sure that all your source code, including _variable names_(变量名), _textual strings_(文本字符串), _comments_(注释), _literals_(常量), and _commit messages_(Git 的提交信息), is spelt correctly.

For this purpose, IntelliJ IDEA provides a dedicated **Typo** inspection which is enabled by default.

{:refdef: style="text-align: center;"}
![](/assets/images/intellij/ij_typo_change_to.png)
{:refdef}





## Configure Dictionaries

```text
Settings/Preferences | Editor | Natural Languages | Spelling
```

IntelliJ IDEA includes **bundled dictionaries** for all configured languages. You cannot modify them directly but you can extend the **spellchecker** in other ways:

- Save words to a built-in global or project dictionary.
- Add plain-text files with the `.dic` extension that contain lists of words.
- If you have the [Hunspell plugin](https://plugins.jetbrains.com/plugin/10275-hunspell) installed and enabled, you can add [Hunspell](https://hunspell.github.io/) dictionaries, which comprise of **two files**: the `DIC` file that contains a list of words with the applicable modification rules and the `AFF` file that lists prefixes and suffixes regulated by a specific modification rule. For example, `en_GB.dic` and `en_GB.aff`.

### Configure the spellchecker dictionaries

- Press `Ctrl+Alt+S` to open IDE settings and select `Editor | Natural Languages | Spelling`.
- Configure the list of custom dictionaries:
  - To add a new **custom dictionary** to the list, click ![the Add button](/assets/images/intellij/icons.general.add.svg) or press `Alt+Insert` and specify the location of the required file.
  - To edit the contents of a **custom dictionary** in IntelliJ IDEA, select it and click ![the Edit button](/assets/images/intellij/icons.actions.edit.svg) or press `Enter`. The corresponding file will open in a new editor tab.
  - To remove a **custom dictionary** from the list, select it and click ![the Remove button](/assets/images/intellij/icons.general.remove.svg) or press `Alt+Delete`.

{:refdef: style="text-align: center;"}
![](/assets/images/intellij/settings-editor-natural-languages-spelling.png)
{:refdef}

### Select the default dictionary for saving word

By default, IntelliJ IDEA saves words to the **global application-level dictionary**.
You can choose to save words to the **project-level dictionary** if the spelling is correct only for this particular project.

- Press `Ctrl+Alt+S` to open IDE settings and select `Editor | Natural Languages | Spelling`.
- Select either the built-in **project-level** or **application-level** dictionary or disable the option to prompt you every time you save a word.

{:refdef: style="text-align: center;"}
![](/assets/images/intellij/settings-editor-natural-languages-spelling.png)
{:refdef}

### Add accepted words manually

- Press `Ctrl+Alt+S` to open IDE settings and select `Editor | Natural Languages | Spelling`.
- Add words to the **Accepted words** list. IntelliJ IDEA adds manually accepted words to the **project-level dictionary**.

You can't add words that are already present in one of the dictionaries and **mixed-case words**, such as `CamelCase` and `snake_case`.

## Configure Inspection

```text
Settings/Preferences | Editor | Inspections | Proofreading | Typo
```

By default, the **Typo inspection** checks all text including _code elements_(代码元素), _string literals_(字符串常量), and _comments_(注释) in all scopes.

- Press `Ctrl+Alt+S` to open IDE settings and select `Editor | Inspections`.
- Expand the `Proofreading` node and click `Typo` in the central pane.
- In the right-hand pane, configure the **Typo inspection**:

<table>
<thead>
<tr>
    <th>Item</th>
    <th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Severity</strong></td>
<td>
Specify the <strong>severity level</strong> and the <strong>scope</strong> in which to apply this level.<br/>
For example, if you want typos to stand out more, select <b>Error</b> or <b>Warning</b> to highlight typos similar to syntax errors or warnings in your code.
</td>
</tr>
<tr>
<td><strong>Options</strong></td>
<td>
Specify the type of content to check:
<ul>
    <li><b>Process code</b>: check various code elements, such as names of classes, fields, and methods.</li>
    <li><b>Process literals</b>: check text inside string literals.</li>
    <li><b>Process comments</b>: check text inside comments.</li>
</ul>
</td>
</tr>
</tbody>
</table>

**To disable the Typo inspection, clear the checkbox next to it.**

{:refdef: style="text-align: center;"}
![](/assets/images/intellij/settings-editor-inspections-proofreading-typo.png)
{:refdef}



## Take Actions

The **Typo inspection** detects and highlights words not included in any dictionary.

- Correct the spelling（知错就改）
- Accept the word as correct（有意为之）
- Disable the Typo inspection if you want to ignore all spelling mistakes（阻塞言路）

### Correct a misspelled word

- Place the caret at any word highlighted by the **Typo inspection**.
- Click ![the Intention action icon](/assets/images/intellij/icons.actions.intentionBulb.svg) or press `Alt+Enter` to show the available intention actions.
- Select one of the suggested fixes from the list.

{:refdef: style="text-align: center;"}
![](/assets/images/intellij/ij_typo_change_to.animated.gif)
{:refdef}

To jump to the next misspelled word, press `F2`.

### Accept a misspelled word

- Place the caret at a word highlighted by the **Typo inspection**.
- Click ![the Intention action icon](/assets/images/intellij/icons.actions.intentionBulb.svg) or press `Alt+Enter` to show the available intention actions.
- Select the **Save to dictionary** action to add the word to the user's dictionary and skip it in the future.

If you have added the word by mistake, press `Ctrl+Z` to remove it from the dictionary.

By default, IntelliJ IDEA saves words to the **global application-level dictionary**.
You can choose to save words to the **project-level dictionary** if the spelling is correct only for this particular project.

## References

- [jetbrains: Spellchecking](https://www.jetbrains.com/help/idea/spellchecking.html)
