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
