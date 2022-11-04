---
date: 2022-04-03
author: SakumyZ
categories: Vue
tag: Obsidian
tags: Obsidian
---

# 使用 Obsidian 内置 API

Obsidian API 接口定义 参考文档: https://github.com/obsidianmd/obsidian-api/blob/master/obsidian.d.ts

上述网址可以看到所有 Obsidian 开放的接口定义。

我们在可以书写 JS 的地方，可以使用 Obsidian 暴露出来的全局变量 `app` 来使用所定义的 api。

例如,我想使用 FileManager 这个类。

其在 Obsidian 中的定义是这样的。

```ts
/**
 * Manage the creation, deletion and renaming of files from the UI.
 * @public
 */
export class FileManager {
  /**
   * Gets the folder that new files should be saved to, given the user's preferences.
   * @param sourcePath - The path to the current open/focused file,
   * used when the user wants new files to be created "in the same folder".
   * Use an empty string if there is no active file.
   * @public
   */
  getNewFileParent(sourcePath: string): TFolder

  /**
   * Rename or move a file safely, and update all links to it depending on the user's preferences.
   * @param file - the file to rename
   * @param newPath - the new path for the file
   * @public
   */
  renameFile(file: TAbstractFile, newPath: string): Promise<void>

  /**
   * Generate a markdown link based on the user's preferences.
   * @param file - the file to link to.
   * @param sourcePath - where the link is stored in, used to compute relative links.
   * @param subpath - A subpath, starting with `#`, used for linking to headings or blocks.
   * @param alias - The display text if it's to be different than the file name. Pass empty string to use file name.
   * @public
   */
  generateMarkdownLink(file: TFile, sourcePath: string, subpath?: string, alias?: string): string
}
```

所有的接口，Obsidian 都帮我们实例化并暴露了出去，所以在代码中，我们只需要使用 app 实例就可以使用 FileManager 了。

```ts
app.fileManager.getNewFileParent(sourcePath)
```

若想使用其他接口，直接访问 app 的原型方法就可以调用了。

可以 使用 `Ctrl + Shift + I` 打开开发者工具，输入 app , 可以快速看到有哪些方法可以使用。

![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/20220403101602.png)

当然也别忘了原型链上的方法
![](https://images-1257722820.cos.ap-guangzhou.myqcloud.com/20220403101700.png)

不过要知道该方法的用法及其传参，还是要参照 API 接口定义。
