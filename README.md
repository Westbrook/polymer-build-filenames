On the command line:
```bash
mkdir build-test
cd build-test
git clone https://github.com/Polymer/tools.git
cd tools/packages/build
yarn
```
At this point, if you'd like to see the file names as they are processed, open `tools/packages/build/src/optimize-streams.ts` and update the method `notExcluded` at about line 258 to include the following:
```js
function notExcluded(option: boolean|{exclude?: string[]}) {
  const exclude = typeof option === 'object' && option.exclude || [];
  return (fs: vinyl) => {
    console.log(fs.path);
    return !exclude.some(
             (pattern: string) => matcher.isMatch(fs.relative, pattern));
           }
}
```
Back on the command line:
```bash
yarn build
yarn link
cd ../cli
yarn
yarn link polymer-build
yarn build
yarn link
cd ../../../
git clone https://github.com/Westbrook/polymer-build-filenames.git
cd polymer-build-filenames
yarn
bower install
yarn link polymer-cli
yarn build
```
Expect to see output like:
```bash
yarn run v1.6.0
$ polymer build --preset es5-bundled
info: [cli.command.build]    Clearing build/ directory...
info: [cli.build.build]    (es5-bundled) Building...
/Users/you/Documents/web/repos/new-repo/index.html_script_0.js
/Users/westbrook/Documents/web/repos/new-repo/index.html_script_0.js
/Users/you/Documents/web/repos/new-repo/index.html_script_1.js
/Users/you/Documents/web/repos/new-repo/index.html_script_1.js
/Users/you/Documents/web/repos/new-repo/index.html_script_2.js
/Users/you/Documents/web/repos/new-repo/index.html_script_2.js
/Users/you/Documents/web/repos/new-repo/index.html_script_3.js
/Users/you/Documents/web/repos/new-repo/index.html_script_3.js
/Users/you/Documents/web/repos/new-repo/index.html_script_4.js
/Users/you/Documents/web/repos/new-repo/index.html_script_4.js
/Users/you/Documents/web/repos/new-repo/index.html_script_5.js
/Users/you/Documents/web/repos/new-repo/index.html_script_5.js
/Users/you/Documents/web/repos/new-repo/index.html_script_6.js
/Users/you/Documents/web/repos/new-repo/index.html_script_6.js
/Users/you/Documents/web/repos/new-repo/index.html_script_7.js
/Users/you/Documents/web/repos/new-repo/index.html_script_7.js
/Users/you/Documents/web/repos/new-repo/index.html_script_8.js
/Users/you/Documents/web/repos/new-repo/index.html_script_8.js
/Users/you/Documents/web/repos/new-repo/index.html_script_9.js
/Users/you/Documents/web/repos/new-repo/index.html_script_9.js
/Users/you/Documents/web/repos/new-repo/index.html_script_10.js
/Users/you/Documents/web/repos/new-repo/index.html_script_10.js
/Users/you/Documents/web/repos/new-repo/index.html_script_11.js
/Users/you/Documents/web/repos/new-repo/index.html_script_11.js
/Users/you/Documents/web/repos/new-repo/index.html_script_12.js
/Users/you/Documents/web/repos/new-repo/index.html_script_12.js
/Users/you/Documents/web/repos/new-repo/index.html_script_13.js
/Users/you/Documents/web/repos/new-repo/index.html_script_13.js
/Users/you/Documents/web/repos/new-repo/index.html_script_14.js
/Users/you/Documents/web/repos/new-repo/index.html_script_14.js
/Users/you/Documents/web/repos/new-repo/index.html_script_15.js
/Users/you/Documents/web/repos/new-repo/index.html_script_15.js
/Users/you/Documents/web/repos/new-repo/index.html_script_16.js
/Users/you/Documents/web/repos/new-repo/index.html_script_16.js
/Users/you/Documents/web/repos/new-repo/index.html_script_17.js
/Users/you/Documents/web/repos/new-repo/index.html_script_17.js
/Users/you/Documents/web/repos/new-repo/index.html_script_18.js
/Users/you/Documents/web/repos/new-repo/index.html_script_18.js
/Users/you/Documents/web/repos/new-repo/index.html_script_19.js
/Users/you/Documents/web/repos/new-repo/index.html_script_19.js
/Users/you/Documents/web/repos/new-repo/index.html_script_20.js
/Users/you/Documents/web/repos/new-repo/index.html_script_20.js
/Users/you/Documents/web/repos/new-repo/index.html
/Users/you/Documents/web/repos/new-repo/index.html
info: [cli.build.build]    (es5-bundled) Build complete!
✨  Done in 6.43s.
```
