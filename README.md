# zipsave.js

A thin wrapper around [JSZip](https://stuk.github.io/jszip/) and [FileSaver.js](https://github.com/eligrey/FileSaver.js/) to make it easy to bundle multiple files into a zip and offer it to the user to download.

## Example

```js
zipsave([
  {url: "https://example.com/image.png", name: "google.png"},
  {data: blob, name: "out/blob.pdf"},
  {data: "Some text.", name: "text.txt"}
], "something.zip");
```

## Usage

Only tested in recent versions of Firefox and Chrome. Safari likely has some issues.

In your page's head:
```HTML
<script src="jszip.js"></script>
<script src="FileSaver.js"></script>
<script src="zipsave.js"></script>
```

Including this file in a script tag defines the `zipsave` function in global scope. It takes four parameters, two optional:
- A list of file descriptor objects, which have either a `url` or a `data` property specifying their contents, and a `name` property which can include folders. The `data` property can be a string, [Uint8Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array), [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), canvas element (as a png, and only if `toBlob` or a [polyfill](https://github.com/blueimp/JavaScript-Canvas-to-Blob) is available), or [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) (including [Files](https://developer.mozilla.org/en-US/docs/Web/API/File)).
- The name of the zip.
- Optionally a function to call on encountering an error. Either way, encountering an error aborts the process. This argument is discarded if not callable, so you can pass `null` if you just want the next parameter.
- Optionally a function to call when the zip is ready, which gets as its sole parameter the JSZip object created. If not specified, the file will be immediately offered to the user for download when ready.