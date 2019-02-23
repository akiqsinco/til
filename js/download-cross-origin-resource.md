# クロスオリジンの画像を名前付きで保存する方法
JavaScriptで画像を保存する際に、ソースURLが別オリジンだと`download`属性で指定したファイル名で保存されない。  
以下のように一度画像を取得してソースURLにblobとして埋め込むことで、名前付きで保存することができる。  

```js
const forceDownload = (blob, filename) => {
    const anchor = document.createElement('a')
    anchor.download = filename
    anchor.href = blob
    document.body.appendChild(anchor)
    anchor.click()
    anchor.remove()
}

const downloadResource = (url, filename) => {
    if (!filename) {
        filename = url.split('\\').pop().split('/').pop()
    }

    fetch(url, {
        headers: new Headers({
            'Origin': location.origin
        }),
        mode: 'cors'
    })
        .then(response => response.blob())
        .then(blob => {
            let blobUrl = window.URL.createObjectURL(blob)
            forceDownload(blobUrl, filename)
        })
        .catch(e => console.error(e))
}
```

## 参考
- [javascript - Chrome 65 blocks cross-origin <a download>. Client-side workaround to force download? - Stack Overflow](https://stackoverflow.com/questions/49474775/chrome-65-blocks-cross-origin-a-download-client-side-workaround-to-force-down)